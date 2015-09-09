# Creating and managing pods

* Deploy a pod with the kubectl cli tool
* Manage the basic life cycle of a pod

## Listing Pods

```
kubectl get pods
```

## Creating Pods

```
kubectl run inspector \
  --labels="app=inspector,track=stable" \
  --replicas=1 \
  --image=b.gcr.io/kuar/inspector:1.0.0
```

## Watch for status

```
kubectl get pods --watch
```

## Get Pod info

```
kubectl describe pods inspector
```

## Visit the running service

Grab the `IP` address for the pod

```
kubectl describe pods inspector
```

And run this command on one of your Kubernetes nodes:

```
curl http://IP
```
