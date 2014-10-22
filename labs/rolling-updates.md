# Rolling Updates

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
kubecfg --image "quay.io/kelseyhightower/hello:2.0.0" rollingupdate helloStableController
```
