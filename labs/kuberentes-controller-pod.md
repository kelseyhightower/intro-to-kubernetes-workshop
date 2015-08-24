# Install and configure the Kubernetes controller

## Install and configure the Kubelet

### Controller Node

Pick one of the three nodes to be the controller

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
export CONTROLLER_NODE_HOSTNAME=`hostname`
```

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

## Deploy the Kubernetes Controller

```
sudo mkdir -p /etc/kubernetes/manifests
sudo mkdir -p /var/run/kubernetes
sudo mkdir -p /var/lib/etcd
```

Copy certs

```
sudo cp apiserver-key.pem apiserver.pem ca.pem /var/run/kubernetes/
```

Download the controller pod manifest:

```
sudo curl -o /etc/kubernetes/manifests/kube-controller-pod.yaml \
  https://kuar.io/kube-controller-pod.yaml
```

Verify:

```
docker ps
```

### Allow external access to the API server secure port

```
gcloud compute firewall-rules create default-allow-kubernetes-secure \
  --allow tcp:6443 \
  --source-ranges 0.0.0.0/0
```
