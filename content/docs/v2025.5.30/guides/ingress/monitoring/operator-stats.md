---
title: Monitoring Voyager operator
menu:
  docs_v2025.5.30:
    identifier: operator-stats-monitoring
    name: Monitoring Voyager operator
    parent: monitoring-ingress
    weight: 25
product_name: voyager
menu_name: docs_v2025.5.30
section_menu_id: guides
info:
  cli: v0.0.17
  installer: v2025.5.30
  version: v2025.5.30
---

> New to Voyager? Please start [here](/docs/v2025.5.30/concepts/overview).

# Monitoring Voyager operator

Voyager operator exposes Prometheus ready metrics via the following endpoints on port `:8443`:

- `/metrics`: Scrape this to monitor operator.

Follow the steps below to view the metrics:

1. Give `system:anonymous` user access to `/metrics` url. **This is not safe to do on a production cluster.**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: appscode:system:metrics-collector
rules:
- nonResourceURLs: ["/metrics"]
  verbs: ["get"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: appscode:system:metrics-collector
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: appscode:system:metrics-collector
subjects:
- apiGroup: rbac.authorization.k8s.io
  kind: User
  name: system:anonymous
```

```bash
$ kubectl auth reconcile -f docs/examples/monitoring/metrics-collector.yaml
clusterrole.rbac.authorization.k8s.io "appscode:system:metrics-collector" reconciled
clusterrolebinding.rbac.authorization.k8s.io "appscode:system:metrics-collector" reconciled
```

2. Now, forward the port `:8443` to your workstation.

```
$ kubectl get pods -n voyager | grep voyager
voyager-operator-f89dcccdb-plvmt        1/1       Running   0          27m

$ kubectl port-forward -n voyager voyager-operator-f89dcccdb-plvmt 8443
Forwarding from 127.0.0.1:8443 -> 8443
Forwarding from [::1]:8443 -> 8443
```

3. Now, visit the url: https://127.0.0.1:8443/metrics

![operator-metrics](/docs/v2025.5.30/images/monitoring/operator-metrics.png)

4. Once you are done, remove access to `system:anonymous` user.

```bash
$ kubectl delete -f docs/examples/monitoring/metrics-collector.yaml
clusterrole.rbac.authorization.k8s.io "appscode:system:metrics-collector" deleted
clusterrolebinding.rbac.authorization.k8s.io "appscode:system:metrics-collector" deleted
```
