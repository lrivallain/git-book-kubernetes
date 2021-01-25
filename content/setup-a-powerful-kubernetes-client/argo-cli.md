---
title: Argo cli
weight: 99
date: 2021-01-24
---

{{% notice info %}}
If you need to use Argo from this client machine.
{{% /notice %}}

```bash
curl -sL https://github.com/argoproj/argo/releases/download/latest/argo-linux-amd64.gz | gunzip > argo
chmod +x argo && sudo mv ./argo /usr/local/bin/argo
argo version
```

## Configuration

```bash
# Argo namespace
export ARGO_NAMESPACE=argo

# Start port forwarding
kubectl -n $ARGO_NAMESPACE port-forward deployment/argo-server 2746:2746 &
# keep it running in bg; user the following command to get the job number:
jobs

# if needed: get it back in foreground:
fg 1
```
