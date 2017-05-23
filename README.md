# psgsk8s
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
  - port: 8989
    protocol: TCP
  selector:
    app: hello-world
```
