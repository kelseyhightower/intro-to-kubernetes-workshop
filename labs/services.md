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

## Validation

Try hitting the external IP address for each instance in your web browser.

```
gcloud compute instances list
```

## Deleting Services

Only do this if you need to start over or clean up after you are done.

```
kubecfg delete services/hello
```
