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

Set the `--bip` flag to `10.200.0.1/24` (docker0 interface address which will be used by docker daemon) and `--log-level=error` flag to suppress docker verbosity:

```
sudo sed -i -e "s/BRIDGE_IP/10.200.0.1\/24 --log-level=error/g;" /etc/systemd/system/docker.service
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

#### Download and configure the docker unit file

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

Set the `--bip` flag to `10.200.1.1/24` and `--log-level` flag to `error`:

```
sudo sed -i -e "s/BRIDGE_IP/10.200.1.1\/24 --log-level=error/g;" /etc/systemd/system/docker.service
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
