---
title: Setup a powerful Kubernetes client
type: docs
---

This section provides some tools and tricks to apply to a *nix based
workstation or jump server to have a powerful Kubernetes (and other tools)
client machine.

# Setup a powerful Kubernetes client

## Generic pre-requisites

We will need pip and gcc for some tools, so lets install them if needed:

```bash
sudo apt-get install python3-pip gcc -y
```

## Install `kubectl` CLI tool

In order to test and manage the k3s cluster, it could be useful to have a `kubectl` cli install in the master nodes:

```bash
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

# Test it
kubectl version --client
```

### `kubectl` auto-complete

Use the following commands to add auto-completion to your bash shell for the `kubectl` command \(or it's `k` alias\)

```bash
echo 'source <(kubectl completion bash)' >>~/.bashrc
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -F __start_kubectl k' >>~/.bashrc
```

## Heml

Easy peasy:

```text
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```