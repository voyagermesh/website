---
title: Configure Ingress Keep Source IP
menu:
  docs_7.4.0:
    identifier: keep-source-ip-configuration
    name: Keep Source IP
    parent: config-ingress
    weight: 10
product_name: voyager
menu_name: docs_7.4.0
section_menu_id: guides
info:
  version: 7.4.0
---

> New to Voyager? Please start [here](/docs/7.4.0/concepts/overview).

# Keep Source IP

You can preserve client source IP by setting annotation `ingress.appscode.com/keep-source-ip` to `true`.

For `LoadBalancer` type ingresses, the actual configuration generated depends on the underlying cloud provider.

- `GCE, GKE, Azure, ACS`: Sets `ExternalTrafficPolicy` to `Local` for services used to expose HAProxy. See [here](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip).
- `AWS`: Enables [accept-proxy](accept-proxy.md) that enforces the use of the PROXY protocol over any connection accepted by any of the sockets declared on the same line.

For `NodePort` type ingresses, it sets `ExternalTrafficPolicy` to `Local` regardless the cloud provider.

## Ingress Example

```yaml
apiVersion: voyager.appscode.com/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
  annotations:
    ingress.appscode.com/keep-source-ip: "true"
    ingress.appscode.com/health-check-nodeport: "32312"
spec:
  rules:
  - host: voyager.appscode.test
    http:
      paths:
      - path: /foo
        backend:
          serviceName: test-server
          servicePort: 80
```

Here `health-check-nodeport` annotation specifies `HealthCheckNodePort` field for services used to expose HAProxy. If not specified, it will be auto-assigned by kubernetes. Note that, it is only effective when `keep-source-ip` is `true` and ingress type is `LoadBalancer`.