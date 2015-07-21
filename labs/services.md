# Creating and managing services

* Create a service using the kubectl cli tool
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
cat hello-svc.yaml
```

```
kubectl create -f hello-svc.yaml
```

```
kubectl get services
```

```
gcloud compute firewall-rules create default-allow-hello --allow tcp:36000
```

## Validation

Try hitting the external IP address for each instance in your web browser.

```
gcloud compute instances list
```
