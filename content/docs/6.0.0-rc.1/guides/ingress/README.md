---
title: Ingress | Voyager
menu:
  docs_6.0.0-rc.1:
    identifier: readme-ingress
    name: Readme
    parent: ingress-guides
    weight: -1
product_name: voyager
menu_name: docs_6.0.0-rc.1
section_menu_id: guides
url: /docs/6.0.0-rc.1/guides/ingress/
aliases:
- /docs/6.0.0-rc.1/guides/ingress/README/
info:
  version: 6.0.0-rc.1
---

# Guides

Guides show you how to use Voyager as a Kubernetes Ingress controller.

- HTTP
  - [Exposing Service via Ingress](/docs/6.0.0-rc.1/guides/ingress/http/single-service)
  - [Virtual Hosting](/docs/6.0.0-rc.1/guides/ingress/http/virtual-hosting)
  - [Supports Loadbalancer Source Range](/docs/6.0.0-rc.1/guides/ingress/http/source-range)
  - [URL and Request Header Re-writing](/docs/6.0.0-rc.1/guides/ingress/http/rewrite-rules)
  - [Enable CORS](/docs/6.0.0-rc.1/guides/ingress/http/cors)
  - [Custom HTTP Port](/docs/6.0.0-rc.1/guides/ingress/http/custom-http-port)
  - [Using External Service as Ingress Backend](/docs/6.0.0-rc.1/guides/ingress/http/external-svc)
  - [HSTS](/docs/6.0.0-rc.1/guides/ingress/http/hsts)
  - [Forward Traffic to StatefulSet Pods](/docs/6.0.0-rc.1/guides/ingress/http/statefulset-pod)
  - [Configure Sticky session to Backends](/docs/6.0.0-rc.1/guides/ingress/http/sticky-session)
  - [Blue Green Deployments using weighted Loadbalancing](/docs/6.0.0-rc.1/guides/ingress/http/blue-green-deployment)
- TLS/SSL
  - [TLS Termination](/docs/6.0.0-rc.1/guides/ingress/tls/overview)
  - [Backend TLS](/docs/6.0.0-rc.1/guides/ingress/tls/backend-tls)
  - [Supports AWS certificate manager](/docs/6.0.0-rc.1/guides/ingress/tls/aws-cert-manager)
- TCP
  - [TCP LoadBalancing](/docs/6.0.0-rc.1/guides/ingress/tcp/overview)
- Configuration
  - [Customize generated HAProxy config via BackendRule](/docs/6.0.0-rc.1/guides/ingress/configuration/backend-rule) (can be used for [http rewriting](https://www.haproxy.com/doc/aloha/7.0/haproxy/http_rewriting.html), add [health checks](https://www.haproxy.com/doc/aloha/7.0/haproxy/healthchecks.html), etc.)
  - [Apply Frontend Rules](/docs/6.0.0-rc.1/guides/ingress/configuration/frontend-rule)
  - [Supported Annotations](/docs/6.0.0-rc.1/guides/ingress/configuration/annotations)
  - [Specify NodePort](/docs/6.0.0-rc.1/guides/ingress/configuration/node-port)
  - [Configure global options](/docs/6.0.0-rc.1/guides/ingress/configuration/default-options)
  - [Configure Custom Timeouts for HAProxy](/docs/6.0.0-rc.1/guides/ingress/configuration/default-timeouts)
  - [Using Custom HAProxy Templates](/docs/6.0.0-rc.1/guides/ingress/configuration/custom-templates)
- Security
  - [Configure Basic Auth for HTTP Backends](/docs/6.0.0-rc.1/guides/ingress/security/basic-auth)
  - [TLS Authentication](/docs/6.0.0-rc.1/guides/ingress/security/tls-auth)
- Monitoring
  - [Exposing HAProxy Stats](/docs/6.0.0-rc.1/guides/ingress/monitoring/stats)
- [Scaling Ingress](/docs/6.0.0-rc.1/guides/ingress/scaling)
- [Placement of Ingress Pods](/docs/6.0.0-rc.1/guides/ingress/pod-placement)
