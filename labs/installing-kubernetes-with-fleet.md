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
sed -i -e 's/CONTROL-NODE-INTERNAL-IP/${KCONTROL_INTERNAL_IP}/g' *
```

## Deploying services

Take a moment to review the Kubernetes services files

```
ls *.service
```

Review machines and running units

```
fleetctl list-machines
fleetctl list-units
```

### Kubelet

```
fleetctl start kube-kubelet.service 
```

### Kubernetes Proxy

```
fleetctl start kube-proxy.service
```

### Kubernetes API Service

```
fleetctl start kube-apiserver.service
```

### Controller Manager

```
fleetctl start kube-controller-manager.service
```

### Kubernetes Scheduler

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
ssh -f -nNT -L 8080:127.0.0.1:8080 core@${KUBE-APISERVER_EXTERNAL_IP}
```

```
kubecfg list minions
```
