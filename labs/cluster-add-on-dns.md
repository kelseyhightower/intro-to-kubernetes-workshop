# Cluster Add-on: DNS

Kubernetes offers a DNS cluster add-on that provides DNS A and SRV records for Kubernetes services. The heavy lifting is done by SkyDNS, an etcd backed DNS server that supports dynamic updates from the Kubernetes API.

### laptop

Allow add-ons to query the API server

```
gcloud compute firewall-rules create default-allow-local-api \
  --allow tcp:8080 \
  --source-ranges 10.200.0.0/16
```

Download the SkyDNS replication controller configuration:

```
wget https://kuar.io/skydns-rc.yaml
```

Edit the SkyDNS rc config:

```
vim skydns-rc.yaml
```

```
- -kube_master_url=http://node0.c.PROJECT_ID.internal:8080
```

Create the SkyDNS replication controller:

```
kubectl create -f skydns-rc.yaml
```

Next create the SkyDNS service:

```
kubectl create -f https://kuar.io/skydns-svc.yaml
```

### Validate

```
kubectl get rc --all-namespaces
```

Wait for "Running" status

```
kubectl get pods --namespace=kube-system --watch
```

Test DNS lookups

```
wget https://kuar.io/busybox.yaml
```

```
cat busybox.yaml
```

```
kubectl create -f busybox.yaml
```

```
kubectl get pods busybox
```

```
kubectl exec busybox -- nslookup kubernetes
```
