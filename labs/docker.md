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
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
```

Verify

```
ifconfig
docker version
```

### node2

```
gcloud compute ssh node2
```

Download the docker unit file:

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

```
sudo vim /etc/systemd/system/docker.service
```

```
--bip=10.200.2.1/24 \
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

### node3

```
gcloud compute ssh node3
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
--bip=10.200.3.1/24 \
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
