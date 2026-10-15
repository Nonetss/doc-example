---
name: homelab
description: How to work with the homelab documented on this platform. Use it before touching any home server, container or backup, or when documenting something new in the homelab.
---

# Homelab

This skill says how to work, not what there is. What there is is always looked up live on the platform, because this copy may be out of date.

## Before touching anything

- Look the service up in the documentation (`search`) and read its page (`read`) before acting: it says where it runs, how it is deployed and what breaks if it goes down.
- Almost everything runs in containers managed by Komodo. Never edit a compose file by hand on the server: change it in Komodo.
- Every service with data has its backup in Duplicati. If you run a new one, create its backup too.

## Credentials

Never ask the user for a password. Use the platform's connections (`connections`, `query`, `act`) and, when a request needs a secret, its reference `{{secret:<name>}}`.

## When documenting

- Every service has its folder in `docs/` with an `index.mdx`, and its entity in `catalogo/services/`.
- Every new stack goes to `catalogo/stacks/`, with the id `<server>-<project>`.
