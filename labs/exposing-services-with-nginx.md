# Exposing Services with Nginx

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

### Prep 

Edit etcd hosts on your local machine.

```
sudo vim /etc/hosts
```

```
NGINX_EXTERNAL_IP hello.PROJECT_NAME.io
```

### Configure nginx

```
gcloud compute ssh nginx
```

```
git clone https://github.com/kelseyhightower/intro-to-kubernetes-workshop.git
```

Review the nginx vhost configuration:

```
cat intro-to-kubernetes-workshop/nginx/hello.conf
```

Substitute the project name:

```
sed -i -e 's/PROJECT_NAME/kuarlab/g;' intro-to-kubernetes-workshop/nginx/hello.conf
```

Copy the vhost configuration:

```
sudo mkdir -p /etc/nginx/conf.d
```

```
sudo cp intro-to-kubernetes-workshop/nginx/hello.conf  /etc/nginx/conf.d/
```

### Start nginx

```
sudo docker run -d --net=host \
  -v /etc/nginx/conf.d:/etc/nginx/conf.d \
  nginx
```

### Testing 

#### laptop

```
gcloud compute firewall-rules create default-allow-nginx --allow tcp:80
```

Visit 

```
http://hello.PROJECT_NAME.io
```
