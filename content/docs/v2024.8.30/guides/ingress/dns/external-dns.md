---
title: Configure External DNS for Kubernetes Ingress
menu:
  docs_v2024.8.30:
    identifier: external-dns-dns
    name: External DNS
    parent: dns-ingress
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

# Configuring external DNS servers

[external-dns](https://github.com/kubernetes-incubator/external-dns) project can be used to configure external DNS servers for Voyager managed ingresses.

## LoadBalancer Ingress

For a [LoadBalancer](/docs/v2024.8.30/concepts/ingress-types/loadbalancer) type Ingress, apply `"external-dns.alpha.kubernetes.io/hostname"` annotation on the **service** that exposes HAProxy pods. This service should have a name like `voyager-{ingress-name}` in the same namespace of the Ingress object. Since, Voyager uses its own CRD for Ingress, `external-dns` project must use the service to discover loadbalancer ip.

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress-voyager
  namespace: vdimov-dev
  annotations:
     ingress.appscode.com/annotations-service: |
         {
           "external-dns.alpha.kubernetes.io/hostname" : "voyager.example.com,voyager-1.example.com,voyager-2.example.com"
         }
     ingress.appscode.com/replicas: '2'
spec:
  rules:
  - host: voyager.example.com
    http:
      paths:
       - backend:
          service:
            name: web
            port:
              number: 80
```

## NodePort Ingress

Since [v0.5.3](https://github.com/kubernetes-incubator/external-dns/releases/tag/v0.5.3), `external-dns` supports [NodePort](/docs/v2024.8.30/concepts/ingress-types/nodeport) ingress.


## HostPort Ingress

[HostPort](/docs/v2024.8.30/concepts/ingress-types/hostport) type Ingress is [supported by external-dns](https://github.com/kubernetes-incubator/external-dns/blob/v0.5.2/docs/tutorials/hostport). Here, apply `"external-dns.alpha.kubernetes.io/hostname"` annotation on the HAProxy **services**.

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress-voyager
  namespace: vdimov-dev
  annotations:
     ingress.appscode.com/type: HostPort
     ingress.appscode.com/annotations-service: |
         {
           "external-dns.alpha.kubernetes.io/hostname" : "voyager.example.com,voyager-1.example.com,voyager-2.example.com"
         }
     ingress.appscode.com/replicas: '2'
spec:
  rules:
  - host: voyager.example.com
    http:
      paths:
       - backend:
          service:
            name: web
            port:
              number: 80
```

## Internal Ingress

[Internal](/docs/v2024.8.30/concepts/ingress-types/internal) ingress is not accessible from outside a cluster. Hence, there is nothing to configure in external DNS servers.
