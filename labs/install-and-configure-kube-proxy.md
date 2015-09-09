# Install and configure the kube-proxy

## node0

```
gcloud compute ssh node0
```

## Create the kube-proxy pod

```
cat <<EOF > kube-proxy-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: kube-proxy
  version: 1.0.4
spec:
  hostNetwork: true
  volumes:
    - name: "etc-kubernetes"
      hostPath:
        path: "/etc/kubernetes"
    - name: "ssl-certs"
      hostPath:
        path: "/usr/share/ca-certificates"
    - name: "usr"
      hostPath:
        path: "/usr"
    - name: "lib64"
      hostPath:
        path: "/lib64"
  containers:
    - name: "kube-proxy"
      image: "b.gcr.io/kuar/kube-proxy:1.0.4"
      args:
        - "--master=http://node0.c.PROJECT_ID.internal:8080"
        - "--v=2"
      securityContext:
        privileged: true
      volumeMounts:
        - mountPath: /etc/kubernetes
          name: "etc-kubernetes"
        - mountPath: /etc/ssl/certs
          name: "ssl-certs"
        - mountPath: /usr
          name: "usr"
        - mountPath: /lib64
          name: "lib64"
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

Check iptables (search for rules with 'kubernetes' comments):

```
sudo iptables -vL -n -t nat
```

### node1

```
gcloud compute ssh node1
```

Repeat the steps from above.
