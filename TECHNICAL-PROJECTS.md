**English** | [Português (Brasil)](pt-BR/PROJETOS-TECNICOS.md)

[Home](README.md) · [Profile](PROFILE.md) · [Projects](TECHNICAL-PROJECTS.md) · [Review](ROADMAP.md) · [Pending items](IDEAS-AND-PENDING.md) · [History](HISTORY.md)

---

<sub>02 / PROJECTS · GUILHERME MARTINS</sub>

# Technical decisions in practice

Cases connecting software engineering, platform and operations. Each summary covers the **problem, my contribution and the result**; full details remain available in each record.

<a id="indice-de-projetos"></a>

## Project catalogue

| ID | Case | Main evidence |
|---|---|---|
| P01 | [Transforming the delivery process](#p01--transformacao-do-processo-de-entrega) | Quarterly deployments → weekly or every two weeks |
| P02 | [Kubernetes infrastructure standards](#p02--padroes-de-infraestrutura-kubernetes) | ~4–5 days → ~1–2 days |
| P03 | [Corporate Lambda standard](#p03--padrao-corporativo-lambda) | Standardized configuration, IAM and delivery |
| P04 | [OpenTelemetry and traceability](#p04--opentelemetry-e-rastreabilidade) | Platform, examples and Correlation ID |
| P05 | [ARO](#p05--aro) | AWS resource promotion between accounts/environments |
| P06 | [User Permissions](#p06--user-permissions) | SQL Server permission management through a portal |
| P07 | [Parameter Store Comparator](#p07--comparador-de-parameter-store) | Automated detection of configuration differences |
| P08 | [Authentication incident and database locking](#p08--incidente-de-autenticacao-e-bloqueio-no-banco) | Diagnosis, mitigation and login recovery |
| P09 | [Database scaling and read/write separation](#p09--escala-de-banco-e-separacao-de-leituraescrita) | >50% less load; almost 50% less response time |
| P10 | [Selective recovery after an UPDATE](#p10--recuperacao-seletiva-apos-update) | Isolated snapshot restore and filtered correction |
| P11 | [Database upgrade](#p11--upgrade-de-banco) | >100 GB; ~2 hours of downtime |
| P12 | [Kubernetes/EKS upgrades](#p12--upgrades-de-kuberneteseks) | Playbook, validation and cluster replacement |

Unconfirmed project dates are not inferred from interview dates. Direct upload is an evaluation example preserved in [Ideas and pending items](IDEAS-AND-PENDING.md#exemplo-de-avaliacao-arquitetural-upload-direto), not counted as a delivery.

> **Interpreting the results:** metrics and experience are self-reported. The catalogue includes cases, initiatives and recurring practices; its 12 records do not necessarily represent 12 independent deliveries.

---

<a id="p01--transformacao-do-processo-de-entrega"></a>

<sub>SOFTWARE DELIVERY</sub>

## P01 — Transforming the delivery process

**Problem.** Manual, infrequent releases with a lengthy process to reach production.

**My contribution.** I created pipelines, organized branching and code review, documented standards and trained developers.

**Result.** Deployment frequency increased from approximately quarterly to weekly or every two weeks. The changes also brought traceability and less manual intervention.

<details>
<summary>Read the full account, decisions and sources</summary>

One of the highest-impact projects reported took place when the company did not yet have an established DevOps structure.

<a id="situacao-anterior"></a>

### Previous situation

- Production releases occurred approximately every **3 months**.
- The Head deployed manually.
- Deployment required connecting to environments and running builds manually.
- An approximately **30-page** tutorial described Kubernetes deployment.
- The process depended heavily on human intervention.

<a id="mudancas-implementadas"></a>

### Changes implemented

Guilherme created the first pipelines; defined Git Flow and the branching process; made Pull Requests mandatory; introduced code review; defined the Development → Stage/Staging → Production flow; integrated it with Jira; established environment promotion criteria; and standardized branch names, such as `feature/<task-name>`.

<a id="resultado"></a>

### Result

Release frequency changed from approximately **one deployment every 3 months** to **weekly deployments or deployments every two weeks, usually at the end of the sprint**.

Builds stopped depending on developers' machines; manual intervention decreased; merge-related conflicts and problems decreased significantly; code review became part of the process; and task progress could be tracked through the Jira-integrated workflow.

The standard is still in use in the recorded account. F5 §4 also reports fewer direct changes to the main branch. It dates the organization-wide workflow to approximately six years before the September 23, 2026 record; this is a relative recollection, not a confirmed implementation year.

<a id="papel-e-implementacao-adicional"></a>

### Role and subsequent implementation

Guilherme created pipelines, defined and documented standards, and trained developers. Improvements were incremental, later adding SonarQube, Trivy, Semgrep and GitLeaks. The customized workflow used Jira task identifiers in branches/commits, integration into develop and approved releases to the main branch. Shared pipelines replaced the earlier approach of centralized reusable shell scripts.

<a id="limites-da-evidencia"></a>

### Evidence limitations

There are no measurements of change failure rate, end-to-end lead time, MTTR or rollback tests for this project. Reported frequency must not be converted into an individual productivity metric.

*Sources: F1 §10; F2 §36; F5 §4. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p02--padroes-de-infraestrutura-kubernetes"></a>

<sub>KUBERNETES PLATFORM</sub>

## P02 — Kubernetes infrastructure standards

**Problem.** Preparing infrastructure for new applications required repeating configuration and procedures.

**My contribution.** I created reusable deployment and configuration components, documented them and evolved them through use.

**Result.** Infrastructure preparation fell from approximately 4–5 to 1–2 days, reaching 1 day in some cases. Application development time is not included.

<details>
<summary>Read the full account, decisions and sources</summary>

<a id="contexto-e-implementacao"></a>

### Context and implementation

Created standards and reusable repositories/assets for workload provisioning, including Deployment, Service, ConfigMap and other resources according to the service. Standards were documented, tested and refined over the years.

<a id="resultado-1"></a>

### Result

Preparing infrastructure for a new service fell from **~4–5 days** to **~1–2 days**, sometimes **1 day**. Application development remains the corresponding team's responsibility.

<a id="limites"></a>

### Limitations

The improvement concerns infrastructure preparation/provisioning. The number of services benefiting and total time saved were not reported. No specific rollback case was described.

*Sources: F1 §§11 and 34; F2 §35. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p03--padrao-corporativo-lambda"></a>

<sub>AWS LAMBDA</sub>

## P03 — Corporate Lambda standard

**Problem.** Services needed a common standard for configuration, permissions and delivery between environments.

**My contribution.** I defined a standard using containers, external configuration in Parameter Store, variable conventions and IAM isolation.

**Result.** A corporate reference for building and operating Lambdas. The account includes no measured time or cost reduction.

<details>
<summary>Read the full account, decisions and sources</summary>

Different developers were creating Lambdas in different ways. Guilherme defined a corporate standard to reduce inconsistencies.

<a id="containerizacao"></a>

### Containerization

Lambdas were to use a Dockerfile / Docker image according to the defined standard.

<a id="configuracao"></a>

### Configuration

Previously, some `.env` files were shipped with the code/ZIP. Configuration was to be externalized using **AWS Systems Manager Parameter Store**, following a convention similar to `<environment>/<service>/<variable>`.

Conceptual examples: `dev/service/DB_USER`, `dev/service/DB_NAME` and `prd/service/DB_USER`.

<a id="iam-e-isolamento"></a>

### IAM and isolation

Roles/policies restricted parameter reads by environment: DEV Lambdas could access only DEV parameters, and PROD Lambdas only PROD parameters. Development workloads were therefore not supposed to access production parameters.

<a id="identificacao-do-servico"></a>

### Service identification

A variable/convention allowed a Lambda to identify its service/repository and load the required parameters at startup.

<a id="padronizacao-de-variaveis"></a>

### Variable naming

Variable names were standardized. Earlier variations included `username`, `DB_USERNAME`, `DATABASE_USER` and `DATABASE_USER_NAME`. Consistent conventions such as `DB_USER` and `DB_NAME` were adopted.

<a id="logging"></a>

### Logging

A logging standard was also defined. In some Lambda workloads, Graylog was chosen with consideration for the impact of telemetry solutions on cold starts.

<a id="entrega-e-limites"></a>

### Delivery and limitations

The initial record also includes a build/deploy pipeline in the standard. No reduction in cold start time, incidents, cost or hours spent was measured. Graylog was a contextual choice, not a general rule for every workload.

*Sources: F1 §12; F5 §7. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p04--opentelemetry-e-rastreabilidade"></a>

<sub>OBSERVABILITY</sub>

## P04 — OpenTelemetry and traceability

**Problem.** Troubleshooting required connecting application behavior to platform telemetry.

**My contribution.** I built the OpenTelemetry structure in the cluster, with documentation, examples for different stacks and Correlation ID usage.

**Result.** Cross-service traceability and a qualitative improvement in investigation. No reduction in MTTR was measured.

<details>
<summary>Read the full account, decisions and sources</summary>

The reported project included building an OpenTelemetry structure/cluster from scratch, defining how applications would send telemetry, documenting integration and creating instrumentation examples.

Examples were created for Node.js, C#/.NET, Python, React Native and Angular so that different teams could consistently adopt the observability standard.

<a id="correlation-id"></a>

### Correlation ID

Request traceability through **Correlation ID** was introduced/used, making it possible to follow a request across components/services and find related logs.

Perceived impact included faster problem identification, better end-to-end traceability and more efficient troubleshooting.

<a id="resultado-e-limites"></a>

### Result and limitations

More consistent instrumentation and investigation across teams, with a perceived qualitative benefit. Before/after MTTR, trace volumes, retention and detailed physical architecture were not confirmed.

*Sources: F1 §§14–15; F5 §6. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p05--aro"></a>

<sub>INTERNAL TOOL · AWS</sub>

## P05 — ARO

**Problem.** Promoting resources between environments and accounts required repeating and checking configurations.

**My contribution.** I developed ARO to collect configuration, present a plan for review and recreate/promote resources after approval.

**Result.** A promotion workflow with prior review. Stack, adoption, rollback and metrics still need further detail.

<details>
<summary>Read the full account, decisions and sources</summary>

Has a history of creating internal tools to eliminate repetitive tasks and reduce errors.

<a id="aro--aws-resource-operation"></a>

### ARO — AWS Resource Operation

A tool built to facilitate AWS resource promotion/creation between environments/accounts. An example scenario is promoting several development Lambdas to production.

The tool:

1. Collects resource configuration through AWS.
2. Displays the configuration.
3. Generates a plan-like representation.
4. Allows review/approval.
5. Recreates/promotes resources in the destination account.
6. Applies environment-specific prefixes and configuration.

The aims are to reduce manual work, accelerate promotions, reduce errors and standardize AWS operations.

<a id="limites-1"></a>

### Limitations

This is a custom tool; do not claim coverage of every AWS resource or full equivalence to Terraform. Language, adoption, time saved and rollback model were not detailed.

*Sources: F1 §17; F5 §8. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p06--user-permissions"></a>

<sub>INTERNAL TOOL · SQL SERVER</sub>

## P06 — User Permissions

**Problem.** Permission administration depended on cumbersome scripts, especially on Linux and macOS.

**My contribution.** I created the User Permissions portal to manage logins, users, roles and permissions.

**Result.** Operations brought together in one interface: list, create, remove, grant and revoke. Authentication, auditing and adoption still need detailing.

<details>
<summary>Read the full account, decisions and sources</summary>

An internal tool/portal was created to manage Microsoft SQL Server users and permissions.

Script-based management on Linux/macOS was cumbersome and involved different concepts: Login, User, Roles and Permissions.

The tool supports listing, creating and deleting users, granting and removing permissions, and managing roles. It turns a script-based operational activity into a simpler internal interface.

<a id="limites-2"></a>

### Limitations

The interface stack, authentication model, audit trail, user count and measured time savings were not described. Do not infer unreported controls.

*Sources: F1 §18; F5 §8. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p07--comparador-de-parameter-store"></a>

<sub>INTERNAL TOOL · CONFIGURATION</sub>

## P07 — Parameter Store Comparator

**Problem.** Checking dozens or more than a hundred parameters across DEV, HOMOLOG and PROD was laborious.

**My contribution.** I automated comparison of Parameter Store configuration across environments.

**Result.** Detection of configuration differences. The account confirms comparison; editing and automatic synchronization were not confirmed.

<details>
<summary>Read the full account, decisions and sources</summary>

A tool was created to compare AWS Systems Manager Parameter Store configuration between environments, such as DEV versus HOMOLOG (staging) and HOMOLOG versus PROD.

Some services had dozens or more than 100 parameters, making manual comparison slow and error-prone. The tool automates the identification of differences between environments.

<a id="limites-3"></a>

### Limitations

The confirmed behavior is configuration comparison. Automatic synchronization, value editing and exposure of secrets in the interface were not confirmed. Time saved was not measured.

*Sources: F1 §19; F5 §8. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p08--incidente-de-autenticacao-e-bloqueio-no-banco"></a>

<sub>INCIDENT · DIAGNOSIS AND RECOVERY</sub>

## P08 — Authentication incident and database locking

**Problem.** Login/SSO failures required investigation across the application, Kubernetes and the database.

**My contribution.** I correlated pod health, traces and locks, contributed to mitigation and guided actions to prevent recurrence.

**Result.** Login was restored. There are two related worker accounts whose relationship remains unresolved; their details are preserved without counting two incidents.

<details>
<summary>Read the full account, decisions and sources</summary>

<a id="sintoma"></a>

### Symptom

**SSO stopped working in production**: users could not properly load the login page/flow.

<a id="investigacao"></a>

### Investigation

1. Started with observability dashboards (**Grafana/Datadog**) to check pod health and errors.
2. Identified **increased response time** in the metrics.
3. Investigated **traces** and found latency concentrated in database access.
4. Moved to RDS/database investigation, checking resource consumption, connections, queries and possible locks.
5. Found a **data extraction worker** that had become stuck, keeping queries/transactions active and locking tables used by the critical flow.

<a id="mitigacao"></a>

### Mitigation

- Terminated the problematic database transaction/connection (kill).
- Temporarily stopped the extraction worker.
- After the database was unblocked, restarted the necessary pods/containers through Kubernetes.
- Monitored recovery through observability signals until the service returned to normal.

<a id="prevencao-de-recorrencia"></a>

### Preventing recurrence

- Applied **limits to the worker**.
- Rescheduled extraction to **overnight hours**, reducing contention during peak usage.
- Added alerts for relevant RDS peaks/limits, including **CPU, memory and connections**.

<a id="papel-em-incidentes-p0"></a>

### Role in P0 incidents

- When a manager escalates a critical incident, pauses current work and begins investigating.
- Performs initial infrastructure/observability diagnosis and involves developers when application-specific knowledge is needed.
- Works with development to correlate application behavior, infrastructure and dependencies.
- Communicates directly with **technology managers** when needed.
- Communication with Product normally stays within management channels/routines and is not his primary responsibility.

<a id="pos-incidente--rca"></a>

### Post-incident / RCA

- Creates a **postmortem card/task** on the board after significant incidents.
- Documents what happened, recovery actions and preventive/corrective improvements.
- Where possible, applies improvements during or immediately after the incident, as in this case.

<a id="evidencias-profissionais-demonstradas-pelo-caso"></a>

### Capabilities demonstrated by the case

End-to-end troubleshooting; production incident response; interpreting metrics, logs and distributed tracing; Kubernetes; RDS and database diagnosis; lock/transaction analysis; correlation between application and infrastructure; technical coordination with developers; immediate mitigation and recurrence prevention; and postmortem/RCA documentation.

<a id="complemento-do-relato-de-15102026"></a>

### Additional account from October 15, 2026

**Context:** users experienced slow login.

**Diagnosis:** identified a background worker responsible for user integration and data recalculation. According to the account, a possible failure left the routine stuck/retrying transactions and blocking data used by login.

**Intervention:** assessed whether the transaction/connection could be terminated, the impact on the routine and its ability to resume. The problematic connection/transaction was terminated to remove the lock.

**Confirmed result:** login returned to normal.

**Guilherme's responsibility:** diagnosis, mitigation, identification of the suspected routine, guidance to development, follow-up on the correction and availability to clarify questions.

**Boundary:** the development team owned the final code fix. Do not attribute its implementation to Guilherme or claim the specific defect was established beyond the reported investigation.

This may relate to the earlier SSO description preserved in the same record; do not automatically count them as separate incidents.

<a id="reconciliacao-dos-relatos"></a>

### Reconciling the accounts

The earlier record calls it a data extraction worker; the October 15 account describes user integration/recalculation. Their relationship was not confirmed. They remain grouped as a related authentication/locking case, without automatically counting two events or combining the routines into one proven implementation. Operational mitigation is distinct from implementing the final code fix. Duration/MTTR was not confirmed.

*Sources: F1 §§32 and 38; F2 §32. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p09--escala-de-banco-e-separacao-de-leituraescrita"></a>

<sub>DATABASE · CAPACITY</sub>

## P09 — Database scaling and read/write separation

**Problem.** High load on the primary database affected application response times.

**My contribution.** I worked on resizing and proposed read/write separation through a read replica, alongside application changes.

**Result.** The combined changes reduced primary load by more than 50% and response time by almost 50%, according to the account. Unit, measurement window and absolute latency were not recorded.

<details>
<summary>Read the full account, decisions and sources</summary>

**Context:** a single-instance database required more capacity after a large feature was introduced.

**Reported changes:** vertical scaling to a larger instance; creation of a read replica; an architectural proposal, while supporting the team in a tech-lead capacity, to route reads to the read-only replica and writes to the primary; and changes to the main applications to use the appropriate destinations.

Guilherme described the proposal as CQRS. The detailed evidence confirms separated read/write access; it does not establish separate domain models or event sourcing.

**User-reported result:** **more than 50% less load on the primary database** and **almost 50% less application response time**.

These metrics refer to the combined changes. Do not isolate the causal effect of instance resizing from that of the replica. The specific unit of “load”, measurement window and absolute values were not provided.

**Consistency:** no perceived impact from replication lag in this project. Do not state this as a guarantee of fixed millisecond lag.

**Multi-AZ:** has never created a Multi-AZ configuration. The conversation clarified and confirmed that Multi-AZ uses different availability zones within the same region.

<a id="testes-riscos-e-rollback"></a>

### Testing, risks and rollback

The account confirms no perceived replication-lag impact in this project. It does not detail formal consistency tests, RPO/RTO, a rollback plan or lag metrics. Do not turn the solution into a claim of full CQRS or event sourcing.

*Source: F1 §38, account from October 15, 2026. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p10--recuperacao-seletiva-apos-update"></a>

<sub>DATABASE · RECOVERY</sub>

## P10 — Selective recovery after an UPDATE

**Problem.** An incorrect UPDATE changed the same field across multiple records.

**My contribution.** I restored a snapshot to an isolated instance and used an auxiliary table to apply a correction filtered by value and modification time.

**Result.** Selective recovery avoided replacing the entire database. The strategy cannot guarantee preservation of every legitimate later change.

<details>
<summary>Read the full account, decisions and sources</summary>

**Problem:** an incorrect UPDATE affected user records, setting the same incorrect value in a field. A document/ID field was used as an example in the account.

**Procedure performed:**

1. Used a specific snapshot from before the error, taken hours or a day earlier.
2. Restored the database to a new instance.
3. Extracted the necessary data and created an auxiliary table.
4. Created a script to selectively correct affected existing records.
5. Combined two selection criteria: the common incorrect value applied by the UPDATE and the modification-date interval.
6. Avoided replacing the entire production table, preserving new records inserted after the snapshot.

**Explicit limitation:** preservation of every legitimate change after the snapshot could not be guaranteed in all cases. Filters narrowed the correction scope; they do not establish lossless recovery.

**Capabilities demonstrated:** restore to an isolated instance, selective SQL recovery, impact assessment and care with data added after the backup.

<a id="limites-de-recuperacao"></a>

### Recovery limitations

Used a snapshot, not demonstrated PITR. No affected-record count, total recovery time or evidence of preservation of every legitimate change after the snapshot was provided.

*Source: F1 §38, account from October 15, 2026. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p11--upgrade-de-banco"></a>

<sub>DATABASE · EVOLUTION</sub>

## P11 — Database upgrade

**Problem.** An upgrade had to account for compatibility, dependencies and application continuity.

**My contribution.** I ran a POC and validation in a parallel environment, planned migration with a new instance and DNS cutover, and documented backup and rollback.

**Result.** A database of more than 100 GB was upgraded without reported issues, with approximately 2 hours of downtime. A return procedure was planned; testing it was not confirmed.

<details>
<summary>Read the full account, decisions and sources</summary>

**Preparation:**

- Created a POC with the main services.
- Updated libraries required for compatibility.
- Created a new instance and a parallel development environment referred to as Dev 2.
- Validated service execution and queries.
- Organized the database and application upgrade plan.

**Execution:**

- Stopped services/writes for maintenance.
- Used a new instance containing the data for migration.
- Changed the database DNS/address used by applications.
- Followed a strategy described as similar to blue-green, without claiming use of managed AWS RDS Blue/Green Deployments.
- Avoided the need for active synchronization between two databases during cutover by maintaining the service interruption.

**Rollback:** a documented procedure, with no return test reported; mandatory backup; PR reversions and application redeployment; full database restore according to the procedure if needed.

**Confirmed result:** upgrade completed without issues, approximately **two hours** of downtime, and a database of **more than 100 GB**.

Source/target versions and the exact database engine were not confirmed.

*Source: F1 §38, account from October 15, 2026. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="p12--upgrades-de-kuberneteseks"></a>

<sub>KUBERNETES · OPERATIONS</sub>

## P12 — Kubernetes/EKS upgrades

**Problem.** Evolving clusters required managing version changes and incompatibilities.

**My contribution.** I led research, documentation, testing, planning and execution of upgrades, while guiding junior engineers.

**Result.** A cluster replacement procedure with a DNS-based return option. The account includes documented NGINX/LB issues and downtime windows aligned with management.

<details>
<summary>Read the full account, decisions and sources</summary>

- Led multiple Kubernetes/EKS upgrades, responsible for research, documentation, execution planning and technical execution.
- Identifies version changes and breaking changes before the upgrade, documenting impacts and solutions.
- For larger changes, validates in development first and records problems and how they were resolved.
- In production, assesses downtime and maintenance needs; the window is aligned with management/business stakeholders.
- For critical upgrades, prefers cluster replacement/blue-green rather than relying on a downgrade: keeps the old cluster available, creates and validates the new one, and redirects traffic/DNS; on failure, returns the pointer to the previous cluster.
- Executes the procedure and trains junior DevOps engineers to perform it, turning knowledge into reusable documentation/playbooks.
- One incompatibility encountered involved NGINX/load balancer annotation/settings changes affecting parameters such as body size; the correction was investigated and added to the playbook.

<a id="resultado-e-limites-1"></a>

### Result and limitations

Experience with multiple upgrades and a reusable playbook, including guidance for junior engineers. Versions, cluster count, maintenance-window duration and downtime metrics were not confirmed. The replacement strategy concerns clusters and is distinct from database upgrade P11.

*Sources: F2 §35; F4 §35. Source identities are in [History](HISTORY.md#fontes-de-referencia).*

</details>

[↑ Back to catalogue](#indice-de-projetos)

---

<a id="formulacoes-factuais-para-futuro-curriculo"></a>

<details>
<summary><strong>Factual wording for a future résumé</strong></summary>

- Investigated and mitigated RDS locks affecting authentication by correlating metrics, queries and application routines, guiding and supporting the development team on the correction.
- Proposed read/write separation in applications, combined with database resizing and a read replica, with reported reductions of more than 50% in primary-instance load and almost 50% in response time.
- Performed selective data recovery after an incorrect UPDATE using a snapshot restored to a separate instance, an auxiliary table and scripts filtered by affected value and modification date.
- Planned and executed an upgrade of a database larger than 100 GB, with prior validation in a parallel environment, dependency updates and approximately two hours of downtime, completed without issues.

This wording preserves the limits of the accounts and still needs adaptation for the final résumé. Source: F1 §38.

</details>

<a id="modelo-para-novos-casos"></a>

<details>
<summary><strong>Template for new cases</strong></summary>

For a new case, record context/problem, personal role, previous architecture, alternatives considered, decision, implementation, validation, risks/rollback and outcome. Mark fields without evidence as not reported. Distinguish personal execution, proposals, coordination, team outcomes and hypothetical examples.

</details>

---

[← Profile](PROFILE.md) · [Home](README.md) · [Review roadmap →](ROADMAP.md)

<sub>Professional knowledge base · Updated October 15, 2026 · Branch develop</sub>
