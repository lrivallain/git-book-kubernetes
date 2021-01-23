---
title: Monitoring with Prometheus
weight: 2
---

The [kube-prometheus](https://github.com/prometheus-operator/kube-prometheus) project collects Kubernetes manifests,
Grafana dashboards, and Prometheus rules combined with documentation and scripts to provide easy to operate end-to-end
Kubernetes cluster monitoring with Prometheus using the Prometheus Operator.

```bash
git clone https://github.com/prometheus-operator/kube-prometheus.git /tmp/kube-prometheus
cd /tmp/kube-prometheus
# create the namespace and CRDs
kubectl create -f manifests/setup
# wait for them to be availble
until kubectl get servicemonitors --all-namespaces ; do date; sleep 1; echo ""; done
# create the remaining resources
kubectl create -f manifests/
```

## Port-forward method to access dashboard

```bash
# Prometheus on https://127.0.0.1:9090
kubectl --namespace monitoring port-forward --address 0.0.0.0 svc/prometheus-k8s 9090

# Grafana with user:password admin:admin on https://127.0.0.1:3000
kubectl --namespace monitoring port-forward --address 0.0.0.0 svc/grafana 3000

# Alert Manager on http://127.0.0.1:9093
kubectl --namespace monitoring port-forward --address 0.0.0.0 svc/alertmanager-main 9093
```

## Ingress access to dashboards

The following section will explain how you can expose the 3 previously created dashboards through a simple `ingress` configuration with a basic authentication.

### DNS records

Create DNS records for 3 new hosts with a `CNAME` type and target on the endpoint of your Kubernetes cluster. For example:

* `alert.vlab.lcl`
* `prometheus.vlab.lcl`
* `grafana.vlab.lcl`

### Authentication

```bash
# To get `htpasswd` tool
sudo apt install apache2-utils -y

# Create an auth file with data for user "admin"
htpasswd -c ./users admin # you will be prompted for password and confirmation

# If needed, add other user(s) to the file with **almost** the same command:
htpasswd ./users otheradmin

# Create a secret named `admin-auth`
kubectl create secret generic admin-auth --from-file users --namespace=monitoring
```

### Deploy an ingress based on Traefik

{{% notice note %}}
If needed, please apply content from the *Traefik* section to prepare Ingress controller.
{{% /notice %}}

Download the `kube-prometheus-ingress-traefik.yaml` attached file, customized with your DNS records and apply it:

{{%attachments title="Related files" style="grey" pattern="kube-prometheus-ingress-traefik.yaml"/%}}

```bash
kubectl apply -f kube-prometheus-ingress-traefik.yaml
```

### Test access from ingress

Following commands provide a quick way to test the behavior of deployed ingress:

```bash
# Show ingress status
kubectl describe ingress grafana-gateway-ingress --namespace=monitoring

# Test your access without authentication
curl http://grafana.vlab.lcl -Is | head -n 1
# Outpout: HTTP/1.1 401 Unauthorized

# Test your access with authentication
curl http://grafana.vlab.lcl -u 'admin:*****' -Is | head -n 1
# Outpout: HTTP/1.1 200 OK
```
