**English** | [Português (Brasil)](pt-BR/IDEIAS-E-PENDENCIAS.md)

[Home](README.md) · [Profile](PROFILE.md) · [Projects](TECHNICAL-PROJECTS.md) · [Review](ROADMAP.md) · [Pending items](IDEAS-AND-PENDING.md) · [History](HISTORY.md)

---

<sub>04 / PENDING ITEMS · GUILHERME MARTINS</sub>

# What still needs exploring

A place for questions, initiatives and open decisions, separate from consolidated experience.

**Next priority:** [Networking / Multi-account](ROADMAP.md#6-networking--multi-account).<br>
**Already decided:** `guihmartins` is the source of truth; work takes place on `develop`; professional positioning is **Senior Cloud Platform Engineer**. English is the default, with the complete Portuguese version in `pt-BR/`.

[Content gaps](#pendencias-de-conteudo) · [AI initiative](#padroes-corporativos-para-ia-generativa) · [Portfolio](#portfolio-github--segundo-linkedin) · [Career](#posicionamento-profissional)

<a id="pendencias-de-conteudo"></a>

## Content gaps

| Topic | What still needs confirmation or detail | Tracking |
|---|---|---|
| Networking / Multi-account | VPC, subnet, CIDR, connectivity and isolation cases; personal responsibilities | Roadmap 6 |
| Leadership / documentation | More mentoring/influence cases, adoption and decision processes; RFC/ADR only if confirmed | Roadmap 8 |
| Tools and AI | Architecture, stack, adoption, maintenance, metrics and actual implementation status | Roadmap 9 |
| Earlier experience | Projects, Azure, impact, overlapping dates and seniority assessment | Roadmap 10 |
| Metrics | Scale, traffic, costs, MTTR and adoption only where data exists | Profile / Projects |
| Authentication incident | Relationship between the extraction worker and the integration/recalculation worker | P08 / History |
| Databases | Engines/versions/classes in the cases and metric units/time windows, if recoverable | P09–P11 |

The last two rows are optional opportunities to enrich the records; they do not automatically reopen Databases or Observability. Do not require the user to produce metrics that do not exist.

<a id="auditoria-library-pendencias"></a>

## Library audit follow-up

- **Conexia date conflict:** F6 lists Senior DevOps from February 2020; F7 lists June 2019, overlapping the earlier DevOps role. Keep February 2020–December 2024 until Guilherme confirms the transition date.
- **Interview practice:** F8 is the Thaloz / HE SRE job description. Use it to prepare examples around hybrid .NET Core and WCF/SOAP systems, delivery with rollback, observability and Azure. Its requirements are interview prompts, not evidence of Guilherme's experience or certifications.
- **Original still unread:** `Guilherme_Martins_English_Interview_Training.docx` could not be opened in the current Library viewer. Retain this file until it can be exported and compared; its contents have not been assumed or recovered.
- **Preservation boundary:** this audit compared rendered professional content, not a complete binary backup of the Library. Retain original files until a separate backup is verified. The unrelated historical spreadsheet also could not be opened.

The audit adds source detail without changing the **6/10** review status or the next topic.

<a id="portfolio-github--segundo-linkedin"></a>

## GitHub portfolio — a second LinkedIn

The idea of organizing the review into navigable Markdown documentation was implemented on **October 15, 2026**, at the user's request, in the existing `guihmartins` repository at `/home/guilherme/repositorios/pessoal/guihmartins`.

**Status:** navigable structure adopted as the Profile source of truth on `develop`. The previous README was replaced by the entry point to the six documents. Content, reviews, confirmations and future decisions are maintained and versioned in this repository.

Using the repository as the working base does not complete review topics or define the final public presentation scope. The ZIP was the import source; Markdown documents are the working files.

**Language decision:** English is the default at the root; the same six documents are available in Brazilian Portuguese under `pt-BR/`. Each page links to its counterpart, and content changes must keep both languages aligned.

<a id="decisoes-ainda-abertas"></a>

### Decisions still open

- Audience and scope of the portfolio presentation.
- Case selection and level of detail to publish.
- Treatment of internal information, personal data and company/system identification before final publication.
- When to turn the working records into the final public presentation and résumé.

**Resolved decisions:** use the existing profile repository as the source of truth, and make English the default with a Brazilian Portuguese option. Source: the user's explicit instructions in this conversation on October 15, 2026, recorded in [History](HISTORY.md#estrutura-bilingue-2026-10-15).

<a id="padroes-corporativos-para-ia-generativa"></a>

## Corporate standards for generative AI

Guilherme was assigned responsibility for helping define how the company will use generative AI tools.

Reported scope:

- Define the architecture for AI use.
- Create/define a **corporate harness**.
- Establish permitted tools.
- Define what should not be used.
- Define permitted skills/capabilities.
- Establish repository structure standards.
- Apply standards to development and potentially other areas, including design.
- Create documentation.
- Create examples/reference implementations.
- Monitor adherence to the standards.

The objective is to establish organizational rules for other teams to follow.

This initiative is an important example of technical work across teams with organizational reach.

<a id="estado-e-pontos-a-aprofundar"></a>

### Status and remaining questions

The record establishes assigned responsibility and intended scope. It does not clarify whether the harness and standards are fully implemented, which tools were approved, how many teams adopted the solution or which results were measured. These points belong to topic 9 and must not be filled in by assumption.

Sources: F1 §20; F5 §10.

<a id="exemplo-de-avaliacao-arquitetural-upload-direto"></a>

<details>
<summary><strong>Architecture reasoning example · direct upload</strong></summary>

- Uploading directly from the frontend, without passing through the cluster, Load Balancer or API Gateway, could provide **performance gains and cost savings**.
- However, Guilherme **would reject** the solution if a file were accessible through a public URL to anyone with the link, without adequate access control (a signed URL was cited as an example) and appropriate cryptographic protection.
- The example shows that isolated traffic/infrastructure optimization does not take precedence over security and compliance; the trade-offs of the complete design must be evaluated.
- **Precision note:** the conversation did not specify the storage mechanism, the type of encryption missing or an implemented corrective solution. Do not present it as an actual incident or a delivered project.

**Classification:** an evaluation example and approval/rejection criterion. It is not a confirmed incident or delivered project. The signed URL reference preserves the example mentioned; it does not by itself establish a complete security design.

Sources: F2 §39; F3 update of October 13, 2026. Criteria and authority are described in the Profile.

</details>

<a id="posicionamento-profissional"></a>

## Professional positioning

- **Decided on October 13:** Senior Cloud Platform Engineer for the market/LinkedIn.
- **Preserved:** Senior Platform Engineer (SRE / DevOps), the historical current job title in the CV.
- **For future assessment:** Staff/Principal on the IC track, based on scope, autonomy, impact and target-company expectations.
- **Recorded preference:** technical influence across teams, architecture, platform, automation and prevention; no current interest in formal people management.
- **English:** potentially use personal professional stories to practice interviews; no approved study plan or schedule exists here.

Sources: F1 §§23, 25–27; F2 §§1 and 27; F5 §§12 and 15. The explicit October 13 update supersedes the earlier hypothesis that the title was still undecided.

<a id="proximas-decisoes"></a>

## Next decisions

Continue with topic 6. After the review, decide the résumé/LinkedIn format, assess positioning against the evidence and choose the final public portfolio scope. Working content remains versioned on this repository's `develop` branch, with English and Portuguese kept in sync.

---

[← Roadmap](ROADMAP.md) · [Home](README.md) · [History →](HISTORY.md)

<sub>Professional knowledge base · Updated October 15, 2026 · Branch develop</sub>
