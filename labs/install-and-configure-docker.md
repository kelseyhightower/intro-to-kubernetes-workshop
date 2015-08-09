## Configure the Docker bridge


### node0

```
gcloud compute ssh node0
```

Download the docker unit file:

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

Edit:

```
sudo vim /etc/systemd/system/docker.service
```

```
--bip=10.200.0.1/24 \
```

Start docker:

```
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
```

Verify

```
ifconfig
docker version
```

### node1

```
gcloud compute ssh node1
```

Download the docker unit file:

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

```
sudo vim /etc/systemd/system/docker.service
```

```
--bip=10.200.1.1/24 \
```

Start docker:

```
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
```

Verify

```
ifconfig
docker version
```
