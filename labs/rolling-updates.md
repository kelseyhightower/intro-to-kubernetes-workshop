# Rolling Updates

* Use multiple replication controllers with a single service
* Deploy a canary application for testing
* Zero downtime rolling update to a new Docker image

## Send the Canary

```
kubectl run hello-canary \
  --labels="app=hello,track=canary" \
  --replicas=1 \
  --image=quay.io/kelseyhightower/hello:2.0.0
```

### Validation

```
kubectl get pods
```

Try hitting the service port on any of the knode instances.

```
gcloud compute instances list
```

```
while true; do curl http://${EXTERNAL_IP}; echo; sleep 2; done
```

Did you find the canary?

## Rolling Update

Open three terminals

### Terminal 1

```
kubectl rolling-update hello --update-period=3s --image=quay.io/kelseyhightower/hello:2.0.0
```

### Terminal 2

```
while true; do curl http://${EXTERNAL_IP}; echo; sleep 2; done
```

### Terminal 3

```
kubectl get pods --watch
```
