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
cat hello-controller.json
```

```
kubecfg -c hello-controller.json create replicationControllers
```

## Update a replicationController

Edit: hello-controller.json

```
"replicas": 4
```

```
kubecfg -c hello-controller.json update replicationControllers/hello
```

## Deleting a replicationController and pods

### Update the replicationController

Edit: hello-controller.json

```
"replicas": 0
```

```
kubecfg -c hello-controller.json update replicationControllers/hello
```

```
kubecfg delete replicationControllers/hello
```
