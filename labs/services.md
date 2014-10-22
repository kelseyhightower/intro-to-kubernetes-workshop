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
cat hello-service.json
```

```
kubecfg -c hello-service.json create services
```

## Deleting Services

```
kubecfg delete services/hello
```
