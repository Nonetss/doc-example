# AGENTS.md

A **documentation content repository** for the `doc` platform, and the example
to copy when starting your own. It holds only content: pages (MDX), structured
data (YAML) and the skills the platform serves to other agents. The platform,
a separate repository, clones it, validates it and publishes it. Nothing here
is built or run.

## About this document

- Agent instructions are this `AGENTS.md` plus the `documentation` skill
  (`.agents/skills/documentation/`). `CLAUDE.md` only imports this file
  (`@AGENTS.md`) so every agent reads the same text: never add instructions to
  `CLAUDE.md`.
- This file holds only what applies to **every** task: what this repository
  is, the map, the hard rules and the pointer to the skill. Convention detail
  lives in the skill's references.
- Skills live in `.agents/skills/<name>/`; `.claude/skills/<name>` is a symlink
  to them (`../../.agents/skills/<name>`). A new skill goes in `.agents/skills/`
  and gets the same symlink.
- New convention detail goes into a reference under
  `.agents/skills/documentation/references/` plus a row in the skill's routing
  table, not into a new skill.
- A change to a convention updates the file that states it, in the same commit.

## Map

| Path | What it holds |
| --- | --- |
| `doc.config.yaml` | The site: name, platform contract version, extra page header fields |
| `docs/` | The pages (`.mdx`). Every folder is a menu section with its `index.mdx` |
| `catalogo/<type>/_tipo.yaml` | The declaration of a data type |
| `catalogo/<type>/<id>.yaml` | One entity: the file name is its id |
| `skills/<name>/SKILL.md` | Skills the platform **serves to other agents** to work with this site |
| `.agents/skills/documentation/` | The skill for **you**, the agent writing here |
| `.claude/commands/questions.md` | `/questions`: question rounds to finish documenting a section |
| `.vscode/settings.json` | The platform's schema catalog, for completion in the editor |

Details and conventions: the `documentation` skill.

## Project skill

Before writing or changing anything, load the `documentation` skill (Skill
tool in Claude Code, or read `.agents/skills/documentation/SKILL.md`). Its
`SKILL.md` holds the mental model (contract names vs this site's names), the
rules that always apply and a routing table to the reference for the task:
layout, pages, catalog, diagrams, served skills and question rounds. Read only
the references the task needs; a task crossing areas reads several.

## Hard rules

### Never write a secret

No password, token, API key, passphrase or private key enters this repository:
not in a page, an entity, an example or a comment. A content repository is
cloned onto servers and read by agents; whatever goes in stops being secret.

- Document **where** the credential is and **which account** to use ("the
  `admin` account, in the vault as connection `komodo`"), never its value.
- If someone gives you a secret to document something, use it only for the
  task and never copy it into a file.
- If you find one already written, tell the user instead of carrying on.

### Don't rename the contract

The platform reads a fixed set of names, written in Spanish: `catalogo/`,
`_tipo.yaml`, the keys of `doc.config.yaml` and `_tipo.yaml`, the field kinds,
the common page header (`titulo`, `descripcion`, `icono`, `orden`,
`actualizado`), `fuente` and `catalogo:` links. Translating them breaks
validation. Everything else (type ids, field names, values, folders, prose) is
this site's own and is written in English. The full table is in the skill,
`references/layout.md`.

### Declare before use

The platform knows nothing about the domain: types and their fields are
declared here. Never add an entity field its `_tipo.yaml` does not declare, or
a page header field `doc.config.yaml` does not declare under `cabecera`.

### Pages have no code

Markdown and the platform's components only. Never `import`, `export` or
`{…}` expressions: the platform rejects them.

### One entity per file

Never put several entities in one YAML or keep catalogs outside
`catalogo/<type>/`. Structured data goes to the catalog; explanations, to a
page.

## Validation

- The editor validates every YAML file through the platform's schema catalog
  (`yaml.schemaStore.url` in `.vscode/settings.json`, which needs the Red Hat
  YAML extension).
- The platform validates each push when it syncs (within five minutes, or right
  away from `/admin/content`). Invalid content never replaces valid content; the
  problems are logged with their file and reason.
- Before calling something done: every YAML you touched validates, and every
  link, `ficha` field and reference points at something that exists.

## Commits

Only when the user asks. One sentence saying what changes and why, following
the existing history. Never credit an AI tool: no `Co-Authored-By`, no
"Generated with…".
