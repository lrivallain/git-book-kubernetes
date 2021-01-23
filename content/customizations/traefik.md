---
title: Traefik as ingress controler
weight: 1
---

{{% notice note %}}
As mentionned on [Traefik website](https://traefik.io/): *Traefik is an open-source Edge Router that makes publishing your services a fun and easy experience.*
{{% /notice %}}

It could be used as a powerfull Ingress controler to handle incoming requests on the cluster and forward them to the appropriate service.

## Installation

```bash
helm repo add traefik https://helm.traefik.io/traefik
helm repo update
helm install traefik traefik/traefik
```

## Test it

Get the `whoami.yaml` file form the bellow attachement files, then:

{{%attachments title="Related files" style="grey" pattern="whoami.yaml"/%}}

```bash
# Deploy it
kubectl apply -f ./whoami.yaml

# Run a test command
curl -i http://k3s.vlab.lcl -H "Host: mydomain.com"

# Output:
HTTP/1.1 200 OK
Content-Length: 406
Content-Type: text/plain; charset=utf-8
Date: Fri, 22 Jan 2021 14:59:46 GMT

Hostname: whoami-app-7564dd9695-dtzrh
IP: 127.0.0.1
IP: ::1
IP: 10.42.2.6
IP: fe80::f099:c3ff:fe3e:7071
RemoteAddr: 10.42.1.6:46964
GET / HTTP/1.1
Host: mydomain.com
User-Agent: curl/7.68.0
Accept: */*
Accept-Encoding: gzip
X-Forwarded-For: 10.42.0.8
X-Forwarded-Host: mydomain.com
X-Forwarded-Port: 80
X-Forwarded-Proto: http
X-Forwarded-Server: traefik-79fdc967bf-5nkxt
X-Real-Ip: 10.42.0.8
```

Here we simulate a DNS record `mydomain.com` by using the `Host` HTTP header. It provides a easy way to make a test but of course, for a real service, a DNS record is mandatory.

## Expose the dashboard

It is possible to expose both Traefik UI dashboard and API through Traefik itself.

Get the `dashboard.yaml` file from below attachements. Before applying, ensure that the content fits your needs, especially the *host* specified as a matching criteria.

{{%attachments title="Related files" style="grey" pattern="dashboard.yaml"/%}}

### Create a secret for basic-authentication

```bash
# To get `htpasswd` tool
sudo apt install apache2-utils -y

# Create an auth file with data for user "admin"
htpasswd -c ./users admin # you will be prompted for password and confirmation

# If needed, add other user(s) to the file with **almost** the same command:
htpasswd ./users otheradmin

# Deploy the file as a new secret
kubectl create secret generic admin-auth --from-file users --namespace=default
```

### Deploy the dashboard IngressRoute

```bash
# Deploy it
kubectl apply -f ./dashboard.yaml

# Test it:
curl -I -X GET http://lb.vlab.lcl/dashboard/ | head -n1
# Output: HTTP/1.1 401 Unauthorized

curl -Is -X GET http://lb.vlab.lcl/dashboard/ -u 'admin:*****' | head -n 1
# Output: HTTP/1.1 200 OK
```

Now, you probably can reach: http://lb.vlab.lcl/dashboard/# from your favorite web brower.

![Traefik dashboard](/images/customizations/traefik-dashboard.png)