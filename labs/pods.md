# Creating and managing pods

* Deploy a pod with the kubectl cli tool
* Manage the basic life cycle of a pod

## Workspace

```
cd intro-to-kubernetes-workshop/kubernetes-configs
```

## Listing Pods

```
kubectl get pods
```

## Creating Pods

```
cat hello-pod.json
```

```
kubectl create -f hello-pod.json
```

```
gcloud compute firewall-rules create default-allow-hello --allow tcp:80
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
gcloud compute instances list | grep $HOST_IP_ADDRESS
```

## Delete the hello pod

Yes. Delete the hello pod right now!

```
kubectl delete pods hello
```
