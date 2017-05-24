# psgsk8s
## 4. Kubernetes Architecture


## 6. Working with Pods
### 2 Deploying Your First Pod
```
apiVersion: v1
kind: Pod
metadata:
  name: hello-pod
spec:
  containers:
  - name: hello-ctr
    image: ni
    ports:
    - containerPort: 8080
  
```

## 7. Kubernetes Services
### 3 Creating a Service the Iterative
```
kubectl expose rc hello-rc --name=hello-svc -- target-port=8080 --type=NodePort
```

```
kubectl describe svc hello-svc
```

### 4 Creating aService the Declarative Way
```
kubectl delete svc hello-svc
```

#### 01:16
```
spec:
  type: NodePort
  ports:
  - port: 8080
    protocol: TCP
  selector:
    app: hello-world
```
servicetype
- ClusterIP stable internal cluster IP
- NodePort Exposes the app outside of the cluster by adding a cluster-wide port on top of clusterIP
- LoadBalancer integrates nodeport with cloud-based load balancers


exp
```
apiVersion: v1
kind: Service
metadata:
  name: hello-svc
  labels:
    app: hello-world
spec:
  type: NodePort
  ports:
  - port:8080
    nodePort: 30001
    protocol: TCP
  selector:
    app: hello-world
```

```
kubectl describe pods | grep app
```


```
kubectl create -f svc.yml
kubectl get svc
```

## 8.Kubernetes Deployments
### 2 Deployment Theory
```
kubectl colling-update -f updated-rc.yml
```
```
kubectl delete rc hello-rc
```
### 3 Creating Your First Kubernetes Deployment
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: hello-deploy
spec:
  replicas: 10
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-pod
      image: nigelpoulton/pluralsight-docker-ci:latest
      ports:
      - containerPort: 8080
```
```
kubectl create -f deploy.yml
kubectl get rs
```


### 4 Updating a Deployment
```
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: hello-deploy
spec:
  replicas: 10
  minReadySeconds: 10
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-pod
      image: nigelpoulton/pluralsight-docker-ci:latest
      ports:
      - containerPort: 8080
```
```
kubectl apply -f deploy.yml --record
kubectl rollout status deployment hello-deploy
kubectl get deploy hello-deploy
```
```
kubectl rollout history deployment hello-deploy
```

```
kubectl describe deploy hello-deploy
```

```
kubectl rollout undo deployment hello-deploy --to-revision=1
```
