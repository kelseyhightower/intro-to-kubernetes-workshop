# Hands on with kubectl

### node0

```
gcloud compute ssh node0
```

Download and install kubectl:

```
sudo curl -o /opt/bin/kubectl https://kuar.io/linux/kubectl
sudo chmod +x /opt/bin/kubectl
```

Check the health status of the cluster components:

```
/opt/bin/kubectl get cs
```

List pods:

```
/opt/bin/kubectl get pods
```

List nodes:

```
/opt/bin/kubectl get nodes
```

List services:

```
/opt/bin/kubectl get services
```
