---
title: Voyager Export
menu:
  docs_v12.0.0-rc.2:
    identifier: voyager-export
    name: Voyager Export
    parent: reference
product_name: voyager
menu_name: docs_v12.0.0-rc.2
section_menu_id: reference
info:
  version: v12.0.0-rc.2
---

## voyager export

Export Prometheus metrics for HAProxy

### Synopsis

Export Prometheus metrics for HAProxy

```
voyager export [flags]
```

### Options

```
      --address string                        Address to listen on for web interface and telemetry. (default ":56790")
      --haproxy.server-metric-fields string   Comma-separated list of exported server metrics. See http://cbonte.github.io/haproxy-dconv/configuration-1.5.html#9.1 (default "2,3,4,5,6,7,8,9,13,14,15,16,17,18,21,24,33,35,38,39,40,41,42,43,44")
      --haproxy.timeout duration              Timeout for trying to get stats from HAProxy. (default 5s)
  -h, --help                                  help for export
      --kubeconfig string                     Path to kubeconfig file with authorization information (the master location is set by the master flag).
      --master string                         The address of the Kubernetes API server (overrides any value in kubeconfig)
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

* [voyager](/docs/v12.0.0-rc.2/reference/voyager)	 - Voyager by Appscode - Secure HAProxy Ingress Controller for Kubernetes

