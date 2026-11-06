# Repository taxonomy

Every `dsh-works` repository carries exactly one `kind` topic, plus the `dsh-` prefix so org-wide queries cannot collide with unrelated topics.

| Topic | Kind | What the repository contains | Importable as a bundle |
|---|---|---|---|
| `dsh-plugin` | plugin | `package.json` whose `dsh.bundle.patch` declares a bundle patch | yes |
| `dsh-skill` | skill | `skills/<name>/SKILL.md`, optionally with process documents | no — link or copy into `~/.dsh/skills` |
| `dsh-process` | process | reference documents and tooling for a workflow; no runtime payload | no |
| `dsh-org` | org metadata | the `.github` profile repository | no |

## The manifest decides, topics describe

A repository's kind is derived from its contents, never from its topic or its name:

- **plugin** — `package.json` declares `dsh.bundle.patch`, and the row it inserts mounts the package.
- **skill** — a `SKILL.md` exists under `skills/`.
- **process** / **org metadata** — neither of the above.

A topic that disagrees with the contents is a bug: fix the topic. Any consumer that imports repositories (Viburnum's organisation door, a future indexer) gates on the manifest and uses topics only to group, filter, and label. A repository tagged `dsh-plugin` with no bundle is reported as an error row, never imported. The name is not evidence either: `dsh-plugin-development` is a skill repository.

## Applying the taxonomy

- Set one kind topic per repository. Do not add topics for the org name or for lifecycle state; lifecycle is derived from the manifest and repository state.
- Topics are lowercase `[a-z0-9-]`, at most 20 per repository.
- Topics on private repositories are visible only to members, which is the intended scope.
- If the organisation enables custom properties, `kind` can move to a typed, enforced property; topics remain the portable fallback.

## Current repositories (2026-11-06)

| Repository | Visibility | Kind |
|---|---|---|
| `.github` | public | `dsh-org` |
| `dsh-fren` | private | `dsh-plugin` |
| `dsh-plugin-alerts` | private | `dsh-plugin` |
| `dsh-plugin-development` | public | `dsh-skill` |
| `dsh-plugin-pixelart` | private | `dsh-plugin` |
| `dsh-tb-workflow` | private | `dsh-process` |
| `viburnum` | private | `dsh-plugin` |
