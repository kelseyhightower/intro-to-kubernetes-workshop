# Kubelet Auto Registration

* Sync healthy kubelet nodes from the fleet API to the Kubernetes API
* Health check kubelet before adding to Kubernetes API
* Filter machines with fleet metadata

```
metadata=role=knode
```

## Workspace

```
cd intro-to-kubernetes-workshop/units
```

## Install kube-register with fleet

```
cat kube-register.service
```

```
fleetctl start kube-register.service
```

## Validation

```
fleetctl list-units
```

```
kubecfg list minions
```
