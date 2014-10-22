# Managing Subnets and Routes with Flannel

* Sync the flannel route table from etcd to GCE
* Enable cross container communication

## Workspace

```
cd intro-to-kubernetes-workshop/units
```

## Environment

```
export FLEETCTL_TUNNEL="${KCONTROL_EXTERNAL_IP}"
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
fleet list-units
```

```
fleetctl journal -f flannel-route-manager.service
```

### View networks on the GCE control panel

### View the subnet allocations in etcd

```
etcdctl --no-sync ls / --recursive
```

### Ping between the hosts
