# DevOps Capstone Project: Deploying a 3-Tier Application on EKS with CI/CD

## Part 1 (3 hours) – Architecture & environment setup

**Goals:** Design the 3‑tier system and prepare base infra.

- Activities:
    - Whiteboard a 3‑tier architecture:
        - UI (React/simple web) in one container.
        - Backend API (e.g., “account-summary-service”) in another container.
        - Database layer using a managed DB or in‑cluster DB for the lab.
    - Decide basic non‑functional requirements: availability target, simple RPO/RTO, basic security (HTTPS, Secrets), and cost constraints (small instance types, no unused resources).
    - Confirm the EKS cluster and supporting resources are available (namespace for the project, container registry, basic Ingress or LoadBalancer service).

- Deliverables:
    - Architecture diagram (logical + mapping to AWS/EKS).
    - Simple specification for endpoints (e.g., `/accounts`, `/health`) and UI screens.

***

## Part 2 (4 hours) – Containerization & Kubernetes/EKS deployment

**Goals:** Package services into containers and deploy to EKS using manifests, ConfigMaps, and Secrets.

- Activities:
    - Build Dockerfiles for UI and backend services; push images to ECR or another registry.
    - Write Kubernetes manifests:
        - Deployments and Services for UI and backend.
        - ConfigMaps for non‑secret config (API URLs, log levels).
        - Secrets for DB credentials and any API keys.
    - Deploy to a dedicated namespace; verify pod health, service connectivity, and external access (via Ingress/LoadBalancer).

- Deliverables:
    - Working UI + backend running on EKS.
    - YAML manifests checked into Git.

***

## Part 3 (3 hours) – CI/CD pipeline for deployments

**Goals:** Automate build, test, image push, and deploy to EKS.

- Activities:
    - Set up a pipeline in GitHub Actions/GitLab/Jenkins with stages:
        - Code checkout → unit tests → Docker build → image scan (basic) → push to registry.
        - Apply manifests/Helm chart to a “dev” namespace using a service account or GitOps‑style tooling.
    - Add basic quality gates: build fails on tests or scan failure, and protect main branch with PR + approval.
    - Trigger a pipeline via commit, confirm that a new version is deployed, and validate the app through the UI.

- Deliverables:
    - Pipeline definition file (e.g., `github-actions.yml` or `Jenkinsfile`).
    - Screenshots or notes of successful runs and deployed image tags.

***

## Part 4 (3 hours) – Logging, debugging, and small cost & security review

**Goals:** Observe the system, debug issues, and review cost and security basics.

- Activities:
    - Configure logging:
        - Ensure app logs go to stdout/stderr and are collected by CloudWatch or a logging add‑on.
        - Use log queries (e.g., Log Insights) to filter errors/time ranges and trace a sample request path.
    - Inject failures:
        - Break a config (wrong backend URL, wrong DB password) via ConfigMap/Secret change; use logs and pod events to identify the root cause and fix.
    - Cost & security mini‑review:
        - Check node/pod sizes and replica counts, discuss right‑sizing and scaling policy to control costs.
        - Review public endpoints, Secrets usage, and basic IAM roles (for EKS and registry access); identify at least 3 improvement actions (e.g., restrict public access, enable encryption, tighten IAM).

- Deliverables:
    - A short checklist of observed issues and applied fixes.
    - Cost and security improvement recommendations for this environment.

***

## Part 5 (3 hours) – Final hardening & demo presentations

**Goals:** Stabilize app, polish documentation, and present.

- Activities:
    - Implement one or two key improvements identified in Block 4 (e.g., add resource requests/limits, enable HTTPS on Ingress, reduce replica count in non‑peak times, adjust autoscaling thresholds).
    - Prepare a short runbook:
        - How to deploy a new version.
        - How to roll back.
        - How to check health, logs, and metrics.
    - Final demo (per team):
        - Walk through architecture and manifests.
        - Show a pipeline run triggering a new deployment.
        - Demonstrate the app working end‑to‑end from UI to DB, plus a short failure injection and recovery.

- Deliverables:
    - Final working demo with slides/diagram.
    - Runbook and repo (code, Dockerfiles, manifests, pipeline definition) that trainers can reuse for future cohorts.