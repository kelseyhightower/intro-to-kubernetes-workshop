# Provisioning CoreOS on Google Compute Engine

In this lab you will provision two GCE instances running CoreOS.

## Provision 2 GCE instances

### Provision CoreOS using the gcloud CLI

#### node0

```
gcloud compute instances create node0 \
 --image-project coreos-cloud \
 --image coreos-stable-835-12-0-v20160202 \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward
```

#### node1

```
gcloud compute instances create node1 \
 --image-project coreos-cloud \
 --image coreos-stable-835-12-0-v20160202 \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward
```

#### Verify

```
gcloud compute instances list
```
