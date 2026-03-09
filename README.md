## kubernetes-cicd-pipeline

**Short description**: Demo project showing a CI/CD pipeline that builds a containerized Flask app and deploys it to Kubernetes.

### Stack & structure

- **App**: `app/app.py` (Flask, `/` + `/health`)
- **Container**: `docker/Dockerfile` (Python 3.11 slim, `gunicorn`, non-root user)
- **Kubernetes**: `k8s/deployment.yaml` (2 replicas) + `k8s/service.yaml` (NodePort on `30080`)
- **CI/CD**: `.github/workflows/cicd.yaml` (push to `main`, build + test Docker image, push to GHCR, print deploy command)

### Run locally

- **Without Docker**:
  - `cd app`
  - Create venv, `pip install -r requirements.txt`
  - `python app.py`
  - Visit `http://localhost:5000/`

- **With Docker** (from repo root):
  - `docker build -f docker/Dockerfile -t kubernetes-cicd-pipeline:local .`
  - `docker run --rm -p 5000:5000 kubernetes-cicd-pipeline:local`

### Deploy to Kubernetes (basic)

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

Then access: `http://<node-ip>:30080/`

