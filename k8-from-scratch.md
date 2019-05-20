# Installing Kubernetes from Scratch on Ubuntu 18.10

## Installing Master Nodes

master-1 IP

### Required Components

For a fully functional master server or control plane, we will need the following compontents:

* API Server --> kube-apiserver
* Controller Manager/Replication Controller --> kube-controller-manager
* Scheduler --> kube-scheduler
* Key/Value Store --> etcd

### Adding The Repos

## Installing Worker Nodes

node-1 IP 
node-2 IP

### Required Components

For a worker node we are in need of the following parts:

* Container Runtime --> docker
* Pod Starter --> kubelet
* Network Router --> kube-proxy
* Network Addon/CNI --> flannel

## Installing kubectl
