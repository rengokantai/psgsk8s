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

