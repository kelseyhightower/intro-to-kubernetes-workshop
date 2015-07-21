# Provisioning CoreOS on Google Compute Engine

* Provision 4 Kubernetes nodes on GCE
* Configure client SSL tunnels for remote access to Kubernete API

## Kubernetes Nodes

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

You should see output like this:

```
Created [https://www.googleapis.com/compute/v1/projects/avian-cat-91305/zones/us-central1-a/instances/node0].
NAME  ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP   EXTERNAL_IP   STATUS
node0 us-central1-a n1-standard-1             10.240.241.71 104.197.62.14 RUNNING
Created [https://www.googleapis.com/compute/v1/projects/avian-cat-91305/zones/us-central1-a/instances/node1].
NAME  ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP    EXTERNAL_IP    STATUS
node1 us-central1-a n1-standard-1             10.240.150.126 104.197.61.200 RUNNING
Created [https://www.googleapis.com/compute/v1/projects/avian-cat-91305/zones/us-central1-a/instances/node2].
NAME  ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP    EXTERNAL_IP    STATUS
node2 us-central1-a n1-standard-1             10.240.216.120 146.148.32.135 RUNNING
Created [https://www.googleapis.com/compute/v1/projects/avian-cat-91305/zones/us-central1-a/instances/node3].
NAME  ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP    EXTERNAL_IP  STATUS
node3 us-central1-a n1-standard-1             10.240.214.146 104.197.7.33 RUNNING

```

You can confirm what you have running by issuing gcloud compute instances list:

```
$ gcloud compute instances list
NAME                 ZONE          MACHINE_TYPE  PREEMPTIBLE INTERNAL_IP    EXTERNAL_IP    STATUS
node0                us-central1-a n1-standard-1             10.240.241.71  104.197.62.14  RUNNING
node1                us-central1-a n1-standard-1             10.240.150.126 104.197.61.200 RUNNING
node2                us-central1-a n1-standard-1             10.240.216.120 146.148.32.135 RUNNING
node3                us-central1-a n1-standard-1             10.240.214.146 104.197.7.33   RUNNING
```