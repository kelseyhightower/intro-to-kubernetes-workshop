# Managing Subnets and Routes with Flannel

* Sync the flannel route table from etcd to GCE
* Enable cross container communication

## Workspace

```
cd intro-to-kubernetes-workshop/units
```

## View the current subnet allocation

```
etcdctl --no-sync ls /coreos.com/network --recursive
```

### Explore GCE network using the GCE control panel

## Install the flannel-route-manager


```
cat flannel-route-manager.service
```

```
fleetctl start flannel-route-manager.service
```

## Validation

```
fleetctl list-units
```

```
fleetctl journal -f flannel-route-manager.service
```

### View networks on the GCE control panel

### View the subnet allocations in etcd

```
etcdctl --no-sync ls / --recursive
```

### Communicate between two containers

Open two terminals

#### Terminal 1

```
gcloud compute ssh core@knode1
```

```
docker run -t -i busybox /bin/sh -c 'ifconfig eth0 && nc -l -p 80'
```

#### Terminal 2

```
gcloud compute ssh core@knode3
```

Replace eth0-ip with the ip address from above.

```
docker run -t -i busybox /bin/sh -c 'nc ${eth0-ip}:80'
```
