# Managing Subnets and Routes with Flannel

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
export FLEETCTL_TUNNEL="${KCONTROL_EXTERNAL_IP}"
```

```
fleetctl list-machines
```

```
fleetctl list-units
```

```
fleetctl start flannel-route-manager.service
```

## Validation

### View networks on the GCE control panel

### View the subnet allocations in etcd

```
etcdctl --no-sync ls / --recursive
```

### Ping between the hosts
