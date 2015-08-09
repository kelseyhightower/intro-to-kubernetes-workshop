# Generate Server and Client Certs

## Generate the kube-apiserver server cert

```
cat <<EOF > apiserver-csr.json
{
  "CN": "*.c.PROJECT_ID.internal",
  "hosts": [
    "127.0.0.1",
    "EXTERNAL_IP",
    "*.c.PROJECT_ID.internal"
  ],
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
    {
      "C": "US",
      "L": "Portland",
      "O": "Kubernetes",
      "OU": "API Server",
      "ST": "Oregon"
    }
  ]
}
EOF
```

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
cat <<EOF > admin-csr.json
{
  "CN": "admin",
  "hosts": [""],
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
    {
      "C": "US",
      "L": "Portland",
      "O": "Kubernetes",
      "OU": "Cluster Admins",
      "ST": "Oregon"
    }
  ]
}
EOF
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
