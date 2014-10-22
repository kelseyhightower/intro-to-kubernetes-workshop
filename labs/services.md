# Creating and managing services

* Create a service using the kubecfg cli tool
* Map a service to pod lables

## Workspace

```
cd intro-to-kubernetes-workshop/kubernetes-configs
```

## Listing Services

```
kubecfg list services
```

## Creating Services

```
cat hello-service.json
```

```
kubecfg -c hello-service.json create services
```

```
gcloud compute firewall-rules create default-allow-hello --allow tcp:80
```

```
gcloud compute instances list
```

## Deleting Services

```
kubecfg delete services/hello
```
