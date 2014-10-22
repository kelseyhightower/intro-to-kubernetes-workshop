# Creating and managing services

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
cat hello-stable-service.json
```

```
kubecfg -c hello-stable-service.json create services
```

```
gcloud compute instances list
```

## Deleting Services

```
kubecfg delete services/hello
```
