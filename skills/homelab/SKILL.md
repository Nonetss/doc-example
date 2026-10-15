---
name: homelab
description: Cómo trabajar con el homelab documentado en esta plataforma. Úsala antes de tocar cualquier servidor, contenedor o copia de casa, o al documentar algo nuevo del homelab.
---

# Homelab

Esta skill dice cómo trabajar, no qué hay. Lo que hay se consulta siempre en vivo en la plataforma, porque esta copia puede estar desfasada.

## Antes de tocar nada

- Busca el servicio en la documentación (`buscar`) y lee su ficha (`leer`) antes de actuar: dice dónde corre, cómo se despliega y qué pasa si se cae.
- Casi todo corre en contenedores gestionados por Komodo. No toques un compose a mano en el servidor: cámbialo en Komodo.
- Todo servicio con datos tiene su copia en Duplicati. Si levantas uno nuevo, crea también su copia.

## Credenciales

Nunca pidas una contraseña al usuario. Usa las conexiones de la plataforma (`conexiones`, `consultar`, `actuar`) y, si hace falta un secreto en una petición, su referencia `{{secreto:<nombre>}}`.

## Al documentar

- Cada servicio tiene su carpeta en `docs/` con un `index.mdx`, y su entidad en `catalogo/servicios/`.
- Cada stack nuevo va a `catalogo/stacks/`, con el id `<servidor>-<proyecto>`.
