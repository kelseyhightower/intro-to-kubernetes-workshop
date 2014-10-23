# Intro to Kubernetes Workshop

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
  * fleet
  * flannel
  * Kubernetes master
  * Kubernetes node

### Client tools
  * fleetctl
  * etcdctl
  * kubecfg

#### Labs
  * [Install the client tools](labs/install-the-client-tools.md)
  * [Provisioning CoreOS, etcd, fleet, and flannel on Google Compute Engine](labs/provisioning-coreos-on-gce.md)
  * [Managing subnets and routes with flannel](labs/managing-subnets-and-routes-with-flannel.md)

### Kubernetes Core Components
  * kubelet
  * proxy
  * apiserver
  * scheduler
  * replication controller

#### Labs
  * [Installing Kubernetes with fleet](labs/installing-kubernetes-with-fleet.md)
  * [kubelet auto-registration with kube-register](labs/kubelet-auto-registration-with-kube-register.md)

### Managing Applications with Kubernetes
  * Kubernetes API
  * kubecfg

#### Labs

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
* [fleet](https://coreos.com/docs/launching-containers/launching/launching-containers-fleet)
* [flannel](https://github.com/coreos/flannel)
* [etcd](https://coreos.com/docs/distributed-configuration/getting-started-with-etcd)
