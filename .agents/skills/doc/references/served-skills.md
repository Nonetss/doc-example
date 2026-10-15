# Served skills (`skills/`)

`skills/<name>/SKILL.md` are skills the platform **serves to other agents**, so
they know how to work with this site from any project. They are not for you
(yours are in `.agents/skills/`).

- **Standard Agent Skills format:** front matter with `name` and
  `description`, instructions below.
- **Thin:** they say *how to work and where to look*, never *what there is*. A
  downloaded skill is a snapshot that goes stale; knowledge is looked up live on
  the site. Good: "look the service up in the documentation before touching
  it". Bad: "Duplicati runs on docker-01".
- **They don't copy procedures:** they point at the pages that explain them.
- **Site-specific only.** What is particular to this site ("everything is
  deployed with Komodo", "every service with data has its Duplicati backup")
  goes here. What is common to every site the platform serves itself; don't
  repeat it.
- **Credentials:** a served skill tells agents to use the platform's
  connections and `{{secret:<name>}}` references, and never to ask a person
  for a password.
