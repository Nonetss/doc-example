# Diagrams

A diagram is **declared**, not drawn: say which boxes exist, how they connect
and how they group, and the platform lays them out, with edges that never
cross a box. No coordinates, no hand-made SVG, no text art in a code block.

## Where it goes

Inside the page that explains it, in a ` ```diagram ` block:

````mdx
## How it all fits together

```diagram
direction: right
nodes:
  srv: { name: /srv, sub: the stacks' volumes, kind: input }
  duplicati: { entity: services/duplicati }
  nas: { entity: machines/nas }
edges:
  - srv -> duplicati: reads (read-only)
  - duplicati -> nas: encrypted backup every night
```
````

The usual place is a `## How it all fits together` section in the service's
`index.mdx`.

## The parts

### `direction`

`right` (left to right) or `down` (top to bottom). Follow the flow: a chain of
steps goes right; a hierarchy goes down.

### `nodes`

Each node has an id (the key, lowercase) and is one of:

- **A catalog entity:** `{ entity: <type>/<id> }`. It takes its name, icon and
  link from the entity. Use it whenever the node exists in `catalogo/`.
- **A free box:** `{ name: Periphery, sub: agent on every server }`. `sub` is a
  small line under the name.
- **Just a name:** `runner: Runner`.

`kind` (optional) changes the look: `input` where the flow starts, `store` for
data (disks, registries, databases).

### `edges`

A list of `from -> to: label`, using node ids:

```yaml
edges:
  - gitea -> runner: starts the workflow
  - runner -> registry: pushes the image
```

The label says **what travels** along the edge, in a few words ("encrypted
backup every night", not "connection").

### `zones`

Group nodes in a titled box: where things are (home, VPS, outside) or which
network they belong to.

```yaml
zones:
  outside:
    title: From outside
    nodes: [vps]
  home:
    title: Home
    nodes: [docker, nas, pve]
```

## Guidelines

- **One diagram, one idea.** Past about a dozen nodes, split it or leave the
  detail to each service's page.
- **Only the connections that matter** to understand the page; the rest goes in
  the text.
- **Node ids are local to the diagram**: short and readable (`nas`, not
  `node3`).
- **Nothing sensitive** in labels or subtitles.
- Every diagram will be interactive (highlight on hover, trace the path from a
  node, see each box's connections) with no extra work.

The platform does not render diagrams yet, but this is the agreed format:
write them this way.
