# Install and configure the kube-proxy

## node0

```
gcloud compute ssh node0
```

Download the kube-proxy pod:

```
sudo curl -O https://kuar.io/kube-proxy-pod.yaml
```

Configure the master flag:

```
PROJECT_ID=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/project/project-id)
```

```
sudo sed -i -e "s/PROJECT_ID/${PROJECT_ID}/g;" kube-proxy-pod.yaml
```

```
cat kube-proxy-pod.yaml
```

Start the kube-proxy service:

```
sudo cp kube-proxy-pod.yaml /etc/kubernetes/manifests
```

Verify:

```
docker ps
```

Check iptables

```
sudo iptables -vL -n -t nat
```

### node1

```
gcloud compute ssh node1
```

Repeat the steps from above.
