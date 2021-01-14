---
title: Initial master node
weight: 2
---
The following section will explain how to deploy the initial master node of
the k3s cluster.

### Install `kubectl` CLI tool

In order to test and manage the k3s cluster, it could be useful to have a `kubectl` cli install in the master nodes:

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# Test it
kubectl version --client
```

#### Auto-complete

Use the following commands to add auto-completion to your bash shell for the `kubectl` command \(or it's `k` alias\)

```bash
echo 'source <(kubectl completion bash)' >>~/.bashrc
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -F __start_kubectl k' >>~/.bashrc
```

### Deploy

```bash
# Deploy a new k3s master node
curl -sfL https://get.k3s.io | sh -
```

### Configuration file

```bash
# enable read for other users
sudo chmod 644 /etc/rancher/k3s/k3s.yaml
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```

You can test the connection to the cluster by listing the deployed _pods_ and the list of _nodes_ in the cluster \(only one will be listed by now\):

```bash
kubectl get pods --all-namespaces
kubectl get nodes
```

### Retrieve the cluster token

This token will be used to join the other nodes to the current k3s deployment:

```bash
sudo cat /var/lib/rancher/k3s/server/node-token
```

### \(optional\) Proxy declaration

If you are in a corporate-proxy situation, you can specify it in the Kubernetes deployment by deploying the following _configMap_:

{% code title="proxy.yaml" %}
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: lab-proxy
  labels:
    app: proxy
data:
  HTTPS_PROXY: http://X.X.X.X:8080
  HTTP_PROXY: http://X.X.X.X:8080
  NO_PROXY: .vlab.lcl,192.168.0.0/16,127.0.0.1,localhost
```
{% endcode %}

```bash
kubectl apply -f proxy.yaml
```
