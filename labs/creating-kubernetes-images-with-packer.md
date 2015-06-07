# Creating Kubernetes Images with Packer

The following lab will walk you through creating a Kubernetes image on GCE using Packer.

## Download Kubestack

In this workshop we will be using the kubestack Packer configs to create customer Kubernetes images.

Download the kubestack repo

```
git clone https://github.com/kelseyhightower/kubestack.git
```

Move into the Kubestack directory

```
cd kubestack
```

## Reviewing the Packer Configs

* packer/settings.json
* packer/kubestack.json

## Reviewing the System Unit Files

* packer/units/*

## Creating a Kubernetes Image with Packer

[Kubestack](https://github.com/kelseyhightower/kubestack#kubestack)
