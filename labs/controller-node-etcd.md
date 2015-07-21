# Bootstrapping etcd

### node0

```
gcloud compute ssh node0
```

Download the etcd unit file:

```
sudo curl https://kuar.io/etcd.service \
  -o /etc/systemd/system/etcd.service
```

Review the etcd unit file:

```
cat /etc/systemd/system/etcd.service
```

Start the etcd service:

```
sudo systemctl daemon-reload
sudo systemctl enable etcd
sudo systemctl start etcd
```
