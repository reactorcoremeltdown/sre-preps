### **30 Common Kubernetes Interview Questions for SRE/DevOps (with Answers)**  

Kubernetes is a **critical skill** for **SRE/DevOps** professionals, and interviews often test knowledge of **deployment strategies, networking, security, observability, and troubleshooting**. Below are 30 commonly asked Kubernetes interview questions and their answers.

---

## **1. What is Kubernetes, and why is it used?**  
Kubernetes is an **open-source container orchestration system** that automates **deployment, scaling, and management** of containerized applications. It is used for:  
- **Scalability**: Auto-scales applications based on demand.  
- **Self-healing**: Restarts failed containers.  
- **Load balancing**: Distributes traffic across pods.  
- **Declarative management**: Infrastructure as code (IaC).  

---

## **2. What are Pods in Kubernetes?**  
A **Pod** is the smallest deployable unit in Kubernetes. It can contain **one or more containers** that share:  
- **Network namespace** (same IP, ports).  
- **Storage volumes** (shared data).  

---

## **3. How do Deployments work in Kubernetes?**  
A **Deployment** is a higher-level abstraction that:  
- Ensures a specified number of replicas are running.  
- Supports **rolling updates** and **rollbacks**.  
- Uses a **ReplicaSet** under the hood.  

Example:  
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: nginx
```

---

## **4. What is a Service in Kubernetes?**  
A **Service** exposes Pods to the network. Types:  
- **ClusterIP** (default, internal-only).  
- **NodePort** (exposes on a port of each node).  
- **LoadBalancer** (cloud provider integration).  

Example:  
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
  type: ClusterIP
```

---

## **5. What is a Namespace?**  
A **Namespace** is a logical separation of resources inside a Kubernetes cluster. It helps isolate workloads.

Check existing namespaces:  
```sh
kubectl get namespaces
```

Create a namespace:  
```sh
kubectl create namespace my-namespace
```

---

## **6. What is a StatefulSet?**  
A **StatefulSet** is used for **stateful applications** like databases. Differences from Deployments:  
- **Pods have stable network identities**.  
- **Uses Persistent Volumes (PVs)** for storage.  
- **Pods are created in order and are not replaced randomly**.  

---

## **7. What is a DaemonSet?**  
A **DaemonSet** ensures that a copy of a pod runs on every (or some) node in the cluster.  
Example use cases:  
- **Log collectors** (Fluentd, Filebeat).  
- **Monitoring agents** (Prometheus Node Exporter).  

Example:  
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: log-collector
spec:
  selector:
    matchLabels:
      app: log-collector
  template:
    metadata:
      labels:
        app: log-collector
    spec:
      containers:
      - name: log-agent
        image: fluentd
```

---

## **8. What is an Ingress in Kubernetes?**  
An **Ingress** is a **Layer 7 (HTTP/HTTPS) load balancer** that routes traffic to Services.  

Example Ingress rule:  
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```

---

## **9. How does Kubernetes networking work?**  
Kubernetes **assigns each Pod a unique IP** and enables **pod-to-pod communication** without NAT. Components:  
- **CNI (Container Network Interface)**: Calico, Cilium, Flannel.  
- **Kube-proxy**: Handles Service routing.  

---

## **10. How does Kubernetes handle storage?**  
Kubernetes supports **Persistent Volumes (PVs)** and **Persistent Volume Claims (PVCs)** for stateful workloads.  

Example PVC:  
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

## **11. What is a ConfigMap?**  
A **ConfigMap** stores configuration data as key-value pairs.

Example:  
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  app.env: "production"
```

Mounting in a Pod:  
```yaml
envFrom:
- configMapRef:
    name: my-config
```

---

## **12. What is a Secret in Kubernetes?**  
A **Secret** stores sensitive data like passwords and API keys.

Example:  
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  password: c2VjcmV0MTIz  # Base64 encoded "secret123"
```

---

## **13. What are Init Containers?**  
Init containers run **before** the main container starts and perform setup tasks.

---

## **14. What are Liveness, Readiness, and Startup Probes?**  
- **Liveness Probe**: Restarts a stuck container.  
- **Readiness Probe**: Determines if a pod is ready to receive traffic.  
- **Startup Probe**: Ensures a slow-starting app is fully up.  

Example:  
```yaml
livenessProbe:
  httpGet:
    path: /health
    port: 8080
  initialDelaySeconds: 3
  periodSeconds: 10
```

---

## **15. How do you troubleshoot a failing pod?**  
Check logs:  
```sh
kubectl logs pod-name
```
Describe pod:  
```sh
kubectl describe pod pod-name
```

---

## **16. What is Horizontal Pod Autoscaler (HPA)?**  
HPA automatically scales pods based on CPU/memory.

Example:  
```sh
kubectl autoscale deployment my-app --cpu-percent=50 --min=2 --max=10
```

---

## **17. What is Vertical Pod Autoscaler (VPA)?**  
VPA adjusts pod CPU and memory requests automatically.

---

## **18. How do you perform rolling updates?**  
```sh
kubectl set image deployment/my-app my-app=nginx:1.21
```

---

## **19. What is Helm?**  
Helm is a **package manager** for Kubernetes.

---

## **20. What is ArgoCD?**  
ArgoCD is a **GitOps** tool for declarative Kubernetes deployments.

---

## **21. How do you debug a Kubernetes network issue?**  
Use `kubectl exec`, `kubectl logs`, `nslookup`, and `tcpdump`.

---

## **22. What is a Service Mesh?**  
A service mesh like **Istio** or **Linkerd** provides **observability, security, and traffic control** for microservices.

---

## **23. How do you back up and restore Kubernetes clusters?**  
Use **Velero** or cloud provider snapshots.

---

## **24. What is kubelet?**  
The **kubelet** runs on each node and manages pod execution.

---

## **25. What are taints and tolerations?**  
Taints prevent pods from running on certain nodes unless tolerated.

---

## **26. What are affinity and anti-affinity rules?**  
Control pod placement based on labels.

---

## **27. What is a Node in Kubernetes?**  
A Node is a worker machine in the cluster.

---

## **28. How do you expose a Kubernetes application externally?**  
Use **NodePort, LoadBalancer, or Ingress**.

---

## **29. How do you secure a Kubernetes cluster?**  
- RBAC policies.  
- Network Policies.  
- Pod Security Policies.  

---

## **30. What is the difference between StatefulSet and Deployment?**  
StatefulSet maintains **stable identity** and **ordered deployments**, while Deployment does not.

---

### **Final Thoughts**  
Mastering these **30 Kubernetes interview questions** will prepare you for **SRE/DevOps roles**! 🚀