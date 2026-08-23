# GCP Python FastAPI

Dockerized FastAPI sample app for the Cloud Native DevSecOps Pipeline on GCP project.

## Run Locally

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
pytest
uvicorn main:app --host 0.0.0.0 --port 8080
```

Open `http://localhost:8080`.

## Run With Docker

```bash
docker build -t gcp-fastapi .
docker run --rm -p 8080:8080 gcp-fastapi
```

## Pipeline

`cloudbuild.yaml` builds and pushes the image, runs tests, scans with Trivy and Snyk, deploys to Cloud Run, and grants public invoker access.

Before using it in your GCP project, confirm:

- Secret Manager contains `cloudbuild-snyk-token`.
- The Cloud Build service account can read the secret.
- The artifact bucket `${PROJECT_ID}-cb-builds` exists, or update the artifact location.
- The Cloud Run region is correct for your project.
