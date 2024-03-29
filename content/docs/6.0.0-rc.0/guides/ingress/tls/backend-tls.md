---
title: Backend TLS Support | Kubernetes Ingress
menu:
  docs_6.0.0-rc.0:
    identifier: backend-tls
    name: Backend TLS
    parent: tls-ingress
    weight: 20
product_name: voyager
menu_name: docs_6.0.0-rc.0
section_menu_id: guides
info:
  version: 6.0.0-rc.0
---

# Backend TLS Support

Voyager can connect to a tls enabled backend server with or without ssl verification.

   ssl:
    Creates a TLS/SSL socket when connecting to this server in order to cipher/decipher the traffic

    if verify not set the following error may occurred
    [/etc/haproxy/haproxy.cfg:49] verify is enabled by default but no CA file specified.
    If you're running on a LAN where you're certain to trust the server's certificate,
    please set an explicit 'verify none' statement on the 'server' line, or use
    'ssl-server-verify none' in the global section to disable server-side verifications by default.

   verify (none|required):
    Sets HAProxy‘s behavior regarding the certificated presented by the server:
   none :
    doesn’t verify the certificate of the server

   required (default value) :
    TLS handshake is aborted if the validation of the certificate presented by the server returns an error.

   veryfyhost <hostname>:
    Sets a <hostname> to look for in the Subject and SubjectAlternateNames fields provided in the
    certificate sent by the server. If <hostname> can’t be found, then the TLS handshake is aborted.
    ie.
    ingress.appscode.com/backend-tls: "ssl verify none"

    If this annotation is not set HAProxy will connect to backend as http,
    This value should not be set if the backend do not support https resolution.

Example:
```yaml
kind: Service
apiVersion: v1
metadata:
  name: my-service
  annotations:
      ingress.appscode.com/backend-tls: ssl verify none
spec:
  selector:
    app: MyApp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 9376

```

```yaml
apiVersion: voyager.appscode.com/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
spec:
  backend:
    serviceName: test-service
    servicePort: '80'
  rules:
  - host: appscode.example.com
    http:
      paths:
      - backend:
          serviceName: my-service
          servicePort: '80'
```