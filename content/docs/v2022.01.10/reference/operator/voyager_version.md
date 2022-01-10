---
title: Voyager Version
menu:
  docs_v2022.01.10:
    identifier: voyager-version
    name: Voyager Version
    parent: reference-operator
product_name: voyager
menu_name: docs_v2022.01.10
section_menu_id: reference
info:
  cli: v0.0.5
  installer: v2022.01.10
  version: v2022.01.10
---

## voyager version

Prints binary version number.

```
voyager version [flags]
```

### Options

```
      --check string   Check version constraint
  -h, --help           help for version
      --short          Print just the version number.
```

### Options inherited from parent commands

```
      --bypass-validating-webhook-xray   if true, bypasses validating webhook xray checks
      --enable-analytics                 Send analytical events to Google Analytics (default true)
      --use-kubeapiserver-fqdn-for-aks   if true, uses kube-apiserver FQDN for AKS cluster to workaround https://github.com/Azure/AKS/issues/522 (default true)
```

### SEE ALSO

* [voyager](/docs/v2022.01.10/reference/operator/voyager)	 - Voyager by AppsCode - Secure L7/L4 Ingress Controller for Kubernetes
