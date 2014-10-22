# Creating and managing pods

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

## Deleting Pods

```
kubecfg delete pods/hello-pod
```
