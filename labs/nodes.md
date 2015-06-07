# Creating and managing nodes

Nodes represent the workers in a Kubernetes clusters and will run pods scheduled by the Kubernetes scheduler.

### View existing nodes

```
kubectl get nodes
```

### Adding nodes a Kubernetes cluster

Edit `kubernetes-configs/node-template.json`

``` 
{
  "kind": "Node",
  "apiVersion": "v1beta3",
  "metadata": {
    "name": "",
    "labels": {
      "environment": "",
      "name": ""
    }
  },
  "spec": {
    "externalID": ""
  }
}
```

Copy the node template:

```
cp kubernetes-configs/node-template.json kubernetes-configs/${cluster_name}-kube0.json
```

```
{
  "kind": "Node",
  "apiVersion": "v1beta3",
  "metadata": {
    "name": "testing-kube0.c.kubestack.internal",
    "labels": {
      "environment": testing"",
      "name": "kube0"
    }
  },
  "spec": {
    "externalID": "testing-kube0.c.kubestack.internal"
  }
}
```
