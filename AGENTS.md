# Profile maintenance instructions

## Source of truth

- This repository is the source of truth for Guilherme Martins's professional profile, including content, reviews, confirmations, pending items and history.
- Work on `develop` unless the user explicitly directs otherwise.
- Consult `README.md`, `ROADMAP.md` and relevant pending items before starting a review.
- Conversations, Library files and old ZIPs are source references. Incorporate new confirmations into this repository rather than maintaining parallel primary versions.

## Languages and document mapping

English is the default presentation language at the root. The same six documents are available in Brazilian Portuguese in `pt-BR/`.

| Purpose | English | Brazilian Portuguese |
|---|---|---|
| Entry point and maintenance workflow | `README.md` | `pt-BR/README.md` |
| Review status and next topic | `ROADMAP.md` | `pt-BR/ROADMAP.md` |
| Career history and capabilities | `PROFILE.md` | `pt-BR/PERFIL-CONSOLIDADO.md` |
| Cases, decisions, personal contribution, results and evidence limits | `TECHNICAL-PROJECTS.md` | `pt-BR/PROJETOS-TECNICOS.md` |
| Hypotheses, questions, discrepancies and confirmations needed | `IDEAS-AND-PENDING.md` | `pt-BR/IDEIAS-E-PENDENCIAS.md` |
| Sources, decisions, reviews and confirmations | `HISTORY.md` | `pt-BR/HISTORICO.md` |

- Keep both languages semantically equivalent in the same commit. Do not leave detailed sections untranslated or translate only summaries.
- Reviews and user confirmations may continue in Portuguese. The language used for an interview does not change the default presentation language.
- Every document starts with a language selector linking directly to its counterpart. Within-language navigation stays in that language.
- Keep original explicit anchors stable across both versions. They are link identifiers, not visible prose to translate.
- Use relative links. Portuguese pages reach shared assets and `AGENTS.md` through `../`.
- Keep the English cover in `assets/profile-cover.svg` and the Portuguese cover in `assets/profile-cover-pt-BR.svg`. Preserve the same visual identity.
- Use natural professional English while preserving factual scope. Translate dates unambiguously; retain company names, code identifiers, source filenames, technical product names and source IDs.

## Updates and validation

- Preserve imported content and relevant detail when reorganizing documents.
- Distinguish reported facts, user-confirmed information and hypotheses. Importing or translating an account does not validate it again.
- Do not invent dates, metrics, job titles, seniority, responsibilities, deliveries or evidence.
- Preserve metric limitations and distinguish team outcomes from personal contribution.
- Keep conflicts in Pending Items until confirmed; do not resolve discrepancies silently.
- When a confirmation or decision occurs, record its date, subject, source and affected documents in both History versions.
- Update related documents together. Change a topic's status only when there is evidence of progress or closure.
- Check local links, anchors, counterpart selectors and language parity after reorganizing.
- Preserve earlier history. Correct old decisions through a new explanatory entry.
- Commit coherent changes with messages identifying the topic reviewed. Publish to the remote when requested by the user.
