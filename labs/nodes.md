# Creating and managing nodes

Nodes represent the workers in a Kubernetes clusters and will run pods scheduled by the Kubernetes scheduler.

### View existing nodes

```
kubectl get nodes
```

### Adding nodes with kubectl

Copy the node template:

```
cp kubernetes-configs/node-template.json kubernetes-configs/testing-kube0.c.${project-id}.internal.json
```

Edit: `kubernetes-configs/testing-kube0.c.${project-id}.internal.json`

```
{
  "kind": "Node",
  "apiVersion": "v1beta3",
  "metadata": {
    "name": "testing-kube0.c.${project-id}.internal",
    "labels": {
      "environment": "testing",
      "name": "kube0"
    }
  },
  "spec": {
    "externalID": "testing-kube0.c.${project-id}.internal"
  }
}
```

Register the node using kubectl

```
kubectl create -f kubernetes-configs/testing-kube0.c.${project-id}.internal.json
```

```
kubectl get nodes
```

### Viewing node details

```
kubectl describe nodes testing-kube0.c.kubestack.internal
```

### Troubleshooting

If you need to troubleshoot a node, start with the kubelet.

```
gcloud compute instances list
```

```
ssh core@${node-ip-address}
```

Review the logs:

```
sudo journalctl --no-pager -u kube-kubelet
```

Check the service status

```
sudo systemctl status kube-kubelet
```

If all else fails, trying restarting the kubelet service

```
sudo systemctl restart kube-kubelet
```
