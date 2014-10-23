# Rolling Updates

* Use multiple replication controllers with a single service
* Deploy a canary application for testing
* Zero downtime rolling update to a new Docker image

## Send the Canary

```
cat hello-canary-controller.json 
```

```
kubecfg -c hello-canary-controller.json create replicationControllers
```

### Validation

```
kubecfg list pods
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

```
kubecfg get replicationControllers/helloStableController
```

```
kubecfg list pods
```

Open three terminals

### Terminal 1

```
kubecfg --image "quay.io/kelseyhightower/hello:2.0.0" rollingupdate helloStableController
```

### Terminal 2

```
while true; do curl http://${EXTERNAL_IP}; echo; sleep 2; done
```

### Terminal 3

```
kubecfg list pods
```
