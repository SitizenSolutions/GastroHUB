---
tags: [agents, overview]
created: 2026-06-23
---

# Agent Overview

| Agent | Rolle | Profil | Modell | Skills |
|-------|-------|--------|--------|--------|
| [[ZEUS]] | CEO | default | `deepseek/deepseek-v4-pro` | Orchestration |
| [[HERA]] | CHRO | hera | `minimax/minimax-m3` | 73 Skills |
| [[HADES]] | CIO | hades | `deepseek/deepseek-v4-pro` | Infra/Security |
| [[POSEIDON]] | CTO | poseidon | `deepseek/deepseek-v4-pro` | Tech Strategy |
| [[DEMETER]] | CFO | — | — | Finance |
| [[APOLLO]] | UI/UX | — | — | 6 Design |
| [[HEPHAESTUS]] | Dev | — | — | 6 Dev |
| [[ATHENA]] | PM | athena | `deepseek/deepseek-v4-pro` | PM |

## Modell-Prioritäten

→ [[orchestrator/ZEUS Policy|ZEUS Orchestrator Policy]]

## Startbefehle

```bash
hermes -p hera       # Hera (minimax-m3)
hermes -p hades      # Hades
hermes -p poseidon   # Poseidon
hermes -p athena     # Athena
```