# [Kubernetes Tutorial for Beginners](https://www.youtube.com/watch?v=X48VuDVv0do&t=10645s)

## Basic K8S Components overview
* node - worker machine in K8S cluster
* pod - abstraction over a container (or few related containers)
* container - ready-to-run software package
* service - a static IP address attached to a Pods + load balancer
* virtual network - each pod on start obtains random IP address
* Ingress - route external requests to a service
* config-map - key value store shared across the pods
* secret - the same as config-map but only admins can see and modify the values
* volume - attaches physical storage to the pod (local or remote storage)
* deployment - specification of pod to be deployed on K8S. Specifies image-template, number of replicas, service, volumes etc
* stateful set - deployment for stateful applications. F.e. databases

## K8s architecture basics
* each node has multiple Pods on it
* Worker nodes processes:
    * Container runtime
    * Kubelet - starts the pod with container inside
    * Kube proxy - communication
* Master nodes processes:
  * API Server - allows to manage the K8S cluster
  * Scheduler - decides on which Node new Pod should be started
  * Controller manager - detects cluster state changes
  * etcd - distributed across all master nodes key-value store of a cluster state

## Minikube & kubectl
* minukube - one node cluster runs on virtual box or docker for development/testing purposes
* kubectl - command line tool to interact with K8S API service
```
minikube start --memory 8192 --cpus 3
kubectl get nodes
minikube status
minikube version
kubectl version
kubectl create deployment nginx-depl --image=nginx
kubectl get pod -o wide
kubectl get replicaset
kubectl get deployments
kubectl get deployment ${deployment-name} -o yaml
kubectl get services
kubectl create deployment mongo-depl --image=mongo
kubectl describe pod mongo-depl-5fd6b7d4b4-4pvkt
kubectl logs mongo-depl-5fd6b7d4b4-4pvkt
kubectl exec -i ${podname} -- bin/bash
kubectl exec -i mongo-depl-5fd6b7d4b4-4pvkt -- bin/bash
kubectl delete  deployment ${deployment-name}
```

## Yarn Configuration file n K8S
```
kubectl apply -f ./mongo
minikube service mongo-express-service
```

## Namespace
- Organise resources in namespace
- Virtual cluster inside a cluster
- > kubectl get namespace
  - default - default fot the resources if other namespace is specified
  - kube-node-lease - holds information about nodes availability
  - kube-public - publicly accessible data
  - kube-system - for system
  - kubernetes-dashboard - shipped with minikube
- Why to use namespaces?
  - helps to logically group related resources
  - helps to organize many teams, many configurations
  - Separate environments
  - Blue/green deployment
  - Limit access to the resources within a Namespace. Each team has separated environment
  - Limit CPU, RAM, Storage per Namespace
- > kubectl apply -f ${file} -n ${namespace}
  > kubectl get pod -n ${namespace}
```
apiVersion: v1
kind: Namespace
metadata:
name: <insert-namespace-name-here>
```
- set active namespace: 
  - install kubectx
  - > kubens # lists all namespaces
  - > kubens ${namespace} - set ${namespace} as default
  