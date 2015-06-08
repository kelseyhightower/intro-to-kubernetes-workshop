# Creating and managing services

* Create a service using the kubecfg cli tool
* Map a service to pod lables

## Workspace

```
cd intro-to-kubernetes-workshop/kubernetes-configs
```

## Listing Services

```
kubectl get services
```

## Creating Services

```
cat hello-service.json
```

```
kubectl create -f hello-service.json
```

```
kubectl get services
```

```
gcloud compute firewall-rules create default-allow-hello --allow tcp:80 --project kubestack
```

## Validation

Try hitting the external IP address for each instance in your web browser.

```
gcloud compute instances list --project kubestack
```

Why does it not work?

### Fix it

```
kubectl delete services hello
```

```
gcloud compute instances list --project kubestack
```

Edit `hello-service.json`

Add the `INTERNAL_IP`s to the publicIPs list:

```
"publicIPs": ["10.240.32.10", "10.240.98.37", "10.240.53.14"],
```

## Deleting Services

Only do this if you need to start over or clean up after you are done.

```
kubectl delete services hello
```
