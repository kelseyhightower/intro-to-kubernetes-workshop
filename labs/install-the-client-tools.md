# Installing the client tools

## Darwin

### etcdctl

```
wget http://storage.googleapis.com/k8s/darwin/etcdctl
```

### fleetctl

```
wget http://storage.googleapis.com/k8s/darwin/fleetctl
```

### kubecfg

```
wget http://storage.googleapis.com/k8s/darwin/kubecfg
```

## Linux

### etcdctl

```
wget http://storage.googleapis.com/k8s/linux/etcdctl
```

### fleetctl

```
wget http://storage.googleapis.com/k8s/linux/fleetctl
```

### kubecfg

```
wget http://storage.googleapis.com/k8s/linux/kubecfg
```

## Add client tools to your path

```
chmod +x etcdctl fleetctl kubecfg
mkdir -p /usr/local/bin/
mv etcdctl fleetctl kubecfg /usr/local/bin/
```

