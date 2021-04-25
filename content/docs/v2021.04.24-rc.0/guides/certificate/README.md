---
title: Certificate | Voyager
menu:
  docs_v2021.04.24-rc.0:
    identifier: readme-certificate
    name: Readme
    parent: certificate-guides
    weight: -1
product_name: voyager
menu_name: docs_v2021.04.24-rc.0
section_menu_id: guides
url: /docs/v2021.04.24-rc.0/guides/certificate/
aliases:
- /docs/v2021.04.24-rc.0/guides/certificate/README/
info:
  installer: v2021.04.24-rc.0
  version: v2021.04.24-rc.0
---

# Guides

Guides show you how to use Voyager's built-in certificate manager to issue free TLS/SSL certificates from Let's Encrypt.

## Features
- Provision free TLS certificates (including wildcard certificates) from Let's Encrypt.
- Manage certificates declaratively using a Kubernetes Custom Resource Definition (CRD).
- Domain validation using ACME http-01 and dns-01 challenges.
- Support for many popular [DNS providers](/docs/v2021.04.24-rc.0/guides/certificate/dns/providers).
- Auto Renew certificates.
- Use issued certificates with Ingress to secure communications.

## Next Steps
- [Issue Let's Encrypt certificate using HTTP-01 challenge](/docs/v2021.04.24-rc.0/guides/certificate/http/overview)
- DNS-01 challenge providers
  - [Issue Let's Encrypt certificate using AWS Route53](/docs/v2021.04.24-rc.0/guides/certificate/dns/route53)
  - [Issue Let's Encrypt certificate using Google Cloud DNS](/docs/v2021.04.24-rc.0/guides/certificate/dns/google-cloud)
  - [Supported DNS Challenge Providers](/docs/v2021.04.24-rc.0/guides/certificate/dns/providers)
- [Deleting Certificate](/docs/v2021.04.24-rc.0/guides/certificate/delete)
- [Frequently Asked Questions](/docs/v2021.04.24-rc.0/guides/certificate/faq)
