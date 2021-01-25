---
title: Octant
weight: 50
date: 2021-01-24
---

Octant is a tool for developers to understand how applications run on a
Kubernetes cluster.

{{% notice note %}}
It aims to be part of the developer's toolkit for gaining insight and approaching complexity found in Kubernetes. Octant offers a combination of introspective tooling, cluster navigation, and object management along with a plugin system to further extend its capabilities.
{{% /notice %}}

## Installation

```bash
curl -L https://github.com/vmware-tanzu/octant/releases/download/v0.16.3/octant_0.16.3_Linux-64bit.deb > /tmp/octant.deb
dpkg -i /tmp/octant.deb

# To run and access octant from http://localhost:7777
octant

# To remotly run and access octant:
OCTANT_LISTENER_ADDR=X.X.X.X:7777 OCTANT_ACCEPTED_HOSTS=Y.Y.Y.Y octant --disable-open-browser
```

![Example of Octant UI](/images/powerfull-client/octant.png)