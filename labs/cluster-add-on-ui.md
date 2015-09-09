# Cluster Add-on: UI


## Create kube-system namespace:

### laptop

```
cat <<EOF > kube-system-ns.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: kube-system
EOF
```

```
kubectl create -f kube-system-ns.yaml 
```

List the all namespaces:

```
kubectl get namespaces
```

## Spawn kube-ui Replication Controller:

```
cat <<EOF > kube-ui-rc.yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: kube-ui-v1
  namespace: kube-system
  labels:
    k8s-app: kube-ui
    version: v1
    kubernetes.io/cluster-service: "true"
spec:
  replicas: 1
  selector:
    k8s-app: kube-ui
    version: v1
  template:
    metadata:
      labels:
        k8s-app: kube-ui
        version: v1
        kubernetes.io/cluster-service: "true"
    spec:
      containers:
      - name: kube-ui
        image: gcr.io/google_containers/kube-ui:v1.1
        resources:
          limits:
            cpu: 100m
            memory: 50Mi
        ports:
        - containerPort: 8080
EOF
```

```
kubectl create -f kube-ui-rc.yaml
```

### Create the kube-ui Service:

```
cat <<EOF > kube-ui-svc.yaml
apiVersion: v1
kind: Service
metadata:
  name: kube-ui
  namespace: kube-system
  labels:
    k8s-app: kube-ui
    kubernetes.io/cluster-service: "true"
    kubernetes.io/name: "KubeUI"
spec:
  selector:
    k8s-app: kube-ui
  ports:
  - port: 80
    targetPort: 8080
EOF
```

```
kubectl create -f kube-ui-svc.yaml
```

Verify:

```
kubectl --namespace=kube-system get rc,services
```

At this point the Kubernetes UI add-on should be up and running. The Kubernetes API server provides access to the UI via the /ui endpoint.

```
kubectl proxy --port=8080 &
```

The UI is available at http://127.0.0.1:8080/api/v1/proxy/namespaces/kube-system/services/kube-ui/#/dashboard/ on the client machine.
