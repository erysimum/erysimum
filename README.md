# Hi, I'm Amit 👋

I'm a DevOps and Cloud Engineer in Melbourne, mostly working with AWS and Kubernetes. A lot of what I do is taking deployments that only work because someone remembers the right steps, and turning them into something boring and repeatable.

I've been in software about 4 years. These days it's mostly infrastructure as code, GitOps, and trying to make observability actually useful instead of just noisy.

- 🔭 Building a full EKS platform right now: GitOps, SLO alerting, some chaos testing, and an AI agent for on-call. More below.
- 🌱 Day to day: Terraform, Argo CD, Istio, Prometheus, Pyrra
- 🛠️ RHCSA certified (RHEL 9)
- 📫 Say hi on [LinkedIn](https://www.linkedin.com/in/amit10shahi)

---

## 🚀 AI SRE Agent (`retail-store-ai`)

This is my favourite thing I've built lately. It helps with on-call for the EKS platform below. When an alert fires, it goes and looks at the cluster, works out what's probably wrong, and writes it up in Slack. It never changes anything itself. It tells you what it found and what it'd run, and you decide.

A few bits I'm happy with:

- When an alert lands, a small FastAPI service starts two investigators at once. Each one is its own `claude -p` process allowed to touch exactly one thing: one reads Prometheus, one reads Kubernetes, with a quick git-log check on the side. They're real separate processes, not async pretending to be parallel.
- Once they're done, a final step with no tools pulls it all into clean JSON (validated with Pydantic) and posts a Slack card: what broke, who's hit, the evidence, and commands you can paste.
- It's locked down on purpose. Each investigator gets only the one tool it needs, everything has a timeout, repeat alerts get dropped, and the Slack post is guarded.

I tried to be honest about where it slips, too. It correctly says "no data on that" instead of inventing numbers, and it caught a stale alert on a system that had already recovered. But once it blamed a random pod restart instead of the fault I'd actually injected, because it had no way of knowing a human caused it. That's exactly why it only ever advises and keeps a person in the loop.

Want to see it run? Chapter 5 of the [walkthrough](https://github.com/erysimum/retail-store-gitops/tree/main/docs/walkthrough/05-ai-agent) has screenshots of the whole thing: the subagents kicking off, then the Slack card with root cause, evidence, and the fix.

🔗 [github.com/erysimum/retail-store-ai](https://github.com/erysimum/retail-store-ai)

---

## 🏗️ The platform it runs on — EKS

A full Kubernetes platform on AWS EKS that I built and run solo. I split it across five repos on purpose, the way different teams would own different pieces at a real company. A 5-service retail app runs on top, wired up so I can follow a single request all the way through.

What it does:

- One `terraform apply` brings up around 100 AWS resources in about 15 minutes. No clicking around the console.
- Argo CD keeps the cluster in step with Git, so what's running is always what's committed.
- SLOs done properly with Pyrra (multi-window burn rate, the Google SRE way), with alerts to Slack or PagerDuty depending on severity.
- I can break things on purpose with Istio fault injection. No code changes, no restarts.
- I checked it really works by putting a real order through all 5 services and watching it land in Postgres.

Honestly, the first run took me about 4 hours with a pile of manual fixes. I folded every one of those back into Terraform, so now it's one command and ~15 minutes.

📸 Rather see it than read about it? The [walkthrough](https://github.com/erysimum/retail-store-gitops/tree/main/docs/walkthrough) goes through the whole thing in screenshots: first traffic and SLOs, a Locust load test, tracing a failure down to one broken request, fault injection, and the AI agent's diagnosis at the end.

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
