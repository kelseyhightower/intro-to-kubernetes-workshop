# Deploying the Kubelet

## Install and configure the Kubelet

### node1

```
gcloud compute ssh node1
```

Download the kubelet unit file:

```
sudo curl https://kuar.io/kubelet.service \
  -o /etc/systemd/system/kubelet.service
```

Get your project name:
```
gcloud config list project
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

### node2

```
gcloud compute ssh node2
```

Repeat the steps from above.

### node3

```
gcloud compute ssh node3
```

Repeat the steps from above.

## List registered nodes

### node0

```
gcloud compute ssh node0
```

```
/opt/bin/kubectl get nodes
```
