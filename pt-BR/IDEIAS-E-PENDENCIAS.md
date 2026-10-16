[English](../IDEAS-AND-PENDING.md) | **Português (Brasil)**

[Início](README.md) · [Perfil](PERFIL-CONSOLIDADO.md) · [Projetos](PROJETOS-TECNICOS.md) · [Revisão](ROADMAP.md) · [Pendências](IDEIAS-E-PENDENCIAS.md) · [Histórico](HISTORICO.md)

---

<sub>04 / PENDÊNCIAS · GUILHERME MARTINS</sub>

# O que falta aprofundar

Um lugar para manter perguntas, iniciativas e decisões abertas sem misturá-las às experiências consolidadas.

**Próxima prioridade:** [Networking / Multi-account](ROADMAP.md#6-networking--multi-account).<br>
**Já decidido:** repositório `guihmartins` como fonte da verdade, trabalho na `develop` e posicionamento **Senior Cloud Platform Engineer**. Inglês como padrão, com a versão completa em português em `pt-BR/`.

[Lacunas de conteúdo](#pendencias-de-conteudo) · [Iniciativa de IA](#padroes-corporativos-para-ia-generativa) · [Portfólio](#portfolio-github--segundo-linkedin) · [Carreira](#posicionamento-profissional)

<a id="pendencias-de-conteudo"></a>

## Pendências de conteúdo

| Tema | O que falta confirmar ou aprofundar | Onde acompanhar |
|---|---|---|
| Networking / Multi-account | Casos de VPC, subnets, CIDR, conectividade, isolamento e escopo pessoal | Roadmap 6 |
| Liderança / documentação | Mais casos de mentoria/influência, adoção e processo de decisões; RFC/ADR só se confirmado | Roadmap 8 |
| Ferramentas e IA | Arquitetura, stack, adoção, manutenção, métricas e estado real de implantação | Roadmap 9 |
| Experiências anteriores | Projetos, Azure, impacto, datas sobrepostas e calibração de senioridade | Roadmap 10 |
| Métricas | Escala, tráfego, custos, MTTR e adoção apenas quando existirem dados | Perfil / Projetos |
| Incidente de autenticação | Relação entre o worker de extração e o de integração/recálculo | P08 / Histórico |
| Bancos | Engine/versões/classes dos casos e unidade/janela das métricas, se recuperáveis | P09–P11 |

As últimas duas linhas são limites documentais opcionais de enriquecimento; não reabrem automaticamente Bancos ou Observabilidade. Não exigir que o usuário produza métricas inexistentes.

<a id="auditoria-library-pendencias"></a>

## Continuidade da auditoria da Library

- **Divergência na Conexia:** F6 informa Senior DevOps a partir de fevereiro/2020; F7 informa junho/2019, sobrepondo o cargo anterior de DevOps. Manter fevereiro/2020–dezembro/2024 até Guilherme confirmar a transição.
- **Treino de entrevista:** F8 é a descrição da vaga Thaloz / HE SRE. Usá-la para preparar exemplos sobre sistemas híbridos .NET Core e WCF/SOAP, entrega com rollback, observabilidade e Azure. Os requisitos da vaga são perguntas de preparação, não evidências de experiência ou certificações de Guilherme.
- **Original ainda não lido:** `Guilherme_Martins_English_Interview_Training.docx` não abriu no visualizador atual da Library. Preservar esse arquivo até conseguir exportá-lo e compará-lo; seu conteúdo não foi presumido nem recuperado.
- **Limite de preservação:** a auditoria comparou conteúdo profissional renderizado; não gerou backup binário integral da Library. Preservar os originais até verificar uma cópia separada. A planilha histórica sem relação com o perfil também não abriu.

A auditoria acrescenta detalhes das fontes sem alterar o estado de revisão **6/10** ou o próximo tópico.

<a id="portfolio-github--segundo-linkedin"></a>

## Portfólio GitHub — segundo LinkedIn

A ideia de organizar o levantamento em documentação Markdown navegável foi implementada em **15/10/2026**, por solicitação do usuário, no repositório existente `guihmartins`, em `/home/guilherme/repositorios/pessoal/guihmartins`.

**Estado:** estrutura navegável adotada como fonte da verdade do Profile, na branch `develop`. O README anterior foi substituído pelo índice dos seis documentos. Conteúdo, revisões, validações e decisões futuras passam a ser mantidos e versionados neste repositório.

A adoção do repositório como base de trabalho não conclui os blocos de revisão nem define o escopo de uma apresentação pública. O ZIP foi usado como origem da importação; os Markdown passam a ser os arquivos de trabalho.

**Decisão de idioma:** inglês como padrão na raiz; os mesmos seis documentos em português brasileiro em `pt-BR/`. Cada página leva à versão equivalente, e alterações de conteúdo devem manter os dois idiomas alinhados.

<a id="decisoes-ainda-abertas"></a>

### Decisões ainda abertas

- Público e escopo da apresentação do portfólio.
- Seleção dos casos e nível de detalhe a publicar.
- Tratamento de informações internas, dados pessoais e identificação de empresas/sistemas antes da apresentação pública final.
- Quando transformar os registros de trabalho em apresentação pública e currículo final.

**Decisões resolvidas:** utilizar o repositório de perfil existente como fonte da verdade e adotar inglês como padrão, com opção em português brasileiro. Origem: instruções explícitas do usuário nesta conversa em 15/10/2026, registradas no [Histórico](HISTORICO.md#estrutura-bilingue-2026-10-15).

<a id="padroes-corporativos-para-ia-generativa"></a>

## Padrões corporativos para IA generativa

Foi atribuída a Guilherme a responsabilidade de ajudar a definir como a empresa utilizará ferramentas de IA generativa.

Escopo relatado:

- definição da arquitetura de uso de IA;
- criação/definição de um **harness corporativo**;
- estabelecimento das ferramentas permitidas;
- definição do que não deve ser utilizado;
- definição de skills/capacidades permitidas;
- padrões de estrutura dos repositórios;
- aplicação dos padrões para desenvolvimento e potencialmente outras áreas, incluindo design;
- criação de documentação;
- criação de exemplos/implementações de referência;
- acompanhamento da aderência aos padrões.

O objetivo é estabelecer regras organizacionais que outras equipes deverão seguir.

Esse projeto é uma evidência importante de atuação técnica transversal com alcance organizacional.

<a id="estado-e-pontos-a-aprofundar"></a>

### Estado e pontos a aprofundar

O registro comprova atribuição de responsabilidade e escopo pretendido. Não esclarece se o harness e os padrões já estão integralmente implementados, quais ferramentas foram aprovadas, quantos times adotaram a solução ou quais resultados foram medidos. Esses pontos pertencem ao bloco 9; não devem ser preenchidos por suposição.

Origem: F1 §20; F5 §10.

<a id="exemplo-de-avaliacao-arquitetural-upload-direto"></a>

<details>
<summary><strong>Exemplo de raciocínio arquitetural · upload direto</strong></summary>

- A proposta de fazer upload diretamente do front-end, sem atravessar cluster, Load Balancer ou API Gateway, pode representar **ganho de performance e economia**.
- Entretanto, Guilherme **barraria** a solução se o arquivo ficasse acessível por URL pública a qualquer pessoa com o link, sem controle adequado de acesso (por exemplo, URL assinada) e sem proteção criptográfica apropriada.
- O exemplo demonstra que otimização isolada de tráfego/infraestrutura não prevalece sobre segurança e conformidade; é preciso avaliar os trade-offs do desenho completo.
- **Nota de precisão:** a conversa não especificou o mecanismo de armazenamento, o tipo de criptografia ausente ou a solução corretiva efetivamente implementada. Não apresentar como incidente ocorrido ou como projeto já entregue.

**Classificação:** exemplo de avaliação e critério de aprovação/reprovação. Não é incidente comprovado nem projeto entregue. A referência a URL assinada preserva o exemplo citado; não estabelece, por si só, um desenho de segurança completo.

Origem: F2 §39; F3 atualização de 13/10/2026. Critérios e autoridade estão no perfil.

</details>

<a id="posicionamento-profissional"></a>

## Posicionamento profissional

- **Decidido em 13/10:** Senior Cloud Platform Engineer para mercado/LinkedIn.
- **Preservado:** Senior Platform Engineer (SRE / DevOps), título histórico do cargo atual no CV.
- **Em avaliação futura:** Staff/Principal na trilha de IC, com análise de escopo, autonomia, impacto e expectativas das empresas-alvo.
- **Preferência registrada:** influência técnica entre times, arquitetura, plataforma, automação e prevenção; sem interesse atual em gestão formal de pessoas.
- **Inglês:** possibilidade de usar as próprias histórias profissionais no treino de entrevistas; não há aqui um plano de estudo aprovado ou agenda criada.

Origem: F1 §§23, 25–27; F2 §§1 e 27; F5 §§12 e 15. A atualização explícita de 13/10 prevalece sobre a antiga hipótese de título ainda indefinido.

<a id="proximas-decisoes"></a>

## Próximas decisões

Continuar pelo bloco 6. Ao concluir o levantamento, decidir formato do currículo/LinkedIn, calibrar posicionamento com as evidências e escolher o escopo da apresentação pública final. O conteúdo de trabalho permanece versionado na `develop` deste repositório.


---

[← Roadmap](ROADMAP.md) · [Início](README.md) · [Histórico →](HISTORICO.md)

<sub>Base profissional · Atualizada em 15/10/2026 · Branch develop</sub>
