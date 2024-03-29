---
title: Configure External DNS for Kubernetes Ingress
menu:
  docs_7.0.0-rc.3:
    identifier: external-dns-dns
    name: External DNS
    parent: dns-ingress
    weight: 10
product_name: voyager
menu_name: docs_7.0.0-rc.3
section_menu_id: guides
info:
  version: 7.0.0-rc.3
---

> New to Voyager? Please start [here](/docs/7.0.0-rc.3/concepts/overview).

# Configuring external DNS servers

[external-dns](https://github.com/kubernetes-incubator/external-dns) project can be used to configure external DNS servers for Voyager managed ingresses.

## LoadBalancer Ingress

For a [LoadBalancer](/docs/7.0.0-rc.3/concepts/ingress-types/loadbalancer) type Ingress, apply `"external-dns.alpha.kubernetes.io/hostname"` annotation on the **service** that exposes HAProxy pods. This service should have a name like `voyager-{ingress-name}` in the same namespace of the Ingress object. Since, Voyager uses its own CRD for Ingress, `external-dns` project must use the service to discover loadbalancer ip.

```yaml
apiVersion: voyager.appscode.com/v1beta1
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
          serviceName: web
          servicePort: '80'
```

## NodePort Ingress

`external-dns` does not support [NodePort](/docs/7.0.0-rc.3/concepts/ingress-types/nodeport) ingress.


## HostPort Ingress

[HostPort](/docs/7.0.0-rc.3/concepts/ingress-types/hostport) type Ingress is supported by external-dns, since version [v0.5.0-alpha.1](https://github.com/kubernetes-incubator/external-dns/releases/tag/v0.5.0-alpha.1). Here, apply `"external-dns.alpha.kubernetes.io/hostname"` annotation on the HAProxy **pods**.

```yaml
apiVersion: voyager.appscode.com/v1beta1
kind: Ingress
metadata:
  name: test-ingress-voyager
  namespace: vdimov-dev
  annotations:
     ingress.appscode.com/type: HostPort
     ingress.appscode.com/annotations-pod: |
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
          serviceName: web
          servicePort: '80'
```

## Internal Ingress

[Internal](/docs/7.0.0-rc.3/concepts/ingress-types/internal) ingress is not accessible from outside a cluster. Hence, there is nothing to configure in external DNS servers.
