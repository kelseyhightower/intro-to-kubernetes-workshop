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

## Environment

### fleet tunnel configuration

```
export FLEETCTL_TUNNEL="${KCONTROL_EXTERNAL_IP}"
```

### Kubernetes API SSH tunnel

```
ssh -f -nNT -L 8080:127.0.0.1:8080 core@${KUBE_APISERVER_EXTERNAL_IP}
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
