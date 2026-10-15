# Layout

```
doc.config.yaml          # the site: name, contract version, extra header fields
docs/
├── index.mdx            # the home page
├── getting-started.mdx  # a page at the top level
└── network/             # a section of the menu
    ├── index.mdx        # its entry page: required in every folder
    └── dns.mdx          # a page of the section
catalogo/
└── machines/            # a type: the folder name is its id
    ├── _tipo.yaml       # its declaration
    └── nas.yaml         # an entity: the file name is its id
skills/
└── homelab/SKILL.md     # a skill the platform serves to other agents
```

## Sections and pages

- **Every folder under `docs/` is a menu section** and needs its `index.mdx`;
  without it the section has no title or entry page.
- **Group by topic, don't nest deeper than needed.** One folder per group
  (`network/`, `containers/`, `backups/`) and inside it one folder per service
  that has several pages (`containers/komodo/`). A single-page service is a
  loose file (`network/dns.mdx`).
- **Order** within a section comes from each page's `orden` header field.

## Naming

- Files and folders: lowercase, digits and hyphens (`new-stack.mdx`,
  `create-backup.mdx`). They are the URL and the path other pages link to.
- Renaming a page means updating every link to it and every `ficha`-kind field
  that names it (`page: backups/duplicati`).
- A page's path is its file path under `docs/` without `.mdx`; a folder's
  `index.mdx` is named by the folder (`containers/komodo`), and `docs/index.mdx`
  has no path.

## Contract words vs site words

The platform reads a fixed set of names. They are Spanish and must be written
exactly as they are:

| Where | Contract names (never change them) |
| --- | --- |
| Folders and files | `catalogo/`, `_tipo.yaml`, `doc.config.yaml`, `docs/`, `skills/`, `index.mdx` |
| `doc.config.yaml` | `nombre`, `descripcion`, `plataforma`, `cabecera` |
| `_tipo.yaml` | `nombre`, `plural`, `icono`, `descripcion`, `etiqueta`, `campos`, `vista`, `columnas` |
| A field declaration | `tipo`, `opcional`, `descripcion`, `valores`, `a` (a reference's target), `de` (a list's element), `campos` (an object's fields) |
| Field kinds | `texto`, `numero`, `entero`, `booleano`, `fecha`, `url`, `email`, `ip`, `ficha`, `enum`, `ref`, `lista`, `objeto` |
| Every page header | `titulo`, `descripcion`, `icono`, `orden`, `actualizado` |
| Every entity | `fuente`, `actualizado` |
| Links | `catalogo:<type>/<id>`, `catalogo:<type>` |

Everything else is this site's choice and is written in English: type ids
(`machines`), field names (`location`, `purpose`), enum values (`physical`),
header fields declared under `cabecera` (`services`, `machines`,
`open_questions`), section folders and file names, and all prose.
