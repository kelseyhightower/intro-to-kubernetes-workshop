# Intro to Kubernetes Workshop

Kubernetes Version: 0.17.1

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
  * flannel
  * Kubernetes master
  * Kubernetes node

### Client tools
  * packer
  * terraform
  * etcdctl
  * kubectl

#### Labs
  * [Install the client tools](labs/install-the-client-tools.md)
  * [Creating Kubernetes Images with Packer](labs/creating-kubernetes-images-with-packer.md)

### Kubernetes Core Components
  * kubelet
  * proxy
  * apiserver
  * scheduler
  * replication controller

#### Labs
  * [Provisioning Kubernetes Clusters with Terraform](labs/provisioning-kubernetes-clusters-with-terraform.md)

### Managing Applications with Kubernetes
  * Kubernetes API
  * kubectl

#### Labs

  * [Creating and managing nodes](labs/nodes.md)
  * [Creating and managing pods](labs/pods.md)
  * [Creating and managing replication controllers](labs/replication-controllers.md)
  * [Creating and managing services](labs/services.md)
  * [Rolling updates](labs/rolling-updates.md)
  * Running the Kubernetes examples

## Links

* [Kubernetes](http://googlecloudplatform.github.io/kubernetes)
* [gcloud Tool Guide](https://cloud.google.com/sdk/gcloud)
* [Docker](https://docs.docker.com)
* [CoreOS](https://coreos.com)
* [Packer](https://packer.io)
* [Terraform](https://www.terraform.io)
* [flannel](https://github.com/coreos/flannel)
* [etcd](https://coreos.com/docs/distributed-configuration/getting-started-with-etcd)
