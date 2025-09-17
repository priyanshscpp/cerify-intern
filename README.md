# Cerify Systems — Software Engineer Intern (Jan 2025 – Jun 2025)

![Profile Views](https://komarev.com/ghpvc/?username=priyanshscpp&color=blue) ![Status](https://img.shields.io/badge/status-active-success?style=for-the-badge&logo=verizon)

> **Priyanshu Yadav — Software Engineer Intern**  
> Cerify Systems • Jan 2025 – Jun 2025 • New Delhi, India (Hybrid)

---

This README is a compact, interviewer-friendly summary of my internship contributions, architecture decisions, and measured impact. It is suitable for attaching to a resume, sharing as a portfolio link, or presenting during interviews.

---

## Table of Contents
1. [Overview](#overview)
2. [Internship at Cerify Systems](#internship-at-cerify-systems)
   - [Scalable Cloud Backend Platform](#scalable-cloud-backend-platform)
   - [Automated LLM Retraining CI/CD Pipeline](#automated-llm-retraining-cicd-pipeline)
3. [Technical Architecture (high-level)](#technical-architecture-high-level)
4. [Performance & Impact](#performance--impact)
5. [Tools & Technologies](#tools--technologies)
6. [Representative Code Snippets](#representative-code-snippets)
7. [Learnings & Skills](#learnings--skills)
8. [Future Roadmap](#future-roadmap)
9. [Contact](#contact)

---

## Overview
During my internship at **Cerify Systems** I focused on production-grade backend engineering and MLOps automation. My primary deliverables were:

- A highly available, low-latency cloud backend serving 1K+ daily active users.
- A CI/CD pipeline for automating LLM retraining, validation, and deployment—optimizing developer velocity and GPU spend.

**Key outcomes:**

- Achieved **99.95% uptime** for critical backend services.
- Sustained **< 200 ms** p95 API latency under typical load (1K+ DAU).
- Built end-to-end CI/CD and monitoring for automated model retraining and safe rollout, materially improving iteration speed and operational cost-efficiency.

---

## Internship at Cerify Systems

### Scalable Cloud Backend Platform  
**Role:** Backend / Systems Engineer  
**Goal:** Deliver production-ready backend services that are resilient, observable, and low-latency for customer-facing product flows.

**STAR**
- **Situation:** The product needed reliable, low-latency backend infrastructure to support real-time user workflows and integrations with external partners.
- **Task:** Design and deploy cloud-native services with automated observability and failover so SLAs could be met for users across regions.
- **Action:**
  - Containerized services with Docker and deployed on Kubernetes (EKS/GKE) with Horizontal Pod Autoscaling.
  - Implemented API gateway + gRPC for internal services and HTTP REST for external integrations.
  - Introduced Redis caching and optimized DB access patterns (connection pooling, prepared statements).
  - Built Prometheus + Grafana observability stack and SLO-based alerting.
  - Hardened services with circuit breakers, rate-limiting, and graceful shutdowns.
- **Result:**
  - **99.95% uptime** for production services.
  - **<200 ms** p95 API latency across 1k+ daily active users.
  - Improved reliability and reduced incident MTTR with actionable dashboards & runbooks.

---

### Automated LLM Retraining CI/CD Pipeline  
**Role:** MLOps / Platform Engineer  
**Goal:** Automate the model retraining lifecycle to enable frequent, safe updates with minimal manual intervention and controlled GPU spend.

**STAR**
- **Situation:** Model updates were manual, slow, and costly; retrain jobs required significant human coordination and GPU provisioning.
- **Task:** Create an automated CI/CD flow for retraining, validating, and deploying models (with rollback safety).
- **Action:**
  - Designed a GitOps-triggered workflow (GitHub Actions / GitLab CI) to: run pre-checks → launch retraining on spot GPU instances → run validation suites → stage model to canary and monitor metrics.
  - Integrated experiment tracking (MLflow / W&B) and automated metric gating (accuracy/regression thresholds) before promotion.
  - Implemented automated cost controls: spot instance use, smart batching of jobs, and pruning of stale artifacts to reduce GPU spend.
  - Built retrain orchestration with Kubernetes Jobs and a lightweight scheduler to consolidate runs and reduce overhead.
- **Result:**
  - Reliable, repeatable retraining lifecycle with automated gating and safe rollout.
  - Measurable reductions in model update cycle time and GPU costs through automation and smarter scheduling.

---

## Technical Architecture (high-level)
- **Platform:** AWS / GCP (hybrid); Kubernetes (EKS/GKE) for orchestration  
- **Compute:** Docker containers, Kubernetes Jobs for ML tasks, spot GPU instances for cost efficiency  
- **API / Services:** FastAPI / Node.js microservices, gRPC internal calls, REST endpoints for external integrations  
- **Data & Storage:** PostgreSQL (primary), Redis (cache), S3 (artifact storage), MongoDB for event logs  
- **MLOps:** MLflow / W&B for experiments, model registry, GitOps triggers for retrains  
- **CI/CD & Infra as Code:** GitHub Actions + Terraform for infra provisioning  
- **Observability:** Prometheus (metrics), Grafana (dashboards), ELK / Fluentd (logs)  
- **Security / Ops:** JWT/OAuth for auth, RBAC in Kubernetes, secrets in Vault/KMS, SLO-based alerts & PagerDuty integration

---

## Performance & Impact

| KPI                          | Value / Result |
|-----------------------------:|:---------------|
| Production uptime            | **99.95%** |
| p95 API latency (typical)    | **< 200 ms** |
| Daily active users served    | **1,000+** |
| Model retrain automation     | Automated GitOps-triggered pipeline with validation gates |
| Cost optimizations (GPU)     | Reduced via spot instances, job consolidation, artifact pruning |

> These metrics reflect system-level guarantees and operational outcomes achieved during the internship.

---

## Tools & Technologies
**Languages:** Python, Node.js, Bash

**Frameworks / Libraries:** FastAPI, Express, TensorFlow / PyTorch (for experimentation)

**Infrastructure:** Kubernetes, Docker, Terraform, AWS / GCP

**Storage / DB:** PostgreSQL, Redis, S3, MongoDB

**MLOps & CI/CD:** GitHub Actions, MLflow / W&B, Kubernetes Jobs

**Monitoring:** Prometheus, Grafana, ELK

**Integrations:** OAuth/JWT, SSO, Webhooks, Slack/PagerDuty alerts

---

## Representative Code Snippets

**Simple health-check endpoint (FastAPI)**

```python
from fastapi import FastAPI
import time
app = FastAPI()

@app.get("/health")
def health():
    return {"status": "ok", "timestamp": time.time()}
```

**Minimal GitHub Actions snippet (trigger retrain on merge to `main`)**

```yaml
name: model-retrain
on:
  push:
    branches: [ main ]
jobs:
  retrain:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Setup Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      - name: Start retrain (dispatch to cluster / scheduler)
        run: |
          python scripts/trigger_retrain.py --config configs/retrain.yaml
```

---

## Learnings & Skills
**Technical**
- Production-grade backend patterns: autoscaling, caching, connection pooling.
- Observability & SLOs to reduce incident MTTR.
- Practical MLOps: experiment tracking, automated validation, canary rollouts.
- Cost-conscious ML engineering (spot instances, job batching).

**Soft / Operational**
- Cross-functional collaboration with product, QA, and data-science teams.
- Writing runbooks, defining SLAs, and documenting safe rollback procedures.
- Prioritizing reliability and developer velocity in platform work.

---

## Future Roadmap
1. **Feature store & unified data contracts** — reduce labeling / feature drift by centralizing features.
2. **Adaptive retrain scheduling** — retrain cadence driven by data drift detection.
3. **Fine-grained canary & automatic rollback** — more automated safety checks for model deployments.
4. **Cost-aware scheduler** — dynamic job placement to maximize use of spot capacity while meeting deadlines.

---

## Contact
**Priyanshu Yadav**  
Email: priyanshs.ece@gmail.com  
LinkedIn: https://linkedin.com/in/priyanshuhbti  
GitHub: https://github.com/priyanshscpp

Cerify Systems — [Company Link] ← *(replace with official URL)*

---

## Notes for Interviewers
- Happy to walk through architecture diagrams, code, and incident reports from the production deployments.
- Can present a short demo (local or recorded) of the retraining pipeline, canary promotion, and a live metrics dashboard.

---

*Special thanks to the Cerify engineering team for mentorship and code reviews during the internship.*
