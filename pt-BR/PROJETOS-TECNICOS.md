[English](../TECHNICAL-PROJECTS.md) | **Português (Brasil)**

[Início](README.md) · [Perfil](PERFIL-CONSOLIDADO.md) · [Projetos](PROJETOS-TECNICOS.md) · [Revisão](ROADMAP.md) · [Pendências](IDEIAS-E-PENDENCIAS.md) · [Histórico](HISTORICO.md)

---

<sub>02 / PROJETOS · GUILHERME MARTINS</sub>

# Decisões técnicas na prática

Casos que conectam engenharia de software, plataforma e operação. Cada resumo apresenta **problema, atuação e resultado**; os detalhes completos permanecem disponíveis em cada registro.

<a id="indice-de-projetos"></a>

## Índice de projetos

| ID | Caso | Evidência principal |
|---|---|---|
| P01 | [Transformação do processo de entrega](#p01--transformacao-do-processo-de-entrega) | Deploy trimestral → semanal/quinzenal |
| P02 | [Padrões de infraestrutura Kubernetes](#p02--padroes-de-infraestrutura-kubernetes) | ~4–5 dias → ~1–2 dias |
| P03 | [Padrão corporativo Lambda](#p03--padrao-corporativo-lambda) | Configuração, IAM e entrega padronizados |
| P04 | [OpenTelemetry e rastreabilidade](#p04--opentelemetry-e-rastreabilidade) | Plataforma, exemplos e Correlation ID |
| P05 | [ARO](#p05--aro) | Promoção de recursos AWS entre contas/ambientes |
| P06 | [User Permissions](#p06--user-permissions) | Operação de permissões SQL Server por portal |
| P07 | [Comparador de Parameter Store](#p07--comparador-de-parameter-store) | Diferenças de configuração automatizadas |
| P08 | [Incidente de autenticação e bloqueio no banco](#p08--incidente-de-autenticacao-e-bloqueio-no-banco) | Diagnóstico, mitigação e recuperação do login |
| P09 | [Escala de banco e separação de leitura/escrita](#p09--escala-de-banco-e-separacao-de-leituraescrita) | >50% menos carga; quase 50% menos tempo de resposta |
| P10 | [Recuperação seletiva após UPDATE](#p10--recuperacao-seletiva-apos-update) | Snapshot isolado e correção filtrada |
| P11 | [Upgrade de banco](#p11--upgrade-de-banco) | >100 GB; parada ~2 horas |
| P12 | [Upgrades de Kubernetes/EKS](#p12--upgrades-de-kuberneteseks) | Playbook, validação e substituição de cluster |

Datas dos projetos não confirmadas não são deduzidas das datas das entrevistas. O caso de upload direto é um exemplo de avaliação, preservado em [Ideias e pendências](IDEIAS-E-PENDENCIAS.md#exemplo-de-avaliacao-arquitetural-upload-direto), sem ser contado como entrega.

> **Leitura dos resultados:** métricas e experiências são autorrelatadas. O catálogo reúne casos, iniciativas e práticas recorrentes; os 12 registros não equivalem necessariamente a 12 entregas independentes.

---

<a id="p01--transformacao-do-processo-de-entrega"></a>

<sub>ENTREGA DE SOFTWARE</sub>

## P01 — Transformação do processo de entrega

**Problema.** Publicações manuais e espaçadas, com um processo extenso para chegar à produção.

**Minha atuação.** Criei pipelines, organizei o fluxo de branches e revisão de código, documentei padrões e capacitei desenvolvedores.

**Resultado.** A frequência passou de aproximadamente trimestral para semanal ou quinzenal. A evolução também trouxe rastreabilidade e menor intervenção manual.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

Um dos projetos de maior impacto relatados ocorreu quando a empresa ainda não possuía uma estrutura DevOps estabelecida.

<a id="situacao-anterior"></a>

### Situação anterior

- Publicações em produção aconteciam aproximadamente a cada **3 meses**.
- O Head realizava deploy manualmente.
- Era necessário conectar aos ambientes e executar builds manualmente.
- Existia um tutorial de aproximadamente **30 páginas** para realizar publicação em Kubernetes.
- O processo dependia fortemente de intervenção humana.

<a id="mudancas-implementadas"></a>

### Mudanças implementadas

Guilherme:

- criou os primeiros pipelines;
- definiu Git Flow;
- estruturou o processo de branches;
- estabeleceu Pull Requests obrigatórios;
- introduziu Code Review;
- definiu o fluxo Development → Stage/Homolog → Production;
- integrou o fluxo ao Jira;
- estabeleceu critérios para promoção entre ambientes;
- padronizou nomenclatura de branches, por exemplo:
  - `feature/<nome-da-tarefa>`

<a id="resultado"></a>

### Resultado

A frequência de publicação passou de aproximadamente:

**1 deploy a cada 3 meses**

para:

**deploys semanais ou quinzenais, normalmente ao final da sprint.**

Além disso:

- builds deixaram de depender das máquinas dos desenvolvedores;
- reduziu-se intervenção manual;
- conflitos e problemas relacionados a merges diminuíram significativamente;
- Code Review passou a fazer parte do processo;
- tornou-se possível rastrear o estágio de uma tarefa através do fluxo integrado ao Jira.

Esse padrão continua sendo utilizado.

<a id="papel-e-implementacao-adicional"></a>

### Papel e implementação adicional

Guilherme criou pipelines, definiu e documentou padrões e capacitou os desenvolvedores. A evolução foi incremental, incluindo posteriormente SonarQube, Trivy, Semgrep e GitLeaks. O fluxo customizado usava identificação da tarefa do Jira em branches/commits, integração em develop e releases aprovadas para a branch principal. Shared pipelines passaram a substituir a centralização antiga de scripts shell reutilizados.

<a id="limites-da-evidencia"></a>

### Limites da evidência

Não há medição de change failure rate, lead time de toda a cadeia, MTTR ou testes de rollback deste projeto. A frequência relatada não deve ser convertida em uma métrica de produtividade individual.

*Origem: F1 §10; F2 §36; F5 §4; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p02--padroes-de-infraestrutura-kubernetes"></a>

<sub>PLATAFORMA KUBERNETES</sub>

## P02 — Padrões de infraestrutura Kubernetes

**Problema.** Preparar a infraestrutura de novas aplicações exigia repetir configurações e procedimentos.

**Minha atuação.** Estruturei componentes reutilizáveis de implantação e configuração, com documentação e evolução a partir do uso.

**Resultado.** A preparação da infraestrutura passou de cerca de 4–5 para 1–2 dias, chegando a 1 dia em alguns casos. O tempo de desenvolvimento da aplicação não está incluído.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

<a id="contexto-e-implementacao"></a>

### Contexto e implementação

Criou padrões e repositórios/assets reutilizáveis para provisionar workloads, incluindo Deployment, Service, ConfigMap e demais recursos conforme o serviço. Os padrões foram documentados, testados e refinados ao longo dos anos.

<a id="resultado-1"></a>

### Resultado

Preparação de infraestrutura para um novo serviço passou de **~4–5 dias** para **~1–2 dias**, podendo chegar a **1 dia**. O desenvolvimento da aplicação continua sob responsabilidade do time correspondente.

<a id="limites"></a>

### Limites

O ganho é de preparação/provisionamento da infraestrutura; quantidade de serviços beneficiados e duração economizada total não foram informadas. Não há caso específico de rollback descrito.

*Origem: F1 §§11 e 34; F2 §35; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p03--padrao-corporativo-lambda"></a>

<sub>AWS LAMBDA</sub>

## P03 — Padrão corporativo Lambda

**Problema.** Serviços precisavam de um padrão comum para configuração, permissões e entrega entre ambientes.

**Minha atuação.** Defini o padrão com containers, configuração externa no Parameter Store, convenções de variáveis e isolamento por IAM.

**Resultado.** Uma referência corporativa para construir e operar Lambdas. O relato não inclui uma métrica de redução de tempo ou custo.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

Foi identificado que diferentes desenvolvedores criavam Lambdas de formas distintas.

Guilherme definiu um padrão corporativo para reduzir inconsistências.

<a id="containerizacao"></a>

### Containerização

As Lambdas deveriam utilizar Dockerfile / Docker image conforme o padrão definido.

<a id="configuracao"></a>

### Configuração

Anteriormente existiam casos de `.env` enviados junto com o código/ZIP.

Foi definido que configurações seriam externalizadas.

Uso de:

**AWS Systems Manager Parameter Store**

Foi estabelecida uma convenção semelhante a:

`<ambiente>/<serviço>/<variável>`

Exemplos conceituais:

- `dev/servico/DB_USER`
- `dev/servico/DB_NAME`
- `prd/servico/DB_USER`

<a id="iam-e-isolamento"></a>

### IAM e isolamento

Foram definidas roles/policies para limitar leitura de parâmetros por ambiente.

Exemplo:

- Lambda DEV → acesso somente aos parâmetros DEV;
- Lambda PROD → acesso somente aos parâmetros PROD.

Assim, workloads de desenvolvimento não deveriam acessar parâmetros de produção.

<a id="identificacao-do-servico"></a>

### Identificação do serviço

Foi estabelecida uma variável/padrão que permitia à Lambda identificar o serviço/repositório correspondente e carregar os parâmetros necessários na inicialização.

<a id="padronizacao-de-variaveis"></a>

### Padronização de variáveis

Também foi padronizada a nomenclatura de variáveis.

Antes existiam variações como:

- `username`
- `DB_USERNAME`
- `DATABASE_USER`
- `DATABASE_USER_NAME`

Passou-se a utilizar convenções consistentes, como:

- `DB_USER`
- `DB_NAME`

<a id="logging"></a>

### Logging

Foi definido também um padrão de logging.

Em determinados workloads Lambda, Graylog foi utilizado considerando inclusive o impacto de soluções de telemetria no cold start.

<a id="entrega-e-limites"></a>

### Entrega e limites

O registro inicial também inclui pipeline de build/deploy no padrão. Não há medição de redução de cold start, incidentes, custo ou horas economizadas; Graylog foi uma escolha contextual, sem generalização para todos os workloads.

*Origem: F1 §12; F5 §7; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p04--opentelemetry-e-rastreabilidade"></a>

<sub>OBSERVABILIDADE</sub>

## P04 — OpenTelemetry e rastreabilidade

**Problema.** O diagnóstico exigia conectar o comportamento das aplicações à telemetria da plataforma.

**Minha atuação.** Construí a estrutura de OpenTelemetry no cluster, com documentação, exemplos para diferentes stacks e uso de Correlation ID.

**Resultado.** Rastreabilidade entre serviços e melhoria qualitativa na investigação. Não há medição de redução de MTTR.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

Projeto relatado:

- criação de uma estrutura/cluster OpenTelemetry do zero;
- definição de como aplicações enviariam telemetria;
- documentação da integração;
- criação de exemplos de instrumentação.

Foram criados exemplos para diferentes stacks:

- Node.js;
- C#/.NET;
- Python;
- React Native;
- Angular.

O objetivo era permitir que diferentes equipes adotassem o padrão de observabilidade de maneira consistente.

<a id="correlation-id"></a>

### Correlation ID

Foi introduzida/utilizada rastreabilidade de requisições através de **Correlation ID**.

Isso possibilitou acompanhar uma requisição ao longo de diferentes componentes/serviços e pesquisar os logs relacionados.

Impacto percebido:

- identificação mais rápida de problemas;
- melhor rastreabilidade ponta a ponta;
- troubleshooting mais eficiente.

<a id="resultado-e-limites"></a>

### Resultado e limites

Instrumentação e investigação mais consistentes entre equipes, com ganho qualitativo percebido. Não há valor de MTTR antes/depois, volume de traces, retenção ou arquitetura física detalhada confirmados.

*Origem: F1 §§14–15; F5 §6; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p05--aro"></a>

<sub>FERRAMENTA INTERNA · AWS</sub>

## P05 — ARO

**Problema.** Promover recursos entre ambientes e contas exigia repetir e conferir configurações.

**Minha atuação.** Desenvolvi o ARO para coletar configurações, apresentar um plano para revisão e recriar/promover os recursos após aprovação.

**Resultado.** Um fluxo de promoção com revisão prévia. Stack, adoção, rollback e métricas ainda precisam de aprofundamento.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

Possui histórico de criação de ferramentas internas para eliminar tarefas repetitivas e reduzir erros.

<a id="aro--aws-resource-operation"></a>

### ARO — AWS Resource Operation

Ferramenta criada para facilitar promoção/criação de recursos AWS entre ambientes/contas.

Exemplo de cenário:

- existem diversas Lambdas em desenvolvimento;
- é necessário promover esses recursos para produção.

A ferramenta:

1. coleta configurações dos recursos via AWS;
2. apresenta as configurações;
3. gera uma espécie de plano;
4. permite revisão/aprovação;
5. recria/promove os recursos na conta de destino;
6. aplica prefixos e configurações correspondentes ao ambiente.

Objetivo:

- reduzir trabalho manual;
- acelerar promoções;
- diminuir erros;
- padronizar operações AWS.

<a id="limites-1"></a>

### Limites

Ferramenta própria: não atribuir a ela cobertura de todos os recursos AWS nem equivalência completa a Terraform. Linguagem, adoção, duração economizada e modelo de rollback não foram detalhados.

*Origem: F1 §17; F5 §8; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p06--user-permissions"></a>

<sub>FERRAMENTA INTERNA · SQL SERVER</sub>

## P06 — User Permissions

**Problema.** A administração de permissões dependia de scripts pouco práticos, especialmente no uso por Linux e macOS.

**Minha atuação.** Criei o portal User Permissions para gerenciar logins, usuários, roles e permissões.

**Resultado.** Operações reunidas em uma interface: listar, criar, remover, conceder e revogar. Autenticação, auditoria e adoção aguardam detalhamento.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

Foi criada uma ferramenta/portal interno para gerenciamento de usuários e permissões do Microsoft SQL Server.

Motivação:

O gerenciamento por scripts em Linux/macOS era trabalhoso e envolvia diferentes conceitos:

- Login;
- User;
- Roles;
- Permissions.

A ferramenta permite ações como:

- listar usuários;
- criar usuários;
- excluir usuários;
- conceder permissões;
- remover permissões;
- gerenciar roles.

A solução transforma uma atividade operacional baseada em scripts em uma interface interna mais simples.

<a id="limites-2"></a>

### Limites

Não foram descritos stack da interface, modelo de autenticação, trilha de auditoria, número de usuários ou ganho de tempo mensurado. Não inferir controles não relatados.

*Origem: F1 §18; F5 §8; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p07--comparador-de-parameter-store"></a>

<sub>FERRAMENTA INTERNA · CONFIGURAÇÃO</sub>

## P07 — Comparador de Parameter Store

**Problema.** Conferir dezenas ou mais de cem parâmetros entre DEV, HOMOLOG e PROD era trabalhoso.

**Minha atuação.** Automatizei a comparação de configurações do Parameter Store entre os ambientes.

**Resultado.** Identificação de diferenças de configuração. O relato confirma comparação; edição e sincronização automática não foram confirmadas.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

Foi criada uma ferramenta para comparar configurações do AWS Systems Manager Parameter Store entre ambientes.

Exemplos:

- DEV × HOMOLOG;
- HOMOLOG × PROD.

Motivação:

Alguns serviços possuíam dezenas ou mais de 100 parâmetros, tornando comparação manual lenta e sujeita a erro.

A ferramenta automatiza a identificação de diferenças entre ambientes.

<a id="limites-3"></a>

### Limites

O comportamento confirmado é comparar configurações. Não foi confirmada sincronização automática, edição de valores ou exposição dos segredos na interface. Não há duração economizada medida.

*Origem: F1 §19; F5 §8; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p08--incidente-de-autenticacao-e-bloqueio-no-banco"></a>

<sub>INCIDENTE · DIAGNÓSTICO E RECUPERAÇÃO</sub>

## P08 — Incidente de autenticação e bloqueio no banco

**Problema.** Falhas de login/SSO exigiram investigação entre aplicação, Kubernetes e banco.

**Minha atuação.** Correlacionei saúde dos pods, traces e locks, participei da mitigação e orientei ações para prevenir recorrência.

**Resultado.** O login foi restabelecido. Há dois relatos relacionados de workers cuja relação permanece em aberto; os detalhes estão preservados sem contar dois incidentes.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

<a id="sintoma"></a>

### Sintoma

O **SSO parou de funcionar em producao**: usuarios nao conseguiam carregar adequadamente a pagina/fluxo de login.

<a id="investigacao"></a>

### Investigacao

1. Iniciou pelos dashboards de observabilidade (**Grafana/Datadog**) para validar saude dos pods e ocorrencia de erros.
2. Identificou nas metricas **aumento do tempo de resposta**.
3. Investigou os **traces** e identificou que a latencia estava concentrada no acesso ao banco de dados.
4. Passou para a investigacao do RDS/banco, verificando consumo, conexoes, queries e possiveis locks.
5. Encontrou um **worker de extracao de dados** que havia travado e mantinha queries/transacoes causando lock em tabelas utilizadas pelo fluxo critico.

<a id="mitigacao"></a>

### Mitigacao

- Encerrou a transaction/connection problematica no banco (kill).
- Interrompeu temporariamente o worker responsavel pela extracao.
- Depois da liberacao do banco, reiniciou os pods/containers necessarios via Kubernetes.
- Acompanhou a recuperacao pelos sinais de observabilidade ate a normalizacao do servico.

<a id="prevencao-de-recorrencia"></a>

### Prevencao de recorrencia

- Aplicou **limitacao no worker**.
- Alterou o agendamento da extracao para a **madrugada**, reduzindo concorrencia com o horario de maior uso.
- Adicionou alertas para picos/limites relevantes do RDS, incluindo **CPU, memoria e conexoes**.

<a id="papel-em-incidentes-p0"></a>

### Papel em incidentes P0

- Quando um incidente critico e escalado pelo gerente, interrompe a atividade corrente e inicia a investigacao.
- Faz o diagnostico inicial de infraestrutura/observabilidade e envolve desenvolvedores quando a analise exige conhecimento especifico da aplicacao.
- Trabalha em conjunto com desenvolvimento para correlacionar comportamento da aplicacao, infraestrutura e dependencias.
- Comunica-se diretamente com **gerentes das areas de tecnologia** quando necessario.
- A comunicacao com Produto normalmente fica nos canais/rituais de gestao e nao e uma responsabilidade primaria sua.

<a id="pos-incidente--rca"></a>

### Pos-incidente / RCA

- Cria **card/tarefa de pos-mortem** no board apos incidentes relevantes.
- Documenta o que aconteceu, as acoes executadas para recuperacao e melhorias preventivas/corretivas.
- Quando possivel, as melhorias ja sao aplicadas durante ou imediatamente apos o incidente, como ocorreu neste caso.

<a id="evidencias-profissionais-demonstradas-pelo-caso"></a>

### Evidencias profissionais demonstradas pelo caso

Este caso demonstra, de forma concreta:

- troubleshooting ponta a ponta;
- incident response em producao;
- leitura de metricas, logs e distributed tracing;
- Kubernetes;
- RDS e diagnostico de banco de dados;
- analise de locks/transacoes;
- correlacao entre aplicacao e infraestrutura;
- coordenacao tecnica com desenvolvedores;
- mitigacao imediata e prevencao de recorrencia;
- documentacao de pos-mortem/RCA.

<a id="complemento-do-relato-de-15102026"></a>

### Complemento do relato de 15/10/2026

**Contexto:** usuários enfrentavam lentidão para fazer login.

**Diagnóstico:** identificou um worker em background responsável por integração de usuários e recálculo de dados. Segundo o relato, uma possível falha fazia a rotina permanecer presa/repetindo tentativas de transação e bloqueando dados utilizados pelo login.

**Intervenção:** avaliou a possibilidade de encerrar a transação/conexão, o impacto na rotina e a possibilidade de retomada. A conexão/transação problemática foi encerrada para remover o bloqueio.

**Resultado confirmado:** o login voltou ao normal.

**Responsabilidade de Guilherme:** diagnóstico, mitigação, identificação da rotina suspeita, direcionamento para desenvolvimento, acompanhamento da correção e disponibilidade para esclarecer dúvidas.

**Limite:** a correção definitiva do código ficou com o time de desenvolvimento. Não atribuir a Guilherme sua implementação nem afirmar que o defeito específico foi comprovado além da investigação relatada.

O relato pode se relacionar à descrição anterior de SSO, preservada neste mesmo registro; não contar automaticamente os dois como incidentes distintos.

<a id="reconciliacao-dos-relatos"></a>

### Reconciliação dos relatos

O registro anterior chama o worker de extração de dados; o de 15/10 descreve integração de usuários/recálculo. A relação entre eles não foi confirmada. Os relatos ficam agrupados como um caso relacionado de autenticação/locks, sem contar automaticamente duas ocorrências nem fundir as rotinas em uma mesma implementação comprovada. A mitigação operacional não equivale à implementação da correção definitiva de código. Não há duração/MTTR confirmado.

*Origem: F1 §§32 e 38; F2 §32; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p09--escala-de-banco-e-separacao-de-leituraescrita"></a>

<sub>BANCO DE DADOS · CAPACIDADE</sub>

## P09 — Escala de banco e separação de leitura/escrita

**Problema.** Carga elevada no banco principal afetava a resposta das aplicações.

**Minha atuação.** Atuei no redimensionamento e propus a separação de leitura e escrita com réplica, em conjunto com as mudanças de aplicação.

**Resultado.** O conjunto das mudanças reduziu a carga no principal em mais de 50% e o tempo de resposta em quase 50%, segundo o relato. Unidade, janela e latência absoluta não foram registradas.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

**Contexto:** banco com uma única instância demandou mais capacidade após uma funcionalidade de grande porte.

**Mudanças relatadas:**

- aumento do tamanho da instância, com escala vertical;
- criação de réplica de leitura;
- proposta arquitetural, em atuação de apoio como tech lead, para direcionar leituras à réplica read-only e escritas à instância principal;
- alterações nas principais aplicações para utilizar os destinos adequados.

Guilherme descreveu a proposta como CQRS. A evidência detalhada confirma separação de acessos de leitura e escrita; não pressupõe modelos de domínio separados ou event sourcing.

**Resultado relatado pelo usuário:**

- redução de **mais de 50% na carga do banco principal**;
- redução de **quase 50% no tempo de resposta das aplicações**.

As métricas se referem ao conjunto das mudanças; não isolar causalmente o efeito do aumento da instância do efeito da réplica. A unidade específica de “carga”, a janela de medição e os valores absolutos não foram informados.

**Consistência:** não houve impacto percebido do atraso de replicação nesse projeto. Não registrar como garantia de atraso fixo em milissegundos.

**Multi-AZ:** nunca criou uma configuração Multi-AZ. Foi esclarecido e confirmado na conversa que Multi-AZ utiliza zonas de disponibilidade distintas dentro da mesma região.

<a id="testes-riscos-e-rollback"></a>

### Testes, riscos e rollback

O relato confirma que não houve impacto percebido de atraso da réplica nesse projeto. Não detalha teste formal de consistência, RPO/RTO, plano de rollback ou métricas de lag. Não converter a solução em CQRS completo ou event sourcing.

*Origem: F1 §38, relato de 15/10/2026; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p10--recuperacao-seletiva-apos-update"></a>

<sub>BANCO DE DADOS · RECUPERAÇÃO</sub>

## P10 — Recuperação seletiva após UPDATE

**Problema.** Um UPDATE indevido alterou o mesmo campo em múltiplos registros.

**Minha atuação.** Restaurei um snapshot em instância isolada e usei uma tabela auxiliar para realizar uma correção filtrada por valor e horário de modificação.

**Resultado.** Recuperação seletiva, evitando substituir a base inteira. A estratégia não permite garantir a preservação de toda alteração legítima posterior.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

**Problema:** UPDATE indevido afetou registros de usuários, atribuindo um mesmo valor incorreto a um campo. Documento/ID foi usado como exemplo no relato.

**Procedimento executado:**

1. Utilizou um snapshot específico anterior ao erro, de horas ou de um dia antes.
2. Restaurou o banco em uma nova instância.
3. Extraiu os dados necessários e criou uma tabela auxiliar.
4. Criou um script de correção seletiva dos registros existentes afetados.
5. Combinou dois critérios de seleção: o valor incorreto comum aplicado pelo UPDATE e o intervalo da data de modificação.
6. Evitou substituir integralmente a tabela de produção, para preservar os registros novos que haviam entrado após o snapshot.

**Limitação explicitada:** não era possível garantir em todos os casos a preservação de todas as alterações legítimas posteriores ao snapshot. Os filtros reduziram o escopo da correção; não equivalem a comprovação de recuperação sem perda.

**Competências demonstradas:** restore em instância isolada, recuperação seletiva por SQL, avaliação de impacto e cuidado com dados posteriores ao backup.

<a id="limites-de-recuperacao"></a>

### Limites de recuperação

Usou snapshot, não PITR comprovado. Não há contagem de registros afetados, tempo total de recuperação ou evidência de preservação de todas as alterações legítimas após o snapshot.

*Origem: F1 §38, relato de 15/10/2026; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p11--upgrade-de-banco"></a>

<sub>BANCO DE DADOS · EVOLUÇÃO</sub>

## P11 — Upgrade de banco

**Problema.** Um upgrade precisava considerar compatibilidade, dependências e continuidade das aplicações.

**Minha atuação.** Conduzi POC e validações em ambiente paralelo, planejei a migração com nova instância e troca de DNS e documentei backup e rollback.

**Resultado.** Banco de mais de 100 GB atualizado sem problemas relatados, com parada de aproximadamente 2 horas. O retorno foi planejado; seu teste não foi confirmado.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

**Preparação:**

- criou uma POC com os principais serviços;
- atualizou bibliotecas necessárias à compatibilidade;
- criou uma nova instância e um ambiente paralelo de desenvolvimento, referido como Dev 2;
- validou execução dos serviços e consultas;
- organizou roteiro de atualização do banco e das aplicações.

**Execução:**

- realizou parada técnica dos serviços/gravações;
- utilizou uma nova instância com os dados para a migração;
- mudou o DNS/endereço de banco utilizado pelas aplicações;
- adotou uma estratégia descrita como semelhante a blue-green, sem afirmar uso do recurso gerenciado AWS RDS Blue/Green Deployments;
- evitou a necessidade de sincronização ativa entre dois bancos durante a troca, mantendo a parada técnica.

**Rollback:**

- procedimento documentado, sem teste de retorno relatado;
- backup como passo obrigatório;
- reversão dos PRs e redeploy das aplicações;
- restauração integral do banco conforme procedimento, se necessário.

**Resultado confirmado:**

- atualização concluída sem problemas;
- indisponibilidade de aproximadamente **duas horas**;
- banco com **mais de 100 GB**.

Não foram confirmadas as versões de origem/destino nem o engine exato deste upgrade.

*Origem: F1 §38, relato de 15/10/2026; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="p12--upgrades-de-kuberneteseks"></a>

<sub>KUBERNETES · OPERAÇÃO</sub>

## P12 — Upgrades de Kubernetes/EKS

**Problema.** A evolução dos clusters exigia lidar com mudanças de versão e incompatibilidades.

**Minha atuação.** Liderei estudo, documentação, testes, planejamento e execução de upgrades, com orientação de profissionais juniores.

**Resultado.** Procedimento de substituição de cluster e possibilidade de retorno por DNS. O relato inclui problemas de NGINX/LB documentados e janelas de parada alinhadas com a gestão.

<details>
<summary>Ver relato completo, decisões e fontes</summary>

- Liderou diversas atualizações de Kubernetes/EKS, sendo responsável pelo estudo, documentação, plano de execução e execução técnica.
- Antes do upgrade, levanta mudanças de versão e breaking changes, documentando impactos e respectivas soluções.
- Para mudanças maiores, valida primeiro em desenvolvimento e registra problemas encontrados e como foram resolvidos.
- Em produção, avalia necessidade de indisponibilidade e parada técnica; a definição da janela é alinhada com a gestão/negócio.
- Para upgrades críticos, prefere estratégia de substituição/blue-green de cluster em vez de depender de downgrade: mantém o cluster antigo disponível, cria e valida o novo e direciona o tráfego/DNS; em caso de falha, retorna o apontamento ao cluster anterior.
- Também executa o procedimento e capacita DevOps juniores a realizá-lo, transformando o conhecimento em documentação/playbook reutilizável.
- Exemplo de incompatibilidade já enfrentada: mudanças de annotations/configurações relacionadas ao NGINX/load balancer afetando parâmetros como body size; a correção foi investigada e incorporada ao playbook.

<a id="resultado-e-limites-1"></a>

### Resultado e limites

Experiência em diversas atualizações e criação de playbook reutilizável, incluindo orientação de profissionais juniores. Não há versões, quantidade de clusters, duração de janela ou métrica de indisponibilidade confirmadas. A estratégia de substituição descrita é de cluster, distinta do upgrade de banco P11.

*Origem: F2 §35; F4 §35; identificação das fontes em [Histórico](HISTORICO.md#fontes-de-referencia).*

</details>

[↑ Voltar ao catálogo](#indice-de-projetos)

---

<a id="formulacoes-factuais-para-futuro-curriculo"></a>

<details>
<summary><strong>Formulações factuais para futuro currículo</strong></summary>

- Investigou e mitigou bloqueios em RDS que afetavam autenticação, correlacionando métricas, consultas e rotinas de aplicação, com direcionamento e apoio à equipe de desenvolvimento na correção.
- Propôs separação de leitura/escrita nas aplicações, combinada a redimensionamento do banco e réplica de leitura, com redução relatada de mais de 50% na carga da instância principal e de quase 50% no tempo de resposta.
- Executou recuperação seletiva de dados após UPDATE indevido, utilizando snapshot restaurado em instância separada, tabela auxiliar e scripts filtrados por valor afetado e data de modificação.
- Planejou e executou upgrade de banco com mais de 100 GB, com validação prévia em ambiente paralelo, atualização de dependências e parada técnica de aproximadamente duas horas, concluído sem problemas.

Essas formulações preservam os limites do relato e ainda devem ser adaptadas ao currículo final. Origem: F1 §38.

</details>

<a id="modelo-para-novos-casos"></a>

<details>
<summary><strong>Modelo para novos casos</strong></summary>

Para incorporar um novo caso, registrar contexto/problema, papel pessoal, arquitetura anterior, alternativas consideradas, decisão, implementação, validação, riscos/rollback e resultado. Campos sem evidência devem ser marcados como não informados. Distinguir execução própria, proposta, coordenação, resultado da equipe e exemplo hipotético.

</details>


---

[← Perfil](PERFIL-CONSOLIDADO.md) · [Início](README.md) · [Roadmap da revisão →](ROADMAP.md)

<sub>Base profissional · Atualizada em 15/10/2026 · Branch develop</sub>
