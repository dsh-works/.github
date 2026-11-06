# Repository taxonomy

Every `dsh-works` repository carries **at most one** `kind` topic, always prefixed with `dsh-` so
org-wide queries cannot collide with unrelated topics. A repository with none is *unclassified* — see
below. Absence is a state, not a kind.

| Topic | Kind | What the repository contains | Importable as a bundle |
|---|---|---|---|
| `dsh-plugin` | plugin | `package.json` whose `dsh.bundle.patch` declares a bundle patch | yes |
| `dsh-skill` | skill | `SKILL.md` at the root or under `skills/<name>/` | no — link or copy into `~/.dsh/skills` |
| `dsh-process` | process | reference documents and tooling for a workflow, chosen deliberately; no runtime payload | no |
| `dsh-org` | org metadata | the `.github` profile repository | no |

## The manifest decides, topics describe

A repository's kind is derived from its contents, never from its topic or its name:

- **plugin** — `package.json` declares `dsh.bundle.patch`, and the row it inserts mounts the package.
- **skill** — a `SKILL.md` exists at the root or under `skills/`.
- **process** — chosen by a person; never inferred from the absence of the others.
- **org metadata** — the `.github` repository.

**Absence is not a kind.** A repository with no kind topic is *unclassified*: consumers ignore it, and
that is not an error. Kinds are declared, not inferred by exclusion — otherwise every scratch, template
or experiment repository silently becomes a "process" repository and the label stops meaning anything.

**A bundle wins.** A repository that declares a bundle patch and also ships skills is a plugin; the
skills are payload inside the bundle, not a second kind.

A topic that disagrees with the contents is a bug: fix the topic. Any consumer that imports repositories
(viburnum's organisation door, a future indexer) gates on the manifest and uses topics only to group,
filter and label. It handles both failure directions: a repository tagged `dsh-plugin` with no bundle
manifest is an **error row**, never an import; a repository with a bundle but no kind topic is
importable and shown as **untagged**. The name is not evidence either: `dsh-plugin-development` is a
skill repository.

**Archived repositories are out.** A consumer skips any repository whose `archived` flag is true,
whatever its topic says. Archiving is the lifecycle signal; the topic describes what a repository is,
not where it is in its life.

## Applying the taxonomy

- Set one kind topic per repository, chosen deliberately. Do not add topics for the org name or for
  lifecycle state.
- Topics are lowercase `[a-z0-9-]`, at most 20 per repository.
- Topics on private repositories are visible only to members, which is the intended scope.
- If the organisation enables custom properties, `kind` can move to a typed, enforced property; topics
  remain the portable fallback.
- Until a check exists, a topic is a claim. A small org workflow comparing topic to manifest would make
  the rule enforceable, and a consumer's error rows would use the same comparison.

## Current repositories (2026-11-06)

| Repository | Visibility | Kind |
|---|---|---|
| `.github` | public | `dsh-org` |
| `dsh-fren` | private | `dsh-plugin` |
| `dsh-plugin-alerts` | private | `dsh-plugin` |
| `dsh-plugin-development` | public | `dsh-skill` |
| `dsh-plugin-pixelart` | private | `dsh-plugin` |
| `dsh-tb-workflow` | private | `dsh-process` |
| `viburnum` | public | `dsh-plugin` |
