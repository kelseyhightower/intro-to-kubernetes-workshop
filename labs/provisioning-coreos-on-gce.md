# Provisioning CoreOS on Google Compute Engine

In this lab you will provision two GCE instances running CoreOS.

## Provision 2 GCE instances

### Provision CoreOS using the gcloud CLI

#### node0

```
gcloud compute instances create node0 \
 --image-project coreos-cloud \
 --image coreos-stable-723-3-0-v20150804 \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward \
 --scopes compute-rw
```

#### node1

```
gcloud compute instances create node1 \
 --image-project coreos-cloud \
 --image coreos-stable-723-3-0-v20150804 \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward \
 --scopes compute-rw
```

List nodes:

```
gcloud compute instances list
```
