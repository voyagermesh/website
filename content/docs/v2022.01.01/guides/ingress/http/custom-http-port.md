---
title: Custom HTTP Port | Kubernetes Ingress
menu:
  docs_v2022.01.01:
    identifier: custom-port-http
    name: Custom HTTP Port
    parent: http-ingress
    weight: 35
product_name: voyager
menu_name: docs_v2022.01.01
section_menu_id: guides
info:
  cli: v0.0.4
  installer: v2022.01.01
  version: v2022.01.01
---

> New to Voyager? Please start [here](/docs/v2022.01.01/concepts/overview).

# Custom HTTP Port

Voyager 3.2+ supports using any non-standard port (beyond 80 and 443) for L7 traffic. If no port is specified, port 80 or 443 will be used depending on whether TLS is used or not.

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
spec:
  rules:
  - host: one.example.com
    http:
      port: '8989'
      paths:
      - path: /admin
        backend:
          service:
            name: admin-service
            port:
              number: 80
      - path: /
        backend:
          service:
            name: test-service
            port:
              number: 80
  - host: other.example.com
    http:
      port: '8989'
      paths:
      - backend:
          service:
            name: other-service
            port:
              number: 80
  - host: one.example.com
      http:
        port: '4343'
        paths:
        - backend:
            service:
              name: test-service
              port:
                number: 80

```

For this configuration, the loadbalancer will listen to `8989` and `4343` port for incoming HTTP connections, and will
pass any request coming to it to the desired backend.

### Restrictions:
- For one Ingress resource you cannot have multiple `tcp` rules listening to same port, even if they do not have
same `host`.

- Different hosts can use the same port for `http` rules
