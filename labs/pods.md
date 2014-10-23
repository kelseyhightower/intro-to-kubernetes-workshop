# Creating and managing pods

* Deploy a pod with the kubecfg cli tool
* Manage the basic life cycle of a pod

## Workspace

```
cd intro-to-kubernetes-workshop/kubernetes-configs
```

## Listing Pods

```
kubecfg list pods
```

## Creating Pods

```
cat hello-pod.json
```

```
kubecfg -c hello-pod.json create pods
```

```
gcloud compute firewall-rules create default-allow-hello --allow tcp:80
```

## Get Pod info

```
kubecfg get pods/hello
```

### More details with the -json flag

```
kubecfg -json get pods/hello
```

### Format output with a template

```
kubecfg -template_file pod.tmpl get pods/hello
```

## Visit the running service

Grab the `HOST` IP address for the pod

```
kubecfg -template_file pod.tmpl get pods/hello
```

```
gcloud compute instances list | grep $HOST_IP_ADDRESS
```

## Deleting Pods

```
kubecfg delete pods/hello
```
