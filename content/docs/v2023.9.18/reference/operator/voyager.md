---
title: Voyager
menu:
  docs_v2023.9.18:
    identifier: voyager
    name: Voyager
    parent: reference-operator
    weight: 0
product_name: voyager
menu_name: docs_v2023.9.18
section_menu_id: reference
url: /docs/v2023.9.18/reference/operator/
aliases:
- /docs/v2023.9.18/reference/operator/voyager/
info:
  cli: v0.0.14
  installer: v2023.9.18
  version: v2023.9.18
---

## voyager

Voyager by AppsCode - Secure L7/L4 Ingress Controller for Kubernetes

### Options

```
      --bypass-validating-webhook-xray   if true, bypasses validating webhook xray checks
      --enable-analytics                 Send analytical events to Google Analytics (default true)
  -h, --help                             help for voyager
      --use-kubeapiserver-fqdn-for-aks   if true, uses kube-apiserver FQDN for AKS cluster to workaround https://github.com/Azure/AKS/issues/522 (default true)
```

### SEE ALSO

* [voyager coordinator](/docs/v2023.9.18/reference/operator/voyager_coordinator)	 - Synchronizes HAProxy config
* [voyager init](/docs/v2023.9.18/reference/operator/voyager_init)	 - Initialize HAProxy config
* [voyager operator](/docs/v2023.9.18/reference/operator/voyager_operator)	 - Launch Voyager Ingress Operator
* [voyager run](/docs/v2023.9.18/reference/operator/voyager_run)	 - Launch Voyager Ingress Webhook Server
* [voyager version](/docs/v2023.9.18/reference/operator/voyager_version)	 - Prints binary version number.

