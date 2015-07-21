## Configure the Docker bridge

Connect to your first node by typing: `gcloud compute ssh node1`

Once on the server:

```
$ sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

Edit the Docker unit file:
```
    [Unit]
    Description=Docker Application Container Engine
    Documentation=http://docs.docker.io
    [Service]
    ExecStart=/usr/bin/docker --daemon \
      --bip=10.200.0.1/24 \
      --iptables=false \
      --ip-masq=false \
      --host=unix:///var/run/docker.sock \
      --storage-driver=overlay
    Restart=on-failure
    RestartSec=5
    [Install]
    WantedBy=multi-user.target
```


```
$ sudo systemctl daemon-reload
$ sudo systemctl enable docker
$ sudo systemctl start docker
```

Do the same for the nodes 2 and 3, remember to chang the bip flag!