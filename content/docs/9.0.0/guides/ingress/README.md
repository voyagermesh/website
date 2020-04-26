---
title: Ingress | Voyager
menu:
  docs_9.0.0:
    identifier: readme-ingress
    name: Readme
    parent: ingress-guides
    weight: -1
product_name: voyager
menu_name: docs_9.0.0
section_menu_id: guides
url: /docs/9.0.0/guides/ingress/
aliases:
- /docs/9.0.0/guides/ingress/README/
info:
  version: 9.0.0
---

# Guides

Guides show you how to use Voyager as a Kubernetes Ingress controller.

- HTTP
  - [Exposing Service via Ingress](/docs/9.0.0/guides/ingress/http/single-service)
  - [Virtual Hosting](/docs/9.0.0/guides/ingress/http/virtual-hosting)
  - [Supports Loadbalancer Source Range](/docs/9.0.0/guides/ingress/http/source-range)
  - [URL and Request Header Re-writing](/docs/9.0.0/guides/ingress/http/rewrite-rules)
  - [Enable CORS](/docs/9.0.0/guides/ingress/http/cors)
  - [Custom HTTP Port](/docs/9.0.0/guides/ingress/http/custom-http-port)
  - [Using External Service as Ingress Backend](/docs/9.0.0/guides/ingress/http/external-svc)
  - [HSTS](/docs/9.0.0/guides/ingress/http/hsts)
  - [Forward Traffic to StatefulSet Pods](/docs/9.0.0/guides/ingress/http/statefulset-pod)
  - [Configure Sticky session to Backends](/docs/9.0.0/guides/ingress/http/sticky-session)
  - [Blue Green Deployments using weighted Loadbalancing](/docs/9.0.0/guides/ingress/http/blue-green-deployment)
- TLS/SSL
  - [TLS Termination](/docs/9.0.0/guides/ingress/tls/overview)
  - [Multiple TLS Entries](/docs/9.0.0/guides/ingress/tls/multiple-tls)
  - [Backend TLS](/docs/9.0.0/guides/ingress/tls/backend-tls)
  - [Supports AWS certificate manager](/docs/9.0.0/guides/ingress/tls/aws-cert-manager)
- TCP
  - [TCP LoadBalancing](/docs/9.0.0/guides/ingress/tcp/overview)
  - [TCP SNI](/docs/9.0.0/guides/ingress/tcp/tcp-sni)
- Configuration
  - [Customize generated HAProxy config via BackendRule](/docs/9.0.0/guides/ingress/configuration/backend-rule) (can be used for [http rewriting](https://www.haproxy.com/doc/aloha/7.0/haproxy/http_rewriting.html), add [health checks](https://www.haproxy.com/doc/aloha/7.0/haproxy/healthchecks.html), etc.)
  - [Apply Frontend Rules](/docs/9.0.0/guides/ingress/configuration/frontend-rule)
  - [Supported Annotations](/docs/9.0.0/guides/ingress/configuration/annotations)
  - [Specify NodePort](/docs/9.0.0/guides/ingress/configuration/node-port)
  - [Configure global options](/docs/9.0.0/guides/ingress/configuration/default-options)
  - [Configure Custom Timeouts for HAProxy](/docs/9.0.0/guides/ingress/configuration/default-timeouts)
  - [Configure Load balancing algorithm](/docs/9.0.0/guides/ingress/configuration/loadbalance-algorithm)
  - [Using Custom HAProxy Templates](/docs/9.0.0/guides/ingress/configuration/custom-templates)
  - [Using Additional Configuration Files](/docs/9.0.0/guides/ingress/configuration/config-volumes)
  - [Using HTTP/2 and gRPC](/docs/9.0.0/guides/ingress/configuration/http-2)
- Security
  - [Configure Basic Auth for HTTP Backends](/docs/9.0.0/guides/ingress/security/basic-auth)
  - [Configure External Auth for HTTP Backends](/docs/9.0.0/guides/ingress/security/oauth)
  - [TLS Authentication](/docs/9.0.0/guides/ingress/security/tls-auth)
- Monitoring
  - [Exposing HAProxy Stats](/docs/9.0.0/guides/ingress/monitoring/haproxy-stats)
- [Scaling Ingress](/docs/9.0.0/guides/ingress/scaling)
- [Placement of Ingress Pods](/docs/9.0.0/guides/ingress/pod-placement)
