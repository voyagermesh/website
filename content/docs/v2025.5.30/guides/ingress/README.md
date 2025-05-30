---
title: Ingress | Voyager
menu:
  docs_v2025.5.30:
    identifier: readme-ingress
    name: Readme
    parent: ingress-guides
    weight: -1
product_name: voyager
menu_name: docs_v2025.5.30
section_menu_id: guides
url: /docs/v2025.5.30/guides/ingress/
aliases:
- /docs/v2025.5.30/guides/ingress/README/
info:
  cli: v0.0.17
  installer: v2025.5.30
  version: v2025.5.30
---

# Guides

Guides show you how to use Voyager as a Kubernetes Ingress controller.

- HTTP
  - [Exposing Service via Ingress](/docs/v2025.5.30/guides/ingress/http/single-service)
  - [Virtual Hosting](/docs/v2025.5.30/guides/ingress/http/virtual-hosting)
  - [Supports Loadbalancer Source Range](/docs/v2025.5.30/guides/ingress/http/source-range)
  - [URL and Request Header Re-writing](/docs/v2025.5.30/guides/ingress/http/rewrite-rules)
  - [Enable CORS](/docs/v2025.5.30/guides/ingress/http/cors)
  - [Custom HTTP Port](/docs/v2025.5.30/guides/ingress/http/custom-http-port)
  - [Using External Service as Ingress Backend](/docs/v2025.5.30/guides/ingress/http/external-svc)
  - [HSTS](/docs/v2025.5.30/guides/ingress/http/hsts)
  - [Forward Traffic to StatefulSet Pods](/docs/v2025.5.30/guides/ingress/http/statefulset-pod)
  - [Configure Sticky session to Backends](/docs/v2025.5.30/guides/ingress/http/sticky-session)
  - [Blue Green Deployments using weighted Loadbalancing](/docs/v2025.5.30/guides/ingress/http/blue-green-deployment)
- TLS/SSL
  - [TLS Termination](/docs/v2025.5.30/guides/ingress/tls/overview)
  - [Multiple TLS Entries](/docs/v2025.5.30/guides/ingress/tls/multiple-tls)
  - [Backend TLS](/docs/v2025.5.30/guides/ingress/tls/backend-tls)
  - [Supports AWS certificate manager](/docs/v2025.5.30/guides/ingress/tls/aws-cert-manager)
- TCP
  - [TCP LoadBalancing](/docs/v2025.5.30/guides/ingress/tcp/overview)
  - [TCP SNI](/docs/v2025.5.30/guides/ingress/tcp/tcp-sni)
- Configuration
  - [Customize generated HAProxy config via BackendRule](/docs/v2025.5.30/guides/ingress/configuration/backend-rule) (can be used for [http rewriting](https://www.haproxy.com/doc/aloha/7.0/haproxy/http_rewriting.html), add [health checks](https://www.haproxy.com/doc/aloha/7.0/haproxy/healthchecks.html), etc.)
  - [Apply Frontend Rules](/docs/v2025.5.30/guides/ingress/configuration/frontend-rule)
  - [Supported Annotations](/docs/v2025.5.30/guides/ingress/configuration/annotations)
  - [Specify NodePort](/docs/v2025.5.30/guides/ingress/configuration/node-port)
  - [Configure global options](/docs/v2025.5.30/guides/ingress/configuration/default-options)
  - [Configure Custom Timeouts for HAProxy](/docs/v2025.5.30/guides/ingress/configuration/default-timeouts)
  - [Configure Load balancing algorithm](/docs/v2025.5.30/guides/ingress/configuration/loadbalancing-algorithm)
  - [Using Custom HAProxy Templates](/docs/v2025.5.30/guides/ingress/configuration/custom-templates)
  - [Using Additional Configuration Files](/docs/v2025.5.30/guides/ingress/configuration/config-volumes)
  - [Using HTTP/2 and gRPC](/docs/v2025.5.30/guides/ingress/configuration/http-2)
- Security
  - [Configure Basic Auth for HTTP Backends](/docs/v2025.5.30/guides/ingress/security/basic-auth)
  - [Configure External Auth for HTTP Backends](/docs/v2025.5.30/guides/ingress/security/oauth)
  - [TLS Authentication](/docs/v2025.5.30/guides/ingress/security/tls-auth)
- Monitoring
  - [Exposing HAProxy Stats](/docs/v2025.5.30/guides/ingress/monitoring/haproxy-stats)
- [Scaling Ingress](/docs/v2025.5.30/guides/ingress/scaling)
- [Placement of Ingress Pods](/docs/v2025.5.30/guides/ingress/pod-placement)
- [Avoid 503 with Graceful Server Shutdown](/docs/v2025.5.30/guides/ingress/graceful-reload)