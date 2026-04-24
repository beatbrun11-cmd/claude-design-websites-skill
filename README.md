# Claude Design Websites — Skill

Optimaler Workflow-Skill für **Claude Design** (Anthropic, Launch April 2026), basierend auf einer NotebookLM-Recherche von 13 Quellen (10 YouTube-Tutorials + 3 Reddit-Diskussionen, alle nach 17.04.2026).

Die Skill stellt sicher, dass der Agent die Anthropic-Defaults aktiv umgeht (Teal Gradient, Serif Font, Container-Soup), Tokens schont (Macro-to-Micro + Tweaks-Panel) und sauber zu Claude Code handoffed.

## Was die Skill macht

- 7-Phasen-Workflow (Kontext-Anker → Design-System → Plan Mode → Macro → Tweaks → Assets → Handoff)
- 5 erprobte Prompt-Templates (Wireframe, Design-System-Mix, Asset-Integration, Makro-Varianten, Tweaks-Forcing)
- Anti-Pattern-Tabelle (9 harte Verbote + Gegenmassnahmen)
- Quality Gates Checkliste vor Claude-Code-Handoff
- Token-Budget-Warnungen (Design-System = 20–25% Weekly-Limit)

## Installation

### Claude Code CLI
```bash
mkdir -p ~/.claude/skills/claude-design-websites
cp SKILL.md ~/.claude/skills/claude-design-websites/SKILL.md
```

### Claude Cowork (Web/Desktop)
1. ZIP packen: `zip -r claude-design-websites.zip SKILL.md`
2. claude.ai → Customize → Skills → "+" → Create skill → Upload ZIP

## Aktivierung

Triggert automatisch bei:
- "bau mir eine Website / Landing Page / Hero Section"
- "erstell mir ein UI / Dashboard / SaaS-Mockup"
- "nutze Claude Design für …"

## Quellen

Vollständige Recherche in NotebookLM. Top-Tutorials:
- Viktor Oddy — CLAUDE DESIGN FULL COURSE (1h)
- UI Collective — Complete Guide
- Nate Herk — 3D Websites Full Tutorial
- Brock Mesarich — Master 95% in 17 Minutes
- Chase AI — The ONLY Guide

## Lizenz

MIT
