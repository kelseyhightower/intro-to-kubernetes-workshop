# Installing Kubernetes with fleet

* Deploy Kubernetes service units with fleet
* Provide HA for Kubernetes components
* Use fleet global units to simplify deployment
* Use fleet metadata to co-locate Kubernetes master components
* Setup Kubernetes API SSH Tunnel

## Workspace

```
cd intro-to-kubernetes-workshop/units
```

## Environment

### fleet tunnel configuration

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

#### Setup Kubernetes API SSH Tunnel

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

Why is the minion list empty?
