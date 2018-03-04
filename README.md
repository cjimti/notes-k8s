# Kubernetes

Getting started with Kubernetes for local development. I develop on a
Mac however much of this is easily translated to windows. 

The following is essentially a getting started guide wrapped around my
personal development notes. This is also for my co-workers in helping them get
up to speed quickly. If you see an error feel free make a pull request or just
add an issue.

## Deeper Reading and Resources

### Free Courses

- [Official Kubernetes Tutorials](https://kubernetes.io/docs/tutorials/)
- Udacity: [Scalable Microservices with Kubernetes](https://www.udacity.com/course/scalable-microservices-with-kubernetes--ud615)
- [Kubernetes The Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way)
For anyone planning to support a production Kubernetes cluster and wants to understand how everything fits together.

### Paid Courses
- Lynda: [Learning Kubernetes](https://www.lynda.com/Kubernetes-tutorials/Learning-Kubernetes/647663-2.html)
- Lynda: [Kubernetes: Native Tools](https://www.lynda.com/Kubernetes-tutorials/Kubernetes-Native-Tools/661764-2.html)
- Udemy: [Learn DevOps: The Complete Kubernetes Course](https://www.udemy.com/learn-devops-the-complete-kubernetes-course/learn/v4/content)
- Udemy: [Learn DevOps: Advanced Kubernetes Usage](https://www.udemy.com/learn-devops-advanced-kubernetes-usage)


## Prerequisites

- Install [Docker](https://store.docker.com/search?type=edition&offering=community)
- Install [Virtualbox](https://www.virtualbox.org/)
- Install [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- Install [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/#install-minikube)

## Test Installation

```bash
$ minikube version
minikube version: v0.25.0

$ minikube start
Starting local Kubernetes v1.9.0 cluster...
Starting VM...
Getting VM IP address...
Moving files into cluster...
Setting up certs...
Connecting to cluster...
Setting up kubeconfig...
Starting cluster components...
Kubectl is now configured to use the cluster.
Loading cached images from config file.

$ minikube addons list
- addon-manager: enabled
- coredns: disabled
- dashboard: enabled
- default-storageclass: enabled
- efk: disabled
- freshpod: disabled
- heapster: disabled
- ingress: disabled
- kube-dns: enabled
- registry: disabled
- registry-creds: disabled
- storage-provisioner: enabled


# enable heapster for cpu and mem
$ minikube addons enable heapster
heapster was successfully enabled

# open the dashboard (in browser)
$ minikube dashboard

```

## Get some status

```bash
# are we running a cluster?
$ kubectl cluster-info
Kubernetes master is running at https://192.168.99.100:8443

# we should have a minikube node
$ kubectl get nodes
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     <none>    2d        v1.9.0

```

### Architecture

Read [Kubernetes Basics] for a better understanding.

- A Cluster has Nodes
- A Node has Pods
- A Pod has (Docker in our case) containers and volumes

## Create a Deployment

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

## Useful Commands

Command | Description
------- | -----------
`kubectl get pod`              | Get information about all running pods
`kubectl describe pod <pod>`   | Describe one pod
`kubectl expose pod <pod> --port=2701 --name=api` | Expose the port of a pod (creates a new service)
`kubectl attach <podname> -i`          | Attach to a pod
`kubectl exec <pod> -- command`        | Execute a command in the pod
`kubectl label pods <pod> mylabel=fun` | Add a new label to a pod
`kubectl run -i --tty alpine --image=alpine --restart=Never --sh` | Run a shell in a pod




[Kubernetes Basics]: https://kubernetes.io/docs/tutorials/kubernetes-basics/