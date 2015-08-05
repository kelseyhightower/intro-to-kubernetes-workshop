# Deploying the Service Proxy

### node0

```
gcloud compute ssh node0
```

Download the kube-proxy unit file:

```
sudo curl https://kuar.io/kube-proxy.service \
  -o /etc/systemd/system/kube-proxy.service
```

Get your project name:
```
gcloud config list project
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

Check iptables

```
sudo iptables -vL -n -t nat
```

### node1

```
gcloud compute ssh node1
```

Repeat the steps from above.
