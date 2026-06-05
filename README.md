# Hi, I'm Amit 👋

**DevOps & Cloud Engineer** based in Melbourne, Australia. I build and operate production-grade platforms on **AWS** and **Kubernetes** — turning fragile, manual deployments into reliable, reproducible pipelines.

4+ years in software engineering, now focused on infrastructure as code, GitOps, and SRE-grade observability.

- 🔭 Currently building a full EKS platform with GitOps, SLO observability, and chaos engineering (see below)
- 🌱 Working with Terraform, Argo CD, Istio, Prometheus, and Pyrra
- 🛠️ Red Hat Certified System Administrator (RHCSA, RHEL 9)
- 📫 Reach me on [LinkedIn](https://www.linkedin.com/in/amit10shahi)

---

## 🚀 Featured Project — Production-Grade EKS Platform

A complete, reproducible Kubernetes platform on AWS EKS, built and operated solo across **four repositories** that mirror real-world team boundaries. A 5-service polyglot retail app runs on top of it, instrumented end to end.

**What it does:**
- `terraform apply` brings up ~100 AWS resources in about 15 minutes, zero manual steps
- GitOps via Argo CD ApplicationSet — the cluster always matches Git
- Multi-tier SLOs with Pyrra (Google SRE multi-window burn-rate) and severity-tiered alerting to Slack + PagerDuty
- Chaos engineering via Istio fault injection — no code changes, no restarts
- Validated end to end with a real order traced across 5 services into PostgreSQL

**The four repos:**

| Repo | What it owns |
|------|-------------|
| 🏗️ [retail-store-infra](https://github.com/erysimum/retail-store-infra) | Terraform: VPC, EKS, RDS, ECR, IAM, observability stack — **start here** |
| 🔐 [retail-store-platform](https://github.com/erysimum/retail-store-platform) | Cluster policies: namespaces, RBAC, NetworkPolicy, quotas (Kustomize) |
| 🔄 [retail-store-gitops](https://github.com/erysimum/retail-store-gitops) | Helm charts, Argo CD config, SLOs, dashboards, fault injection |
| 🛍️ [retail-store-app](https://github.com/erysimum/retail-store-app) | The polyglot microservices application |

---

## 🧰 Tech I work with

![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazonwebservices&logoColor=FF9900)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat&logo=terraform&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo%20CD-EF7B4D?style=flat&logo=argo&logoColor=white)
![Istio](https://img.shields.io/badge/Istio-466BB0?style=flat&logo=istio&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=flat&logo=helm&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat&logo=grafana&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat&logo=jenkins&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat&logo=gnubash&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)

**Cloud (AWS):** EKS · VPC · IAM · RDS · Lambda · API Gateway · SQS · CloudWatch
**Platform:** Kubernetes · Docker · Helm · Istio · NGINX
**GitOps & CI/CD:** Argo CD · GitHub Actions (OIDC) · Jenkins · GitLab CI · SonarQube · Trivy
**IaC:** Terraform · CloudFormation
**Observability:** Prometheus · Grafana · Pyrra · Alertmanager · PagerDuty

---

## 📊 Other projects

**Soccerize** — a real-time, event-driven soccer app on AWS EKS with Lambda, DynamoDB Streams, and API Gateway WebSockets. CI/CD with Jenkins, Trivy, and SonarQube cut deploy time from ~1 hour to ~8 minutes, with GitOps promotion via Argo CD.

---

<sub>📍 Melbourne, VIC · 🎓 Master of Applied IT, Victoria University · 🏅 RHCSA (RHEL 9)</sub>
