---
title: Additional master nodes
weight: 4
---

The following section will explain how to join additional master nodes to your
k3s deployment.

{{% notice note %}}
To run K3s in this mode, you must have an **odd** number of server nodes.
{{% /notice %}}

First of all, you will need to get the cluster token, as explained in the previous section and the master node _fqdn_.

## Deploy k3s to join an existing cluster

```bash

curl -sfL https://get.k3s.io | \
    K3S_URL="https://k3s-mstr-01.vlab.lcl:6443" \
    K3S_TOKEN="K10d1...fe537::server:26a92...e34f9" \
    INSTALL_K3S_EXEC="server" \
    sh - --no-deploy=traefik
```

## Check

From the master node or any client device with access to the Kubernetes cluster, ensure that the node is now added to the cluster:

```bash
kubectl get nodes

# Output:
NAME          STATUS   ROLES                       AGE     VERSION
k3s-mstr-01   Ready    control-plane,etcd,master   4m25s   v1.20.2+k3s1
k3s-mstr-02   Ready    control-plane,etcd,master   3m33s   v1.20.2+k3s1
k3s-mstr-03   Ready    control-plane,etcd,master   2m27s   v1.20.2+k3s1
```
