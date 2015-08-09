# Deploying the Kubelet

## Install and configure the Kubelet

Get your project name:
```
gcloud config list project
```

### node0

```
gcloud compute ssh node0
```

Download the kubelet unit file:

```
sudo curl https://kuar.io/kubelet.service \
  -o /etc/systemd/system/kubelet.service
```

Edit the kubelet unit file and set the api-server flag:

```
sudo vim /etc/systemd/system/kubelet.service
```

```
--api-servers=http://node0.c.PROJECT_NAME.internal:8080 \
```

Start the kubelet service:

```
sudo systemctl daemon-reload
sudo systemctl enable kubelet
sudo systemctl start kubelet
```

Verify:

```
sudo systemctl status kubelet
```

### node1

```
gcloud compute ssh node1
```

Repeat the steps from above.

### node0

```
gcloud compute ssh node0
```

```
/opt/bin/kubectl get nodes
```
