Create Kubernetes routes.

```
$ gcloud compute routes create default-route-10-200-0-0-24 \
    --destination-range 10.200.0.0/24 \
    --next-hop-instance node0

$ gcloud compute routes create default-route-10-200-1-0-24 \
    --destination-range 10.200.1.0/24 \
    --next-hop-instance node1

$ gcloud compute routes create default-route-10-200-2-0-24 \
    --destination-range 10.200.2.0/24 \
    --next-hop-instance node2

$ gcloud compute routes create default-route-10-200-3-0-24 \
    --destination-range 10.200.3.0/24 \
    --next-hop-instance node3
```

Setup Client SSH Tunnel to Master

`gcloud compute ssh node0 -- -f -nNT -L 8080:127.0.0.1:8080`


Setup masquerading

#FIXME need for loop?
`gcloud compute ssh node0 --command "sudo iptables -t nat -A POSTROUTING ! -d 10.0.0.0/8 -o ens4v1 -j MASQUERADE"`

Confirm networking

`gcloud compute ssh node0`
`docker run -t -i --rm busybox /bin/sh`

You are inside the container, run this command:

`ip -f inet addr show eth0`

And get your container's ip address:

```
    4: eth0: <BROADCAST,UP,LOWER_UP> mtu 1460 qdisc noqueue state UP group default
        inet 10.200.0.2/24 scope global eth0
           valid_lft forever preferred_lft forever
```
Open another terminal and launch a busybox container on a different node:

`gcloud compute ssh node1`
`docker run -t -i --rm busybox /bin/sh`

At the command prompt ping the IP address of the first busybox container:

`ping -c 3 10.200.0.2`

You should get a response:

```
PING 10.200.0.2 (10.200.0.2): 56 data bytes
64 bytes from 10.200.0.2: seq=0 ttl=62 time=0.914 ms
64 bytes from 10.200.0.2: seq=1 ttl=62 time=0.678 ms
64 bytes from 10.200.0.2: seq=2 ttl=62 time=0.667 ms
--- 10.200.0.2 ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.667/0.753/0.914 ms
```

While you're there, confirm your container can talk to the outside:

`ping -c google.com`


If you get simliar output it means you’ve successfully setup routes between two Docker hosts. Type the exit command at both busybox command prompts to exit the containers.

Next Step: (Something)[http://google.com]