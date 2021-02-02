---
title: Kubectl tips
weight: 1
date: 2021-02-01
---

This page will gather some tips to use [`kubectl`](/setup-a-powerful-kubernetes-client/basics/) in a more effective way.

## Watch resources status change

`kubectl` have a useful feature to monitor the changes in the status of a resource. For example, when you deploy a *pod*, there are multiple status before `Running` (See [Pod Lifecycle documentation](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)). 

Using the `--watch/-w` option for a `get` command, enable to watch continuously the status changes of resources:

```bash
# Will provide a new line for each status change in the pods list
kubectl get <resource-type> --watch  # long format
kubectl get <resource-type> -w       # short format
```

## More and more details

The following commands will provide you more and more details about a specific resource.

```bash
# get resource items names only
kubectl get <resource-type> -o name
# list resource items
kubectl get <resource-type>
# display labels
kubectl get <resource-type> --show-labels
# list resource items with more details
kubectl get <resource-type> -o wide
# get a specific resource item
kubectl get <resource-type> <resource-name>
# get a specific resource item with more details
kubectl describe <resource-type> <resource-name>
# yaml export
kubectl get <resource-type> <resource-name> -o yaml
# json export
kubectl get <resource-type> <resource-name> -o json
```

## Troubelshooting

You can use `kubectl` to troubleshoot your clusters, deployments or other resources.

```bash
# Monitor pod metrics
kubectl top pod <pod-name>
# Monitor node metrics
kubectl top node <node-name>

# Look at pod's logs
kubectl logs -f <pod-name>
# Look at a specific pod's container logs
kubectl logs -f <pod-name> -c <container>

# Mark node as unschedulable
kubectl cordon <node-name>
# Empty node in preparation for maintenance
kubectl drain <node-name>

# Cluster info
kubectl cluster-info
# Dump cluster state
kubectl cluster-info dump --output-directory=/tmp/dump.txt

# Config
kubectl config view
```


## Pod interractions

Interact with your pods with the following commands:

```bash
# Run an interactive pod
kubectl run -i --tty busybox --image=busybox -- sh
# Attach to an existing pod
kubectl attach <pod-name> -i
# or
kubectl exec --stdin --tty <pod-name> -- /bin/sh
# Exec a single command in a pod (single container pod)
kubectl exec <pod-name> -- ls /
# Exec a single command in a pod (multi container pod)
kubectl exec <pod-name> -c <container> -- ls /

# Forward port 6000 from the pod to local machine port 5000
kubectl port-forward <pod-name> 5000:6000
# Forward port 6000 from the pod to machine port 5000
kubectl port-forward --address 0.0.0.0 <pod-name> 5000:6000
```

## All !

Use following commands to list (all) resources from (all) namespace(s):

```bash
# List resource-type items from all namespaces
kubectl get <resource-type> -A
# List all resources in current context
kubectl get all
# List all resources from all namespaces
kubectl get all -A
```