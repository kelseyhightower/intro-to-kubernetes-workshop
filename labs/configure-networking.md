# Configuring the Network

In this lab you will configure the network between hosts to ensure cross host connectivity. You will also ensure containers can communicate across hosts and reach the internet.

### Getting Containers Online

```
ssh core@nodeX
sudo iptables -t nat -A POSTROUTING ! -d 10.0.0.0/8 -o ens4v1 -j MASQUERADE
```

### Confirm networking

#### Terminal 1

```
ssh core@nodeX
```
```
docker run -t -i --rm busybox /bin/sh
```

```
ip -f inet addr show eth0
```

```
4: eth0: <BROADCAST,UP,LOWER_UP> mtu 1460 qdisc noqueue state UP group default 
    inet 10.200.0.2/24 scope global eth0
       valid_lft forever preferred_lft forever
```

#### Terminal 2

```
ssh core@nodeX
```

```
docker run -t -i --rm busybox /bin/sh
```

```
ping -c 3 10.200.0.2
```

```
ping -c 3 google.com
```

Exit both busybox instances.
