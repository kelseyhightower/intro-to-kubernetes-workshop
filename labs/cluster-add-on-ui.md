# Cluster Add-on: UI

### laptop

```
kubectl create -f https://kuar.io/kube-ui-rc.yaml
```

Next create the service for the UI:

```
kubectl create -f https://kuar.io/kube-ui-svc.yaml
```

Verify:

```
kubectl get pods --all-namespaces
```

At this point the Kubernetes UI add-on should be up and running. The Kubernetes API server provides access to the UI via the /ui endpoint.

```
kubectl proxy --port=8080 &
```

The UI is available at http://127.0.0.1:8080/api/v1/proxy/namespaces/kube-system/services/kube-ui/#/dashboard/ on the client machine.
