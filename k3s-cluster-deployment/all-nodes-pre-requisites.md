# All nodes pre-requisites

### Network configuration

```bash
# Network setup
vi /etc/netplan/50-cloud-init.yaml
netplan apply
```

### DNS resolver

This step enable the use of `systemd-resolved` in Ubuntu based distribution OS:

```bash
# Local DNS resolver for local fqdn
echo "192.168.2.4 k3s-mstr k3s-mstr.vlab..lcl" >> /etc/hosts
sudo service systemd-resolved stop
sudo rm -f /etc/resolv.conf
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf
sudo service systemd-resolved start
```

### Software pre-requisites

```bash
# Upgrade packages
sudo apt update
sudo apt upgrade -y

# Install software pre-requisites
sudo apt-get install python3-pip gcc nfs-common -y
```

### \(_optionnal_\) proxy configuration

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



