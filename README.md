# 1. Install Argo CD :

### 1.1. Install Argo CD

```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 1.2. Expose the Argo CD API Server

```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

We can use an Ingress or Port Forwarding to access the Argo CD API Server.

### 1.3. Get the Argo CD password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

# 2. Install Argo CD Image Updater

### 2.1. Install Argo CD Image Updater

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj-labs/argocd-image-updater/stable/manifests/install.yaml
```

### 2.2. Create a secret for the Git repository

```bash
kubectl create secret generic git-creds \
    -n argocd \
    --from-literal=username=<GIT_USERNAME> \
    --from-literal=password=<GIT_PASSWORD>
```

# 3. Apply an Application manifest
