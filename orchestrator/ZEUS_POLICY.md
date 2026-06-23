# ZEUS Orchestrator Policy v1.0

> **Inkrafttreten:** 2026-06-23  
> **Gültig für:** Alle GastroHUB-Agenten-Delegationen  
> **Orchestrator:** ZEUS (deepseek/deepseek-v4-pro)

---

## 1. Modell-Prioritäten

| Priorität | Modell-ID | Einsatzgebiet | max_price/call |
|-----------|-----------|---------------|----------------|
| **1 (Standard)** | `deepseek/deepseek-v4-pro` | Routine-Tasks, Coding, Analyse | $0.50 |
| **2 (Langkontext)** | `qwen/qwen3-coder` | Research, >200k Tokens | $0.50 |
| **2b (Langkontext Fallback)** | `glm/glm-5.2` | Research, >200k Tokens (wenn Qwen fehlt) | $0.50 |
| **3 (Multimodal)** | `minimax/minimax-m3` | Bilder/Video, 1M+ Kontext | $0.50 |
| **4 (Verifikation)** | `anthropic/claude-opus-4-8` | Kritische Releases, Final Audit | $2.00 |
| **4b (Verifikation Alt)** | `nemetron-3-ultra` | Alternative zu Opus | $2.00 |

## 2. Fallback-Kette

```
deepseek-v4-pro (Standard)
  ↓ Timeout/Fehler + Kontext >200k
qwen3-coder oder glm-5.2
  ↓ Fehlschlag + Task = KRITISCH
opus-4.8 ← NUR NACH KOSTENFREIGABE ($2.00)
```

## 3. Delegations-Template

```yaml
Task:        [Titel]
Ziel:        [konkretes Ergebnis]
Agent:       [Hera|Hades|Poseidon|Demeter|Apollo|Hephaestus|Athena]
Deadline:    [ISO-8601 Timestamp]
Priority:    [High|Med|Low]
ContextEstimate: [Token-Anzahl]
Model:       [auto|deepseek-v4-pro|qwen3-coder|glm-5.2|minimax-m3|opus-4.8]
MaxPriceUsd: [0.50|2.00]
ReturnFormat: [Checklist|JSON|Link|Code]
CacheTTL:    [Sekunden]
```

## 4. ZEUS Check (Ergebnisprüfung)

| Kriterium | Frage |
|-----------|-------|
| **Vollständigkeit** | Alle geforderten Punkte vorhanden? |
| **Konsistenz** | Keine Widersprüche zu bestehenden Artefakten? |
| **Qualität** | Mindestkriterien erfüllt? |
| **Risiko** | Risiken identifiziert + Maßnahmen? |

**Entscheidung:** `ACCEPT` | `REVISE` | `ESCALATE`

## 5. Automatisierte Policies

- **Accept-Rate < 70%:** Automatisches Audit mit GLM 5.2
- **Kosten > 2× Ziel:** Modellqualität senken, Cache-Nutzung erhöhen
- **Kritische Releases:** Zwingende Opus-4.8 Verifikation
- **Kosten > $2.00:** Warten auf explizite Benutzer-Freigabe

## 6. Delegation-Log

Jede Delegation wird geloggt mit:
- `timestamp`, `agent`, `model`, `cost_estimate`, `result_status`, `zeus_decision`

Log-Datei: `C:\GastroHUB\orchestrator\logs\delegations.jsonl`

---

## Agenten-Übersicht

| Agent | Rolle | Profil | Modell | Skills |
|-------|-------|--------|--------|--------|
| Zeus | CEO/Orchestrator | default | deepseek-v4-pro | — |
| Hera | CHRO | hera | **minimax-m3** | 73 |
| Hades | CIO | hades | deepseek-v4-pro | — |
| Poseidon | CTO | poseidon | deepseek-v4-pro | — |
| Demeter | CFO | — | — | — |
| Apollo | UI/UX | — | — | superdesign, sketch, claude-design, excalidraw, popular-web-designs, ui-ux-design |
| Hephaestus | Dev | — | — | architecture-diagram, tdd, systematic-debugging, github-pr, code-review |
| Athena | PM | athena | deepseek-v4-pro | social-media-scheduler, architecture-diagram, plan |