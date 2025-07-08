# 🚀 React App Deployment on Kubernetes

This repository contains Kubernetes configuration files to deploy a **React application** in a Kubernetes cluster using a dedicated namespace, deployment, and service.

## 📁 Files Included

- `namespace.yml`: Creates a separate namespace called `react-site` for isolation.
- `deployment.yml`: Deploys the React application from a Docker image hosted on GitLab Container Registry.
- `service.yml`: Exposes the deployment as a ClusterIP service within the Kubernetes cluster.

---

## 📦 Docker Image Used

Image:  
`registry.gitlab.com/hilal.ahmad.developer-group/react-simple-site:latest`

Make sure the image is public or create a Kubernetes secret if it's private.

---

## 🧰 Prerequisites

- A running Kubernetes cluster (local or cloud-based)
- `kubectl` installed and configured
- Docker image available in a container registry (e.g., GitLab, Docker Hub)

---

## 📌 Deployment Steps

### 1. Clone the Repository

```bash
git clone https://github.com/hilalahmad0101/k8s-react-site.git
cd k8s-react-site
```

### 2. Apply Namespace

```bash
kubectl apply -f namespace.yml
```

### 3. Apply Deployment

```bash
kubectl apply -f deployment.yml
```

### 4. Apply Service

```bash
kubectl apply -f service.yml
```

---

## 🌐 Accessing the App

The `service.yml` exposes the app using a `ClusterIP`. To access it:

### Option 1: Port-forward the service

```bash
kubectl port-forward svc/react-service 8080:80 -n react-site
```

Then open:

```
http://localhost:8080
```

### Option 2: Expose externally

Change the `type` in `service.yml` to `NodePort`, or configure an Ingress Controller (like NGINX) for production-grade routing.

---

## 🔐 Private Image Access (Optional)

If the Docker image is private, create a Docker registry secret:

```bash
kubectl create secret docker-registry gitlab-registry-secret \
  --docker-server=registry.gitlab.com \
  --docker-username=YOUR_GITLAB_USERNAME \
  --docker-password=YOUR_GITLAB_PAT \
  --docker-email=you@example.com \
  --namespace=react-site
```

Then, in your `deployment.yml`, add:

```yaml
spec:
  template:
    spec:
      imagePullSecrets:
        - name: gitlab-registry-secret
```

---

## 🤝 Contributing

Feel free to fork this repo and contribute via Pull Requests.

---

## 🧑‍💻 Author

**Hilal Ahmad**  
GitHub: [@hilalahmad0101](https://github.com/hilalahmad0101)  
GitLab: [hilal.ahmad.developer-group](https://gitlab.com/hilal.ahmad.developer-group)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
