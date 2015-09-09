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
cat <<'EOF' > kube-controller-pod.yaml
apiVersion: v1
kind: Pod
metadata: 
  name: kube-controller
spec: 
  hostNetwork: true
  volumes:
    - name: "etc-kubernetes"
      hostPath:
        path: "/etc/kubernetes"
    - name: "ssl-certs"
      hostPath:
        path: "/usr/share/ca-certificates"
    - name: "var-run-kubernetes"
      hostPath:
        path: "/var/run/kubernetes"
    - name: "var-lib-kubernetes"
      hostPath:
        path: "/var/lib/kubernetes"
    - name: "etcd-datadir"
      hostPath:
        path: "/var/lib/etcd"
  containers: 
    - name: "etcd"
      image: "b.gcr.io/kuar/etcd:2.1.3"
      args: 
        - "--data-dir=/var/lib/etcd"
        - "--advertise-client-urls=http://127.0.0.1:2379"
        - "--listen-client-urls=http://127.0.0.1:2379"
        - "--listen-peer-urls=http://127.0.0.1:2380"
        - "--name=etcd"
      volumeMounts:
        - mountPath: /var/lib/etcd
          name: "etcd-datadir"
    - name: "kube-apiserver"
      image: "b.gcr.io/kuar/kube-apiserver:1.0.4"
      args: 
        - "--admission-control=NamespaceLifecycle,NamespaceExists,LimitRanger,SecurityContextDeny,ServiceAccount,ResourceQuota"
        - "--allow-privileged=true"
        - "--etcd-servers=http://127.0.0.1:2379"
        - "--tls-cert-file=/var/lib/kubernetes/apiserver.pem"
        - "--tls-private-key-file=/var/lib/kubernetes/apiserver-key.pem"
        - "--client-ca-file=/var/lib/kubernetes/ca.pem"
        - "--insecure-bind-address=0.0.0.0"
        - "--service-cluster-ip-range=10.200.100.0/24"
        - "--service-node-port-range=30000-37000"
        - "--v=2"
      volumeMounts:
        - mountPath: /etc/kubernetes
          name: "etc-kubernetes"
        - mountPath: /var/run/kubernetes
          name: "var-run-kubernetes"
        - mountPath: /var/lib/kubernetes
          name: "var-lib-kubernetes"
    - name: "kube-controller-manager"
      image: "b.gcr.io/kuar/kube-controller-manager:1.0.4"
      args:
        - "--root-ca-file=/var/lib/kubernetes/ca.pem"
        - "--service-account-private-key-file=/var/lib/kubernetes/ca-key.pem"
        - "--master=http://127.0.0.1:8080"
        - "--v=2"
      volumeMounts:
        - mountPath: /var/run/kubernetes
          name: "var-run-kubernetes"
        - mountPath: /var/lib/kubernetes
          name: "var-lib-kubernetes"
    - name: "kube-scheduler"
      image: "b.gcr.io/kuar/kube-scheduler:1.0.4"
      args:
        - "--master=http://127.0.0.1:8080"
        - "--v=2"
EOF
```

Copy the pod manifest to the Kubelets configuration directory:

```
sudo mv kube-controller-pod.yaml /etc/kubernetes/manifests/
```

Verify:

```
docker ps
```
