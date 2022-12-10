---
title: cert-manager | Voyager
menu:
  docs_v2022.12.11:
    identifier: readme-cert-manager
    name: Readme
    parent: cert-manager-guides
    weight: -1
product_name: voyager
menu_name: docs_v2022.12.11
section_menu_id: guides
url: /docs/v2022.12.11/guides/cert-manager/
aliases:
- /docs/v2022.12.11/guides/cert-manager/README/
info:
  cli: v0.0.11
  installer: v2022.12.11
  version: v2022.12.11
---

# Guides

Guides show you how to use [jetstack/cert-manager](https://github.com/jetstack/cert-manager) with Voyager to issue free TLS/SSL certificates from Let's Encrypt.

## Features

- Provision free TLS certificates (including wildcard certificates) from Let's Encrypt.
- Manage certificates declaratively using a Kubernetes Custom Resource Definition (CRD).
- Domain validation using ACME http-01 and dns-01 challenges.
- Support for many popular DNS providers.
- Auto Renew certificates.
- Use issued certificates with Ingress to secure communications.

## Next Steps

- [Issue Let's Encrypt certificate using HTTP-01 challenge](/docs/v2022.12.11/guides/cert-manager/http01_challenge/overview)
- DNS-01 challenge providers
  - [Issue Let's Encrypt certificate using AWS Route53](/docs/v2022.12.11/guides/cert-manager/dns01_challenge/aws-route53)
  - [Issue Let's Encrypt certificate using Azure DNS](/docs/v2022.12.11/guides/cert-manager/dns01_challenge/azure-dns)
  - [Issue Let's Encrypt certificate using Google Cloud DNS](/docs/v2022.12.11/guides/cert-manager/dns01_challenge/google-cloud-dns)
  - [Multiple Providers](/docs/v2022.12.11/guides/cert-manager/dns01_challenge/multiple-challenge-solver)
