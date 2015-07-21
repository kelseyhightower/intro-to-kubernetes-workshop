# Deploying the Scheduler

### node0 

```
gcloud compute ssh node0
```

Download the kube-scheduler unit file:

```
sudo curl https://kuar.io/kube-scheduler.service \
  -o /etc/systemd/system/kube-scheduler.service
```

Review the kube-scheduler unit file:

```
cat /etc/systemd/system/kube-scheduler.service
```

Start the kube-scheduler service:

```
sudo systemctl daemon-reload
sudo systemctl enable kube-scheduler
sudo systemctl start kube-scheduler
```
