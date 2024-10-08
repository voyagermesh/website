---
title: Profiling Voyager operator
menu:
  docs_v2024.8.30:
    identifier: operator-stats-profiling
    name: Profiling Voyager operator
    parent: monitoring-ingress
    weight: 30
product_name: voyager
menu_name: docs_v2024.8.30
section_menu_id: guides
info:
  cli: v0.0.16
  installer: v2024.8.30
  version: v2024.8.30
---

> New to Voyager? Please start [here](/docs/v2024.8.30/concepts/overview).

# Profiling Voyager operator

Voyager operator serves [runtime profiling data](https://golang.org/pkg/net/http/pprof/) in the format expected by the pprof visualization tool on port `:8443`. The handled paths all begin with /debug/pprof/.

Follow the steps below to expose profiling data:

1. Give `system:anonymous` user access to `/debug/pprof/` paths. **This is not safe to do on a production cluster.**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: appscode:system:profiler
rules:
- nonResourceURLs: ["/debug/pprof/", "/debug/pprof/*"]
  verbs: ["get", "post"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: appscode:system:profiler
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: appscode:system:profiler
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: system:anonymous
```

```bash
$ kubectl auth reconcile -f docs/examples/monitoring/profiler.yaml
clusterrole.rbac.authorization.k8s.io "appscode:system:profiler" reconciled
clusterrolebinding.rbac.authorization.k8s.io "appscode:system:profiler" reconciled
```

2. Now, forward the port `:8443` to your workstation.

```
$ kubectl get pods -n voyager | grep voyager
voyager-operator-f89dcccdb-plvmt        1/1       Running   0          27m

$ kubectl port-forward -n voyager voyager-operator-f89dcccdb-plvmt 8443
Forwarding from 127.0.0.1:8443 -> 8443
Forwarding from [::1]:8443 -> 8443
```

3. Now, visit the url: https://127.0.0.1:8443/debug/pprof/

![operator-profiler](/docs/v2024.8.30/images/monitoring/operator-profiler.png)

To look at a 30-second CPU profile:

```bash
$ go tool pprof https+insecure://localhost:8443/debug/pprof/profile
Entering interactive mode (type "help" for commands, "o" for options)
(pprof) top10
(pprof) pdf
```

To look at the heap profile:

```bash
$ go tool pprof https+insecure://localhost:8443/debug/pprof/heap
(pprof) top10
(pprof) pdf
```

4. Once you are done, remove access to `system:anonymous` user.

```bash
$ kubectl delete -f docs/examples/monitoring/profiler.yaml
clusterrole.rbac.authorization.k8s.io "appscode:system:profiler" deleted
clusterrolebinding.rbac.authorization.k8s.io "appscode:system:profiler" deleted
```
