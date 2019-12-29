# Gerencie seu cluster Kubernetes com Cockpit

![Cockpit Project](./img/logo.png)

### Requisitos

### Cluster com 03 servers
#### k8s-master - Centos 7 - 2vCPU - 8GBram - 10GB Disco
#### k8s-worker1 - Centos 7 - 2vCPU - 8GBram - 10GB Disco
#### k8s-worker2 - Centos 7 - 2vCPU - 8GBram - 10GB Disco

```
# yum update -y && yum upgrade -y && yum -y install epel-release net-tools wget curl
```
```
# curl -fsSL https://get.docker.com | bash
```
```
# systemctl enable docker && systemctl start docker && systemctl status docker
```
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
```
```
# setenforce 0
```
```
# systemctl stop firewalld
```
```
# systemctl disable firewalld
```
```
# yum install -y kubelet kubeadm kubectl
```
```
# systemctl enable kubelet && systemctl start kubelet && systemctl status kubelet
```

```
# vi /etc/sysctl.conf

net.bridge.bridge-nf-call-ip6tables = 1

net.bridge.bridge-nf-call-iptables = 1
```
```
# sysctl --system
```
```
# modprobe br_netfilter
```
```
# echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables
```
```
# vi /etc/sysconfig/kubelet
```
```
KUBELET_EXTRA_ARGS=cgroup-driver=cgroupfs
```
```
# systemctl daemon-reload
```
```
# systemctl restart kubelet
```
```
# swapoff -a
```
```
# vi /etc/fstab
```
```
# kubeadm init
```
```
# mkdir -p $HOME/.kube
```
```
# sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
```
```
# sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
```
# kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```
```
# kubectl get pods -n kube-system
```
```
# kubectl get nodes
```
```
# yum install -y cockpit cockpit-networkmanager cockpit-dashboard cockpit-storaged cockpit-packagekit cockpit-docker cockpit-kubernetes cockpit-machines cockpit-sosreport cockpit-selinux cockpit-kdump cockpit-subscriptions cockpit-pcp
```

```
# systemctl start cockpit && systemctl enable cockpit.socket 
```

Para acessar nossa interface web: <ip_do_servidor>:9090




