# Exposing Services with Nginx

### Provision nginx

```
gcloud compute instances create nginx \
  --image-project coreos-cloud \
  --image coreos-stable-723-3-0-v20150804 \
  --boot-disk-size 200GB \
  --machine-type n1-standard-1 \
  --can-ip-forward \
  --scopes compute-rw
```

### Prep 

```
gcloud config list project
gcloud compute instances list
```

Edit etcd hosts on your local machine.

```
sudo echo "NGINX_EXTERNAL_IP inspector.PROJECT_ID.io" >> /etc/hosts
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
cat intro-to-kubernetes-workshop/nginx/inspector.conf
```

Substitute the project name:

```
PROJECT_ID=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/project/project-id)
```

```
sed -i -e "s/PROJECT_ID/${PROJECT_ID}/g;" intro-to-kubernetes-workshop/nginx/inspector.conf
```

```
cat intro-to-kubernetes-workshop/nginx/inspector.conf
```

Copy the vhost configuration:

```
sudo mkdir -p /etc/nginx/conf.d
```

```
sudo cp intro-to-kubernetes-workshop/nginx/inspector.conf  /etc/nginx/conf.d/
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
http://inspector.PROJECT_ID.io
```
