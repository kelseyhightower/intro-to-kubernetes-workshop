# Rolling Updates

* Use multiple replication controllers with a single service
* Deploy a canary application for testing

### node0

```
gcloud compute ssh node0
```

## Send the Canary

```
kubectl run hello-canary \
  --labels="app=hello,track=canary" \
  --replicas=1 \
  --image=quay.io/kelseyhightower/hello:2.0.0
```

### Validation

Try hitting the service port on any of the knode instances.

#### laptop

```
while true; do curl http://hello.PROJECT_NAME.io; echo; sleep 1; done
```

Did you find the canary?

## Rolling Update

Open three terminals

### Terminal 1

#### node0

```
gcloud compute ssh node0
```

```
kubectl rolling-update hello --update-period=3s --image=quay.io/kelseyhightower/hello:2.0.0
```

### Terminal 2

#### laptop

```
while true; do curl http://hello.PROJECT_NAME.io; echo; sleep 1; done
```

### Terminal 3

#### node0

```
gcloud compute ssh node0
```

```
kubectl get pods --watch
```
