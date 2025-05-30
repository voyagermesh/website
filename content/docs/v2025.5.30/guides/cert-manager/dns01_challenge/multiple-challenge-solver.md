---
title: Multiple Solver Type
description: Multiple Solver Type
menu:
  docs_v2025.5.30:
    identifier: multiple-solver-type
    name: Multiple Solver Type
    parent: dns01-cert-manager
    weight: 15
product_name: voyager
menu_name: docs_v2025.5.30
section_menu_id: guides
info:
  cli: v0.0.17
  installer: v2025.5.30
  version: v2025.5.30
---

> New to Voyager? Please start [here](/docs/v2025.5.30/concepts/overview).

# Multiple Solver Type

A number of different DNS providers are supported for the ACME issuer. Below is a listing of available providers, their .yaml configurations, along with additional Kubernetes and provider specific notes regarding their usage.

- [ACME-DNS](https://docs.cert-manager.io/en/latest/tasks/issuers/setup-acme/dns01/acme-dns.html)
- [Akamai FastDNS](https://docs.cert-manager.io/en/latest/tasks/issuers/setup-acme/dns01/akamai.html)
- [AzureDNS](/docs/v2025.5.30/guides/cert-manager/dns01_challenge/azure-dns)
- [Cloudflare](https://docs.cert-manager.io/en/latest/tasks/issuers/setup-acme/dns01/cloudflare.html)
- [Google CloudDNS](/docs/v2025.5.30/guides/cert-manager/dns01_challenge/google-cloud-dns)
- [Amazon Route53](/docs/v2025.5.30/guides/cert-manager/dns01_challenge/aws-route53)
- [DigitalOcean](https://docs.cert-manager.io/en/latest/tasks/issuers/setup-acme/dns01/digitalocean.html)
- [RFC-2136](https://docs.cert-manager.io/en/latest/tasks/issuers/setup-acme/dns01/rfc2136.html)

Additionally, you can create only one Issuer/ClusterIssuer for each of http01 or dns01 challenge or even for 
multiple dns providers, like [this](/docs/v2025.5.30/examples/cert-manager/multiple.yaml):

```yaml
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: letsencrypt-staging-dns
  namespace: default
spec:
  acme:
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    email: example@kite.com
    # Name of a secret used to store the ACME account private key
    privateKeySecretRef:
      name: example-issuer-account-key
    solvers:
      - http01:
          ingress:
            name: test-ingress-deploy-k8s
      - dns01:
          route53:
            accessKeyID: KIR2WO5YWT
            region: us-east-1
            secretAccessKeySecretRef:
              name: route53-secret
              key: secret-access-key
            hostedZoneID: J13B3AB
      - dns01:
          azureDNS:
            # Service principal clientId (also called appId)
            clientID: riu478u-486ij8-uiu487j-468rjg8
            # A secretKeyRef to a service principal ClientSecret (password)
            clientSecretSecretRef:
              name: azuredns-secret
              key: client-secret
            # Azure subscription Id
            subscriptionID: 45ji8t4-rgi4859-g845jg-9jjf9945r
            # Azure AD tenant Id
            tenantID: 348585ej-4358fdg8-f4588fg-45889fg
            # ResourceGroup name where dns zone is provisioned
            resourceGroupName: dev
            hostedZoneName: appscode.info
      - dns01:
          cloudDNS:
            # A secretKeyRef to a google cloud json service account
            serviceAccountSecretRef:
              name: clouddns-service-account
              key: service-account.json
            # The project in which to update the DNS zone
            project: test-cert
```
