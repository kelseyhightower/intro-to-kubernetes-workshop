# Install and configure the Kubernetes controller

## Install and configure the Kubelet

### node0

```
gcloud compute ssh node0
```

### Download Kubernetes release tar

```
wget https://github.com/kubernetes/kubernetes/releases/download/v1.0.6/kubernetes.tar.gz
tar -xvf kubernetes.tar.gz
tar -xvf kubernetes/server/kubernetes-server-linux-amd64.tar.gz
sudo cp kubernetes/server/bin/kubelet /opt/bin/
sudo cp kubernetes/platforms/linux/amd64/kubectl /opt/bin/
sudo chmod +x /opt/bin/kubelet /opt/bin/kubectl 
```

### Create the kubelet systemd unit file:

```
curl -O https://storage.googleapis.com/configs.kuar.io/kubelet.service
```

Edit the path to the kubelet. Change

```
ExecStart=/usr/bin/kubelet \
```

to:

```
ExecStart=/opt/bin/kubelet \
```

Configure the api-servers flag:

```
PROJECT_ID=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/project/project-id)
```

```
sed -i -e "s/PROJECT_ID/${PROJECT_ID}/g;" kubelet.service
```

Review the kubelet unit file:

```
cat kubelet.service
```

Start the kubelet service:

```
sudo mv kubelet.service /etc/systemd/system/
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
sudo mkdir -p /var/lib/etcd
sudo mkdir -p /var/lib/kubernetes
sudo mkdir -p /var/run/kubernetes
```

Copy certs

```
sudo cp apiserver-key.pem apiserver.pem ca.pem ca-key.pem /var/lib/kubernetes/
```

Create the Kubernetes controller pod manifest:

```
curl -O https://storage.googleapis.com/kuar/kube-controller-pod.yaml
```

Copy the pod manifest to the Kubelets configuration directory:

```
sudo mv kube-controller-pod.yaml /etc/kubernetes/manifests/
```

Verify:

```
docker ps
```
