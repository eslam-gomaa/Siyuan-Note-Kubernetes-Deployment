# Siyuan-Note-Kubernetes-Deployment
Deploy Siyuan Note on your Kubernetes cluster.

<br>

## Usage

Things to change
* [Storage Class](https://github.com/eslam-gomaa/Siyuan-Note-Kubernetes-Deployment/blob/main/siyuan.yaml#L50)

<br>

---

<br>

```bash
git clone https://github.com/eslam-gomaa/Siyuan-Note-Kubernetes-Deployment.git
cd Siyuan-Note-Kubernetes-Deployment
kubectl apply -f siyuan.yaml
```

```bash
kubectl get pods -l app=siyuan-note
```

Troubleshooting
```bash
kubectl describe pods -l app=siyuan-note
kubectl logs -l app=siyuan-note

# If needed.
kubectl exec -it $(kubectl get pods -l app=siyuan-note -o=name) -- sh
```



---

##  Ingress

This is a sample Ingress resource to access `siyuan` externally, make sure to change **the domain** & **the `ingress.class`** which represents your Ingress controller.

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: siyuan-note
  namespace: default
  annotations:
    kubernetes.io/ingress.class: "haproxy"
spec:
  rules:
  - host: your-domain.com
    http:
      paths:
      - path: /
        backend:
          serviceName: siyuan-note
          servicePort: 80
```
