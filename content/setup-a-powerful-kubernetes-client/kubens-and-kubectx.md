---
title: kubens & kubectx
weight: 10
date: 2021-01-24
---

{{% notice info %}}
Thanks to [@ahmetb](https://github.com/ahmetb): [https://github.com/ahmetb/kubectx](https://github.com/ahmetb/kubectx)
{{% /notice %}}

* `kubectx`is a utility to manage and switch between kubectl **contexts**.
* `kubens`is a utility to switch between Kubernetes **namespaces**.

```bash
sudo git clone https://github.com/ahmetb/kubectx /opt/kubectx
sudo ln -s /opt/kubectx/kubectx /usr/local/bin/kubectx
sudo ln -s /opt/kubectx/kubens /usr/local/bin/kubens
```

Then you can easly switch both `context` and `namespace` by:

```bash
kubectx # list contexts
kubectx <name> # switch context

kubens # list namespace
kubens <name> # switch namespace
```
