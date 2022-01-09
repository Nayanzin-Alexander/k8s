# Kubernetes tutorials

## Installation 
https://phoenixnap.com/kb/install-minikube-on-ubuntu

## Basics
https://kubernetes.io/docs/tutorials/kubernetes-basics/

## Get the memory and CPU settings with the vboxmanage command
```
vboxmanage showvminfo minikube | grep "Memory size\|Number of CPUs"
```

## [Basics](https://minikube.sigs.k8s.io/docs/start/)
```
minikube start --memory 8192 --cpus 2
```