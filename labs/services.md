# Creating and managing services

* Create a service using the kubectl cli tool
* Map a service to pod lables

### Listing Services

```
kubectl get services
```

### Creating Services

```
kubectl create -f https://storage.googleapis.com/configs.kuar.io/inspector-svc.yaml
```

#### Validation
```
kubectl describe service inspector
```

## Create the inspector firewall rule

#### laptop

```
gcloud compute firewall-rules create default-allow-inspector --allow tcp:36000
```

Try hitting the external IP address for each instance in your web browser on port 36000

```
EXTERNAL_IP=$(gcloud compute ssh node0 --command \
  "curl -H 'Metadata-Flavor: Google' \
   http://metadata.google.internal/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip")
```

```
curl http://${EXTERNAL_IP}:36000
```
