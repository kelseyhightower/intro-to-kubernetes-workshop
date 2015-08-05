# Provisioning CoreOS on Google Compute Engine

Provision 2 CoreOS nodes:

```
gcloud compute instances create node0 \
 --image-project coreos-cloud \
 --image coreos-stable-723-3-0-v20150804 \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward \
 --scopes compute-rw
```

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
