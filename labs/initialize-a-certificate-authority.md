# Initialize a certificate authority

The first step in securing Docker and Kubernetes is to set up a PKI infrastructure for managing TLS certificates.

https://github.com/cloudflare/cfssl

## Download cfssl

### node0

```
gcloud compute ssh node0
```

```
sudo curl -o /opt/bin/cfssl https://kuar.io/cfssl
sudo chmod +x /opt/bin/cfssl
```

```
sudo curl -o /opt/bin/cfssljson https://kuar.io/cfssljson
sudo chmod +x /opt/bin/cfssljson
```

## Initialize a CA

```
cat <<EOF > ca-config.json
{
  "signing": {
    "default": {
      "expiry": "8760h"
    },
    "profiles": {
      "server": {
        "usages": ["signing", "key encipherment", "server auth"],
        "expiry": "8760h"
      },
      "client": {
        "usages": ["signing","key encipherment","client auth"],
        "expiry": "8760h"
      }
    }
  }
}
EOF
```

```
cat <<EOF > ca-csr.json
{
  "CN": "Kubernetes CA",
  "key": {
    "algo": "rsa",
    "size": 2048
  },
  "names": [
    {
      "C": "US",
      "L": "Portland",
      "O": "Kubernetes",
      "OU": "CA",
      "ST": "Oregon"
    }
  ]
}
EOF
```

```
cfssl gencert -initca ca-csr.json | cfssljson -bare ca
```

Results:

```
ca-key.pem
ca.csr
ca.pem
```
