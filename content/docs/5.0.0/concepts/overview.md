---
title: Overview | Voyager
menu:
  docs_5.0.0:
    identifier: overview-concepts
    name: Overview
    parent: concepts
    weight: 10
product_name: voyager
menu_name: docs_5.0.0
section_menu_id: concepts
info:
  version: 5.0.0
---

# Voyager
Voyager is a [HAProxy](http://www.haproxy.org/) backed [secure](#certificate) L7 and L4 [ingress](#ingress) controller for Kubernetes developed by
[AppsCode](https://appscode.com). This can be used with any Kubernetes cloud providers including aws, gce, gke, azure, acs. This can also be used with bare metal Kubernetes clusters.


## Ingress
Voyager provides L7 and L4 loadbalancing using a custom Kubernetes [Ingress](/docs/5.0.0/guides/ingress) resource. This is built on top of the [HAProxy](http://www.haproxy.org/) to support high availability, sticky sessions, name and path-based virtual hosting.
This also support configurable application ports with all the options available in a standard Kubernetes [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/).

- HTTP
  - [Exposing Service via Ingress](/docs/5.0.0/guides/ingress/http/single-service)
  - [Virtual Hosting](/docs/5.0.0/guides/ingress/http/virtual-hosting)
  - [Supports Loadbalancer Source Range](/docs/5.0.0/guides/ingress/http/source-range)
  - [URL and Request Header Re-writing](/docs/5.0.0/guides/ingress/http/rewrite-rules)
  - [Enable CORS](/docs/5.0.0/guides/ingress/http/cors)
  - [Custom HTTP Port](/docs/5.0.0/guides/ingress/http/custom-http-port)
  - [Using External Service as Ingress Backend](/docs/5.0.0/guides/ingress/http/external-svc)
  - [HSTS](/docs/5.0.0/guides/ingress/http/hsts)
  - [Forward Traffic to StatefulSet Pods](/docs/5.0.0/guides/ingress/http/statefulset-pod)
  - [Configure Sticky session to Backends](/docs/5.0.0/guides/ingress/http/sticky-session)
  - [Blue Green Deployments using weighted Loadbalancing](/docs/5.0.0/guides/ingress/http/blue-green-deployment)
- TLS/SSL
  - [TLS Termination](/docs/5.0.0/guides/ingress/tls/overview)
  - [Backend TLS](/docs/5.0.0/guides/ingress/tls/backend-tls)
  - [Supports AWS certificate manager](/docs/5.0.0/guides/ingress/tls/aws-cert-manager)
- TCP
  - [TCP LoadBalancing](/docs/5.0.0/guides/ingress/tcp/overview)
- Configuration
  - [Customize generated HAProxy config via BackendRule](/docs/5.0.0/guides/ingress/configuration/backend-rule) (can be used for [http rewriting](https://www.haproxy.com/doc/aloha/7.0/haproxy/http_rewriting.html), add [health checks](https://www.haproxy.com/doc/aloha/7.0/haproxy/healthchecks.html), etc.)
  - [Apply Frontend Rules](/docs/5.0.0/guides/ingress/configuration/frontend-rule)
  - [Supported Annotations](/docs/5.0.0/guides/ingress/configuration/annotations)
  - [Specify NodePort](/docs/5.0.0/guides/ingress/configuration/node-port)
  - [Configure global options](/docs/5.0.0/guides/ingress/configuration/default-options)
  - [Configure Custom Timeouts for HAProxy](/docs/5.0.0/guides/ingress/configuration/default-timeouts)
  - [Using Custom HAProxy Templates](/docs/5.0.0/guides/ingress/configuration/custom-templates)
- Security
  - [Configure Basic Auth for HTTP Backends](/docs/5.0.0/guides/ingress/security/basic-auth)
  - [TLS Authentication](/docs/5.0.0/guides/ingress/security/tls-auth)
- Monitoring
  - [Exposing HAProxy Stats](/docs/5.0.0/guides/ingress/monitoring/stats)
- [Scaling Ingress](/docs/5.0.0/guides/ingress/scaling)
- [Placement of Ingress Pods](/docs/5.0.0/guides/ingress/pod-placement)


## Certificate

Voyager can automagically provision and refresh SSL certificates issued from Let's Encrypt using a custom Kubernetes [Certificate](/docs/5.0.0/guides/certificate) resource.

- Provision free TLS certificates from Let's Encrypt,
- Manage issued certificates using a Kubernetes Third Party Resource,
- Domain validation using ACME dns-01 challenges,
- Support for multiple DNS providers,
- Auto Renew Certificates,
- Use issued Certificates with Ingress to Secure Communications.
