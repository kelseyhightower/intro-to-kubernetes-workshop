# Creating and managing replication controllers

* Create a replication controller using the kubecfg cli tool
* Horizontally scale pods using a replication controller

> You will not be able to access pods after this lab. You need to spin up a Kubernetes service later.

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

## Horizontally scaling pods

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

Only do this if you need to start over or clean up.

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
