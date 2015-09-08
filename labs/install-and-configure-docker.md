## Install and configure the Docker

In this lab you will install and configure Docker on node0 and node1.

### Copy Docker systemd unit file

Docker will run under systemd. Copy the docker.service unit file each node.

```
gcloud compute copy-files units/docker.service node0:~/
```
```
gcloud compute copy-files units/docker.service node1:~/
```

### Configure the Docker Engine

#### node0

```
gcloud compute ssh node0
```

Configure the docker unit file

Set the `--bip` flag to `10.200.0.1/24`:

```
sudo sed -i -e "s/BRIDGE_IP/10.200.0.1\/24/g;" /etc/systemd/system/docker.service
```

Review the docker unit file.

```
cat docker.service
```

Copy the docker unit file into place.

```
sudo mv docker.service /etc/systemd/system/docker.service
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

#### node1

```
gcloud compute ssh node1
```

#### Download and configure the docker unit file

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

Set the `--bip` flag to `10.200.1.1/24`:

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

#### Verify

```
ifconfig
docker version
```
