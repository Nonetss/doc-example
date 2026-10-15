# Diagrams

The format is explained in the guide, `docs/diagrams/index.mdx`. This
reference holds how **this site** uses diagrams.

## This site's diagrams

| File | What it shows | Shown in |
| --- | --- | --- |
| `diagramas/pipeline.yaml` | From a push to the reader, the editor and agents | `docs/index.mdx`, `docs/diagrams/index.mdx`, `docs/publishing/index.mdx` |
| `diagramas/repository.yaml` | The files of a repository and how they relate | `docs/index.mdx`, `docs/repository/index.mdx`, `docs/catalog/index.mdx` |

## Writing one

- One file per diagram in `diagramas/`, the file name as its id; shown with
  `<Diagram id="…" />` in a block of its own.
- Contract keys in Spanish (`titulo`, `descripcion`, `direccion`, `nodos`,
  `entidad`, `nombre`, `sub`, `tipo`, `conexiones`, `zonas`); ids, names and
  labels in English.
- **A node that exists in the catalog is an entity** (`{ entidad: files/menu }`),
  so the entity's page lists the diagram.
- **Text with a comma inside a `{ … }` map goes between quotes**:
  `{ nombre: Reader, sub: "the web, for people" }`. Unquoted, the comma splits
  it into two keys and the node is reported.
- Labels say what travels along a connection, in a few words.
- One diagram, one idea; past about a dozen nodes, split it.
- Before reusing a diagram in another page, check it still says what that page
  needs; otherwise write a new one.
