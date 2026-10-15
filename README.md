# Contenido de ejemplo

Un repositorio de documentación de ejemplo (un homelab) para desarrollar la plataforma contra él. El contenido real de cada sitio vive en su propio repositorio con esta misma forma.

| Ruta | Qué hay |
| --- | --- |
| `doc.config.yaml` | Nombre del sitio, versión de la plataforma y los campos extra de la cabecera de las fichas |
| `docs/` | Las fichas MDX. Cada carpeta es una sección del menú y lleva su `index.mdx` |
| `catalogo/<tipo>/` | Los datos estructurados: `_tipo.yaml` es el esquema del tipo y cada otro `.yaml` una entidad, con el nombre del fichero como id |
| `skills/<nombre>/SKILL.md` | Skills que la plataforma sirve a los agentes: cómo trabajar con este sitio |

## Reglas

- **Fichas**: la cabecera lleva siempre `titulo` y `descripcion`, y si hace falta `icono`, `orden` y `actualizado`. Los demás campos se declaran en `cabecera` de `doc.config.yaml`.
- **MDX sin código**: Markdown y los componentes de la plataforma (`<Entidades>`, `<Aviso>`, los bloques `diagrama`). Sin `import`, `export` ni expresiones `{…}`.
- **Enlaces**: a otra ficha con su ruta relativa (`../komodo/index.mdx`); a una entidad con `catalogo:<tipo>/<id>`, y a la lista de un tipo con `catalogo:<tipo>`.
- **Entidades**: solo datos. Si una necesita explicación, apunta a su ficha con un campo `ficha`. Cualquier entidad admite `fuente` (de dónde sale el dato) y `actualizado` (su fecha) sin declararlos.
