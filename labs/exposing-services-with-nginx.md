# Exposing Services with Nginx

### Prep 

Edit etcd hosts on your local machine.

```
vim /etc/hosts
```

```
NGINX_PUBLIC_IP hello.PROJECT_NAME.io
NGINX_PUBLIC_IP canary.hello.PROJECT_NAME.io
```

### Provision nginx

```
gcloud compute instances create nginx \
  --image-project coreos-cloud \
  --image coreos-stable-717-3-0-v20150710 \
  --boot-disk-size 200GB \
  --machine-type n1-standard-1 \
  --can-ip-forward \
  --scopes compute-rw
```

#### Configure nginx

```
gcloud compute ssh nginx
```

```
git clone https://github.com/kelseyhightower/intro-to-kubernetes-workshop.git
```

```
sudo mkdir -p /etc/nginx/conf.d
sudo cp intro-to-kubernetes-workshop/nginx/*.conf  /etc/nginx/conf.d/
```

#### Start nginx

```
sudo docker run -d --net=host \
  -v /etc/nginx/conf.d:/etc/nginx/conf.d \
  nginx
```
