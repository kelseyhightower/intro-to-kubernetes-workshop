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

## Configure the Docker bridge

|=======
|hostname|bip
|node0.c.kuarlab.internal|10.200.0.1/24
|node1.c.kuarlab.internal|10.200.1.1/24
|node2.c.kuarlab.internal|10.200.2.1/24
|node3.c.kuarlab.internal|10.200.3.1/24
|=======

```
$ sudo curl https://kuar.io/docker.service \
  -o /etc/systemd/system/docker.service
```

```
$ sudo systemctl daemon-reload
$ sudo systemctl enable docker
$ sudo systemctl start docker
```

## Create Kubernetes routes.

```
$ gcloud compute routes create default-route-10-200-0-0-24 \
    --destination-range 10.200.0.0/24 \
    --next-hop-instance node0

$ gcloud compute routes create default-route-10-200-1-0-24 \
    --destination-range 10.200.1.0/24 \
    --next-hop-instance node1

$ gcloud compute routes create default-route-10-200-2-0-24 \
    --destination-range 10.200.2.0/24 \
    --next-hop-instance node2

$ gcloud compute routes create default-route-10-200-3-0-24 \
    --destination-range 10.200.3.0/24 \
    --next-hop-instance node3
```

## Setup Client SSH Tunnels

```
gcloud compute instances list
```
