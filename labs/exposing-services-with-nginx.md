# Exposing Services with Nginx

### Provision the nginx VM

```
gcloud compute instances create nginx \
 --image-project coreos-cloud \
 --image coreos-stable-835-8-0-v20151201 \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward
```

### Prep 

```
NGINX_EXTERNAL_IP=$(gcloud compute ssh nginx --command \
  "curl -H 'Metadata-Flavor: Google' \
   http://metadata.google.internal/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip")
```

```
PROJECT_ID=$(gcloud compute ssh nginx --command \
  "curl -H 'Metadata-Flavor: Google' \
  http://metadata.google.internal/computeMetadata/v1/project/project-id")
```

Edit `/etc/hosts` on your local machine. First run the following command:

```
echo "${NGINX_EXTERNAL_IP} inspector.${PROJECT_ID}.io"
```

Append the output to your `/etc/hosts` file

### Configure nginx

```
gcloud compute ssh nginx
```

Create the inspector nginx vhost configuration:

```
cat <<EOF > inspector.conf
upstream inspector {
    least_conn;
    server node0.c.PROJECT_ID.internal:36000;
    server node1.c.PROJECT_ID.internal:36000;
}

server {
    server_name         inspector.PROJECT_ID.io;
    location / {
        proxy_pass http://inspector;
    }
}
EOF
```

Substitute the project name:

```
PROJECT_ID=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/project/project-id)
```

```
sed -i -e "s/PROJECT_ID/${PROJECT_ID}/g;" inspector.conf
```

```
cat inspector.conf
```

Copy the vhost configuration:

```
sudo mkdir -p /etc/nginx/conf.d
```

```
sudo mv inspector.conf  /etc/nginx/conf.d/
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

Every page refresh should show different MAC and IP address:

```
http://inspector.PROJECT_ID.io/net
```
