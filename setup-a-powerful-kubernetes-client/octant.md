---
description: >-
  Octant is a tool for developers to understand how applications run on a
  Kubernetes cluster
---

# Octant

> It aims to be part of the developer's toolkit for gaining insight and approaching complexity found in Kubernetes. Octant offers a combination of introspective tooling, cluster navigation, and object management along with a plugin system to further extend its capabilities.

## Installation

```bash
curl -L https://github.com/vmware-tanzu/octant/releases/download/v0.16.3/octant_0.16.3_Linux-64bit.deb > /tmp/octant.deb
dpkg -i /tmp/octant.deb
OCTANT_LISTENER_ADDR=X.X.X.X:7777 OCTANT_ACCEPTED_HOSTS=Y.Y.Y.Y octant --disable-open-browser
```

Then go to [http://k3s-mstr.vlab.lcl:7777](http://k3s-mstr.vlab.lcl:7777).

