# Creating and managing pods

* Deploy a pod with the kubectl cli tool
* Manage the basic life cycle of a pod

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
kubectl get pods hello
```

### More details with the describe command

```
kubectl describe pods hello
```

### Format output with a template

```
kubectl get pods -o templatefile --template=pod.tmpl
```

## Visit the running service

Grab the `HOST` IP address for the pod

```
kubectl get pods hello
```

```
gcloud compute instances list
```

```
gcloud compute ssh HOST
```

```
curl ${PodIP}
```
