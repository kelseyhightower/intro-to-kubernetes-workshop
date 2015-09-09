# Install and configure the Kubernetes controller

## Install and configure the Kubelet

### node0

```
gcloud compute ssh node0
```

### Create the kubelet systemd unit file:

```
cat <<'EOF' > kubelet.service
[Unit]
Description=Kubernetes Kubelet
Documentation=https://github.com/GoogleCloudPlatform/kubernetes

[Service]
ExecStartPre=/usr/bin/mkdir -p /etc/kubernetes/manifests
ExecStart=/usr/bin/kubelet \
  --api-servers=http://node0.c.PROJECT_ID.internal:8080 \
  --allow-privileged=true \
  --cluster-dns=10.200.100.10 \
  --cluster-domain=cluster.local \
  --config=/etc/kubernetes/manifests \
  --v=2
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF
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
curl -O https://storage.googleapis.com/configs.kuar.io/kube-controller-pod.yaml
```

Copy the pod manifest to the Kubelets configuration directory:

```
sudo mv kube-controller-pod.yaml /etc/kubernetes/manifests/
```

Verify:

```
docker ps
```
