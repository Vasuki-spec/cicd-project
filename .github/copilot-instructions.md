# Copilot Instructions for cicd-project

- This is a minimal Flask web application in `app.py`. The app exposes two routes:
  - `/` returns a simple HTML success message.
  - `/health` returns a plain health status string.
- `app.py` creates the Flask app at import time and runs it directly when `__main__`.
- Tests use Flask's built-in test client in `test_app.py`; they assert only HTTP status codes.
- Dependency management is explicit in `requirements.txt` (`Flask==3.1.1`).
- Containerization is defined in `Dockerfile`; the image is built from `python:3.11-slim`, installs requirements, copies the repo, exposes port `5000`, and runs `python app.py`.

## What to keep in mind

- Do not introduce a package layout unless a feature clearly requires it. This repo is intentionally flat and small.
- Keep changes aligned with a simple CI/CD demo app: Flask app, Docker container, and tests.
- There is currently no populated `README.md` or `Jenkinsfile`; avoid assuming hidden build logic.

## Recommended commands

- Install dependencies: `pip install -r requirements.txt`
- Run tests: `pytest` or `python -m pytest`
- Run app locally: `python app.py`
- Build Docker image: `docker build -t cicd-project .`
- Run container: `docker run -p 5000:5000 cicd-project`

## When modifying code

- Keep `app.py` simple: route handlers return strings or HTML fragments directly.
- `test_app.py` should continue to use `app.test_client()` and verify response status codes.
- If adding routes or features, keep the Flask app entrypoint in `app.py` and ensure Docker still starts with `python app.py` unless Dockerfile is updated explicitly.

## Notes for AI agents

- There are no existing `.github` agent instruction files in this repo, so this file is the source of truth.
- Prefer small, discoverable changes over broad refactors.
- If you need to add CI logic, target the existing `Jenkinsfile` and preserve the current app/test/docker workflow.
