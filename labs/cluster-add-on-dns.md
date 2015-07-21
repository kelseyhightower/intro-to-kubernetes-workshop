# Cluster Add-on: DNS

Kubernetes offers a DNS cluster add-on that provides DNS A and SRV records for Kubernetes services. The heavy lifting is done by SkyDNS, an etcd backed DNS server that supports dynamic updates from the Kubernetes API.

### laptop

Allow add-ons to query the API server

```
gcloud compute firewall-rules create default-allow-local-api \
  --allow tcp:8080 \
  --source-ranges 10.200.0.0/16
```

### node0

```
gcloud compute ssh node0
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
- -kube_master_url=http://node0.c.PROJECT_NAME.internal:8080
```

Create the SkyDNS replication controller:

```
/opt/bin/kubectl create -f skydns-rc.yaml
```

Next create the SkyDNS service:

```
/opt/bin/kubectl create -f https://kuar.io/skydns-svc.yaml
```

### Validate

```
/opt/bin/kubectl get rc --all-namespaces
```

Test DNS lookups

```
wget https://kuar.io/busybox.yaml
```

```
cat busybox.yaml
```

```
/opt/bin/kubectl create -f busybox.yaml
```

```
/opt/bin/kubectl get pods busybox
```

```
/opt/bin/kubectl exec busybox -- nslookup kubernetes
```
