# Pages

## The header

Every page starts with its YAML header:

```mdx
---
titulo: DNS
descripcion: AdGuard Home resolves the home names and blocks ads
services: [adguard]
machines: [docker-01]
actualizado: 2026-10-15
open_questions:
  - Does the router hand out AdGuard over DHCP?
---
```

- **Always:** `titulo` (the page name) and `descripcion` (one sentence on what
  the page holds; it shows on cards and in search).
- **When needed:** `icono` (a Lucide icon, mostly on `index.mdx` pages),
  `orden` (an integer from 1: its position in the section) and `actualizado`
  (the YYYY-MM-DD date **of the data**, not of the last edit).
- **This site's fields**, declared under `cabecera` in `doc.config.yaml`:
  `services` and `machines` (the entities the page is about; each entity then
  lists the pages that cite it) and `open_questions` (what is still unknown; a
  question round answers them). A field that is not declared there is an
  error: declare it first or don't use it.

## Page structure on this site

- **Every service** has an `index.mdx` with a summary (what it is, URL, key
  facts) and, when it has several pages, a **"Where do I find…?"** table that
  sends each question to the page that answers it.
- **Every page about a service** uses these sections, in this order:
  - `## What it is`: the general explanation.
  - `## Current setup`: how it is set up here, with concrete facts.
  - `## Notes`: what is odd, breaks the conventions or should be reviewed.
- **A procedure** ("create a backup") is a page of its own with numbered steps,
  so a person and an agent can follow it the same way.
- **Open questions** go in `open_questions`, never loose in the text.
- **No emoji in `##` headings**: they break the heading anchors.
- **One idea per paragraph, straight to the point.** These are handover docs,
  read by someone who was not there when things were set up.

## MDX without code

A page is **Markdown plus the platform's components**, nothing else:

- **Forbidden:** `import`, `export` and `{…}` expressions. The platform turns a
  page into a tree without running anything and rejects them.
- **Props are literal strings:** `filter="category=network"`, never
  `filter={{ category: "network" }}`.
- **Images** are plain Markdown (`![Komodo panel](img/panel.png)`), in an
  `img/` folder next to the page that uses them.

Components:

| Component | What for |
| --- | --- |
| `<Entities type="services" />` | The table of a catalog type. Takes `columns="name,status"`, `filter="field=value"` and `group="field"`. |
| `<Callout type="info">…</Callout>` | A highlighted note. `type` is `info` or `danger`. |
| ` ```diagram ` | A diagram: `references/diagrams.md`. |

The platform does not render them yet, but they are the agreed format: use
them anyway.

## Links

| To link to… | Write |
| --- | --- |
| Another page | Its relative path with `.mdx`: `[Komodo](../containers/komodo/index.mdx)` |
| A section | Its `index.mdx`: `[Backups](../backups/index.mdx)` |
| An entity | `catalogo:<type>/<id>`: `[docker-01](catalogo:machines/docker-01)` |
| A type's list | `catalogo:<type>`: `[Stacks](catalogo:stacks)` |
| An outside site | The full URL |

Linking to an entity from the text also counts as "this page is about it",
like citing it in the header.

## Credentials

Never write a secret's value. Write which account is used and where it lives:
"the `admin` account, in the vault as connection `komodo`". In a procedure that
needs a new secret, give its name in the vault (`duplicati-<service>`), never
its value.

## Before finishing

- Every new page has `titulo` and `descripcion`, and its folder has an
  `index.mdx`.
- Every header field is declared in `doc.config.yaml`, and every cited id exists
  in `catalogo/`.
- Every link points at a file or an entity that exists.
