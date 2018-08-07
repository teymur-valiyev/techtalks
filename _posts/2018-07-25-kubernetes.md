---
author: teymur
comments: true
date: 2019-04-09 00:00:00+00:00
layout: post
slug: kubernetes
title: Kubernetes
categories: Tutorial
tags:
- kubernetes
---

## Kubernetes

writter in Go/GOlang

Borg -> Omega -> Kubernetes

k8s

Big picture

Masters
Nodes
Pods
Services
Deloyments


## Masters 

master free for looking after cluster

###  kube-apiserver
front-end to the control plane
Exposes The API
Consumes JSON via mainfest file

### Cluster store
Persistent storage
Cluster state and config
Uses etcd

### Controller
Controller of controllers
Node Controller
Endpoint controller
Namespace controller

Watches for changes

### kube-scheduler
Watchers apiserver for new pods
Assigns work for nodes



## Nodes
* Kublet 
	The main kubernetes agent  
	Registers node with cluster
	Watches apiserver
	Instantiates pods
	Reports back to master

/spec
/healthz
/pods

* Container Engine 
	Pulling image
	Starting/stopping containers

Pluggable
* Usally Docker
* Can be rkt

* kube-proxy
	kubernetes networking
	Pod Ip addresses
	All containers in a pod share a single IP

pods in inside of Node

## Declaratice Model & Desired State

Declaratice Model - we give manifest file (what we want)

Desired State - 

## Pods

kubernetes runs container inside of pods

pods can have multiple containers 

All containers in pod share the pod environment


unit of scale is pods

scale will add pods replicas

Pods exists in single Node

every time new pod


## Services
ip resolver for pods

### label 
server load balance by lables

send trafic only to healthy pods

random loadbalancing by default
default TPC


## Deloyments
tell to cluster what things look like 

----------------------------------------

 
## Minikube

kubectl - kubernetes client

minikube start

kubectl config current-context
kubectl get nodes

minikube stop
minikube delete

kubeadm
kubelet

minikube dashboard














