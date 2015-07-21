# Provisioning CoreOS on Google Compute Engine

Provision 4 CoreOS nodes by issuing the following command:

```
$ for i in {0..3}; do
  gcloud compute instances create node${i} \
  --image-project coreos-cloud \
  --image coreos-stable-717-3-0-v20150710 \
  --boot-disk-size 200GB \
  --machine-type n1-standard-1 \
  --can-ip-forward \
  --scopes compute-rw
done
```

Confirm that your nodes are up with `gcloud compute instances list`

```
NAME                 ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP    EXTERNAL_IP    STATUS
node0                us-central1-a n1-standard-1             10.240.241.71  104.197.62.14  RUNNING
node1                us-central1-a n1-standard-1             10.240.150.126 104.197.61.200 RUNNING
node2                us-central1-a n1-standard-1             10.240.216.120 146.148.32.135 RUNNING
node3                us-central1-a n1-standard-1             10.240.214.146 104.197.7.33   RUNNING
```

Next Step: [Configure Docker](docker.md)