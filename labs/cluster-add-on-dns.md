# Cluster Add-on: DNS

Kubernetes offers a DNS cluster add-on that provides DNS A and SRV records for Kubernetes services. The heavy lifting is done by SkyDNS, an etcd backed DNS server that supports dynamic updates from the Kubernetes API.

### laptop

Create the SkyDNS replication controller configuration:

```
curl -O https://storage.googleapis.com/configs.kuar.io/skydns-rc.yaml
```

Edit the SkyDNS rc config:

```
PROJECT_ID=$(gcloud compute ssh node0 --command \
  "curl -H 'Metadata-Flavor: Google' \
  http://metadata.google.internal/computeMetadata/v1/project/project-id")
```

```
sed -i -e "s/PROJECT_ID/${PROJECT_ID}/g;" skydns-rc.yaml
```

Create the SkyDNS replication controller:

```
kubectl create -f skydns-rc.yaml
```

Next create the SkyDNS service:

```
curl -O https://storage.googleapis.com/configs.kuar.io/skydns-svc.yaml
```

```
kubectl create -f skydns-svc.yaml
```

### Validate

```
kubectl get rc --all-namespaces
```

Wait for "Running" status

```
kubectl get pods --namespace=kube-system --watch-only
```

## Test DNS lookups

```
curl -O https://storage.googleapis.com/configs.kuar.io/busybox-pod.yaml
```

```
kubectl create -f busybox-pod.yaml
```

```
kubectl get pods busybox
```

```
kubectl exec busybox -- nslookup kubernetes
```
