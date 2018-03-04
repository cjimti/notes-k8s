# Kubernetes

Getting started with Kubernetes for local development. I develop on a
Mac however much of this is easily translated to windows. 

The following is essentially a getting started guide wrapped around my
personal development notes. This is also for my co-workers in helping them get
up to speed quickly. If you see an error feel free make a pull request or just
add an issue.

## Deeper Reading and Resources

- [Intro to Kubernetes Workshop](https://github.com/kelseyhightower/intro-to-kubernetes-workshop)
- [Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)
For anyone planning to support a production Kubernetes cluster and wants to understand how everything fits together.



## Prerequisites

- Install [Virtualbox](https://www.virtualbox.org/)
- Install [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- Install [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/#install-minikube)

## Test Installation

```bash
$ minikube addons list

# enable heapster for cpu and mem
$ minikube addons enable heapster

# open the dashboard
$ minikube dashboard

```

## Try a few commands

Run a "hello world" using example echoserver

```bash

# get a list of commands
$ kubectl run --help

# run a hellow world echo server
$ kubectl run hello-minikube --image=gcr.io/google_containers/echoserver:1.4 --port=8080

deployment "hello-minikube" created

# expose the node's port
$ kubectl expose deployment hello-minikube --type=NodePort

service "hello-minikube" exposed

# get the url
$ minikube service hello-minikube --url

http://192.168.99.100:31923

```

