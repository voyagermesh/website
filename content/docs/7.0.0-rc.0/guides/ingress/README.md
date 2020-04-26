---
title: Ingress | Voyager
menu:
  docs_7.0.0-rc.0:
    identifier: readme-ingress
    name: Readme
    parent: ingress-guides
    weight: -1
product_name: voyager
menu_name: docs_7.0.0-rc.0
section_menu_id: guides
url: /docs/7.0.0-rc.0/guides/ingress/
aliases:
- /docs/7.0.0-rc.0/guides/ingress/README/
info:
  version: 7.0.0-rc.0
---

# Guides

Guides show you how to use Voyager as a Kubernetes Ingress controller.

- HTTP
  - [Exposing Service via Ingress](/docs/7.0.0-rc.0/guides/ingress/http/single-service)
  - [Virtual Hosting](/docs/7.0.0-rc.0/guides/ingress/http/virtual-hosting)
  - [Supports Loadbalancer Source Range](/docs/7.0.0-rc.0/guides/ingress/http/source-range)
  - [URL and Request Header Re-writing](/docs/7.0.0-rc.0/guides/ingress/http/rewrite-rules)
  - [Enable CORS](/docs/7.0.0-rc.0/guides/ingress/http/cors)
  - [Custom HTTP Port](/docs/7.0.0-rc.0/guides/ingress/http/custom-http-port)
  - [Using External Service as Ingress Backend](/docs/7.0.0-rc.0/guides/ingress/http/external-svc)
  - [HSTS](/docs/7.0.0-rc.0/guides/ingress/http/hsts)
  - [Forward Traffic to StatefulSet Pods](/docs/7.0.0-rc.0/guides/ingress/http/statefulset-pod)
  - [Configure Sticky session to Backends](/docs/7.0.0-rc.0/guides/ingress/http/sticky-session)
  - [Blue Green Deployments using weighted Loadbalancing](/docs/7.0.0-rc.0/guides/ingress/http/blue-green-deployment)
- TLS/SSL
  - [TLS Termination](/docs/7.0.0-rc.0/guides/ingress/tls/overview)
  - [Backend TLS](/docs/7.0.0-rc.0/guides/ingress/tls/backend-tls)
  - [Supports AWS certificate manager](/docs/7.0.0-rc.0/guides/ingress/tls/aws-cert-manager)
- TCP
  - [TCP LoadBalancing](/docs/7.0.0-rc.0/guides/ingress/tcp/overview)
  - [TCP SNI](/docs/7.0.0-rc.0/guides/ingress/tcp/tcp-sni)
- Configuration
  - [Customize generated HAProxy config via BackendRule](/docs/7.0.0-rc.0/guides/ingress/configuration/backend-rule) (can be used for [http rewriting](https://www.haproxy.com/doc/aloha/7.0/haproxy/http_rewriting.html), add [health checks](https://www.haproxy.com/doc/aloha/7.0/haproxy/healthchecks.html), etc.)
  - [Apply Frontend Rules](/docs/7.0.0-rc.0/guides/ingress/configuration/frontend-rule)
  - [Supported Annotations](/docs/7.0.0-rc.0/guides/ingress/configuration/annotations)
  - [Specify NodePort](/docs/7.0.0-rc.0/guides/ingress/configuration/node-port)
  - [Configure global options](/docs/7.0.0-rc.0/guides/ingress/configuration/default-options)
  - [Configure Custom Timeouts for HAProxy](/docs/7.0.0-rc.0/guides/ingress/configuration/default-timeouts)
  - [Using Custom HAProxy Templates](/docs/7.0.0-rc.0/guides/ingress/configuration/custom-templates)
- Security
  - [Configure Basic Auth for HTTP Backends](/docs/7.0.0-rc.0/guides/ingress/security/basic-auth)
  - [Configure External Auth for HTTP Backends](/docs/7.0.0-rc.0/guides/ingress/security/oauth)
  - [TLS Authentication](/docs/7.0.0-rc.0/guides/ingress/security/tls-auth)
- Monitoring
  - [Exposing HAProxy Stats](/docs/7.0.0-rc.0/guides/ingress/monitoring/stats)
- [Scaling Ingress](/docs/7.0.0-rc.0/guides/ingress/scaling)
- [Placement of Ingress Pods](/docs/7.0.0-rc.0/guides/ingress/pod-placement)
