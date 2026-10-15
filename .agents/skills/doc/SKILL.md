---
name: documentation
description: Map and conventions of this documentation content repository. Covers what goes where (doc.config.yaml, docs/ sections and pages, catalogo/ types and entities, skills/ served to other agents), which names are the platform's contract and which are this site's own, the page header and page conventions, MDX without code, the page components and links, catalog types (_tipo.yaml), field kinds and entities, diagrams as YAML blocks, the skills the platform serves to other agents, question rounds (/questions) and how content is validated. Use before writing or changing any page, entity, type, diagram or served skill, before running a question round, and to check where something belongs.
---

# Documentation

This repository is **content only**: pages, structured data and the skills the
platform serves to other agents. The platform (a separate repository) clones
it, validates it against its contract and publishes it. Nothing here is built
or run.

## Mental model

```
documentation repo (this one)          platform
  doc.config.yaml   site config  ──┐
  docs/**.mdx       pages        ──┼──▶  syncs the repo ──▶ web, editor schema catalog,
  catalogo/<type>/  data         ──┤     validates it       search, MCP (agents)
  skills/<name>/    agent skills ──┘
```

- **Two vocabularies.** The **contract** is what the platform's code reads, and
  it is written in Spanish: the keys of `doc.config.yaml` and `_tipo.yaml`
  (`nombre`, `cabecera`, `campos`, `tipo: texto`…), the common page header
  (`titulo`, `descripcion`, `icono`, `orden`, `actualizado`), the entity
  provenance fields (`fuente`, `actualizado`), the `catalogo/` folder, the
  `_tipo.yaml` file and `catalogo:` links. Never translate or rename them:
  the content stops validating. **Everything else is this site's own**, in
  English: type ids, field names, enum values, header fields declared in
  `doc.config.yaml`, folders, file names and every word of prose.
- **The platform knows nothing about the domain.** Machines, services and
  stacks are types this repository declares. A shop would declare products and
  suppliers instead.
- **Data and prose are separate.** Repeated facts with the same shape go to the
  catalog, one file per entity. Explanations go to pages, which cite entities
  instead of copying them.

## Where to look

| Task | Read |
| --- | --- |
| Where a file goes, the sections of `docs/`, naming files and folders, contract words vs site words | `references/layout.md` |
| Writing or changing a page: the header, the page structure of this site, MDX rules, components, links, credentials | `references/pages.md` |
| Declaring a type, adding a field, writing entities, field kinds, YAML traps, citing entities from pages, data from a panel or API | `references/catalog.md` |
| Drawing or changing a diagram | `references/diagrams.md` |
| Writing a skill under `skills/` for agents that use this site | `references/served-skills.md` |
| Running a question round (`/questions`): what to ask, the `questions.md` format, applying answers | `references/question-rounds.md` |

A task that crosses areas (a new service with its page, entity and diagram)
reads every reference it needs.

## Always true

- **No secret ever enters this repository.** No password, token, API key,
  passphrase or private key, in a page, an entity, an example or a comment.
  Write where the credential lives and which account to use ("the `admin`
  account, in the vault as connection `komodo`"), never its value.
- **Declare before use.** An entity field must be declared in its
  `_tipo.yaml`; a header field must be declared under `cabecera` in
  `doc.config.yaml`. Declare it first, then use it.
- **MDX has no code.** Markdown plus the platform's components; never
  `import`, `export` or `{…}` expressions.
- **One entity per file**, under `catalogo/<type>/`. No catalogs elsewhere.
- **Dated, sourced data.** Facts taken from a panel or an API carry their date
  (`actualizado`) and, on entities, their origin (`fuente`). When the panel
  disagrees with the docs, the panel wins: fix the docs.
- **Link, don't repeat.** If another page or an entity already says it, link it.
- **Ids are lowercase**, digits and hyphens for files and folders
  (`new-stack.mdx`), lowercase and underscores for field names
  (`open_questions`). No accents, no spaces.
- **Validate before calling it done** (below).

## Validation

- **In the editor:** `.vscode/settings.json` points `yaml.schemaStore.url` at
  the platform's schema catalog for this repository. It completes and
  validates `doc.config.yaml`, every `_tipo.yaml` and every entity. New types
  and entities appear in the suggestions after you push and the platform syncs.
- **On the platform:** each push is synced (within five minutes, or right away
  from `/admin/content`). Invalid content never replaces valid content: the
  platform keeps serving the last valid version and logs each problem with its
  file and reason.
- Before finishing, check that every YAML you touched validates and that every
  link, `ficha`-kind field and reference points at something that exists.
