# Generate Server and Client Certs

In this labs you will use cfssl to generate client and server TLS certs.

## Generate the kube-apiserver server cert

### node0

```
gcloud compute ssh node0
```

Create a CSR for the API server:

```
curl -O https://storage.googleapis.com/configs.kuar.io/apiserver-csr.json
```

### Customize apiserver-csr.json

Get the PROJECT_ID:

```
PROJECT_ID=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/project/project-id)
```

Get the EXTERNAL_IP:

```
EXTERNAL_IP=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip)
```

Substitute the PROJECT_ID:

```
sed -i -e "s/PROJECT_ID/${PROJECT_ID}/g;" apiserver-csr.json
```

Substitute the EXTERNAL_IP:

```
sed -i -e "s/EXTERNAL_IP/${EXTERNAL_IP}/g;" apiserver-csr.json
```

Review the apiserver CSR:

```
cat apiserver-csr.json
```

### Generate the API server private key and TLS cert

```
cfssl gencert \
-ca=ca.pem \
-ca-key=ca-key.pem \
-config=ca-config.json \
-profile=server \
apiserver-csr.json | cfssljson -bare apiserver
```

Results

```
apiserver-key.pem
apiserver.csr
apiserver.pem
```

## Generate the admin client cert 

```
curl -O https://storage.googleapis.com/configs.kuar.io/admin-csr.json
```

```
cfssl gencert \
-ca=ca.pem \
-ca-key=ca-key.pem \
-config=ca-config.json \
-profile=client \
admin-csr.json | cfssljson -bare admin
```

Results

```
admin-key.pem
admin.csr
admin.pem
```
