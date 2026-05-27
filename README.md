# onprem-setup-k8s


### Setting Up the Cluster


### 1. Configure Network Prerequisites
This step enables IPv4 forwarding and ensures that iptables sees bridged traffic.

The overlay module is required for Docker to support the overlay network driver,

while the br_netfilter module is necessary for Kubernetes to enable network

filtering and NAT (Network Address Translation).

For more details, refer to the Kubernetes documentation.

Run the following commands on all nodes

```
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF
```
```
sudo modprobe overlay
sudo modprobe br_netfilter
```
```
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
EOF
```
```
sudo sysctl --system
```

#### Verify the modules are loaded:
```
lsmod | grep overlay
lsmod | grep br_netfilter
```

#### Ensure the system variables are correctly set:
```
sysctl net.bridge.bridge-nf-call-iptables net.bridge.bridge-n f-call-ip6tables net.ipv4.ip_forward
```
#### Expected output:
```
et.bridge.bridge-nf-call-iptables = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward = 1
```

### 2. Configure Container Runtime
Kubernetes 1.28 requires a Container Runtime Interface (CRI)-compliant runtime.

We will use containerd .

For more details, refer to the Kubernetes documentation.
```

```

