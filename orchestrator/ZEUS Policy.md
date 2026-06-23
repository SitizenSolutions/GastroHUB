---
tags: [orchestrator, policy]
created: 2026-06-23
version: "1.0"
---

# ZEUS Orchestrator Policy

> **Quelldatei:** `C:\GastroHUB\orchestrator\ZEUS_POLICY.md`

## 1. Modell-Prioritäten

| # | Modell | Einsatz | max_price |
|---|--------|---------|-----------|
| 1 | `deepseek/deepseek-v4-pro` | Routine | $0.50 |
| 2 | `qwen/qwen3-coder` | >200k Tokens | $0.50 |
| 2b | `glm/glm-5.2` | Fallback | $0.50 |
| 3 | `minimax/minimax-m3` | Multimodal/1M+ | $0.50 |
| 4 | `anthropic/claude-opus-4-8` | Releases | $2.00 |

## 2. Fallback

```
deepseek-v4-pro → qwen3-coder (wenn >200k) → opus-4.8 (nach Freigabe)
```

## 3. Delegations-Template

```yaml
Task:        [Titel]
Ziel:        [konkretes Ergebnis]
Agent:       [Name]
Deadline:    [ISO-8601]
Priority:    [High|Med|Low]
ContextEstimate: [Tokens]
Model:       [auto|deepseek-v4-pro|qwen3-coder|glm-5.2|minimax-m3|opus-4.8]
MaxPriceUsd: [0.50|2.00]
ReturnFormat: [Checklist|JSON|Link|Code]
CacheTTL:    [Sekunden]
```

## 4. ZEUS Check

| Kriterium | Frage |
|-----------|-------|
| Vollständigkeit | Alle Punkte vorhanden? |
| Konsistenz | Widerspruchsfrei? |
| Qualität | Mindestkriterien erfüllt? |
| Risiko | Risiken + Maßnahmen? |

→ **ACCEPT | REVISE | ESCALATE**

## 5. Auto-Policies

- <70% Accept-Rate → GLM-5.2 Audit
- >2× Zielkosten → Modell↓ + Cache↑
- Kritische Releases → Opus-4.8 forced
- >$2.00 → Benutzer-Freigabe

## 6. Logs

- `C:\GastroHUB\orchestrator\logs\delegations.jsonl`
- `C:\GastroHUB\orchestrator\logs\audit.jsonl`