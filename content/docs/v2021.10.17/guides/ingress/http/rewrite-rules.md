---
title: Header and URL Rewriting | Voayger
menu:
  docs_v2021.10.17:
    identifier: rewrite-http
    name: Rewrite Support
    parent: http-ingress
    weight: 25
product_name: voyager
menu_name: docs_v2021.10.17
section_menu_id: guides
info:
  installer: v2021.10.17
  version: v2021.10.17
---

> New to Voyager? Please start [here](/docs/v2021.10.17/concepts/overview).

# Header and URL Rewriting

AppsCode Ingress support header and URL modification at the loadbalancer level. To ensure simplicity,
the backend rules follow the HAProxy syntax as it is. To add some rewrite rules for a HTTP path, follow the example below:

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
      - backend:
          service:
            name: test-service
            port:
              number: 80
          backendRules:
          - http-request replace-uri ^/(.*)$ /testings/\\1
          - http-request set-header X-Forwarded-Host %[base]
```

The first rule specified in `backendRules` is used to modify the request url including the host. Current example
will add an `/testings` prefix in every request URI before forwarding it to backend.

The second rule specified in `backendRules` will be applicable before going to the backend.
These rule will add header in the request if the header is already not present in the request header.
In the example `X-Forwarded-Host` header is added to the request if it is not already there, `%[base]` indicates
the base URL the load balancer received the requests.
