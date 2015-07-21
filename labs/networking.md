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

