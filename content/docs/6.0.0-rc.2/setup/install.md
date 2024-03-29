---
title: Install Voyager
description: Voyager Install
menu:
  docs_6.0.0-rc.2:
    identifier: install-voyager
    name: Install
    parent: setup
    weight: 10
product_name: voyager
menu_name: docs_6.0.0-rc.2
section_menu_id: setup
info:
  version: 6.0.0-rc.2
---

# Installation Guide

## Using YAML

Voyager can be installed via installer script included in the [/hack/deploy](https://github.com/appscode/voyager/tree/6.0.0-rc.2/hack/deploy) folder.

```console
# provider=acs
# provider=aws
# provider=azure
# provider=baremetal
# provider=gce
# provider=gke
# provider=minikube
# provider=openstack

$ curl -fsSL https://raw.githubusercontent.com/appscode/voyager/6.0.0-rc.2/hack/deploy/voyager.sh | bash -s -- -h
voyager.sh - install voyager operator

voyager.sh [options]

options:
-h, --help                         show brief help
-n, --namespace=NAMESPACE          specify namespace (default: kube-system)
-p, --provider=PROVIDER            specify a cloud provider
    --rbac                         create RBAC roles and bindings (default: true)
    --docker-registry              docker registry used to pull voyager images (default: appscode)
    --image-pull-secret            name of secret used to pull voyager operator images
    --restrict-to-namespace        restrict voyager to its own namespace
    --run-on-master                run voyager operator on master
    --enable-admission-webhook     configure admission webhook for Voyager CRDs
    --template-cfgmap=CONFIGMAP    name of configmap with custom templates

$ curl -fsSL https://raw.githubusercontent.com/appscode/voyager/6.0.0-rc.2/hack/deploy/voyager.sh \
    | bash -s -- --provider=$provider
```

If you would like to run Voyager operator pod in `master` instances, pass the `--run-on-master` flag:

```console
$ curl -fsSL https://raw.githubusercontent.com/appscode/voyager/6.0.0-rc.2/hack/deploy/voyager.sh \
    | bash -s -- --provider=$provider --run-on-master [--rbac]
```

Voyager operator will be installed in a `kube-system` namespace by default. If you would like to run Voyager operator pod in `voyager` namespace, pass the `--namespace=voyager` flag:

```console
$ kubectl create namespace voyager
$ curl -fsSL https://raw.githubusercontent.com/appscode/voyager/6.0.0-rc.2/hack/deploy/voyager.sh \
    | bash -s -- --provider=$provider --namespace=voyager [--run-on-master] [--rbac]
```

By default, Voyager operator will watch Ingress objects in any namespace. If you would like to restrict Voyager to Ingress and Services in its own namespace, pass the `--restrict-to-namespace` flag:

```console
$ kubectl create namespace voyager
$ curl -fsSL https://raw.githubusercontent.com/appscode/voyager/6.0.0-rc.2/hack/deploy/voyager.sh \
    | bash -s -- --provider=$provider --restrict-to-namespace [--namespace=voyager] [--run-on-master] [--rbac]
```

If you are using a private Docker registry, you need to pull the following 2 docker images:

 - [appscode/voyager](https://hub.docker.com/r/appscode/voyager)
 - [appscode/haproxy](https://hub.docker.com/r/appscode/haproxy)

To pass the address of your private registry and optionally a image pull secret use flags `--docker-registry` and `--image-pull-secret` respectively.

```console
$ kubectl create namespace voyager
$ curl -fsSL https://raw.githubusercontent.com/appscode/voyager/6.0.0-rc.2/hack/deploy/voyager.sh \
    | bash -s -- --provider=$provider --docker-registry=MY_REGISTRY [--image-pull-secret=SECRET_NAME] [--rbac]
```

Voyager implements a [validating admission webhook](https://kubernetes.io/docs/admin/admission-controllers/#validatingadmissionwebhook-alpha-in-18-beta-in-19) to validate Voyager CRDs. This is enabled by default for Kubernetes 1.9.0 or later releases. To disable this feature, pass the `--enable-admission-webhook=false` flag.

```console
$ curl -fsSL https://raw.githubusercontent.com/appscode/voyager/6.0.0-rc.2/hack/deploy/voyager.sh \
    | bash -s -- --provider=$provider --enable-admission-webhook [--rbac]
```

## Using Helm

Voyager can be installed via [Helm](https://helm.sh/) using the [chart](https://github.com/appscode/voyager/tree/6.0.0-rc.2/chart/stable/voyager) included in this repository or from official charts repository. To install the chart with the release name `my-release`:

```console
# Mac OSX amd64:
curl -fsSL -o onessl https://github.com/kubepack/onessl/releases/download/0.1.0/onessl-darwin-amd64 \
  && chmod +x onessl \
  && sudo mv onessl /usr/local/bin/

# Linux amd64:
curl -fsSL -o onessl https://github.com/kubepack/onessl/releases/download/0.1.0/onessl-linux-amd64 \
  && chmod +x onessl \
  && sudo mv onessl /usr/local/bin/

# Linux arm64:
curl -fsSL -o onessl https://github.com/kubepack/onessl/releases/download/0.1.0/onessl-linux-arm64 \
  && chmod +x onessl \
  && sudo mv onessl /usr/local/bin/

# Kubernetes 1.8.x
$ helm repo update
$ helm install stable/voyager --name my-release --set cloudProvider=$provider

# Kubernetes 1.9.0 or later
$ helm repo update
$ helm install stable/voyager --name my-release \
  --set cloudProvider=$provider \
  --set apiserver.ca="$(onessl get kube-ca)" \
  --set apiserver.enableAdmissionWebhook=true
```

To see the detailed configuration options, visit [here](https://github.com/appscode/voyager/tree/6.0.0-rc.2/chart/stable/voyager).

### Installing in GKE Cluster

If you are installing Voyager on a GKE cluster, you will need cluster admin permissions to install Voyager operator. Run the following command to grant admin permision to the cluster.

```console
kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=google-email-for-gce-project
```

### Installing in Minikube

Voyager can be used in minikube using `--provider=minikube`. In Minikube, a `LoadBalancer` type ingress will only assigned a NodePort.

### Installing in Baremetal Cluster

Voyager works great in baremetal cluster. To install, set `--provider=baremetal`. In baremetal cluster, `LoadBalancer` type ingress in not supported. You can use [NodePort](/docs/6.0.0-rc.2/concepts/ingress-types/nodeport), [HostPort](/docs/6.0.0-rc.2/concepts/ingress-types/hostport) or [Internal](/docs/6.0.0-rc.2/concepts/ingress-types/internal) ingress objects.


## Verify installation
To check if Voyager operator pods have started, run the following command:

```console
$ kubectl get pods --all-namespaces -l app=voyager --watch
```

Once the operator pods are running, you can cancel the above command by typing `Ctrl+C`.

Now, to confirm CRD groups have been registered by the operator, run the following command:

```console
$ kubectl get crd -l app=voyager
```

Now, you are ready to create your first ingress using Voyager.


## Configuring RBAC
Voyager creates two CRDs: `Ingress` and `Certificate`. Voyager installer will create 2 user facing cluster roles:

| ClusterRole           | Aggregates To | Desription                            |
|-----------------------|---------------|---------------------------------------|
| appscode:voyager:edit | admin, edit   | Allows edit access to Voyager CRDs, intended to be granted within a namespace using a RoleBinding. |
| appscode:voyager:view | view          | Allows read-only access to Voyager CRDs, intended to be granted within a namespace using a RoleBinding. |

These user facing roles supports [ClusterRole Aggregation](https://kubernetes.io/docs/admin/authorization/rbac/#aggregated-clusterroles) feature in Kubernetes 1.9 or later clusters.


## Using kubectl
Since Voyager uses its own TPR/CRD, you need to use full resource kind to find it with kubectl.

```console
# List all voyager ingress
$ kubectl get ingress.voyager.appscode.com --all-namespaces

# List voyager ingress for a namespace
$ kubectl get ingress.voyager.appscode.com -n <namespace>

# Get Ingress YAML
$ kubectl get ingress.voyager.appscode.com -n <namespace> <ingress-name> -o yaml

# Describe Ingress. Very useful to debug problems.
$ kubectl describe ingress.voyager.appscode.com -n <namespace> <ingress-name>
```


## Detect Voyager version
To detect Voyager version, exec into the operator pod and run `voyager version` command.

```console
$ POD_NAMESPACE=kube-system
$ POD_NAME=$(kubectl get pods -n $POD_NAMESPACE -l app=voyager -o jsonpath={.items[0].metadata.name})
$ kubectl exec -it $POD_NAME -n $POD_NAMESPACE voyager version

Version = 6.0.0-rc.2
VersionStrategy = tag
Os = alpine
Arch = amd64
CommitHash = ab0b38d8f5d5b4b4508768a594a9d98f2c76abd8
GitBranch = release-4.0
GitTag = 6.0.0-rc.2
CommitTimestamp = 2017-10-08T12:45:26
```
