---
title: Loadbalancer Source Range | Kubernetes Ingress
menu:
  docs_v2024.8.30:
    name: Source Range
    parent: http-ingress
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

# Loadbalancer Source Range

When using an Ingress with `ingress.appscode.com/type: LoadBalancer` annotation, you can specify the IP ranges
that are allowed to access the load balancer by using `spec.loadBalancerSourceRanges`.
This field takes a list of IP CIDR ranges, which will be forwarded to Kubernetes, that  will use to
configure firewall exceptions. This feature is currently supported on Google Compute Engine,
Google Container Engine and AWS. This field will be ignored if the cloud provider does not support the feature.

Assuming 10.0.0.0/8 is the internal subnet. In the following example, a load balancer will be created
that is only accessible to cluster internal ips. This will not allow clients from outside of your
Kubernetes cluster to access the load balancer.

```
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
  loadBalancerSourceRanges:
  - 10.0.0.0/8
```

In the following example, a load balancer will be created that is only accessible to clients with
IP addresses from 130.211.204.1 and 130.211.204.2.

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
  loadBalancerSourceRanges:
  - 130.211.204.1/32
  - 130.211.204.2/32
```

NB: Currently there is a [bug in Kubernetes](https://github.com/kubernetes/kubernetes/issues/34218) due to which changing `loadBalancerSourceRanges` does not change SecurityGroup in AWS.
