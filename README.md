# kubernetes_quickly

Node - VM или физическая машина
Pod -  small deployable unit


install Docker
install minicube

```
minikube start --nodes=2
minikube status
minikube delete
```

```
kubectl get nodes
```

```
kubectl get pods -A
```

## Start pods
```kubectl get pods
# No resources found in default namespace.
```

###Create deployment.yml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: amigoscode/kubernetes:springboot-react-fullstack-v1
        resources:
          limits:
            memory: "512Mi"
            cpu: "500m"
        ports:
        - containerPort: 8080

---

apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
  - port: 80
    targetPort: 8080

```

```
kubectl apply -f deployment.yml

# deployment.apps/myapp configured
# service/myapp created
```

```
kubectl get svc
```

### Open service in browser
```
minikube service myapp
```
