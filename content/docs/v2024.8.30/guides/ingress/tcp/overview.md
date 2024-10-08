---
title: TCP LoadBalancing | Kubernetes Ingress
menu:
  docs_v2024.8.30:
    identifier: overview-tcp
    name: Overview
    parent: tcp-ingress
    weight: 10
product_name: voyager
menu_name: docs_v2024.8.30
section_menu_id: guides
info:
  cli: v0.0.16
  installer: v2024.8.30
  version: v2024.8.30
---

> New to Voyager? Please start [here](/docs/v2024.8.30/concepts/overview).

# TCP LoadBalancing

TCP load balancing is one of the core features of Voyager Ingress. Voyager can handle TCP Load balancing with or without TLS. One Voyager Ingress can also be used to load balance both HTTP and TCP.

One Simple TCP Rule Would be:

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: default
spec:
  tls:
  - secretName: mycert
    hosts:
    - other.example.com
  rules:
  - host: one.example.com
    tcp:
      port: 9898
      backend:
        service:
          name: tcp-service
          port:
            number: 50077
  - host: other.example.com
    tcp:
      port: 7878
      backend:
        service:
          name: tcp-service
          port:
            number: 50077
  - host: other.example.com
    tcp:
      port: 7800
      noTLS: true
      backend:
        service:
          name: tcp-service
          port:
            number: 50077
```

For this Ingress, HAProxy will open up 3 separate ports:
- port 9898: Passes traffic to pods behind tcp-service:50077. Uses no TLS, since `spec.TLS` does not have a matching host.

- port 7878: Passes traffic to pods behind tcp-service:50077. Uses TLS, since `spec.TLS` has a matching host.

- port 7880: Passes traffic to pods behind tcp-service:50077. __Uses no TLS__, even though `spec.TLS` has a matching host. This is because `tcp.noTLS` is set to true for this rule.
