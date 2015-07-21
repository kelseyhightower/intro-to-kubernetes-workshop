## Configure the Docker bridge


### node1

```
gcloud compute ssh node1
```

Download the docker unit file:

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

```
cat /etc/systemd/system/docker.service
```

Start docker:

```
$ sudo systemctl daemon-reload
$ sudo systemctl enable docker
$ sudo systemctl start docker
```

```
ifconfig
docker version
```

### node2

```
gcloud compute ssh node2
```

Edit `/etc/systemd/system/docker.service`

```
--bip=10.200.2.1/24 \
```

### node3

```
gcloud compute ssh node3
```

Edit `/etc/systemd/system/docker.service`

```
--bip=10.200.3.1/24 \
```

Next Step: [Configure Networking](networking.md)
