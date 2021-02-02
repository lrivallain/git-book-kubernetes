---
title: OpenFaaS CLI
weight: 99
date: 2021-01-24
---

{{% notice info %}}
If you need to use OpenFaaS from the client machine.
{{% /notice %}}

One-liner:

```bash
# openfaas-cli
curl -sSL https://cli.openfaas.com | sudo sh
```

## Configuration

```bash
# Set namespace
export OS_NS="openfaas"

# Get password
export OF_PASS=$(echo $(kubectl -n $OS_NS get secret basic-auth -o jsonpath="{.data.basic-auth-password}" | base64 --decode))
echo $OF_PASS

# Get URI
echo "export OPENFAAS_URL=http://"$(kubectl -n $OS_NS describe pods $(kubectl -n $OS_NS get pods | grep "gateway-" | awk '{print $1}') | grep "^Node:" | awk -F "/" '{print $2}')":31112"
```

## Login

```bash
echo $OF_PASS | faas-cli login --password-stdin
```
