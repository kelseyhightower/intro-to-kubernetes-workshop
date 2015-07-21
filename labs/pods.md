# Creating and managing pods

* Deploy a pod with the kubectl cli tool
* Manage the basic life cycle of a pod

```
gcloud compute ssh node0
```

## Listing Pods

```
kubectl get pods
```

## Creating Pods

```
kubectl run hello \
  --labels="app=hello,track=stable" \
  --image=quay.io/kelseyhightower/hello:1.0.0
```

## Get Pod info

```
kubectl describe pods hello
```

## Visit the running service

Grab the `IP` address for the pod

```
kubectl describe pods hello
```

```
curl http://IP
```
