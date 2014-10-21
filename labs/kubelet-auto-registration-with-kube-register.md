# Kubelet Auto Registration

## Workspace

```
cd intro-to-kubernetes-workshop/units
```

## Environment

```
export FLEETCTL_TUNNEL="${KCONTROL_EXTERNAL_IP}"
ssh -f -nNT -L 8080:127.0.0.1:8080 core@${KUBE-APISERVER_EXTERNAL_IP}
```

## Install Kube Register with fleet

```
fleetctl start kube-register.service
```

## Validation

```
kubecfg list minions
```
