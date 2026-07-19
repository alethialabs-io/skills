# Alethia skills

The PR-reviewed **source of truth** for Alethia's shared Claude Code skills. Edit skills **here**, then
consumers pick them up one of two ways (below). One canonical home, centrally updatable.

## Skills

Under `plugins/alethia/skills/`:

| skill | what | source |
|---|---|---|
| `grilling` / `grill-me` | adversarial one-question-at-a-time interview that sharpens a plan/spec before building | vendored, MIT |
| `research` | quick primary-source cited dig (lighter than the built-in `deep-research`) | vendored, MIT |
| `handoff` | compact, redacted context transfer to another instance/session | vendored, MIT |
| `domain-modeling` · `codebase-design` | deep-module design vocabulary (rich behavior behind simple interfaces) | vendored, MIT |
| `alethia-security-review` | review a change against Alethia's real threat surface (keyless / ReBAC / RLS / BYO sandbox / secrets / `ee/` boundary / runner) | Alethia original |
| `alethia-design` | the Alethia Labs design system (tokens, components, UI kits, brand assets) | Alethia original |
| `alethia-docs` | author/review the `apps/docs` docs to a consistent bar (Diátaxis structure + plain-language style + the Vale prose lint) | Alethia original |

Vendored skills are from [mattpocock/skills](https://github.com/mattpocock/skills) (MIT) — see `NOTICE`.
`wayfinder` is deliberately not here: Alethia's wayfinder is the coordination board (`.claude/COORDINATION.md`
in the app repo).

## Consuming — two modes (a repo picks one)

### 1. Synced into `.claude/skills/` (autonomous-safe — the default for the app)

Auto-discovered by Claude Code as local, un-namespaced skills (`/grill`, `/research`). **No trust prompt**, so
it works for headless/background instances (the coordination-board workers). The consuming repo runs a small
sync step that copies `plugins/alethia/skills/*` into its `.claude/skills/` and commits them (so every worktree
has them with zero setup). Update by re-running the sync. The app uses this mode — see its
`scripts/sync-skills.sh`.

### 2. Plugin marketplace (interactive — autoUpdate)

For interactive humans / other repos that want versioned auto-updates and don't mind the one-time trust prompt.

```
/plugin marketplace add alethialabs-io/skills
/plugin install alethia@alethia
```

Or declare it in a repo's committed `.claude/settings.json` (skills become namespaced `/alethia:grill`):

```json
{
  "extraKnownMarketplaces": {
    "alethia": { "source": { "source": "github", "repo": "alethialabs-io/skills" }, "autoUpdate": true }
  },
  "plugins": [ { "marketplace": "alethia", "plugin": "alethia", "enabled": true } ]
}
```

**Don't enable both in the same repo** — the plugin's namespaced skills and the synced local skills would
double up. The app uses sync only.

## Updating a skill

Edit under `plugins/alethia/skills/`, bump `version` in `plugins/alethia/.claude-plugin/plugin.json`, open a
PR, merge. Plugin consumers get it on next update (autoUpdate or `/plugin marketplace update`); synced
consumers get it when they re-run their sync step.
