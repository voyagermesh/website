---
title: Backend Rules | Kubernetes Ingress
menu:
  docs_v2021.04.24-rc.0:
    identifier: backend-config
    name: Backend Rule
    parent: config-ingress
    weight: 100
product_name: voyager
menu_name: docs_v2021.04.24-rc.0
section_menu_id: guides
info:
  installer: v2021.04.24-rc.0
  version: v2021.04.24-rc.0
---

> New to Voyager? Please start [here](/docs/v2021.04.24-rc.0/concepts/overview).

# Backend Rules

Voyager supports full spectrum of HAProxy backend rules via `backendRule`. Read [more](https://cbonte.github.io/haproxy-dconv/1.7/configuration.html)
about HAProxy backend rules.

```yaml
apiVersion: voyager.appscode.com/v1beta1
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
          serviceName: test-service
          servicePort: '80'
          backendRules:
          - 'acl add_url capture.req.uri -m beg /test-second'
          - 'http-response set-header X-Added-From-Proxy added-from-proxy if add_url'
```

This example will apply an acl to the server backend, and a extra header from Loadbalancer if request uri
starts with `/test-second`.