---
title: Configure Ingress Annotations
menu:
  docs_8.0.0:
    identifier: annotations-configuration
    name: Annotations
    parent: config-ingress
    weight: 1
product_name: voyager
menu_name: docs_8.0.0
section_menu_id: guides
info:
  version: 8.0.0
---

> New to Voyager? Please start [here](/docs/8.0.0/concepts/overview).

# Configure ingress with annotations

Below is the full list of supported annotations:

|  Keys  |   Value   |  Default |
|--------|-----------|----------|
| [ingress.appscode.com/type](/docs/8.0.0/concepts/README) | LoadBalancer, HostPort, NodePort, Internal | `LoadBalancer` |
| [ingress.appscode.com/api-schema](/docs/8.0.0/concepts/overview) | {APIGroup}/{APIVersion} | `voyager.appscode.com/v1beta1` |
| [ingress.appscode.com/accept-proxy](/docs/8.0.0/guides/ingress/configuration/accept-proxy) | bool | `false` |
| [ingress.appscode.com/affinity](/docs/8.0.0/guides/ingress/http/sticky-session) | `cookie` | |
| [ingress.appscode.com/session-cookie-hash](/docs/8.0.0/guides/ingress/http/sticky-session) | string | |
| [ingress.appscode.com/session-cookie-name](/docs/8.0.0/guides/ingress/http/sticky-session) | string | `SERVERID` |
| [ingress.appscode.com/hsts](/docs/8.0.0/guides/ingress/http/hsts) | bool | `true` |
| [ingress.appscode.com/hsts-include-subdomains](/docs/8.0.0/guides/ingress/http/hsts) | bool | `false` |
| [ingress.appscode.com/hsts-max-age](/docs/8.0.0/guides/ingress/http/hsts) | string | `15768000` |
| [ingress.appscode.com/hsts-preload](/docs/8.0.0/guides/ingress/http/hsts) | bool | `false` |
| [ingress.appscode.com/use-node-port](/docs/8.0.0/concepts/ingress-types/nodeport) | bool | `false` |
| [ingress.appscode.com/enable-cors](/docs/8.0.0/guides/ingress/http/cors) | bool | `false` |
| [ingress.appscode.com/cors-allow-headers](/docs/8.0.0/guides/ingress/http/cors) | string | `DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Authorization` |
| [ingress.appscode.com/cors-allow-methods](/docs/8.0.0/guides/ingress/http/cors) | string | `GET,PUT,POST,DELETE,PATCH,OPTIONS` |
| [ingress.appscode.com/cors-allow-origin](/docs/8.0.0/guides/ingress/http/cors) | string | `*` |
| [ingress.appscode.com/default-option](/docs/8.0.0/guides/ingress/configuration/default-options) | map | `{"http-server-close": "true", "dontlognull": "true"}` |
| [ingress.appscode.com/default-timeout](/docs/8.0.0/guides/ingress/configuration/default-timeouts) | map | `{"connect": "50s", "server": "50s", "client": "50s", "client-fin": "50s", "tunnel": "50s"}` |
| [ingress.appscode.com/auth-type](/docs/8.0.0/guides/ingress/security/basic-auth) | `basic` | |
| [ingress.appscode.com/auth-realm](/docs/8.0.0/guides/ingress/security/basic-auth) | string | |
| [ingress.appscode.com/auth-secret](/docs/8.0.0/guides/ingress/security/basic-auth) | string | |
| [ingress.appscode.com/auth-tls-error-page](/docs/8.0.0/guides/ingress/security/tls-auth) | string | |
| [ingress.appscode.com/auth-tls-secret](/docs/8.0.0/guides/ingress/security/tls-auth) | string | |
| [ingress.appscode.com/auth-tls-verify-client](/docs/8.0.0/guides/ingress/security/tls-auth) | `required` or, `optional` | `required` |
| [ingress.appscode.com/backend-tls](/docs/8.0.0/guides/ingress/tls/backend-tls) | string | |
| [ingress.appscode.com/replicas](/docs/8.0.0/guides/ingress/scaling) | int | `1` |
| [ingress.appscode.com/backend-weight](/docs/8.0.0/guides/ingress/http/blue-green-deployment) | int | |
| [ingress.appscode.com/whitelist-source-range](/docs/8.0.0/guides/ingress/configuration/whitelist) | string | |
| [ingress.appscode.com/max-connections](/docs/8.0.0/guides/ingress/configuration/max-connections) | int | |
| [ingress.appscode.com/ssl-redirect](/docs/8.0.0/guides/ingress/configuration/ssl-redirect) | bool | `true` |
| [ingress.appscode.com/force-ssl-redirect](/docs/8.0.0/guides/ingress/configuration/ssl-redirect) | bool | `false` |
| [ingress.appscode.com/limit-connection](/docs/8.0.0/guides/ingress/configuration/rate-limit) | int | |
| [ingress.appscode.com/limit-rpm](/docs/8.0.0/guides/ingress/configuration/rate-limit) | int | |
| [ingress.appscode.com/limit-rps](/docs/8.0.0/guides/ingress/configuration/rate-limit) | int | |
| [ingress.appscode.com/errorfiles](/docs/8.0.0/guides/ingress/configuration/error-files) | string | |
| [ingress.appscode.com/proxy-body-size](/docs/8.0.0/guides/ingress/configuration/body-size) | int | |
| [ingress.appscode.com/ssl-passthrough](/docs/8.0.0/guides/ingress/configuration/ssl-passthrough) | bool | `false` |
| [ingress.appscode.com/rewrite-target](/docs/8.0.0/guides/ingress/configuration/rewrite-target) | string | |
| [ingress.appscode.com/keep-source-ip](/docs/8.0.0/guides/ingress/configuration/keep-source-ip) | bool | `false` |
| [ingress.appscode.com/health-check-nodeport](/docs/8.0.0/guides/ingress/configuration/keep-source-ip) | int | |
| [ingress.appscode.com/load-balancer-ip](/docs/8.0.0/guides/ingress/configuration/loadbalancer-ip) | string | |
| [ingress.appscode.com/annotations-pod](/docs/8.0.0/guides/ingress/configuration/pod-annotations) | map | |
| [ingress.appscode.com/annotations-service](/docs/8.0.0/guides/ingress/configuration/service-annotations) | map | |
| [ingress.appscode.com/stats](/docs/8.0.0/guides/ingress/monitoring/haproxy-stats) | bool | `false` |
| [ingress.appscode.com/stats-port](/docs/8.0.0/guides/ingress/monitoring/haproxy-stats) | int | `56789` |
| [ingress.appscode.com/stats-secret-name](/docs/8.0.0/guides/ingress/monitoring/haproxy-stats) | string | |
| [ingress.appscode.com/monitoring-agent](/docs/8.0.0/guides/ingress/monitoring/using-coreos-prometheus-operator) | string  |         |
| [ingress.appscode.com/service-monitor-labels](/docs/8.0.0/guides/ingress/monitoring/using-coreos-prometheus-operator) | map     |         |
| [ingress.appscode.com/service-monitor-namespace](/docs/8.0.0/guides/ingress/monitoring/using-coreos-prometheus-operator) | string  |         |
| [ingress.appscode.com/service-monitor-endpoint-port](/docs/8.0.0/guides/ingress/monitoring/using-coreos-prometheus-operator) | integer | 56790   |
| [ingress.appscode.com/service-monitor-endpoint-scrape-interval](/docs/8.0.0/guides/ingress/monitoring/using-coreos-prometheus-operator) | string  |         |
| [ingress.appscode.com/use-dns-resolver](/docs/8.0.0/guides/ingress/http/external-svc#using-external-domain) | bool | `false` |
| [ingress.appscode.com/dns-resolver-nameservers](/docs/8.0.0/guides/ingress/http/external-svc#using-external-domain) | string | |
| [ingress.appscode.com/dns-resolver-check-health](/docs/8.0.0/guides/ingress/http/external-svc#using-external-domain) | bool | `true` |
| [ingress.appscode.com/dns-resolver-retries](/docs/8.0.0/guides/ingress/http/external-svc#using-external-domain) | int | `0` |
| [ingress.appscode.com/dns-resolver-timeout](/docs/8.0.0/guides/ingress/http/external-svc#using-external-domain) | map | |
| [ingress.appscode.com/dns-resolver-hold](/docs/8.0.0/guides/ingress/http/external-svc#using-external-domain) | map | |
| [ingress.appscode.com/workload-kind](/docs/8.0.0/guides/ingress/pod-placement#choosing-workload-kind) | string | `Deployment` |
| [ingress.appscode.com/node-selector](/docs/8.0.0/guides/ingress/pod-placement#using-node-selector) | map | |
| [ingress.appscode.com/tolerations](/docs/8.0.0/guides/ingress/pod-placement#using-taints-and-toleration) | array | |
| [ingress.appscode.com/check](/docs/8.0.0/guides/ingress/configuration/health-check) | bool | `false` |
| [ingress.appscode.com/check-port](/docs/8.0.0/guides/ingress/configuration/health-check) | int | |
