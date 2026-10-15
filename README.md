# Example documentation repository

An example **content repository** for the `doc` platform: the documentation of
a small homelab (a Proxmox host, a Docker VM managed by Komodo, a NAS with
Duplicati backups and a VPS running Pangolin). Copy it to start documenting
your own systems.

It holds only content. The platform, a separate repository, clones it,
validates it and publishes it: a web for people, a schema catalog for your
editor and, later, search and an MCP for AI agents. Nothing here is built or
run.

## What's inside

| Path | What it holds |
| --- | --- |
| `doc.config.yaml` | The site: its name, the platform contract version, and the extra header fields its pages use |
| `docs/` | The pages, in MDX. Every folder is a section of the menu with its `index.mdx` |
| `catalogo/<type>/_tipo.yaml` | The declaration of a data type: its fields, their kinds and how its table looks |
| `catalogo/<type>/<id>.yaml` | One entity of that type; the file name is its id |
| `skills/<name>/SKILL.md` | Skills the platform serves to other agents, so they know how to work with this site |
| `AGENTS.md`, `.agents/`, `.claude/` | Instructions for the AI agent that writes in this repository |
| `.vscode/settings.json` | Completion and validation for every YAML file, from the platform |

The platform knows nothing about the domain. This example declares
`machines`, `services`, `stacks` and `locations`; a shop would declare
`products` and `suppliers` instead.

## Contract names vs your names

The platform reads a fixed set of names, written in **Spanish**, and they must
stay exactly as they are: the `catalogo/` folder and `_tipo.yaml` files, the
keys of `doc.config.yaml` (`nombre`, `descripcion`, `plataforma`, `cabecera`)
and of `_tipo.yaml` (`nombre`, `plural`, `icono`, `descripcion`, `etiqueta`,
`campos`, `vista`, `columnas`), the field kinds (`texto`, `fecha`, `ref`,
`lista`…), the header every page has (`titulo`, `descripcion`, `icono`,
`orden`, `actualizado`), the provenance fields of every entity (`fuente`,
`actualizado`) and `catalogo:` links.

Everything else is yours, in whatever language you write: type ids, field
names, enum values, header fields you declare, folders, file names and every
word of the pages. The full table is in
`.agents/skills/documentation/references/layout.md`.

## Using it as a starting point

1. **Copy this repository** into your own git server and replace the homelab
   with your systems: the types under `catalogo/`, the pages under `docs/`,
   the site name in `doc.config.yaml` and the served skill under `skills/`.
2. **Register it on the platform** at `/admin/content`: a name, a slug, the
   repository's `https://` URL (with credentials in the URL if it is private)
   and the branch. The platform syncs it every five minutes, or right away
   from that page.
3. **Point your editor at it.** Install the Red Hat YAML extension
   (`redhat.vscode-yaml`, suggested by `.vscode/extensions.json`) and set
   `yaml.schemaStore.url` in `.vscode/settings.json` to the catalog URL that
   `/admin/content` shows for your repository. Ctrl+Space then suggests the
   fields of each type, the values of each enum and the ids each reference
   accepts. In a multi-folder workspace, put that setting in the workspace's
   settings instead: the extension ignores it in a folder's `.vscode/`.
4. **Developing against a local platform** (`https://localhost:4321`): the
   extension doesn't trust the local certificate. Add
   `"http.proxyStrictSSL": false` to your editor's **user** settings while you
   do, and remove it afterwards: it turns off certificate checks for every
   extension.

## Writing with an AI agent

`AGENTS.md` (imported by `CLAUDE.md`) and the `documentation` skill tell an
agent how this repository is organised: where each thing goes, how a page and
an entity are written, how diagrams are declared, and the rules that never
bend. `/questions <section>` runs a question round to finish documenting a
section: the agent writes the questions in `questions.md`, someone answers
them, and `/questions` again moves the answers into the pages.

## The one rule

**No secret ever goes in this repository**: no password, token, API key or
passphrase, anywhere. Pages say which account is used and where its
credentials live, never their value. A content repository is cloned onto
servers and read by agents; whatever goes in stops being secret.
