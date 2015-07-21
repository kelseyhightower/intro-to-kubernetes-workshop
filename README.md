# Intro to Kubernetes Workshop

Kubernetes Version: 1.0.1

The slides from this workshop are hosted [online](http://go-talks.appspot.com/github.com/kelseyhightower/intro-to-kubernetes-workshop/slides/talk.slide#1)

## Course Outline

### Kubernetes Core Concepts

  * container
  * pod
  * label
  * service
  * network

### Kubernetes Infrastructure

  * CoreOS
  * Docker
  * etcd
  * Kubernetes master
  * Kubernetes node

### Client tools

  * gcloud

#### Labs

  * [Install the client tools](labs/install-the-client-tools.md)

### Kubernetes Core Components

  * kubelet
  * proxy
  * apiserver
  * scheduler
  * controller manager

#### Labs

  * [Provision CoreOS Cluster](labs/provisioning-coreos-on-gce.md)
  * [Configure Docker](labs/docker.md)
  * [Configure Networking](labs/networking.md)

### Provision the Controller Node

#### Labs

  * [etcd](labs/controller-node-etcd.md)
  * [API Server](labs/controller-node-apiserver.md)
  * [Controller Manager](labs/controller-node-controller-manager.md)
  * [Scheduler](labs/controller-node-scheduler.md)

### Managing Applications with Kubernetes

  * Kubernetes API
  * kubectl

#### Labs

  * [Creating and managing pods](labs/pods.md)
  * [Creating and managing replication controllers](labs/replication-controllers.md)
  * [Creating and managing services](labs/services.md)
  * [Exposing services with nginx](labs/exposing-services-with-nginx.md)
  * [Rolling updates](labs/rolling-updates.md)
  * Running the Kubernetes examples

### Cluster Add-ons

#### Labs

  * [DNS](labs/cluster-add-on-dns.md)
  * [Web UI](labs/cluster-add-on-ui.md)

## Links

  * [Kubernetes](http://googlecloudplatform.github.io/kubernetes)
  * [gcloud Tool Guide](https://cloud.google.com/sdk/gcloud)
  * [Docker](https://docs.docker.com)
  * [CoreOS](https://coreos.com)
  * [etcd](https://coreos.com/docs/distributed-configuration/getting-started-with-etcd)
  * [nginx](http://nginx.org)
