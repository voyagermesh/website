---
title: Voyager Kloader Run
menu:
  docs_5.0.0:
    identifier: voyager-kloader-run
    name: Voyager Kloader Run
    parent: reference
product_name: voyager
menu_name: docs_5.0.0
section_menu_id: reference
info:
  version: 5.0.0
---

## voyager kloader run

Run and hold kloader

### Synopsis

Run and hold kloader

```
voyager kloader run [flags]
```

### Options

```
  -b, --boot-cmd string          Bash script that will be run on every change of the file
      --burst int                The maximum burst for throttle (default 1000000)
  -c, --configmap string         Configmap name that needs to be mount
  -h, --help                     help for run
      --kubeconfig string        Path to kubeconfig file with authorization information (the master location is set by the master flag).
      --master string            The address of the Kubernetes API server (overrides any value in kubeconfig)
  -m, --mount-location string    Volume location where the file will be mounted
      --qps float32              The maximum QPS to the master from this client (default 1e+06)
      --resync-period duration   If non-zero, will re-list this often. Otherwise, re-list will be delayed aslong as possible (until the upstream source closes the watch or times out. (default 5m0s)
  -s, --secret string            Secret name that needs to be mount
```

### Options inherited from parent commands

```
      --alsologtostderr                  log to standard error as well as files
      --analytics                        Send analytical events to Google Analytics (default true)
      --log.format logFormatFlag         Set the log target and format. Example: "logger:syslog?appname=bob&local=7" or "logger:stdout?json=true" (default "logger:stderr")
      --log.level levelFlag              Only log messages with the given severity or above. Valid levels: [debug, info, warn, error, fatal] (default "info")
      --log_backtrace_at traceLocation   when logging hits line file:N, emit a stack trace (default :0)
      --log_dir string                   If non-empty, write log files in this directory
      --logtostderr                      log to standard error instead of files
      --stderrthreshold severity         logs at or above this threshold go to stderr (default 2)
  -v, --v Level                          log level for V logs
      --vmodule moduleSpec               comma-separated list of pattern=N settings for file-filtered logging
```

### SEE ALSO

* [voyager kloader](/docs/5.0.0/reference/voyager_kloader)	 - Reloads HAProxy when configmap changes

