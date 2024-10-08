---
title: TLS Authentication | Kubernetes Ingress
menu:
  docs_v2024.8.30:
    identifier: tls-auth-security
    name: TLS Auth
    parent: security-ingress
    weight: 15
product_name: voyager
menu_name: docs_v2024.8.30
section_menu_id: guides
info:
  cli: v0.0.16
  installer: v2024.8.30
  version: v2024.8.30
---

> New to Voyager? Please start [here](/docs/v2024.8.30/concepts/overview).

# TLS Authentication

This example demonstrates how to configure [TLS Authentication](https://tools.ietf.org/html/rfc2617) on Voyager Ingress controller.

- [Using tls auth in Ingress](#using-tls-authentication)
- [Using tls auth in Frontend](#using-tls-auth-in-frontend)

Before diving into the deep learn about TLS Auth with HAProxy.

- [SSL Client certificate management at application level](https://www.haproxy.com/blog/ssl-client-certificate-management-at-application-level/)
- [Client side ssl certificates](https://raymii.org/s/tutorials/haproxy_client_side_ssl_certificates.html)

## Using TLS Authentication

Voyager Ingress read ca certificates from files stored on secrets with `ca.crt` key.

- `ingress.appscode.com/auth-tls-secret`: Name of secret for TLS client certification validation.
- `ingress.appscode.com/auth-tls-error-page`: The page that user should be redirected in case of Auth error
- `ingress.appscode.com/auth-tls-verify-client`: Enables verification option of client certificates.

### Configure

Create tls secret for enable ssl termination:

```bash
$ kubectl create secret tls server --cert=/path/to/cert/file --key=/path/to/key/file
```

Create ca cert secret:

```bash
$ kubectl create secret generic ca --from-file=/path/to/ca.crt
```

Create an Ingress with TLS Auth annotations:

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  annotations:
    ingress.appscode.com/auth-tls-secret: ca
    ingress.appscode.com/auth-tls-verify-client: required
    ingress.appscode.com/auth-tls-error-page: "https://auth.example.com/errors.html"
  name: hello-tls-auth
  namespace: default
spec:
  tls:
  - secretName: server
    hosts:
    - auth.example.com
  rules:
  - host: auth.example.com
    http:
      paths:
      - path: /testpath
        backend:
          service:
            name: test-server
            port:
              number: 80
```

Test without certificates:

```bash
$ curl -i -vvv 'https://auth.example.com'
* Hostname was NOT found in DNS cache
*   Trying 192.168.99.100...
* Connected to http.appscode.test (192.168.99.100) port 443 (#0)
* successfully set certificate verify locations:
*   CAfile: none
  CApath: /etc/ssl/certs
* SSLv3, TLS handshake, Client hello (1):
* SSLv3, TLS handshake, Server hello (2):
* SSLv3, TLS handshake, CERT (11):
* SSLv3, TLS handshake, Server key exchange (12):
* SSLv3, TLS handshake, Request CERT (13):
* SSLv3, TLS handshake, Server finished (14):
* SSLv3, TLS handshake, CERT (11):
* SSLv3, TLS handshake, Client key exchange (16):
* SSLv3, TLS change cipher, Client hello (1):
* SSLv3, TLS handshake, Finished (20):
* SSLv3, TLS alert, Server hello (2):
* error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure
* Closing connection 0
curl: (35) error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure
```

Send a valid client certificate:

```bash
$ curl -v -s --key client.key --cert client.crt https://auth.example.com
HTTP/1.1 200 OK
Date: Fri, 08 Sep 2017 09:31:43 GMT
Content-Length: 0
Content-Type: text/plain; charset=utf-8

```

Send a invalid client certificate, that will redirect to error page if provided:

```bash
$ curl -v -s --key invalidclient.key --cert invalidclient.crt https://auth.example.com
HTTP/1.1 302
Location: https://auth.example.com/errors.html
```

## Using TLS Auth In Frontend

Basic Auth can also be configured per frontend in voyager ingress via FrontendRules.

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: hello-basic-auth
  namespace: default
spec:
  frontendRules:
  - port: 8080
    auth:
      tls:
        secretName: server
        verifyClient: required
        errorPage: "https://auth.example.com/error.html"
        headers:
          X-SSL-Client-CN: "%{+Q}[ssl_c_s_dn(cn)]"  # Add headers to Request based on SSL verification
          X-SSL:           "%[ssl_fc]",
  tls:
  - ref:
      kind: Secret
      name: server
    hosts:
    - auth.example.com
  rules:
  - host: auth.example.com
    http:
      paths:
      - path: /no-auth
        backend:
          service:
            name: test-server
            port:
              number: 80
  - host: auth.example.com
    http:
      port: 8080
      paths:
      - path: /auth
        backend:
          service:
            name: test-svc
            port:
              number: 80
```

Request in non-tls port:

```bash
$ curl -v -s https://auth.example.com
HTTP/1.1 200 OK
Date: Fri, 08 Sep 2017 09:31:43 GMT
Content-Length: 0
Content-Type: text/plain; charset=utf-8

```

Test without certificates:

```bash
$ curl -i -vvv 'https://auth.example.com:8080'
* Hostname was NOT found in DNS cache
*   Trying 192.168.99.100...
* Connected to http.appscode.test (192.168.99.100) port 443 (#0)
* successfully set certificate verify locations:
*   CAfile: none
  CApath: /etc/ssl/certs
* SSLv3, TLS handshake, Client hello (1):
* SSLv3, TLS handshake, Server hello (2):
* SSLv3, TLS handshake, CERT (11):
* SSLv3, TLS handshake, Server key exchange (12):
* SSLv3, TLS handshake, Request CERT (13):
* SSLv3, TLS handshake, Server finished (14):
* SSLv3, TLS handshake, CERT (11):
* SSLv3, TLS handshake, Client key exchange (16):
* SSLv3, TLS change cipher, Client hello (1):
* SSLv3, TLS handshake, Finished (20):
* SSLv3, TLS alert, Server hello (2):
* error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure
* Closing connection 0
curl: (35) error:14094410:SSL routines:SSL3_READ_BYTES:sslv3 alert handshake failure
```

Send a valid client certificate:

```bash
$ curl -v -s --key client.key --cert client.crt https://auth.example.com:8080
HTTP/1.1 200 OK
Date: Fri, 08 Sep 2017 09:31:43 GMT
Content-Length: 0
Content-Type: text/plain; charset=utf-8
```

Backend server will receive Headers `X-SSL` and `X-SSL-Client-CN`.

Send a invalid client certificate, that will redirect to error page if provided:

```bash
$ curl -v -s --key invalidclient.key --cert invalidclient.crt https://auth.example.com:8080
HTTP/1.1 302
Location: https://auth.example.com/errors.html
```
