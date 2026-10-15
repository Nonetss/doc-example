# Catalog

The catalog holds the **structured data**: machines, services, stacks,
locations… Each type is a folder with its declaration, and each entity is one
file.

## Before creating anything

1. **Look for an existing type** in `catalogo/`. Create a new one only when no
   current type fits.
2. **Data or explanation?** The catalog is for facts that repeat with the same
   shape (IP, location, ports). Explanations go to a page, and the entity
   points at it with its `page` field.

## A type: `_tipo.yaml`

```yaml
nombre: Machine                # singular
plural: Machines
icono: server                  # a Lucide icon
descripcion: Physical servers, virtual machines and VPS. The id is the hostname in lowercase

etiqueta: name                 # the field shown as the entity's name; the id when missing

campos:
  name:
    tipo: texto
    opcional: true
    descripcion: Only when it is written differently from the id (PVE-01)
  ip:
    tipo: ip
  location:
    tipo: ref
    a: locations
  kind:
    tipo: enum
    valores: [physical, vm, vps]

vista:
  columnas: [name, ip, kind, location]   # the type's table
```

- **The type id** is its folder name: lowercase, digits and hyphens, plural
  (`machines`, `locations`).
- **Field names**: lowercase letters, digits and underscores, starting with a
  letter (`public_ip`).
- **`descripcion` on every field that is not obvious.** The editor shows it as
  help and agents read it: it is the only explanation the field gets.
- **`etiqueta`** and every column in `vista.columnas` must be declared fields;
  columns also accept `id`, `fuente` and `actualizado`.
- **`fuente` and `actualizado` are never declared**: every entity accepts them.

### Field kinds

| `tipo` | Value | Extra |
| --- | --- | --- |
| `texto` | One line of text | |
| `numero` / `entero` | A number / an integer | |
| `booleano` | `true` or `false` | |
| `fecha` | `YYYY-MM-DD` | |
| `url` / `email` / `ip` | In that format (IPv4 or IPv6) | |
| `ficha` | The path of a page under `docs/`, without `.mdx` (`containers/komodo`) | |
| `enum` | One of the values | `valores: [a, b]` |
| `ref` | The id of an entity of another type | `a: <type>` |
| `lista` | Several values | `de: { tipo: … }` |
| `objeto` | A group of named fields | `campos: { … }` |

Every kind takes `opcional: true` (required by default) and `descripcion`. They
nest: a list of objects holding lists is valid.

```yaml
containers:
  tipo: lista
  de:
    tipo: objeto
    campos:
      name: { tipo: texto }
      ports:
        tipo: lista
        de: { tipo: texto }
        opcional: true
        descripcion: Published:internal (8080:80)
```

## An entity: `<id>.yaml`

```yaml
# catalogo/machines/nas.yaml → id: nas
ip: 192.168.1.30
location: home
kind: physical
os: TrueNAS SCALE 25.10
purpose: Storage, and the target of the Duplicati backups
page: backups/duplicati
fuente: manual
actualizado: 2026-10-15
```

- **The id is the file name**: lowercase, digits and hyphens. Extension `.yaml`,
  never `.yml`. A file starting with `_` is not an entity.
- **Only the fields its `_tipo.yaml` declares.** Missing one? Add it to the
  type first.
- **Required fields can't be missing**, and a `ref` must be the id of an entity
  that exists (`location: home` needs `catalogo/locations/home.yaml`).
- **Provenance:** `fuente` (where the data comes from: `manual`, or the
  connection it was read from, such as `komodo`) and `actualizado` (the date of
  the data). Set them whenever data comes from a panel or an API.
- **No secret** in an entity, not even "for now".

### YAML traps

- **Text containing `: ` must be quoted:** `purpose: "The way in: Pangolin"`.
  Unquoted, it is invalid YAML.
- **So must text starting with `[`, `{`, `*`, `&`, `!`, `%` or `@`**, and text
  that reads as `yes`, `no`, `on`, `off`, `null` or a number.
- **Dates** are always `YYYY-MM-DD` (`2026-10-15`).
- **Ports with `/`** (`53:53/udp`) are quoted.

## Citing entities from pages

- **In the header**, with the fields `doc.config.yaml` declares under
  `cabecera` (`machines: [nas]`). To cite a type that has no header field yet,
  declare one there (`tipo: lista`, `de: { tipo: ref, a: <type> }`).
- **In the text**, with a `catalogo:<type>/<id>` link.

Either way, the entity lists the pages that talk about it.

## Data from a panel or an API

- Copy it into entities with `fuente` and `actualizado`, and give the date of
  the lookup in the page that explains it too.
- If it disagrees with the docs, the panel wins: fix the entity.
- Big lists (every container on a server) are still one entity per file, never
  one YAML holding everything.

## Before finishing

- Every YAML validates in the editor (completion marks it red otherwise).
- Every `ref` and every `ficha`-kind field points at something that exists.
- After changing a `_tipo.yaml`, the existing entities still validate (a new
  required field has to be filled in on every one of them).
