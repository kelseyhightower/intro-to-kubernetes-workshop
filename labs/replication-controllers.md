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
kubectl get replicationControllers
```

Use `rc` as a shorthand for `replicationControllers`

```
kubectl get rc
```

## Creating a replicationController

```
cat hello-stable-controller-v1.json
```

```
kubectl create -f hello-stable-controller-v1.json
```

```
kubectl get rc
kubectl get pods
```

## Horizontally scaling pods

### Resize the replication controller

```
kubectl resize --replicas=3 rc hello-stable-controller-v1
```

```
kubectl get pods
```

## Deleting a replicationController and pods

Only do this if you need to start over or clean up.

```
kubectl delete rc hello-stable-controller-v1
```
