# Creating and managing services

* Create a service using the kubectl cli tool
* Map a service to pod lables

```
gcloud compute ssh node0
```

```
git clone https://github.com/kelseyhightower/intro-to-kubernetes-workshop.git
```

## Listing Services

```
kubectl get services
```

## Creating Services

```
cat intro-to-kubernetes-workshop/kubernetes-configs/hello-svc.yaml
```

```
kubectl create -f intro-to-kubernetes-workshop/kubernetes-configs/hello-svc.yaml
```

```
kubectl get services
```

## Create Hello firewall rule

### laptop

```
gcloud compute firewall-rules create default-allow-hello --allow tcp:36000
```

## Validation

Try hitting the external IP address for each instance in your web browser on port 36000

```
gcloud compute instances list
```
