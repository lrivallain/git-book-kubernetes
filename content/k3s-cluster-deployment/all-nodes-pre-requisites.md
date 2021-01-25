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
