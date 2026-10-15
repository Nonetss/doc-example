# Writing documentation

A **content repository** for the `doc` platform: the guide to writing one. It
explains how to write the pages, the menu, the catalog and the diagrams the
platform publishes, and it uses every one of those features itself, so its
own files are the examples. Copy it to start your own documentation.

It holds only content. The platform, a separate repository, clones it,
validates it and publishes it: a web for people, a schema catalog for your
editor, and `llms.txt` and each page's `llm.txt` for AI agents. Nothing here
is built or run.

## What's inside

| Path | What it holds |
| --- | --- |
| `doc.config.yaml` | The site: its name, the platform contract version and the extra header fields its pages use |
| `menu.yaml` | The sidebar: four groups (Start, Writing, Data, Publishing) and what each shows |
| `docs/` | The guide's pages, in MDX. Every folder is a section with its `index.mdx` |
| `catalogo/<type>/` | The contract itself as data: the `files` of a repository, the `field-kinds`, the `header-fields` and the page `components`. The guide's reference tables are built from it |
| `diagramas/` | The guide's diagrams, each shown in several pages with `<Diagram id="…" />` |
| `skills/doc-writing/SKILL.md` | A skill the platform serves to other agents that write documentation |
| `AGENTS.md`, `.agents/`, `.claude/` | Instructions for the AI agent that writes in this repository |
| `.vscode/settings.json` | Completion and validation for every YAML file, from the platform |

## Contract names vs your names

The platform reads a fixed set of names, written in **Spanish**, and they must
stay exactly as they are: the files and folders (`doc.config.yaml`,
`menu.yaml`, `docs/`, `catalogo/`, `_tipo.yaml`, `diagramas/`), the keys of
each YAML file, the field kinds (`texto`, `ref`, `lista`…), the header every
page has (`titulo`, `descripcion`, `icono`, `orden`, `actualizado`) and
`catalogo:` links. Everything else is yours, in whatever language you write.
The full table is in `docs/repository/index.mdx`.

## Using it as a starting point

1. **Copy this repository** and replace its pages, menu, catalog types and
   diagrams with your own; keep `doc.config.yaml`'s keys and change its values.
2. **Register it on the platform** at `/admin/content`: a name, a slug, and
   either the repository's `https://` URL and branch, or "hosted on the
   platform" to push it to the platform itself.
3. **Point your editor at it.** Install the Red Hat YAML extension
   (`redhat.vscode-yaml`, suggested by `.vscode/extensions.json`) and set
   `yaml.schemaStore.url` in `.vscode/settings.json` to the catalog URL that
   `/admin/content` shows for your repository. Ctrl+Space then suggests every
   key, the values of each enum, the ids each reference accepts, the paths a
   menu entry can name and the icon names. In a multi-folder workspace, put
   that setting in the workspace's settings instead.
4. **Developing against a local platform** (`https://localhost:4321`): the
   extension doesn't trust the local certificate. Add
   `"http.proxyStrictSSL": false` to your editor's **user** settings while you
   do, and remove it afterwards.

The guide itself, once published, explains each step in detail: start with
its "Getting started" page.

## Writing with an AI agent

`AGENTS.md` (imported by `CLAUDE.md`) and the `documentation` skill tell an
agent how this repository is organised and how the guide's pages are written.
`/questions <section>` runs a question round to finish a section: the agent
writes the questions in `questions.md`, someone answers them, and
`/questions` again moves the answers into the pages.

## The one rule

**No secret ever goes in a content repository**: no password, token, API key
or passphrase, anywhere. Pages say which account is used and where its
credentials live, never their value.
