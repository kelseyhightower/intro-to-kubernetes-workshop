## Install and configure Docker

In this lab you will install and configure Docker on node0 and node1.

### node00X

```
ssh core@
```

#### Download and configure the docker unit file

```
sudo curl https://kuar.io/docker.service -o /etc/systemd/system/docker.service
```

Set the `--bip` flag to `10.200.0.1/24`:

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
