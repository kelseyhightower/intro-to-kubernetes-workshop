## Configure the Docker bridge

Connect to your first node by typing: `gcloud compute ssh node1`

Once on the server:

```
$ sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

Then start docker:

```
$ sudo systemctl daemon-reload
$ sudo systemctl enable docker
$ sudo systemctl start docker
```

Confirm docker is running by typing `docker version`:

```
Client version: 1.6.2
Client API version: 1.18
Go version (client): go1.4.2
Git commit (client): 7c8fca2-dirty
OS/Arch (client): linux/amd64
Server version: 1.6.2
Server API version: 1.18
Go version (server): go1.4.2
Git commit (server): 7c8fca2-dirty
OS/Arch (server): linux/amd64
```

Do the same for the nodes 2 and 3, remember to change the bip flag in the docker unit file!

Node 2 should be:
```
ExecStart=/usr/bin/docker --daemon \
  --bip=10.200.0.2/24 \
  --iptables=false \
```

Node 3 should be:
```
ExecStart=/usr/bin/docker --daemon \
  --bip=10.200.0.3/24 \
  --iptables=false \
```

Docker is now setup!

Next Step: [Configure Networking](networking.md)