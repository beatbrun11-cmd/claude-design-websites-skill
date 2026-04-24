---
name: design-websites-workflow
description: Optimaler Workflow für Claude Design. Aktiviere diese Skill, wenn der User eine Website, Landing Page, Hero Section, Agentur-Site, SaaS-Dashboard, Marketing-Seite oder ähnliches mit Claude Design bauen will. Stellt sicher, dass der Agent die Anthropic-Defaults aktiv umgeht, Tokens schont (Macro-to-Micro + Tweaks-Panel) und sauber zu Claude Code handoffed.
---

# Claude Design — Agent Instructions

## Aktivierung

Trigger-Signale:
- "bau mir eine Website / Landing Page / Hero Section / Agentur-Seite"
- "erstell mir ein UI / Dashboard / SaaS-Mockup"
- "nutze Claude Design für …"
- jeder Design-Task, der via claude.ai/design gelöst werden soll

## Kern-Regel: NIEMALS Zero-Shot prompten

Ohne visuellen Kontext fällt Claude Design automatisch in seine Defaults zurück und produziert generisches "AI-Slop":
- **Teal Gradient** (blaugrüner Farbverlauf)
- **Serif Font** als Default
- **Blinking Status Dot** (blinkender grüner Punkt)
- **Container-Soup Layout** (verschachtelte Boxen)

Jede Aufgabe sieht sonst aus wie ein austauschbares SaaS-Dashboard ("Anthropic Teal Experience").

## Phasen-Workflow (verbindlich)

### Phase 0 — Kontext-Anker sammeln (vor dem ersten Prompt)

Frage den User **zwingend** nach mindestens einem von:
1. Referenz-Screenshot (Dribbble, Linear, Stripe, etc.)
2. Handgezeichnete Skizze (Claude Design hat integriertes Zeichenwerkzeug)
3. Link zu bestehender Live-Website
4. Lokales Code-Repo / GitHub Repo
5. Design-System Text-Extrakt (via getdesign.md für Marken-Kits)

Ohne Anker → Build stoppen und einfordern.

### Phase 1 — Design-System (einmalig, optional)

- Nur einmal pro Projekt generieren → **kostet 20–25% des Weekly-Limits**
- Quellen: bereinigter Code-Ordner (Tailwind config), kleine Figma-Datei, URL einer Live-Site, oder Marken-Kit-Text
- **Vermeide grosse Figma-Uploads** → Token-Burn + fehlerhafte Typografie-Extraktion

### Phase 2 — Plan Mode erzwingen

Jeder erste Build-Prompt MUSS enden mit:

> *"Bevor du etwas baust, stelle mir Fragen, damit wir auf dem gleichen Stand sind."*

Claude stellt dann 5–15 Rückfragen zu Zielgruppe, Stil, Detailgrad → verhindert teure Fehlversuche.

### Phase 3 — Macro-Varianten

- Fordere **2–3 grundlegend unterschiedliche Layout-Stile** an (z.B. "Brutalist", "Terminal", "Editorial", "Editorial Swiss")
- Lass Claude die Varianten-Namen selbst vorschlagen
- **Entscheide dich für EINE Variante** und arbeite nur damit weiter
- **NIEMALS** mehrere Varianten gleichzeitig mit Feinanpassungen → Token-Killer

### Phase 4 — Micro via Tweaks-Panel (NICHT via Prompt)

Sobald Makro steht, forciere das Tweaks-Panel:

> *"Erhöhe die Anzahl der Tweaks aggressiv"*

Ab jetzt:
- Farben, Typografie, Abstände, Section Rhythm, Tabellendichte → **nur über Schieberegler**
- Keine neuen Prompts für kleine visuelle Änderungen → Tokens werden in Echtzeit gespart, kein Code-Rerender
- Text-Änderungen → Inline-Edit direkt auf Canvas
- Einzel-Element-Änderungen → Zeichenwerkzeug + Selektion ("Kreise ein → Mach diesen Button rot")

### Phase 5 — Assets statt Platzhalter

- Keine Emojis als Icons → echte Icon-Sets (Lucide, Heroicons, Phosphor)
- Keine Lorem-Ipsum → echter User-Copy oder Marken-Copy
- **Hero-Videos**: Looping-MP4 aus Kling 3.0 / Nano Banana (bis ~30 MB Upload-Limit)
- Bilder idealerweise aus Midjourney oder echten Shootings

### Phase 6 — Handoff zu Claude Code (bei ~80–90% Fertigstellung)

**Regel:** Sobald Claude Design visuell zu 80–90% steht, **raus aus Claude Design**. Weitere Arbeit verbrennt Tokens, die in Claude Code (lokal) gratis sind.

Zwei Handoff-Methoden:
1. **Primär:** Share/Export → **"Handoff to Claude Code"** → generiert Prompt → in leeren Ordner in VS Code paste
2. **Fallback bei 404:** **"Download as ZIP"** → entpacken → Ordner in VS Code öffnen → Claude Code starten

In Claude Code:
- Statisches HTML/CSS → **Next.js** Framework überführen
- **GSAP (GreenSock)** integrieren für Scroll-Animationen & 3D-Effekte
- **Mobile Responsiveness** explizit einfordern (Claude Design macht das oft schlecht)
- Optional: `claude.md` mit Systeminstruktionen in den Ordner → Claude als Bauplan lesen lassen
- Test auf `localhost:3000`

### Phase 7 — Deployment

1. `push to private GitHub repo` → Claude Code erledigt Auth + Repo-Creation
2. Vercel Account → GitHub verknüpfen → Repo importieren (Preset "Next.js") → Deploy
3. Custom Domain in Vercel hinterlegen
4. Updates: Git push → Vercel deployed auto

## Prompt-Templates

### Template 1 — Wireframe / Struktur-Prompt
```
Erstelle mir ein Wireframe für [Projekt-Typ].
Großer Video-Hero mit H1-Überschrift und CTA unten links.
Das Projekt heißt [Name].
Sektion 2: [X Features mit Beschreibung]
Sektion 3: [News/Testimonials/Pricing]
Abschluss: full-width CTA + Footer.

Bevor du etwas baust, stelle mir Fragen.
```

### Template 2 — Design-System + fremde Struktur
```
Baue eine [Typ]-Website für [Unternehmen] mit [N] Seiten: [Liste].
Nutze das ausgewählte Design-System für Branding.
Für die Struktur: nutze den angehängten Screenshot als Vorlage.

Bevor du etwas baust, stelle mir Fragen.
```

### Template 3 — Asset-Integration
```
Anhänge:
- Skizze = Hero-Section Idee
- MP4 = Endlosschleife Hintergrund
- 23 Zeilen Markenidentität-Text = Copy-Basis

Hero-Text links neben dem Video.
Schreibe auf Basis der Markenidentität vorerst den gesamten Copy-Text.

Bevor du baust, stelle mir Fragen.
```

### Template 4 — Makro-Varianten
```
Erstelle 2-3 Varianten dieser Landing Page, zwischen denen ich klicken kann,
mit völlig unterschiedlichen Stilen.
Schlage mir zuerst die Varianten-Stile vor, bevor du generierst.
```

### Template 5 — Tweaks-Forcing (nach Makro-Entscheidung)
```
Erhöhe die Anzahl der Tweaks aggressiv.
Ich brauche Schieberegler für: Section Rhythm, Typografie-Scale, Accent-Colors,
Container-Padding, Grid-Density.
```

## Anti-Pattern — harte Verbote

Der Agent MUSS folgende Fehler aktiv verhindern:

| Anti-Pattern | Agent-Gegenmassnahme |
|---|---|
| Zero-Shot Prompt ohne Referenz | Stop → Kontext-Anker einfordern |
| "Mach es clean/modern" (vages Adjektiv) | Ersetze durch harte Referenz: *"Stil wie Linear 2023, hohe Informationsdichte"* |
| Mega-Prompt mit 10 Änderungen | Split in Einzel-Prompts — **eine visuelle Dimension pro Prompt** |
| Anthropic-Defaults zulassen | Explizites Negatives Prompting: *"Keine Teal/Blau-Akzente, keine Serif-Fonts, keine blinkenden Status-Dots, keine verschachtelten Container."* |
| Grosse Figma-Datei hochladen | Alternativ: Tailwind-Config oder Design-System-Text |
| Mehrere Makro-Varianten parallel tweaken | Eine Variante wählen, andere verwerfen |
| Text-Prompts für Farb-/Spacing-Änderungen | Tweaks-Panel erzwingen |
| Ewig in Claude Design weiterarbeiten | Bei 80–90% → Handoff zu Claude Code |
| Emojis als Icons, Lorem-Ipsum als Copy | Echte Icon-Libs, echter User-Copy |

## Quality Gates (vor Handoff)

Der Agent prüft und meldet dem User:
- [ ] Keine der 4 Default-Fehler sichtbar (Teal, Serif, Status-Dot, Container-Soup)?
- [ ] Alle Sektionen haben echten Content (keine Platzhalter)?
- [ ] Hero hat echtes Asset (Video/Bild), nicht Default-Gradient?
- [ ] Design-System konsistent angewendet (Farben, Typografie)?
- [ ] Mobile-Optimierung notiert als Claude-Code-Task?

## Token-Budget-Warnung

Informiere den User bei Projektstart:
- Design-System: **20–25% Weekly-Limit**
- 2–3 Makro-Varianten: **weitere 10–15%**
- Tweaks-Panel-Änderungen: **nahezu kostenlos** (keine Neugenerierung)
- Regel: **Pro Projekt max. 1 Design-System + max. 1 Makro-Runde + Tweaks**

## Automation: Routines (optional, fortgeschritten)

Über Claude Desktop App können "Routines" eingerichtet werden, die:
- Web nach Themen durchsuchen
- Täglich/wöchentlich neue SEO-Unterseiten im vorab definierten Design-Template bauen
- Ideal für Content-Sites mit wiederkehrender Template-Struktur

## Quellen (13 Tutorials + Diskussionen, post 2026-04-17)

Vollständig recherchiert in NotebookLM: `ef0e329e-dfc3-43c8-a330-ba1e96783a93`

Top-Tutorials:
- Viktor Oddy — CLAUDE DESIGN FULL COURSE (1h)
- UI Collective — Complete Guide
- Nate Herk — 3D Websites Full Tutorial
- Brock Mesarich — Master 95% in 17 Minutes
- Chase AI — The ONLY Guide

Praktiker-Perspektiven:
- r/ClaudeAI: "Old designer's perspective"
- r/ClaudeAI: "Most Anthropic product ever" (Defaults-Kritik)
- r/ClaudeAI: "Designer's thoughts on Claude Design"
