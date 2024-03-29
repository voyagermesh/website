---
title: Voyager Version
menu:
  docs_v13.0.0-beta.0:
    identifier: voyager-version
    name: Voyager Version
    parent: reference
product_name: voyager
menu_name: docs_v13.0.0-beta.0
section_menu_id: reference
info:
  version: v13.0.0-beta.0
---

## voyager version

Prints binary version number.

### Synopsis

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
      --alsologtostderr                  log to standard error as well as files
      --bypass-validating-webhook-xray   if true, bypasses validating webhook xray checks
      --enable-analytics                 Send analytical events to Google Analytics (default true)
      --log-flush-frequency duration     Maximum number of seconds between log flushes (default 5s)
      --log_backtrace_at traceLocation   when logging hits line file:N, emit a stack trace (default :0)
      --log_dir string                   If non-empty, write log files in this directory
      --logtostderr                      log to standard error instead of files
      --stderrthreshold severity         logs at or above this threshold go to stderr
      --use-kubeapiserver-fqdn-for-aks   if true, uses kube-apiserver FQDN for AKS cluster to workaround https://github.com/Azure/AKS/issues/522 (default true)
  -v, --v Level                          log level for V logs
      --vmodule moduleSpec               comma-separated list of pattern=N settings for file-filtered logging
```

### SEE ALSO

* [voyager](/docs/v13.0.0-beta.0/reference/voyager)	 - Voyager by Appscode - Secure HAProxy Ingress Controller for Kubernetes

