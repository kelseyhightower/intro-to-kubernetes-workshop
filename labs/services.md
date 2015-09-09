# Creating and managing services

* Create a service using the kubectl cli tool
* Map a service to pod lables

### Listing Services

```
kubectl get services
```

### Creating Services

```
cat <<EOF > inspector-svc.yaml
apiVersion: v1
kind: Service
metadata:
  name: inspector
  labels:
    app: inspector
spec:
  type: NodePort
  selector:
    app: inspector
    track: stable
  ports:
  - name: http
    nodePort: 36000
    port: 80
    protocol: TCP
EOF
```

```
kubectl create -f inspector-svc.yaml
```

#### Validation
```
kubectl describe service inspector
```

## Create the inspector firewall rule

#### laptop

```
gcloud compute firewall-rules create default-allow-inspector --allow tcp:36000
```

Try hitting the external IP address for each instance in your web browser on port 36000

```
gcloud compute instances list
```

```
curl EXTERNAL_IP_ADDRESS:36000
```
