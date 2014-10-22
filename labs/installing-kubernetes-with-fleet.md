# Installing Kubernetes with fleet

## Workspace

```
cd intro-to-kubernetes-workshop/units
```

## Environment

```
export FLEETCTL_TUNNEL="${KCONTROL_EXTERNAL_IP}"
```

## Update unit files

```
gcloud compute instances list
```

```
sed -i "" -e 's/CONTROL-NODE-INTERNAL-IP/${KCONTROL_INTERNAL_IP}/g' *
```

## Deploying services

Review running units

```
fleetctl list-units
```

### Kubelet

```
cat kube-kubelet.service
```

```
fleetctl start kube-kubelet.service 
```

### Kubernetes Proxy

```
cat kube-proxy.service
```

```
fleetctl start kube-proxy.service
```

### Kubernetes API Service

```
cat kube-apiserver.service
```

```
fleetctl start kube-apiserver.service
```

### Controller Manager

```
cat kube-controller-manager.service
```

```
fleetctl start kube-controller-manager.service
```

### Kubernetes Scheduler

```
cat kube-scheduler.service
```

```
fleetctl start kube-scheduler.service
```

## Validation

### fleet

```
fleetctl list-units
```

### kubecfg 

#### Setup SSH Tunnel

```
fleetctl list-units
```

```
gcloud compute instances list
```

```
ssh -f -nNT -L 8080:127.0.0.1:8080 core@${KUBE_APISERVER_EXTERNAL_IP}
```

```
kubecfg list minions
```
