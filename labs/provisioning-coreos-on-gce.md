# Provisioning CoreOS on Google Compute Engine

Provision 4 CoreOS nodes by issuing the following command:

```
for i in {0..3}; do
  gcloud compute instances create node${i} \
  --image-project coreos-cloud \
  --image coreos-stable-717-3-0-v20150710 \
  --boot-disk-size 200GB \
  --machine-type n1-standard-1 \
  --can-ip-forward \
  --scopes compute-rw
done
```

Confirm that your nodes are up with:

```
gcloud compute instances list
```
