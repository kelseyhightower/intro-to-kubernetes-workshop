# Install and configure the Docker

In this lab you will install and configure Docker on node0 and node1.

## Configure the Docker Engine

### node0

```
gcloud compute ssh node0
```

### Create the docker systemd unit file

```
curl -O https://storage.googleapis.com/configs.kuar.io/docker.service
```

Configure the docker unit file

Set the `--bip` flag to `10.200.0.1/24`:

```
sed -i -e "s/BRIDGE_IP/10.200.0.1\/24/g;" docker.service
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
ip addr show docker0
```

```
docker version
```

### node1

```
gcloud compute ssh node1
```

### Create the docker systemd unit file

```
curl -O https://storage.googleapis.com/configs.kuar.io/docker.service
```

Configure the docker unit file

Set the `--bip` flag to `10.200.1.1/24`:

```
sudo sed -i -e "s/BRIDGE_IP/10.200.1.1\/24/g;" docker.service
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
ip addr show docker0
```
```
docker version
```
