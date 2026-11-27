# Alethia skills for Claude Code

Claude Code skills from [Alethia Labs](https://alethialabs.io). This repository is generated
from [`.claude/skills/`](https://github.com/alethialabs-io/alethialabs/tree/main/.claude/skills)
in the main repository, so open issues and PRs there.

```
/plugin marketplace add alethialabs-io/skills
/plugin install alethia@alethia
```

| Skill | What it does |
| --- | --- |
| `alethia-design` | Use this skill to generate well-branded interfaces and assets for Alethia Labs and its product Alethia (a multi-cloud Kubernetes control plane), for production or throwaway prototypes/mocks |
| `alethia-docs` | Author or review Alethia's user-facing docs (apps/docs, Fumadocs MDX) to a consistent bar — Diátaxis structure, plain-language prose (STE-informed), canonical terminology, and the Vale lint |
| `alethia-security-review` | Review a change against Alethia's real threat surface — keyless/no-key-leakage, ReBAC authz, Postgres RLS tenant isolation, the untrusted BYO-IaC sandbox + state proxy, secret handling, the open-core ee/ boundary, and the runner's mint-bind/receipt signing |

The general-purpose skills our repo also uses (grilling, research, handoff, domain-modeling,
codebase-design) come from [mattpocock/skills](https://github.com/mattpocock/skills); install
them from there.

Licensed AGPL-3.0-only (see LICENSE), except where a skill's `license:` field says otherwise.
