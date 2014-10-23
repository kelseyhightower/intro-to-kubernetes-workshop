# Installing the client tools

## Install the Google 'gcloud' SDK

Follow the instructions [here](https://cloud.google.com/sdk/) to install gcloud.
Then, set the Google Cloud project that you want to use for this lab as the default, by running:

```
gcloud config set project <your-project-name>
```

Note: if you don't yet have a Google Cloud project created, then follow the signup
instructions [here](https://cloud.google.com/compute/docs/signup).

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

