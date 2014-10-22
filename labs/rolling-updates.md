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

```
kubecfg list pods
```

## Rolling Update

```
kubecfg get replicationControllers/helloStableController
```

```
kubecfg list pods
```

```
kubecfg --image "quay.io/kelseyhightower/hello:2.0.0" rollingupdate helloStableController
```
