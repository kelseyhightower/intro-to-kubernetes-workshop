# Deploying the Controller Manager

### node0

```
gcloud compute ssh node0
```

Download the kube-controller-manager unit file:

```
sudo curl https://kuar.io/kube-controller-manager.service \
  -o /etc/systemd/system/kube-controller-manager.service
```

Review the kube-controller-manager unit file:

```
cat /etc/systemd/system/kube-controller-manager.service
```

Start the kube-controller-manager service:

```
sudo systemctl daemon-reload
sudo systemctl enable kube-controller-manager
sudo systemctl start kube-controller-manager
```

Verify:

```
sudo systemctl status kube-controller-manager
```
