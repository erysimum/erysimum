# Hi, I'm Amit 👋

I'm a DevOps and Cloud Engineer in Melbourne. Most of my work is on AWS and Kubernetes. I like taking the kind of deployment that's held together by manual steps and tribal knowledge and making it boring and repeatable instead.

I've been in software for about 4 years. Lately I'm spending most of my time on infrastructure as code, GitOps, and getting observability to actually tell you something useful.

- 🔭 Right now I'm building out a full EKS platform: GitOps, SLO-based alerting, some chaos engineering, and an AI agent that helps with on-call. More on that below.
- 🌱 Day to day I'm in Terraform, Argo CD, Istio, Prometheus and Pyrra
- 🛠️ RHCSA certified (RHEL 9)
- 📫 Say hi on [LinkedIn](https://www.linkedin.com/in/amit10shahi)

---

## 🚀 AI SRE Agent (`retail-store-ai`)

This is the one I'm most into right now. It's an AI agent that helps with on-call for the EKS platform further down. When an alert fires, it goes and looks at the live cluster, figures out what's probably going on, and writes it up in Slack. It never changes anything itself. It just tells you what it found and what it would run, and you make the call.

A few parts I'm happy with:

- When an alert comes in, a small FastAPI service kicks off two investigators at the same time. Each one is its own `claude -p` process that's only allowed to touch one thing: one talks to Prometheus, one talks to Kubernetes, and there's a quick git-log check alongside them. They're genuinely separate processes running in parallel, not async pretending to be parallel.
- After they finish, a final step with no tools pulls everything together into clean JSON (I validate it with Pydantic) and turns it into a Slack card: what broke, who's affected, the evidence, and commands you can copy and paste.
- It's deliberately locked down. Every investigator only gets the single tool it needs, there are timeouts on each one, repeat alerts get filtered out, and the Slack post is guarded so it can't spam.

I also tried to be honest about where it's weak. On EKS it correctly said "I don't have data on that" instead of inventing numbers, and it caught a stale alert on a system that had already recovered. But it also once pinned the blame on a random pod restart instead of the fault I'd actually injected, because it has no way of knowing a human caused it. That's the whole reason it stays advisory and keeps a person in the loop.

If you'd rather see it than read about it, chapter 5 of the [platform walkthrough](https://github.com/erysimum/retail-store-gitops/tree/main/docs/walkthrough/05-ai-agent) has screenshots of a real run: the subagents firing off in parallel, then the Slack card with the root cause, the evidence, and the commands to fix it.

🔗 [github.com/erysimum/retail-store-ai](https://github.com/erysimum/retail-store-ai)

---

## 🏗️ The platform it runs on — EKS

A full Kubernetes platform on AWS EKS that I built and run on my own. I split it across five repos on purpose, roughly the way separate teams would own separate pieces at an actual company. A 5-service retail app runs on top, wired up so I can follow a request the whole way through.

What it does:

- One `terraform apply` brings up around 100 AWS resources in about 15 minutes. No clicking around in the console.
- Argo CD keeps the cluster matching Git, so whatever's running is whatever's committed.
- SLOs are done the proper way with Pyrra (multi-window burn rate, the Google SRE approach), and alerts go to Slack or PagerDuty depending on how bad it is.
- I can break things on purpose with Istio fault injection, no code changes and no restarts.
- I checked it actually works by pushing a real order through all 5 services and watching it land in Postgres.

📸 If you'd rather see it than read about it, the [platform walkthrough](https://github.com/erysimum/retail-store-gitops/tree/main/docs/walkthrough) goes through the whole thing with screenshots: first traffic and SLOs, a Locust load test, tracing a failure to one broken request, Istio fault injection, and the AI agent's diagnosis at the end.

The five repos:

| Repo | What it owns |
|------|-------------|
| 🏗️ [retail-store-infra](https://github.com/erysimum/retail-store-infra) | Terraform: VPC, EKS, RDS, ECR, IAM, observability stack. Start here. |
| 🔐 [retail-store-platform](https://github.com/erysimum/retail-store-platform) | Cluster policies: namespaces, RBAC, NetworkPolicy, quotas (Kustomize) |
| 🔄 [retail-store-gitops](https://github.com/erysimum/retail-store-gitops) | Helm charts, Argo CD config, SLOs, dashboards, fault injection |
| 🛍️ [retail-store-app](https://github.com/erysimum/retail-store-app) | The polyglot microservices app |
| 🤖 [retail-store-ai](https://github.com/erysimum/retail-store-ai) | The AI SRE agent from above |

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
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)
![Pydantic](https://img.shields.io/badge/Pydantic-E92063?style=flat&logo=pydantic&logoColor=white)
![Claude Code](https://img.shields.io/badge/Claude%20Code-D97757?style=flat&logo=anthropic&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat&logo=gnubash&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)

**Cloud (AWS):** EKS · VPC · IAM · RDS · Lambda · API Gateway · SQS · CloudWatch
**Platform:** Kubernetes · Docker · Helm · Istio · NGINX
**GitOps & CI/CD:** Argo CD · GitHub Actions (OIDC) · Jenkins · GitLab CI · SonarQube · Trivy
**IaC:** Terraform · CloudFormation
**Observability:** Prometheus · Grafana · Pyrra · Alertmanager · PagerDuty
**AI / Agents:** Claude Code (MCP) · FastAPI · Pydantic · asyncio

---

## 📊 Other projects

**Soccerize** is a real-time soccer app on AWS EKS, built around Lambda, DynamoDB Streams and API Gateway WebSockets. The fun part was the pipeline: with Jenkins, Trivy and SonarQube I got deploys down from about an hour to roughly 8 minutes, with Argo CD handling promotion.

---

<sub>📍 Melbourne, VIC · 🎓 Master of Applied IT, Victoria University · 🏅 RHCSA (RHEL 9)</sub>
