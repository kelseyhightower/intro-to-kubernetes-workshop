# Cluster Add-on: DNS

Kubernetes offers a DNS cluster add-on that provides DNS A and SRV records for Kubernetes services. The heavy lifting is done by SkyDNS, an etcd backed DNS server that supports dynamic updates from the Kubernetes API.

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
- name: kube2sky
  image: gcr.io/google_containers/kube2sky:1.11
  resources:
    limits:
      cpu: 100m
      memory: 50Mi
  args:
  # command = "/kube2sky"
  - -domain=cluster.local
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
kubectl get rc --all-namespaces
```
