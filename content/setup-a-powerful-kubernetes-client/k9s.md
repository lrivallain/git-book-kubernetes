---
title: k9s
weight: 10
---

K9s is a terminal based UI to interact with your Kubernetes clusters. The aim
of this project is to make it easier to navigate, observe and manage your
deployed applications in the wild.

K9s continually watches Kubernetes for changes and offers subsequent commands to interact with your observed resources.

## CLI installation

```bash
curl -L https://github.com/derailed/k9s/releases/download/v0.24.2/k9s_Linux_x86_64.tar.gz | tar -xz
chmod +x k9s && sudo mv ./k9s /usr/local/bin/k9s
k9s version
```

### Skin

Apply a pre-defined skin to the output:

```bash
mkdir -p ~/.k9s
curl -L https://raw.githubusercontent.com/derailed/k9s/master/skins/one_dark.yml > ~/.k9s/skin.yml
# or
curl -L https://raw.githubusercontent.com/derailed/k9s/master/skins/solarized_dark.yml > ~/.k9s/skin.yml
```

![Example of Octant UI](/images/powerfull-client/k9s.png)