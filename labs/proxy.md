# Deploying the Service Proxy

### node1

```
gcloud compute ssh node1
```

Download the kube-proxy unit file:

```
sudo curl https://kuar.io/kube-proxy.service \
  -o /etc/systemd/system/kube-proxy.service
```

Edit the kube-proxy unit file and configure the master flag:

```
sudo vim /etc/systemd/system/kube-proxy.service
```

```
--master=http://node0.c.PROJECT_NAME.internal:8080
```

Start the kube-proxy service:

```
sudo systemctl daemon-reload
sudo systemctl enable kube-proxy
sudo systemctl start kube-proxy
```

Verify:

```
sudo systemctl status kube-proxy
```

### node2

```
gcloud compute ssh node1
```

Repeat the steps from above.

### node3

```
gcloud compute ssh node1
```

Repeat the steps from above.
