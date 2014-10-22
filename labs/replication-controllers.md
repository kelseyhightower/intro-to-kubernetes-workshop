# Creating and managing replication controllers

## Workspace

```
cd intro-to-kubernetes-workshop/kubernetes-configs
```

## Listing Replication Controllers

```
kubecfg list replicationControllers
```

## Creating a replicationController

```
cat hello-stable-controller.json
```

```
kubecfg -c hello-stable-controller.json create replicationControllers
```

```
kubecfg list replicationControllers
kubecfg list pods
```

## Update a replicationController

Edit: hello-stable-controller.json

```
"replicas": 4
```

```
kubecfg -c hello-stable-controller.json update replicationControllers/helloStableController
```

```
kubecfg list pods
```

## Deleting a replicationController and pods

### Update the replicationController

Edit: hello-stable-controller.json

```
"replicas": 0
```

```
kubecfg -c hello-stable-controller.json update replicationControllers/helloStableController
```

```
kubecfg delete replicationControllers/helloStableController
```
