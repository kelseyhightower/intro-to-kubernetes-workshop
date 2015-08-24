## Install and configure Docker

In this lab you will install and configure Docker.

### nodeX

```
ssh core@nodeX
```

#### Download and configure the docker unit file

```
sudo curl https://kuar.io/docker.service -o docker.service
```

Set the `--bip` flag to `10.200.X.1/24`, where X == node number. For example 

```
node80 = 10.200.80.1/24
```

```
sudo sed -i -e "s/BRIDGE_IP/10.200.X.1\/24/g;" docker.service
```
```
cat docker.service
```

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

#### Fix broken docker

```
sudo systemctl stop docker
sudo ifconfig docker0 down
sudo brctl delbr docker0
sudo mv /etc/systemd/system/docker /etc/systemd/system/docker.service
```
