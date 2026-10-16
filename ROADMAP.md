[Início](README.md) · [Perfil](PERFIL-CONSOLIDADO.md) · [Projetos](PROJETOS-TECNICOS.md) · [Revisão](ROADMAP.md) · [Pendências](IDEIAS-E-PENDENCIAS.md) · [Histórico](HISTORICO.md)

---

<sub>03 / REVISÃO · GUILHERME MARTINS</sub>

# O que já está consolidado. O que vem agora.

**6 de 10 blocos concluídos · 60%**

O levantamento já reúne AWS, Kubernetes, entrega, observabilidade, segurança e bancos. A próxima etapa é **Networking / Multi-account**, aproveitando as respostas existentes.

Conclusão indica levantamento suficiente da experiência relatada. Novas informações podem complementar um assunto sem reiniciar a entrevista. Nenhum bloco está formalmente em andamento após o fechamento de Bancos em 15/10/2026.

## Mapa da revisão

| Bloco | Estado | Conteúdo |
| :--- | :--- | :--- |
| [01 · AWS / Cloud Architecture / IaC](#1-aws--cloud-architecture--iac) | Concluído | Serviços, arquitetura e IaC |
| [02 · Kubernetes / Containers](#2-kubernetes--containers) | Concluído | Planejamento, operação e upgrades |
| [03 · CI/CD / Developer Experience](#3-cicd--developer-experience) | Concluído | Pipelines, padrões e adoção |
| [04 · Observabilidade / SRE / Incidentes](#4-observabilidade--sre--incidentes) | Concluído | Telemetria, diagnóstico e incidentes |
| [05 · Segurança / IAM / Governança](#5-seguranca--iam--governanca) | Concluído | Permissões, credenciais e controles |
| [06 · Networking / Multi-account](#6-networking--multi-account) | **Próximo** | Conectividade, isolamento e escopo pessoal |
| [07 · Bancos / Backup / DR](#7-bancos--backup--dr) | Concluído | Capacidade, recuperação e migração |
| [08 · Liderança técnica / Arquitetura / Documentação](#8-lideranca-tecnica--arquitetura--documentacao) | Pendente | Influência, mentoria e decisões |
| [09 · Ferramentas internas / IA / Automação](#9-ferramentas-internas--ia--automacao) | Pendente | Stack, adoção e resultados |
| [10 · Experiências anteriores / Impacto / Posicionamento](#10-experiencias-anteriores--impacto--posicionamento) | Pendente | Casos anteriores e posicionamento |

<a id="6-networking--multi-account"></a>

## 6. Networking / Multi-account

**Pendente — próximo bloco.**

Já existe material sobre Organizations/roles cross-account, contas por ambiente, Route 53, ACM, ALB/NLB, entrada de tráfego em Kubernetes e promoção AWS entre contas. Esses pontos devem ser reaproveitados, sem perguntar tudo novamente.

Lacunas a verificar, sem presumir experiência:

- Casos concretos de VPC, subnets, CIDR e rotas; papel pessoal no desenho e operação.
- Conectividade entre ambientes/contas e experiência prática com peering ou outras soluções, se houver.
- Security groups e isolamento de tráfego; decisões e troubleshooting relevantes.
- Alcance das contas administradas e limites de responsabilidade em Organizations/governança.

Essas perguntas são pendências da revisão, não confirmação de uso das tecnologias. Fontes: F1 §§6, 17, 29–31 e 36.

## Registro por bloco

Expanda os blocos concluídos para consultar o que já foi respondido. Os blocos ainda pendentes mostram o material disponível e o aprofundamento necessário.

<a id="1-aws--cloud-architecture--iac"></a>

<details>
<summary><strong>1. AWS / Cloud Architecture / IaC · concluído</strong></summary>

**Concluído.**

Já registrado:

- Seleção de serviços com desenvolvimento, avaliação de complexidade, custo e necessidade real.
- EC2, EKS/Kubernetes, Lambda, RDS, S3, API Gateway e serviços relacionados; não inventariar ambientes sem confirmação.
- SQS Standard/FIFO, DLQ, retries, visibility timeout, retenção, consumidores, batch e deduplicação; SNS e EventBridge. Não usa Step Functions atualmente.
- Route 53: hosted zones, records e necessidades de roteamento; ACM e certificados TLS.
- ALB/NLB: listeners, targets, health checks, regras e certificados; parte automatizada por EKS/kOps.
- S3/CloudFront: entrega de front-end, distributions/behaviors e invalidação em pipeline.
- Secrets Manager e rotação de credenciais de RDS; configurações por Parameter Store.
- Experiência anterior com Terraform, Terragrunt e CloudFormation, inclusive ambientes do zero; uso cotidiano atual limitado pelo contexto da empresa.
- Participa das decisões de custo; Head é responsável principal por FinOps.

Detalhes em [Perfil consolidado](PERFIL-CONSOLIDADO.md); casos P03, P05 e P07. Fonte: F1 §§6–7 e 31.

</details>

<a id="2-kubernetes--containers"></a>

<details>
<summary><strong>2. Kubernetes / Containers · concluído</strong></summary>

**Concluído em 05/10/2026.**

Já registrado:

- Docker, Kubernetes, EKS/kOps, Docker Swarm, Dockerfiles, Deployments, Services, ConfigMaps, Ingress e HPA.
- Planejamento conforme produto: pods, serviços, persistência, entrada, nuvem, ambientes, namespaces/clusters e IaC.
- Padrões reutilizáveis reduziram preparação da infraestrutura de ~4–5 para ~1–2 dias, podendo chegar a 1 dia.
- Operação, capacidade de nodes, réplicas, CrashLoopBackOff, logs atuais/anteriores e investigação de fatores externos.
- Requests/limits orientados por APM, carga, startup, consumo normal e picos.
- Upgrades com estudo, documentação, validação prévia e estratégia de substituição de cluster; capacitação de juniores.
- Uso de Operators prontos, incluindo Prometheus Operator; não desenvolveu Operators próprios/CRDs customizados.
- HPA/Cluster Autoscaler ajustados por workload; redução noturna de capacidade quando aplicável. Sem uso de VPA relatado.

Detalhes no perfil e casos P02/P12. Fontes: F1 §34; F2 §§34–35. Não reabrir perguntas encerradas.

</details>

<a id="3-cicd--developer-experience"></a>

<details>
<summary><strong>3. CI/CD / Developer Experience · concluído</strong></summary>

**Concluído em 05/10/2026.**

Já registrado:

- Bitbucket Pipelines como principal; GitHub Actions, Jenkins e Bitrise em outras experiências.
- Implantação inicial de build/deploy automatizado, documentação e capacitação dos desenvolvedores.
- Git Flow customizado, PR e Code Review, promoção de ambientes e rastreabilidade no Jira.
- Externalização de configuração, convenções de variáveis e remoção de configurações hard-coded.
- Reuso de scripts e posterior uso de shared pipelines/templates.
- Controles incrementais de qualidade/segurança, Docker multi-stage, ECR e OIDC.
- Diagnóstico conjunto de falhas de código, variáveis e pipelines antigas.
- Deploy trimestral passou a semanal/quinzenal; sem série completa de métricas DORA.

Detalhes no perfil e P01/P03. Fontes: F1 §§9–10, 31 e 35; F2 §36.

</details>

<a id="4-observabilidade--sre--incidentes"></a>

<details>
<summary><strong>4. Observabilidade / SRE / Incidentes · concluído</strong></summary>

**Concluído.**

Já registrado:

- Datadog + OpenTelemetry como base principal; experiência também com Grafana, Graylog, Zabbix, Loki, ELK/EFK e New Relic.
- Plataforma OpenTelemetry do zero, documentação e exemplos para Node.js, C#/.NET, Python, React Native e Angular.
- Correlation ID, logs, métricas, APM, traces, alertas e instrumentação com os times.
- CloudWatch focado principalmente em logs e alarmes pontuais.
- Investigação ponta a ponta, atuação em P0, recuperação, comunicação técnica com gerentes e pós-mortem/RCA.
- Caso de login/SSO afetado por locks: contexto de aplicação, banco e Kubernetes; evitar dupla contagem dos relatos relacionados.

Detalhes no perfil e P04/P08. Fontes: F1 §§13–16, 31–32 e 38.

</details>

<a id="5-seguranca--iam--governanca"></a>

<details>
<summary><strong>5. Segurança / IAM / Governança · concluído</strong></summary>

**Concluído em 05/10/2026.**

Já registrado:

- Usuários, grupos, roles, policies, MFA e menor privilégio.
- Modelagem de permissão conforme quem acessa e qual recurso/ação precisa usar; policies gerenciadas ou próprias conforme contexto.
- Reuso de policies e agrupamento de permissões; remoção com checklist e validação do contexto.
- OIDC nas pipelines, Secrets Manager e rotação de credenciais RDS.
- Isolamento por ambiente e prefixo no Parameter Store; acesso cross-account por roles.
- Requisitos de segurança na revisão arquitetural, sem atribuição de responsabilidade jurídica formal.

Detalhes no perfil e P03. Fontes: F2 §37; F1 §§31 e 36.

</details>

<a id="7-bancos--backup--dr"></a>

<details>
<summary><strong>7. Bancos / Backup / DR · concluído</strong></summary>

**Concluído em 15/10/2026.** Foi o sexto bloco encerrado; sua numeração continua sendo 7.

Já registrado:

- Atuação em plataforma/cloud, sem ser DBA dedicado; criação de bancos/usuários, diagnóstico, capacidade, recuperação e upgrades.
- CPU, memória, conexões, waits, locks, queries lentas e correlação com serviço/rotina; comparação de conexões com últimas ~12 horas.
- Planos de execução e sugestões de query/índice de forma pontual, com validação e implementação pelo time responsável.
- Mitigação de bloqueios afetando login, com avaliação de impacto antes de encerrar transação/conexão.
- Redimensionamento e réplica de leitura com separação de acessos: >50% menos carga no principal e quase 50% menos tempo de resposta, como resultado conjunto.
- Restore de snapshot em instância separada e correção seletiva após UPDATE indevido, com limites de preservação das alterações posteriores.
- Upgrade de banco >100 GB, POC/Dev 2, dependências, nova instância, troca de DNS, backup e rollback documentado; parada ~2 horas e conclusão sem problemas.
- Política de backup principalmente com o Head. Sem criação de Multi-AZ, failover confirmado, PITR comprovado ou rotina formal de testes periódicos de DR relatados.

Detalhes no perfil e P08–P11. Fonte principal: F1 §38, que atualiza o estado antigo de F2 §38.

</details>

<a id="8-lideranca-tecnica--arquitetura--documentacao"></a>

## 8. Liderança técnica / Arquitetura / Documentação

**Pendente de revisão dedicada; material já coletado.**

- Referência transversal, sem gestão formal de pessoas; padrões chegaram a ~4 times/~30 desenvolvedores no período citado.
- Kickoffs, arquitetura, POCs/implementações de referência, documentação, orientação e acompanhamento da adesão.
- Anteriormente definia arquiteturas diretamente; hoje revisa propostas dos desenvolvedores, solicita ajustes e pode impedir aprovação imediata.
- Prioridade: custo/ROI, segurança, performance e observabilidade; riscos e trade-offs documentados.
- Em divergências, gestão tem palavra final hierárquica; não atribuir autoridade executiva unilateral.
- Orienta profissionais juniores e documenta procedimentos, inclusive upgrades.

Ainda aprofundar: outros exemplos de influência/mentoria, processo e alcance da documentação/decisões, resultados de adoção. Não presumir uso formal de RFC/ADR somente por constar no escopo original.

Fontes: F1 §§2–4, 21 e 37; F2 §§35–36 e 39. Ver perfil e exemplo em Ideias/Pendências.

<a id="9-ferramentas-internas--ia--automacao"></a>

## 9. Ferramentas internas / IA / Automação

**Pendente de aprofundamento.**

- ARO, User Permissions e Comparador de Parameter Store já descritos, com casos P05–P07.
- Responsabilidade atribuída para padrões corporativos de IA: harness, ferramentas, skills, repositórios, documentação, exemplos e adesão.
- Preferência por automação e prevenção de problemas já registrada.

Ainda aprofundar: arquitetura/stack das ferramentas, usuários e adoção, métricas, manutenção e limites; estado real de implantação da iniciativa de IA e resultados observáveis. Não tratar atribuição de responsabilidade como entrega concluída.

Fontes: F1 §§17–20; F5 §§8 e 10. Ver [Ideias e pendências](IDEIAS-E-PENDENCIAS.md).

<a id="10-experiencias-anteriores--impacto--posicionamento"></a>

## 10. Experiências anteriores / Impacto / Posicionamento

**Pendente de revisão dedicada.**

- Histórico de Conexia, FH_, Beblue, JET, SiplanControl-M, LMS e Artoni preservado no perfil.
- Base forte em C#/.NET e Node.js; experiências com Go, Python, Shell e Azure/Windows Azure.
- Posicionamento **Senior Cloud Platform Engineer** definido em 13/10; cargo histórico preservado.
- Preferência por IC técnico transversal, arquitetura, plataforma, ferramentas e prevenção; sem interesse atual em gestão formal.
- Inglês: boa leitura, conversação limitada e desconforto com entrevistas; sem nível CEFR atribuído.

Ainda aprofundar: projetos anteriores e impacto, escala e métricas disponíveis, experiências Azure e avaliação fundamentada de Senior/Staff/Principal. Datas sobrepostas do CV e durações aproximadas permanecem como registradas até confirmação.

Fontes: F1 §§1, 5–7 e 23–28; F2 §§1 e 27; F5 §§12–16.

<a id="criterios-de-conclusao-e-regras-de-continuidade"></a>

<details>
<summary><strong>Critérios de conclusão e regras de continuidade</strong></summary>

1. Consultar os seis arquivos antes de perguntar novamente.
2. Rever apenas lacunas do bloco escolhido; experiência já respondida não é refeita.
3. Separar execução própria, proposta, responsabilidade da equipe e exemplo hipotético.
4. Preservar métricas aproximadas e limites; ausência de experiência também é resposta válida.
5. Atualizar perfil/projetos, registrar decisões no histórico e salvar antes de avançar.
6. Marcar conclusão somente quando houver registro de fechamento; não alterar o progresso por simples reorganização documental.

</details>

<a id="proximo-passo"></a>

## Próximo passo

Retomar **Networking / Multi-account**, partindo das informações já existentes sobre contas, IAM, DNS, balanceadores e Kubernetes. Os blocos concluídos permanecem encerrados; novos relatos podem complementá-los sem reiniciar a entrevista.

O roadmap de 10 blocos substitui a lista antiga de 36 pontos. Estado reconciliado a partir de F1 §§29, 30, 33 e 38 e dos aprofundamentos de F2, conforme o [Histórico](HISTORICO.md#reconciliacao-entre-versoes). A reorganização editorial não altera o progresso.

---

[← Projetos](PROJETOS-TECNICOS.md) · [Início](README.md) · [Ideias e pendências →](IDEIAS-E-PENDENCIAS.md)

<sub>Base profissional · Atualizada em 15/10/2026 · Branch develop</sub>
