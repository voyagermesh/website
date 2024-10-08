---
title: Backend TLS Support | Kubernetes Ingress
menu:
  docs_v2024.8.30:
    identifier: backend-tls
    name: Backend TLS
    parent: tls-ingress
    weight: 20
product_name: voyager
menu_name: docs_v2024.8.30
section_menu_id: guides
info:
  cli: v0.0.16
  installer: v2024.8.30
  version: v2024.8.30
---

> New to Voyager? Please start [here](/docs/v2024.8.30/concepts/overview).

# Backend TLS Support

Voyager can connect to a tls enabled backend server with or without ssl verification.

Available options:

- `ssl`: Creates a TLS/SSL socket when connecting to this server in order to cipher/decipher the traffic. If verify not set the following error may occurred:

> Verify is enabled by default but no CA file specified. If you're running on a LAN where you're certain to trust the server's certificate, please set an explicit 'verify none' statement on the 'server' line, or use 'ssl-server-verify none' in the global section to disable server-side verifications by default.

- `verify [none|required]`: Sets HAProxy‘s behavior regarding the certificated presented by the server:
  - `none`: Doesn’t verify the certificate of the server
  - `required (default value)`: TLS handshake is aborted if the validation of the certificate presented by the server returns an error.

- `verifyhost <hostname>`: Sets a <hostname> to look for in the Subject and SubjectAlternateNames fields provided in the certificate sent by the server. If <hostname> can’t be found, then the TLS handshake is aborted. This only applies when verify required is configured.

- `ca-file <file-path>`: Specify a CA file to verify the backend server. See [here](/docs/v2024.8.30/guides/ingress/configuration/config-volumes) for complete example.

Example: `ingress.appscode.com/backend-tls: "ssl verify none"`

If this annotation is not set HAProxy will connect to backend as http. This value should not be set if the backend do not support https resolution.

Example:

```yaml
kind: Service
apiVersion: v1
metadata:
  name: my-service
  namespace: default
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
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
spec:
  defaultBackend:
    service:
      name: test-service
      port:
        number: 80
  rules:
  - host: appscode.example.com
    http:
      paths:
      - backend:
          service:
            name: my-service
            port:
              number: 80
```

Reference:

- https://cbonte.github.io/haproxy-dconv/1.8/configuration.html#5.2-ssl
- https://cbonte.github.io/haproxy-dconv/1.8/configuration.html#5.2-verify
- https://cbonte.github.io/haproxy-dconv/1.8/configuration.html#5.2-verifyhost
