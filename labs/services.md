# Creating and managing services

* Create a service using the kubectl cli tool
* Map a service to pod lables

### laptop

```
git clone https://github.com/kelseyhightower/intro-to-kubernetes-workshop.git
```

### Listing Services

```
kubectl get services
```

### Creating Services

```
cat intro-to-kubernetes-workshop/kubernetes-configs/inspector-svc.yaml
```

```
kubectl create -f intro-to-kubernetes-workshop/kubernetes-configs/inspector-svc.yaml
```

#### Validation
```
kubectl describe service inspector
```

```
curl EXTERNAL_IP_ADDRESS:36000
```
