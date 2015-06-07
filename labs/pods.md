# Creating and managing pods

* Deploy a pod with the kubectl cli tool
* Manage the basic life cycle of a pod

## Workspace

```
cd intro-to-kubernetes-workshop/kubernetes-configs
```

## Listing Pods

```
kubectl list pods
```

## Creating Pods

```
cat hello-pod.json
```

```
kubectl -c hello-pod.json create pods
```

```
gcloud compute firewall-rules create default-allow-hello --allow tcp:80
```

## Get Pod info

```
kubectl get pods/hello
```

### More details with the -json flag

```
kubectl -json get pods/hello
```

### Format output with a template

```
kubectl -template_file pod.tmpl get pods/hello
```

## Visit the running service

Grab the `HOST` IP address for the pod

```
kubectl -template_file pod.tmpl get pods/hello
```

```
gcloud compute instances list | grep $HOST_IP_ADDRESS
```

## Delete the hello pod

Yes. Delete the hello pod right now!

```
kubectl delete pods/hello
```
