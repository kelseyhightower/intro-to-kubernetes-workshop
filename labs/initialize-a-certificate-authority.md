# Initialize a certificate authority

In this lab you will setup the necessary PKI infrastructure to secure the Kuberentes API for remote communication. This lab will leverage CloudFlare's PKI toolkit, [cfssl](https://github.com/cloudflare/cfssl), to bootstrap a Certificate Authority.

## Download and install cfssl

### node0

```
gcloud compute ssh node0
```

```
sudo mkdir -p /opt/bin
```

```
sudo curl -o /opt/bin/cfssl https://storage.googleapis.com/bin.kuar.io/cfssl
sudo chmod +x /opt/bin/cfssl
```

```
sudo curl -o /opt/bin/cfssljson https://storage.googleapis.com/bin.kuar.io/cfssljson
sudo chmod +x /opt/bin/cfssljson
```

## Initialize a CA

### Create the CA configuration file

```
curl -O https://storage.googleapis.com/configs.kuar.io/ca-config.json
```

### Generate the CA certificate and private key

Create the CA CSR:

```
curl -O https://storage.googleapis.com/configs.kuar.io/ca-csr.json
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
