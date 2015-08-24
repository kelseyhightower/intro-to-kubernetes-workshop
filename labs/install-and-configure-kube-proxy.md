# Install and configure the kube-proxy

In this lab you will install the kube-proxy on each node in your Kubernetes cluster.

## nodeX

```
ssh core@nodeX
```

Download the kube-proxy pod:

```
sudo curl -O https://kuar.io/kube-proxy-basic-pod.yaml
```

Configure the master flag:

```
export CONTROLLER_NODE_HOSTNAME="your controller node hostname"
```

```
sudo sed -i -e "s/CONTROLLER_NODE_HOSTNAME/${CONTROLLER_NODE_HOSTNAME}/g;" kube-proxy-basic-pod.yaml
```

```
cat kube-proxy-basic-pod.yaml
```

Start the kube-proxy service:

```
sudo mv kube-proxy-basic-pod.yaml /etc/kubernetes/manifests/kube-proxy-pod.yaml
```

Verify:

```
docker ps
```

Check iptables

```
sudo iptables -vL -n -t nat
```

Repeat the steps from above on the other nodes.
