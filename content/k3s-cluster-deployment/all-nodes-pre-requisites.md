---
title: All nodes pre-requisites
weight: 1
date: 2021-01-24
---
## Network configuration

```bash
# Network setup
vi /etc/netplan/50-cloud-init.yaml
netplan apply
```

## Software pre-requisites

```bash
# Upgrade packages
sudo apt update
sudo apt upgrade -y

# Install software pre-requisites
sudo apt-get install python3-pip gcc nfs-common -y
```

## NTP time

```bash
sudo apt-get install ntp -y
# check configured servers in:
sudo vi /etc/ntp.conf
# restart services if needed:
sudo /etc/init.d/ntp restart
# check ntp status:
ntpq -p
```

## \(_optionnal_\) proxy configuration

Use the following commands if you need to use a corporate HTTP proxy server to reach Internet based resources: 

```bash
# Proxy setup
echo "HTTP_PROXY=X.X.X.X:8080
HTTPS_PROXY=X.X.X.X:8080
NO_PROXY=.vlab.lcl,192.168.0.0/16,127.0.0.1,localhost" >> /etc/environment
export HTTP_PROXY="X.X.X.X:8080"
export HTTPS_PROXY="X.X.X.X:8080"
export NO_PROXY=".vlab.lcl,192.168.0.0/16,127.0.0.1,localhost"
echo "Acquire::http::proxy \"http://X.X.X.X:8080\";" >> /etc/apt/apt.conf

# Test
curl https://google.com
```
