---
title: Worker node(s)
weight: 3
---

The following section will explain how to join additional worker nodes to your
k3s deployment.

First of all, you will need to get the cluster token, as explained in the previous section and the master node _fqdn_.

## Deploy k3s to join an existing cluster

```bash
curl -sfL https://get.k3s.io | \
    K3S_URL="https://k3s-mstr.vlab.lcl:6443" \
    K3S_TOKEN="K10d1...fe537::server:26a92...e34f9" \
    sh -
```

## Check

From the master node or any client device with access to the Kubernetes cluster, ensure that the node is now added to the cluster:

```bash
kubectl get nodes
```
