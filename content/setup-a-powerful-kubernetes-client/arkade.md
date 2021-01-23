---
title: Arkade
weight: 2
---

[Arkade](https://github.com/alexellis/arkade) is a great open-source Kubernetes *"market-place"* project initiated by [@alexellis](https://github.com/alexellis).

The `arkade` CLI provides a simple method to download your favourite devops CLIs and install helm charts, with a single command.

```bash
# Note: you can also run without `sudo` and move the binary yourself
curl -sLS https://dl.get-arkade.dev | sudo sh

# Test
arkade --help
```

## Install a CLI tool

```bash
# List available CLI tools
arkade get

# Example:
arkade get yq
```

## Install a K8S app

```bash
# List available apps
arkade install / --help

# Example: kubernetes-dashboard
arkade install kubernetes-dashboard
```