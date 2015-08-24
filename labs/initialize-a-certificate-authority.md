# Initialize a certificate authority

In this lab you will setup the necessary PKI infrastructure to secure the Kuberentes API for remote communication. This lab will leverage CloudFlare's PKI toolkit, [cfssl](https://github.com/cloudflare/cfssl), to bootstrap a Certificate Authority.

## Download and install cfssl

### node0

```
ssh core@nodeX
```

```
sudo mkdir -p /opt/bin
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

### Create the CA configuration file

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

### Generate the CA certificate and private key

Create the CA CSR:

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

Generate the CA certificate and private key:

```
cfssl gencert -initca ca-csr.json | cfssljson -bare ca
```

Results:

```
ca-key.pem
ca.csr
ca.pem
```
