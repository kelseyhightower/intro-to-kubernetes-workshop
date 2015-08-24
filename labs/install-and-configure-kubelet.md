# Install and configure the Kubelet

In this lab you will install the Kubelet on each worker node in your cluster.

## nodeX

```
ssh core@nodeX
```

Download the kubelet unit file:

```
sudo curl https://kuar.io/kubelet-basic.service \
  -o /etc/systemd/system/kubelet.service
```

Configure the api-servers flag:

```
sudo sed -i -e "s/CONTROLLER_NODE_HOSTNAME/${CONTROLLER_NODE_HOSTNAME}/g;" /etc/systemd/system/kubelet.service
```

```
cat /etc/systemd/system/kubelet.service
```

```
sudo systemctl daemon-reload
sudo systemctl enable kubelet
sudo systemctl start kubelet
```

### Verify

```
sudo systemctl status kubelet
```
