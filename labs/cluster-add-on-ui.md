# Cluster Add-on: UI

### node0

```
gcloud compute ssh node0
```

```
/opt/bin/kubectl create -f https://kuar.io/kube-ui-rc.yaml
```

Next create the service for the UI:

```
/opt/bin/kubectl create -f https://kuar.io/kube-ui-svc.yaml
```

At this point the Kubernetes UI add-on should be up and running. The Kubernetes API server provides access to the UI via the /ui endpoint. However the Kubernetes API is not accessable remotely due to the lack of security.

## Securely Exposing the API Server 

Instead of exposing the API server to the public internet over an insecure port, a SSH tunnel can be can be create between the remote client and API server.

Create a SSH tunnel between a remote client machine and the controller node:

```
gcloud compute ssh node0 -- -f -nNT -L 8080:127.0.0.1:8080
```

The UI is available at http://127.0.0.1:8080/ui on the client machine.
