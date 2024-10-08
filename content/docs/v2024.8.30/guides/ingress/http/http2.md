---
title: HTTP2 | Kubernetes Ingress
menu:
  docs_v2024.8.30:
    identifier: h2-http
    name: HTTP2
    parent: http-ingress
    weight: 26
product_name: voyager
menu_name: docs_v2024.8.30
section_menu_id: guides
info:
  cli: v0.0.16
  installer: v2024.8.30
  version: v2024.8.30
---

> New to Voyager? Please start [here](/docs/v2024.8.30/concepts/overview).

# Enable HTTP/2 on ingress resource

Voyager can enable HTTP/2 from version >=8.0.1

To enable http2, you must first setup a [certificate](/docs/v2024.8.30/guides/certificate) (Let's Encrypt), or use an existing one. Then create an ingress object like below:

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: haproxy-ingress # name of the ingress
  namespace: default # namespace (optional)
  annotations:
    ingress.appscode.com/replicas: '2'
    # ... other annotations
spec:
  tls:
  - hosts:
    - host.example.com
    secretName: tls-host
  rules:
  - host: host.example.com
    http:
      paths:
      - path: "/"
        backend:
          service:
            name: host-service
            port:
              number: 8000
      alpn:
      - h2
      - http/1.1
      - http/1.0
```

The important bit here is `alpn`. In this example the ingress can negotiate from `HTTP/2` all the way down to `HTTP/1.0`. If `alpn` isn't specified at all, the negotiated protocol will be `HTTP/1.1` (default).

The above settings are reflected in the generated haproxy `ConfigMap`:

```frontend http-0_0_0_0-443
    bind *:443  ssl no-sslv3 no-tlsv10 no-tls-tickets crt /etc/ssl/private/haproxy/tls/  alpn h2,http/1.1,http/1.0
```
