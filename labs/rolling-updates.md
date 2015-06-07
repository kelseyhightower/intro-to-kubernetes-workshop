# Rolling Updates

* Use multiple replication controllers with a single service
* Deploy a canary application for testing
* Zero downtime rolling update to a new Docker image

## Send the Canary

```
cat hello-canary-controller.json 
```

```
kubectl create -f hello-canary-controller.json
```

### Validation

```
kubectl get pods
```

Try hitting the service port on any of the knode instances.

```
gcloud compute instances list --project kubestack
```

```
while true; do curl http://${EXTERNAL_IP}; echo; sleep 2; done
```

Did you find the canary?

## Rolling Update

Open three terminals

### Terminal 1

```
kubectl rolling-update --update-period=3s hello-stable-controller -f hello-stable-controller-v2.json
```

### Terminal 2

```
while true; do curl http://${EXTERNAL_IP}; echo; sleep 2; done
```

### Terminal 3

```
kubectl get pods
```
