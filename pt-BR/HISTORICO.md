[English](../HISTORY.md) | **Português (Brasil)**

[Início](README.md) · [Perfil](PERFIL-CONSOLIDADO.md) · [Projetos](PROJETOS-TECNICOS.md) · [Revisão](ROADMAP.md) · [Pendências](IDEIAS-E-PENDENCIAS.md) · [Histórico](HISTORICO.md)

---

<sub>05 / HISTÓRICO · GUILHERME MARTINS</sub>

# A memória das decisões

Fontes, revisões e decisões que sustentam o perfil. Cada nova confirmação atualiza o documento temático e deixa aqui um registro de sua origem.

[Última revisão](#auditoria-library-2026-10-15) · [Linha do tempo](#registro-de-sessoes) · [Decisões](#decisoes-consolidadas) · [Fontes](#fontes-de-referencia)

<a id="auditoria-library-2026-10-15"></a>

## 15/10/2026 · Auditoria das fontes da Library

**Pedido:** conferir individualmente os arquivos da Library/Space e recuperar material útil antes da exclusão dos originais pelo usuário.

O navegador autenticado mostrou a Library legada, incluindo as pastas Profile e Reuniões Inglês. O inventário histórico contém **85 arquivos**. As cinco fontes profissionais em Markdown e os seis documentos derivados foram lidos; o texto renderizado dos seis derivados correspondeu ao ZIP importado após remover marcação explícita de âncoras e normalizar acentos, caixa e caracteres não alfanuméricos. Isso confere conteúdo normalizado, não identidade byte a byte.

| Fonte / grupo | Resultado e destino |
|---|---|
| F1 | Estado atual de 6/10, casos de Bancos e limites das evidências já preservados |
| F2 | Revisões detalhadas e governança arquitetural já preservadas |
| F3 | Cópia na pasta comparada separadamente; governança preservada, posicionamento antigo superado por decisões explícitas |
| F4 | Estado anterior de 4/10 preservado no histórico; não substitui 6/10 |
| F5 | Fonte inicial comparada; P01 ganha redução de alterações diretas na principal e referência temporal relativa com ressalva |
| Seis documentos `/Profile/*.md` | Conteúdo renderizado atual conferido com a base importada de seis arquivos |
| ZIP importado | Importação local disponível; o binário atual da Library não foi baixado para comparação byte a byte |
| F6 — CV em português, 2 páginas | Acrescenta contexto de entrega/domínio às experiências anteriores no Perfil |
| F7 — CV do LinkedIn, 5 páginas | Complementa experiências anteriores; divergência no início como Senior DevOps registrada nas Pendências |
| F8 — descrição HE SRE, 2 páginas | Referência de entrevista nas Pendências; requisitos não atribuídos a Guilherme |
| DOCX de treino de entrevista em inglês | Visualizador não abriu; preservar original, conteúdo ainda pendente |
| Demais arquivos | 65 imagens triadas visualmente; transcrição, listagem de pacote e acordo pessoal classificados sem relação com o perfil profissional. Planilha histórica indisponível. Inventário individual privado mantido localmente |

**Detalhes recuperados:** entrega .NET Core/Docker Swarm on-premises na FH_; portais web/e-commerce, integrações com ERPs e busca de produtos SOLR na JET; sistemas para cartórios na SPCM; suporte à infraestrutura e redes locais na Artoni. São relatos das fontes, não novas confirmações do usuário.

**Estado para exclusão:** sem liberação geral. O DOCX de entrevistas continua sem leitura, a planilha histórica está indisponível e a auditoria não constitui backup completo dos arquivos originais. Nenhum original foi apagado. Documentos pessoais, contatos e mídias sem relação com o perfil não foram copiados para o repositório.

**Documentos afetados:** README, Perfil, Projetos, Pendências e Histórico nas duas línguas. **Revisão:** permanece **6/10 — 60%**; próximo tema Networking / Multi-account.

<a id="estrutura-bilingue-2026-10-15"></a>

## 15/10/2026 · Inglês padrão e opção em português brasileiro

**Decisão do usuário:** quem acessar deve ver inglês primeiro e poder trocar para português brasileiro.

- A raiz contém os seis documentos completos em inglês: README, Perfil, Projetos técnicos, Roadmap, Ideias/Pendências e Histórico.
- Os documentos existentes em português foram preservados em `pt-BR/`, com navegação local e links para o documento equivalente em inglês.
- Cada idioma tem sua própria capa. Os recursos compartilhados permanecem em `assets/`.
- As duas versões representam o mesmo conteúdo profissional; novas confirmações devem ser refletidas nos dois idiomas no mesmo commit. As revisões podem continuar em português.
- A escolha de idioma foi resolvida nas Pendências, e o `AGENTS.md` registra as regras de manutenção bilíngue.

**Origem:** esclarecimento explícito do usuário nesta conversa. **Base da tradução:** commit `987cbe2`. **Documentos afetados:** os dois conjuntos de seis Markdown, `AGENTS.md` e as capas. **Estado da revisão:** mantidos **6/10 — 60%**, com Networking / Multi-account como próximo bloco. A tradução não introduz fatos, métricas, responsabilidades ou fechamentos adicionais.

<a id="revisao-editorial-2026-10-15"></a>

## 15/10/2026 · Apresentação e organização editorial

**Solicitação:** melhorar a apresentação dos seis Markdown e preenchê-los com o conteúdo já refinado.

- README reescrito como entrada profissional, com capa, apresentação, resultados contextualizados e navegação para os cinco documentos.
- Perfil com síntese de trajetória, competências e forma de atuação; relatos completos mantidos em seções expansíveis.
- Os 12 registros técnicos ganharam resumos de problema, atuação e resultado; detalhes, limites e fontes foram preservados.
- Roadmap organizado por estado e próximo assunto; pendências e histórico receberam navegação e hierarquia de leitura.
- Corrigida a nota antiga de pendências que tratava toda publicação como não autorizada: o usuário já solicitou o versionamento e a disponibilização da branch. A seleção de conteúdo para a apresentação pública final continua aberta.

**Base utilizada:** conteúdo consolidado dos seis documentos em `6a3aa73`, originado do ZIP importado e das fontes F1–F5. As novas sínteses foram redigidas a partir desse material; esta edição não recupera conversas adicionais nem valida novamente experiências ou métricas.

**Documentos afetados:** os seis Markdown e a capa local em `assets/profile-cover.svg`. **Estado da revisão:** mantidos **6/10 — 60%**, com Networking / Multi-account como próximo bloco. Não houve mudança de cargo, datas ou senioridade.

<a id="registro-de-sessoes"></a>

## Registro de sessões

| Data | Registro preservado | Resultado / continuidade |
|---|---|---|
| 23/09/2026 | Base inicial do CV e entrevistas, trajetória, ferramentas, padrões e preferências | Material inicial F5; não era currículo final |
| 02/10/2026 | Roadmap oficial de 10 blocos e aprofundamento AWS | Substituição da antiga lista de 36 pontos; AWS e Observabilidade já aparecem concluídos nos registros seguintes |
| 05/10/2026 | Fechamentos de Kubernetes, CI/CD e Segurança/IAM; início de Bancos | F2 §§35–38; F4 registra momento intermediário de 4/10 |
| 13/10/2026 | Governança de arquitetura: custos/ROI, segurança, performance, observabilidade, autoridade e escalonamento | Complemento de conteúdo; sem fechar automaticamente o bloco 8 |
| 13/10/2026 | Definição de Senior Cloud Platform Engineer para posicionamento | Cargo histórico não alterado; Staff/Principal permanecem em avaliação |
| 15/10/2026, atualização anterior | Bancos/Backup/DR encerrado; casos e limites adicionados | F1 registra 6/10 — 60%; próximo é Networking/Multi-account |
| 15/10/2026, estrutura de seis arquivos | Criados README, Roadmap, Perfil, Projetos, Ideias e Histórico, além do ZIP | Arquivos continham apenas títulos/modelos; nenhum conteúdo consolidado |
| 15/10/2026, presente consolidação | Comparadas cinco fontes e preenchidos os seis arquivos; ZIP atualizado | Recuperados detalhes que estavam divididos entre versões, preservando originais e identidades dos seis arquivos |

As datas acima registram o que as fontes indicam, sem inferir datas de execução dos projetos. Não há uma transcrição integral de todas as chamadas de voz entre os documentos localizados; o conteúdo consolidado provém dos registros existentes, acrescido da ideia GitHub identificada separadamente como C1.

<a id="decisoes-consolidadas"></a>

## Decisões consolidadas

- Posicionamento: **Senior Cloud Platform Engineer**.
- Cargo histórico atual: **Senior Platform Engineer (SRE / DevOps)**, jan/2025–atual no registro do CV.
- Trilha preferida: IC técnico transversal; sem gestão formal de pessoas.
- Prioridade arquitetural predominante: custo/ROI, seguida da avaliação de segurança, performance, observabilidade e demais requisitos do caso.
- Autoridade técnica para solicitar revisão ou impedir aprovação imediata; decisão hierárquica final em escalonamento permanece com a gestão.
- Head é responsável principal por FinOps e política de backup; participação técnica de Guilherme é descrita sem ampliar sua responsabilidade.
- Revisão atual: **6/10 — 60%**; próximos blocos 6, 8, 9 e 10. Não há novo bloco concluído apenas por reorganizar arquivos.
- O projeto deve aproveitar o material existente e evitar repetição de perguntas respondidas.
- Inglês é o idioma padrão de apresentação; português brasileiro permanece disponível nos documentos equivalentes em `pt-BR/`.

<a id="reconciliacao-entre-versoes"></a>

<details>
<summary><strong>Reconciliação entre versões</strong></summary>

| Divergência | Tratamento adotado | Evidência |
|---|---|---|
| 2/10, 4/10, 5/10 e 6/10 aparecem em registros distintos | Mantido o estado mais recente, 6/10; estados anteriores preservados apenas como histórico | F1 §§29, 33 e 38; F2 §§29, 33 e 35–38; F4 §29 |
| Arquivo datado de 05/10 contém mudanças de 13/10 | Usada a data do conteúdo e a modificação registrada, sem tratar o nome como limite temporal | F2/F3 |
| Detalhes técnicos de Kubernetes foram resumidos em F1 | Recuperados upgrades, requests/limits, logs anteriores, Operators e autoscaling de F2 | F2 §35 |
| CI/CD e Segurança têm resumos e versões aprofundadas | Preservados os aprofundamentos e incorporados ECR/multi-stage/scans descritos em F1 | F1 §§35–36; F2 §§36–37 |
| Título ainda hipotético em trechos antigos | Aplicada decisão explícita de 13/10 para Senior Cloud Platform Engineer; Staff/Principal seguem hipóteses | F2 §§1 e 27; F3 atualização final |
| Bancos em andamento em F2/F3 | Aplicado fechamento de 15/10, com limites de experiência mantidos | F1 §38 |
| Plano de execução “recorrente” em versão anterior | Aplicada descrição mais recente: uso pontual, proposta ao time responsável | F2 §38 versus F1 §38 |
| Trabalhador de extração versus integração/recálculo nos relatos de login | Preservadas as descrições com relação não confirmada; sem contabilizar dois incidentes nem unir detalhes como fato | F1 §§32 e 38 |
| Inglês apontado antigamente como local de retomada | Mantida a preferência, substituído o próximo passo operacional pelo bloco 6 | F1 §25 versus §§29–30 |
| Upload direto descrito como caso concreto de avaliação | Classificado como exemplo, sem afirmar incidente, entrega ou correção implementada | F2 §39 |
| “CQRS” no caso da réplica | Registrado o termo relatado e a evidência de separação de acessos; sem presumir CQRS completo/event sourcing | F1 §38 |
| Upgrade descrito como blue-green | Preservada a analogia, sem atribuir AWS RDS Blue/Green Deployments | F1 §38 |

</details>

<a id="conteudo-validado-documentalmente"></a>

<details>
<summary><strong>Conteúdo validado documentalmente</strong></summary>

“Validado”, neste conjunto, significa conferido contra os registros localizados. As métricas e experiências continuam sendo relatos do usuário, sem comprovação independente.

- Histórico profissional e formação preservados dos documentos de base.
- Posicionamento, preferências, limites de atuação e governança conciliados.
- Fechamentos dos blocos e próximo passo reconciliados.
- Doze registros de projetos/iniciativas e práticas recorrentes organizados; a numeração do catálogo não implica doze entregas independentes ou episódios únicos.
- Resultados numéricos preservados como aproximações ou percentuais relatados, com escopo e limites.

</details>

<a id="questoes-abertas-e-limites"></a>

<details>
<summary><strong>Questões abertas e limites</strong></summary>

- Existem sobreposições de datas registradas em FH_/Beblue e LMS/SPCM. Foram preservadas; não houve inferência de vínculo simultâneo, erro ou correção.
- Aproximações de 18 anos em tecnologia e 12 em desenvolvimento não foram recalculadas a partir do CV incompleto.
- “Atual” nos cargos refere-se ao registro disponível em 15/10/2026.
- A relação entre os dois relatos de worker/login permanece incerta.
- Engine, versões e classes dos casos de banco não foram confirmados.
- Não há PITR comprovado, criação de Multi-AZ ou rotina formal de teste de DR relatados; rollback do upgrade foi documentado, sem teste de retorno informado.
- A iniciativa corporativa de IA tem escopo atribuído, sem conclusão/adoção integral comprovadas.
- Escala atual de times, clusters, contas e usuários e métricas adicionais ainda dependem de evidência.
- Conteúdo não localizado na Library não foi reconstruído como se fosse transcrição de voz.

</details>

<a id="proximo-passo"></a>

## Próximo passo

**Bloco 6 — Networking / Multi-account.** Consultar os pontos existentes no perfil e no roadmap, aprofundar somente lacunas e preservar os seis blocos encerrados. Blocos 8, 9 e 10 continuam pendentes mesmo com material preliminar.

<a id="regras-de-atualizacao"></a>

<details>
<summary><strong>Regras de atualização</strong></summary>

1. README apresenta o projeto; Roadmap controla o estado; Perfil registra competências e trajetória; Projetos preserva os casos; Ideias mantém iniciativas/pendências; Histórico registra fontes e decisões.
2. Para cada nova resposta, atualizar o arquivo temático, registrar decisões relevantes e somente então ajustar o status se houver fechamento.
3. Não repetir a entrevista inteira, transformar ausência em experiência ou ampliar resultado qualitativo para métrica quantitativa.
4. Preservar as fontes originais; a partir da migração para o repositório, alterações ficam nos seis documentos Markdown por idioma e no histórico Git da branch `develop`. O ZIP é uma referência da importação e não precisa ser atualizado.
5. Separar fatos autorrelatados, hipótese de posicionamento, proposta futura e exemplo de avaliação.
6. Atualizar este histórico quando uma evidência mais recente corrigir ou complementar uma afirmação, mantendo os dois idiomas sincronizados.

</details>

<a id="fontes-de-referencia"></a>

<details>
<summary><strong>Fontes de referência</strong></summary>

Identificadores F1–F5 são rótulos editoriais desta consolidação, não novos nomes atribuídos aos arquivos originais. Horários abaixo são UTC conforme metadados.

| Fonte | Arquivo e localização original | Metadados conferidos / papel |
|---|---|---|
| F1 | `/experiencia_profissional_guilherme.md` | 48.700 bytes; versão 5; modificado em 15/10/2026 às 10:49:57 UTC. Estado mais recente, Bancos, casos e limites |
| F2 | `/experiencia_profissional_guilherme_atualizado_2026-10-05.md` | 53.328 bytes; versão 2; modificado em 13/10/2026 às 20:05:58 UTC. Aprofundamentos de 05/10, governança e título de 13/10 |
| F3 | `/Profile/experiencia_profissional_guilherme_atualizado_2026-10-05.md` | 50.937 bytes; modificado em 13/10/2026 às 20:05:33 UTC. Versão intermediária e complemento de arquitetura |
| F4 | `/experiencia_profissional_guilherme_rascunho_2026-10-05.md` | 44.650 bytes; modificado em 05/10/2026 às 11:05:00 UTC. Fechamentos anteriores e estado intermediário |
| F5 | `/experiencia_profissional_guilherme_martins.md` | 14.829 bytes; modificado em 23/09/2026 às 11:34:40 UTC. Base inicial do histórico, ferramentas e preferências |
| F6 | `/CV_Guilherme_Martins_DevOps_PT.pdf` | Duas páginas lidas no visualizador da Library em 15/10/2026; contexto da carreira e início de Senior DevOps em fevereiro/2020 |
| F7 | `/Reuniões Inglês/cv-linkedin.pdf` | Cinco páginas lidas em 15/10/2026; contexto das experiências, início divergente em junho/2019 mantido pendente |
| F8 | `/JD - HE - SRE.pdf` | Duas páginas lidas em 15/10/2026; referência de entrevista Thaloz / HE SRE apenas |
| C1 | Contexto de continuidade fornecido nesta conversa | Ideia previamente solicitada de um portfólio GitHub/“segundo LinkedIn” e existência de repositório de perfil apenas com README. Não é um arquivo encontrado na Library |

Os seis modelos e `profile_estrutura_6_arquivos.zip` estavam em `/Profile`, criados em 15/10/2026 entre 15:32 e 15:33 UTC. Continham a estrutura, sem preenchimento. O ZIP atualizado na consolidação continha exatamente os seis Markdown, com links relativos navegáveis. Ele permanece como retrato da importação; o repositório bilíngue passou a ser a fonte de trabalho.

</details>

<a id="mapa-de-migracao-do-conteudo"></a>

<details>
<summary><strong>Mapa de migração do conteúdo</strong></summary>

| Conteúdo das fontes | Destino principal |
|---|---|
| F1 §§1–9, 13, 16, 21–27 e 31; F2 §§35–37 e 39 | Perfil consolidado; título e continuidade antigos corrigidos conforme atualizações explícitas |
| F1 §§10–12, 14–15, 17–19, 32 e casos do §38; upgrade em F2 §35 | Projetos técnicos |
| F1 §§29–30, 33 e fechamento do §38; fechamentos F2/F4 | Roadmap e Histórico |
| F1 §20 e exemplo de upload F2 §39; ideia GitHub em C1 | Ideias e pendências |
| F1 §28 e métricas do §38; contribuições iniciais F5 | Resultados do perfil e respectivos casos, sem repetir registros como novas entregas |
| F3/F4, comparados com F1/F2; F5 como base inicial | Divergências reconciliadas e informações complementares incorporadas |

</details>

<a id="migracao-para-o-repositorio"></a>

<details>
<summary><strong>15/10/2026 — Migração para o repositório</strong></summary>

**Origem da decisão:** instrução explícita do usuário nesta conversa: utilizar `/home/guilherme/repositorios/pessoal/guihmartins` como fonte da verdade, inclusive para o que for revisado e validado, com estrutura Markdown navegável e substituição do README anterior.

- Importado o conteúdo de `profile_estrutura_6_arquivos.zip`, disponibilizado pelo usuário na pasta do repositório e identificado no chat `arquivos-profile`.
- Preservados integralmente os documentos Roadmap, Perfil consolidado e Projetos técnicos, com adição de navegação comum entre os arquivos.
- Adaptado o README do ZIP para apresentar o repositório como fonte da verdade e descrever o fluxo de atualização na `develop`.
- Atualizada a ideia de portfólio: escolha do repositório e estrutura navegável resolvidas; escopo da apresentação pública e demais decisões permanecem pendentes.
- Adicionado `AGENTS.md` para manter estas regras nas próximas sessões.
- O ZIP local permanece como referência de importação e é ignorado pelo Git para evitar uma cópia paralela dos documentos versionados.

**Efeito sobre a revisão:** nenhum bloco foi reaberto ou concluído. Mantidos **6/10 — 60%** e **Networking / Multi-account** como próximo bloco. Esta migração não constitui nova validação das experiências ou métricas importadas.

Nas próximas revisões, registrar aqui a data, o assunto, a origem da confirmação, os documentos afetados e a mudança de estado, quando houver. Novas confirmações devem atualizar também o documento temático e as pendências correspondentes.

</details>


---

[← Pendências](IDEIAS-E-PENDENCIAS.md) · [Início](README.md) · [Perfil →](PERFIL-CONSOLIDADO.md)

<sub>Base profissional · Atualizada em 15/10/2026 · Branch develop</sub>
