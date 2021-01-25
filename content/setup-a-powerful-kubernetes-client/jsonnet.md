---
title: jsonnet
weight: 40
date: 2021-01-24
---

Jsonnet is a data templating language for app and tool developers

* Generate config data
* Side-effect free
* Organize, simplify, unify
* Manage sprawling config

```bash
# Update or install golang support
sudo apt install golang

# Expand PATH with `go get` binary folder
echo 'PATH="~/go/bin/:"$PATH' >> ~/.bashrc
. ~/.bashrc

# Install with go
go get github.com/google/go-jsonnet/cmd/jsonnet

# Test it
jsonnet --version
```

## gojsontoyaml

`jsonnet` provides *json* files but it is more easy to use *yaml* ones.
`gojsontoyaml` provide a simple way to convert the `jsonnet` result files to *yaml* ones.

```bash
# Install with go
go get github.com/brancz/gojsontoyaml

# Test if
echo "{'installed': true}" | gojsontoyaml
```