**English** | [Português (Brasil)](pt-BR/ROADMAP.md)

[Home](README.md) · [Profile](PROFILE.md) · [Projects](TECHNICAL-PROJECTS.md) · [Review](ROADMAP.md) · [Pending items](IDEAS-AND-PENDING.md) · [History](HISTORY.md)

---

<sub>03 / REVIEW · GUILHERME MARTINS</sub>

# What is consolidated. What comes next.

**6 of 10 topics completed · 60%**

The review already covers AWS, Kubernetes, delivery, observability, security and databases. The next topic is **Networking / Multi-account**, building on existing answers.

Completion means the reported experience has been explored sufficiently. New information can enrich a topic without restarting the interview. No topic is formally in progress following the completion of Databases on October 15, 2026.

## Review map

| Topic | Status | Coverage |
| :--- | :--- | :--- |
| [01 · AWS / Cloud Architecture / IaC](#1-aws--cloud-architecture--iac) | Completed | Services, architecture and IaC |
| [02 · Kubernetes / Containers](#2-kubernetes--containers) | Completed | Planning, operations and upgrades |
| [03 · CI/CD / Developer Experience](#3-cicd--developer-experience) | Completed | Pipelines, standards and adoption |
| [04 · Observability / SRE / Incidents](#4-observabilidade--sre--incidentes) | Completed | Telemetry, troubleshooting and incidents |
| [05 · Security / IAM / Governance](#5-seguranca--iam--governanca) | Completed | Permissions, credentials and controls |
| [06 · Networking / Multi-account](#6-networking--multi-account) | **Next** | Connectivity, isolation and personal responsibilities |
| [07 · Databases / Backup / DR](#7-bancos--backup--dr) | Completed | Capacity, recovery and migration |
| [08 · Technical leadership / Architecture / Documentation](#8-lideranca-tecnica--arquitetura--documentacao) | Pending | Influence, mentoring and decisions |
| [09 · Internal tools / AI / Automation](#9-ferramentas-internas--ia--automacao) | Pending | Architecture, technology, adoption and results |
| [10 · Earlier experience / Impact / Positioning](#10-experiencias-anteriores--impacto--posicionamento) | Pending | Earlier cases and professional positioning |

<a id="6-networking--multi-account"></a>

## 6. Networking / Multi-account

**Pending — next topic.**

Existing material covers Organizations/cross-account roles, accounts per environment, Route 53, ACM, ALB/NLB, Kubernetes ingress and resource promotion between AWS accounts. Reuse these answers instead of asking everything again.

Gaps to explore without assuming experience:

- Concrete VPC, subnet, CIDR and routing cases; personal contribution to design and operations.
- Connectivity between environments/accounts and practical experience with peering or other solutions, if any.
- Security groups and traffic isolation; relevant decisions and troubleshooting.
- Scope of the accounts administered and responsibility boundaries in Organizations/governance.

These are open review questions, not confirmed use of these technologies. Sources: F1 §§6, 17, 29–31 and 36.

## Topic records

Expand completed topics to see what has already been answered. Pending topics show the material available and the remaining areas to explore.

<a id="1-aws--cloud-architecture--iac"></a>

<details>
<summary><strong>1. AWS / Cloud Architecture / IaC · completed</strong></summary>

**Completed.**

Already recorded:

- Service selection with development teams, considering complexity, cost and actual needs.
- EC2, EKS/Kubernetes, Lambda, RDS, S3, API Gateway and related services; do not infer an environment inventory without confirmation.
- SQS Standard/FIFO, DLQs, retries, visibility timeout, retention, consumers, batching and deduplication; SNS and EventBridge. Does not currently use Step Functions.
- Route 53: hosted zones, records and routing needs; ACM and TLS certificates.
- ALB/NLB: listeners, targets, health checks, rules and certificates; some provisioning automated through EKS/kOps.
- S3/CloudFront: frontend delivery, distributions/behaviors and pipeline invalidation.
- Secrets Manager and RDS credential rotation; configuration through Parameter Store.
- Previous experience with Terraform, Terragrunt and CloudFormation, including environments built from scratch; current daily use limited by the company context.
- Contributes to cost decisions; the Head has primary responsibility for FinOps.

Details in the [Profile](PROFILE.md); cases P03, P05 and P07. Source: F1 §§6–7 and 31.

</details>

<a id="2-kubernetes--containers"></a>

<details>
<summary><strong>2. Kubernetes / Containers · completed</strong></summary>

**Completed on October 5, 2026.**

Already recorded:

- Docker, Kubernetes, EKS/kOps, Docker Swarm, Dockerfiles, Deployments, Services, ConfigMaps, Ingress and HPA.
- Product-specific planning: pods, services, persistence, ingress, cloud, environments, namespaces/clusters and IaC.
- Reusable standards reduced infrastructure preparation from ~4–5 to ~1–2 days, sometimes reaching 1 day.
- Operations, node capacity, replicas, CrashLoopBackOff, current/previous logs and investigation of external factors.
- Requests/limits informed by APM, load, startup, normal consumption and peaks.
- Upgrades involving research, documentation, prior validation and cluster replacement; training junior engineers.
- Uses existing Operators, including Prometheus Operator; has not developed custom Operators/CRDs.
- HPA/Cluster Autoscaler tuned per workload; reduced overnight capacity where applicable. No reported use of VPA.

Details in the Profile and cases P02/P12. Sources: F1 §34; F2 §§34–35. Do not reopen answered questions.

</details>

<a id="3-cicd--developer-experience"></a>

<details>
<summary><strong>3. CI/CD / Developer Experience · completed</strong></summary>

**Completed on October 5, 2026.**

Already recorded:

- Bitbucket Pipelines as the primary tool; GitHub Actions, Jenkins and Bitrise in other work.
- Initial implementation of automated build/deploy, documentation and developer training.
- Customized Git Flow, PRs and code review, environment promotion and Jira traceability.
- External configuration, variable conventions and removal of hard-coded settings.
- Script reuse, followed by shared pipelines/templates.
- Incremental quality/security controls, multi-stage Docker builds, ECR and OIDC.
- Joint diagnosis of code failures, missing variables and outdated pipelines.
- Quarterly deployments became weekly or every two weeks; no complete DORA metrics series.

Details in the Profile and P01/P03. Sources: F1 §§9–10, 31 and 35; F2 §36.

</details>

<a id="4-observabilidade--sre--incidentes"></a>

<details>
<summary><strong>4. Observability / SRE / Incidents · completed</strong></summary>

**Completed.**

Already recorded:

- Datadog + OpenTelemetry as the primary foundation; also experience with Grafana, Graylog, Zabbix, Loki, ELK/EFK and New Relic.
- OpenTelemetry platform built from scratch, documentation and examples for Node.js, C#/.NET, Python, React Native and Angular.
- Correlation ID, logs, metrics, APM, traces, alerts and instrumentation with teams.
- CloudWatch mainly used for logs and selected alarms.
- End-to-end investigation, P0 response, recovery, technical communication with managers and postmortem/RCA.
- Login/SSO affected by locks: application, database and Kubernetes context; avoid double-counting related accounts.

Details in the Profile and P04/P08. Sources: F1 §§13–16, 31–32 and 38.

</details>

<a id="5-seguranca--iam--governanca"></a>

<details>
<summary><strong>5. Security / IAM / Governance · completed</strong></summary>

**Completed on October 5, 2026.**

Already recorded:

- Users, groups, roles, policies, MFA and least privilege.
- Permission design based on who needs access and which resource/action they need; managed or custom policies depending on context.
- Reusable policies and grouped permissions; removal with a checklist and contextual validation.
- OIDC in pipelines, Secrets Manager and RDS credential rotation.
- Environment/prefix isolation in Parameter Store; cross-account access through roles.
- Security requirements in architecture review, without attributing formal legal responsibility.

Details in the Profile and P03. Sources: F2 §37; F1 §§31 and 36.

</details>

<a id="7-bancos--backup--dr"></a>

<details>
<summary><strong>7. Databases / Backup / DR · completed</strong></summary>

**Completed on October 15, 2026.** This was the sixth topic completed; its number remains 7.

Already recorded:

- Platform/cloud work rather than a dedicated DBA role; database/user creation, diagnosis, capacity, recovery and upgrades.
- CPU, memory, connections, waits, locks, slow queries and correlation with services/jobs; comparison of connections against the previous ~12 hours.
- Occasional execution plan analysis and query/index suggestions, validated and implemented by the responsible team.
- Mitigation of locks affecting login, with impact assessment before terminating a transaction/connection.
- Resizing and a read replica with separated access: >50% less load on the primary and almost 50% less response time, as a combined result.
- Snapshot restore to a separate instance and selective correction after an incorrect UPDATE, with limitations on preserving later changes.
- Upgrade of a database >100 GB, POC/Dev 2, dependencies, new instance, DNS cutover, backup and documented rollback; ~2 hours of downtime and completion without reported issues.
- Backup policy primarily owned by the Head. No reported creation of Multi-AZ, confirmed failover execution, demonstrated PITR or formal schedule of periodic DR tests.

Details in the Profile and P08–P11. Main source: F1 §38, which updates the earlier status in F2 §38.

</details>

<a id="8-lideranca-tecnica--arquitetura--documentacao"></a>

## 8. Technical leadership / Architecture / Documentation

**Dedicated review pending; material already collected.**

- Technical guidance across teams, without formal people management; standards reached ~4 teams/~30 developers in the period described.
- Kickoffs, architecture, POCs/reference implementations, documentation, guidance and adoption follow-up.
- Previously defined architectures directly; now reviews developers' proposals, requests changes and can withhold immediate approval.
- Priorities: cost/ROI, security, performance and observability; documented risks and trade-offs.
- Management has final hierarchical authority in disagreements; do not attribute unilateral executive authority.
- Guides junior engineers and documents procedures, including upgrades.

Still to explore: further examples of influence/mentoring, documentation/decision processes and reach, and adoption outcomes. Do not assume formal RFC/ADR use just because it appeared in the original scope.

Sources: F1 §§2–4, 21 and 37; F2 §§35–36 and 39. See the Profile and the example in Ideas/Pending Items.

<a id="9-ferramentas-internas--ia--automacao"></a>

## 9. Internal tools / AI / Automation

**Further review pending.**

- ARO, User Permissions and the Parameter Store Comparator are already described in cases P05–P07.
- Assigned responsibility for corporate AI standards: harness, tools, skills, repositories, documentation, examples and adoption.
- Preference for automation and preventing problems already recorded.

Still to explore: tool architecture/stack, users and adoption, metrics, maintenance and limitations; actual implementation status of the AI initiative and observable results. Assigned responsibility must not be presented as a completed delivery.

Sources: F1 §§17–20; F5 §§8 and 10. See [Ideas and pending items](IDEAS-AND-PENDING.md).

<a id="10-experiencias-anteriores--impacto--posicionamento"></a>

## 10. Earlier experience / Impact / Positioning

**Dedicated review pending.**

- Career history at Conexia, FH_, Beblue, JET, SiplanControl-M, LMS and Artoni preserved in the Profile.
- Strong foundation in C#/.NET and Node.js; experience with Go, Python, Shell and Azure/Windows Azure.
- **Senior Cloud Platform Engineer** positioning chosen on October 13; historical job title preserved.
- Preference for a technical IC role across teams, architecture, platform, tools and prevention; no current interest in formal management.
- English: good reading comprehension, limited speaking and discomfort with interviews; no CEFR level assigned.

Still to explore: earlier projects and impact, scale and available metrics, Azure experience and an evidence-based Senior/Staff/Principal assessment. Overlapping CV dates and approximate durations remain as recorded until confirmed.

Sources: F1 §§1, 5–7 and 23–28; F2 §§1 and 27; F5 §§12–16.

<a id="criterios-de-conclusao-e-regras-de-continuidade"></a>

<details>
<summary><strong>Completion criteria and continuity rules</strong></summary>

1. Consult the six documents before asking again.
2. Review only gaps in the chosen topic; do not repeat already answered experience questions.
3. Separate personal execution, proposals, team responsibility and hypothetical examples.
4. Preserve approximate metrics and limitations; lack of experience is also a valid answer.
5. Update the Profile/Projects, record decisions in History and save before moving on, keeping both languages aligned.
6. Mark a topic complete only when closure is recorded; document reorganization alone does not change progress.

</details>

<a id="proximo-passo"></a>

## Next step

Resume **Networking / Multi-account**, building on existing information about accounts, IAM, DNS, load balancers and Kubernetes. Completed topics remain closed; new accounts can supplement them without restarting the interview.

The 10-topic roadmap replaces the old 36-point list. Status was reconciled from F1 §§29, 30, 33 and 38 and the detailed F2 reviews, as described in [History](HISTORY.md#reconciliacao-entre-versoes). Editorial reorganization and translation do not change progress.

---

[← Projects](TECHNICAL-PROJECTS.md) · [Home](README.md) · [Ideas and pending items →](IDEAS-AND-PENDING.md)

<sub>Professional knowledge base · Updated October 15, 2026 · Branch develop</sub>
