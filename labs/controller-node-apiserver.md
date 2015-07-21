# Deploying the API Server

### node0

```
gcloud compute ssh node0
```

Download the kube-apiserver unit file:

```
sudo curl https://kuar.io/kube-apiserver.service \
  -o /etc/systemd/system/kube-apiserver.service
```

Review the kube-apiserver unit file:

```
cat /etc/systemd/system/kube-apiserver.service
```

Start the kube-apiserver service:

```
sudo systemctl daemon-reload
sudo systemctl enable kube-apiserver
sudo systemctl start kube-apiserver
```
