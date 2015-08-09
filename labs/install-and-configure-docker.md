## Install and configure the Docker

In this lab you will install and configure Docker on node0 and node1.

### node0

```
gcloud compute ssh node0
```

#### Download and configure the docker unit file

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

Configure the `--bip` flag:

```
sudo sed -i -e "s/BRIDGE_IP/10.200.0.1\/24/g;" /etc/systemd/system/docker.service
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

#### Verify

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
sudo sed -i -e "s/BRIDGE_IP/10.200.1.1\/24/g;" /etc/systemd/system/docker.service
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
