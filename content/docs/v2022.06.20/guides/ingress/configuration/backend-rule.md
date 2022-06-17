---
title: Backend Rules | Kubernetes Ingress
menu:
  docs_v2022.06.20:
    identifier: backend-config
    name: Backend Rule
    parent: config-ingress
    weight: 100
product_name: voyager
menu_name: docs_v2022.06.20
section_menu_id: guides
info:
  cli: v0.0.9
  installer: v2022.06.20
  version: v2022.06.20
---

> New to Voyager? Please start [here](/docs/v2022.06.20/concepts/overview).

# Backend Rules

Voyager supports full spectrum of HAProxy backend rules via `backendRule`. Read [more](https://cbonte.github.io/haproxy-dconv/1.7/configuration.html)
about HAProxy backend rules.

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
spec:
  rules:
  - host: appscode.example.com
    http:
      paths:
      - path: '/test'
        backend:
          service:
            name: test-service
            port:
              number: 80
          backendRules:
          - 'acl add_url capture.req.uri -m beg /test-second'
          - 'http-response set-header X-Added-From-Proxy added-from-proxy if add_url'
```

This example will apply an acl to the server backend, and a extra header from Loadbalancer if request uri
starts with `/test-second`.