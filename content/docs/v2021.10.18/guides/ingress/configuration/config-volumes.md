---
title: Configuration Volumes
menu:
  docs_v2021.10.18:
    identifier: config-volumes
    name: Configuration Volumes
    parent: config-ingress
    weight: 10
product_name: voyager
menu_name: docs_v2021.10.18
section_menu_id: guides
info:
  cli: v0.0.3
  installer: v2021.10.18
  version: v2021.10.18
---

> New to Voyager? Please start [here](/docs/v2021.10.18/concepts/overview).

# Configuration Volumes

You might want to provide additional files to the haproxy container and use them in the haproxy configuration. For example, specifying a CA file for verifying backend server. Using voyager, you can mount additional files from secrets/configmaps by configuring `spec.configVolumes`.  

Note that, when `spec.configVolumes` is used, operator will skip the validation for generated haproxy configuration.

## Example: Backend Server Verification

First create demo namespace for this example.

```
$ kubectl create namespace demo
namespace/demo created
```

### Deploy Test Server

Deploy a TLS enabled test server.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    run: test-server
  name: test-server
  namespace: demo
spec:
  selector:
    matchLabels:
      run: test-server
  template:
    metadata:
      labels:
        run: test-server
    spec:
      containers:
      - image: appscode/test-server:2.3
        name: test-server
        args:
        - --ca
        imagePullPolicy: Always
---
apiVersion: v1
kind: Service
metadata:
  labels:
    run: test-server
  name: test-server
  namespace: demo
  annotations:
    ingress.appscode.com/backend-tls: ssl ca-file /tmp/ca/ca.pem
spec:
  ports:
  - port: 6443
    targetPort: 6443
    name: https
  selector:
    run: test-server
```

Here, using `ingress.appscode.com/backend-tls` annotation we have specified the path of CA file. HAProxy will use this CA file to verify the backend server. So, we need to provide the CA file inside the haproxy-container in path `/tmp/ca/ca.pem`. 

### Create Secret

If you use your own backend server, you might already have the CA file. Run following commands to get the CA file of the test-server used in this example.

```
$ kubectl get pods -n demo -l run=test-server
NAME                           READY   STATUS    RESTARTS   AGE
test-server-64855d98cc-7bfpr   1/1     Running   0          74s
$ kubectl exec -it -n demo test-server-64855d98cc-7bfpr cat cert.pem > ca.pem
```

Now, create a secret using the CA file.

```
$ kubectl create secret generic ca-secret -n demo --from-file=ca.pem
secret/ca-secret created
```

### Create Ingress

Create the ingress and specify the secret in `spec.configVolumes`.

```yaml
apiVersion: voyager.appscode.com/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: demo
spec:
  configVolumes:
  - name: ca-vol
    secret:
      secretName: ca-secret
    mountPath: /tmp/ca
  rules:
  - host: "ssl.appscode.test"
    http:
      paths:
      - path: /apis
        backend:
          service:
            name: test-server
            port:
              number: 6443
```

### Generated haproxy.cfg

```ini
# HAProxy configuration generated by https://github.com/appscode/voyager
# DO NOT EDIT!
global
  daemon
  stats socket /var/run/haproxy.sock level admin expose-fd listeners
  server-state-file global
  server-state-base /var/state/haproxy/
  # log using a syslog socket
  log /dev/log local0 info
  tune.ssl.default-dh-param 2048
  ssl-default-bind-ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!3DES:!MD5:!PSK
  lua-load /etc/auth-request.lua
  hard-stop-after 30s
defaults
  log global
  # https://cbonte.github.io/haproxy-dconv/1.7/configuration.html#4.2-option%20abortonclose
  # https://github.com/voyagermesh/voyager/pull/403
  option dontlognull
  option http-server-close
  # Timeout values
  timeout client 50s
  timeout client-fin 50s
  timeout connect 5s
  timeout server 50s
  timeout tunnel 50s
  # Configure error files
  # default traffic mode is http
  # mode is overwritten in case of tcp services
  mode http
frontend http-0_0_0_0-80
  bind *:80  
  mode http
  option httplog
  option forwardfor
  acl is_proxy_https hdr(X-Forwarded-Proto) https
  acl is_proxy_https ssl_fc
  http-request set-var(req.scheme) str(https) if is_proxy_https
  http-request set-var(req.scheme) str(http) if ! is_proxy_https
  acl acl_ssl.appscode.test hdr(host) -i ssl.appscode.test
  acl acl_ssl.appscode.test hdr(host) -i ssl.appscode.test:80
  acl acl_ssl.appscode.test:apis path_beg /apis
  use_backend test-server.demo:6443 if acl_ssl.appscode.test acl_ssl.appscode.test:apis
backend test-server.demo:6443
  server pod-test-server-64855d98cc-7bfpr 172.17.0.5:6443     ssl ca-file /tmp/ca/ca.pem
```

### Check Response

```bash
$ minikube service --url voyager-test-ingress -n demo
http://192.168.99.100:32598

$ curl -H "Host: ssl.appscode.test" 'http://192.168.99.100:32598/apis'
{"type":"http","host":"ssl.appscode.test","serverPort":":6443","path":"/apis","method":"GET","headers":{"Accept":["*/*"],"Connection":["close"],"User-Agent":["curl/7.58.0"],"X-Forwarded-For":["172.17.0.1"]}}
```

Note that, in this example, `curl` connects with HAProxy in no-tls mode, but HAProxy connects with backend server in tls mode.

### Cleanup

```
$ kubectl delete ns demo
namespace "demo" deleted
```
