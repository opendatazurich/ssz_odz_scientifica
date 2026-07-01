# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Projekt: SSZ an der Scientifica 2026

Statistik Stadt Zürich (SSZ) nimmt an der Scientifica 2026 teil. Dieses Repository enthält die technische Umsetzung der **OGD-Station** (Open Government Data).

### Kontext Scientifica

- **Datum:** 22.–30. August 2026, städtische Events Mo 24. – Fr 28. August
- **Ort SSZ-Auftritt:** Napfgasse 6, 8001 Zürich (Rundgang durchs Haus)
- **Motto:** «Wie wir Wissen schaffen» — Fokus auf Grundlagen der Wissenschaft, Nachvollziehbarkeit, Transfer in Gesellschaft
- **Format:** Interaktiv, selbstbestimmter Rundgang, 6–8 Stationen à ~10 Min., je 5–10 Besucher*innen gleichzeitig
- **Organisation:** Koordination via Dominique Keller und Ueli Heer (STEZ)

### OGD-Station — Ziel

Besucher*innen erfahren kurz, was OGD ist und was die Stadt Zürich anbietet. Hauptfokus: hands-on zeigen, was man mit OGD machen kann. An 5–10 Laptops können Besucher*innen eigenständig oder angeleitet existierende Anwendungen anschauen, Starter Code ausprobieren oder Datenabfragen via MCP-Servern selber machen.

### OGD-Station — Umsetzungsplan

| Anz. | Typ | Thema | Format | Status |
|------|-----|-------|--------|--------|
| 1 | Präsentation | Was ist OGD und wo finde ich Daten? | PowerPoint auf Endlosschlaufe | Offen |
| 2 | Workstation | Daten auf dem OGD-Katalog suchen | Webseite | Fertig |
| 1 | Workstation | Starter Code ausprobieren | Webseite | Fertig |
| 1 | Workstation | Existierende Anwendungen anschauen | Webseite | Fertig |
| 2 | Workstation | Datenabfragen via MCP-Servern selber machen | Webseite | Fertig |

**Total:** 1 Präsentation + 6 Workstations = 7 Geräte

### Projektstruktur

```
Scientifica/
├── index.html                    ← Startseite / Übersicht aller 4 Workstations (2x2 Grid, viewport-füllend, mit Bild-Platzhaltern)
├── .gitignore                    ← Git-Ignore (Claude-Files, Windows, Editors)
├── CLAUDE.md
├── shared/
│   ├── style.css                 ← Gemeinsames CSS (Design, Navigation, Steps, Kiosk-Overlay)
│   ├── kiosk.js                  ← Auto-Reset nach 3 Min. Inaktivität
│   ├── starterCode.mp4           ← Demo-Video für Starter-Code-Seite
│   ├── startseite_ogd_katalog.png ← Screenshot OGD-Katalog-Startseite (Katalog-Intro)
│   ├── scientifica_wide.jpg      ← Scientifica-Banner (Auge + Logos)
│   ├── OGD_STICKER_final_...png  ← OGD-Logo (Header rechts)
│   ├── eth_Auge1_CMYK_...jpg     ← Scientifica-Auge Original
│   └── eth_Auge1_transparent.png ← Auge mit transparentem Hintergrund (Header links)
├── katalog/
│   └── index.html                ← OGD-Katalog: Einführung, Kategorien, Anleitung (fertig)
├── starter-code/
│   └── index.html                ← Starter Code: Video, Anleitung, Notebook-Inhalt (fertig)
├── mcp-abfragen/
│   └── index.html                ← MCP-Server: Anleitung, Beispiele, Server-Details (fertig)
└── anwendungen/
    └── index.html                ← 6 OGD-Anwendungen als Bildkacheln (fertig)
```

### Shared-Komponenten

Alle Seiten nutzen `shared/style.css` und `shared/kiosk.js`. Jede Seite hat:
- **Navigation** oben: Übersicht / Daten finden / Daten nutzen / Daten abfragen / Daten erleben
- **Header** mit Scientifica-Auge (links, halb abgeschnitten), Titel «Scientifica 2026: Open Government Data» (Mitte, auf allen Seiten identisch), seitenspezifischer Untertitel, OGD-Sticker (rechts)
- **Kiosk-Overlay** nach 3 Min. Inaktivität ("Willkommen! Berühren Sie den Bildschirm...")
- **Footer** einheitlich auf allen Seiten: «Statistik Stadt Zürich — Open Government Data» mit Link zu `stadt-zuerich.ch/opendata`

`shared/style.css` enthält neben den globalen Styles auch gemeinsame Komponenten-Styles:
- `.steps` — Nummerierte Schritte-Listen (`position: absolute` für Counter statt Flex-Layout)
- `.intro`, `.intro-text` — Einführungsabschnitte mit Text + Bild
- `.section-title` — Einheitliche Abschnittsüberschriften (1.4rem, 700)
- `.features` / `.benefits` + `.feature` / `.benefit` — Merkmal-/Vorteil-Boxen
- `.try-cta` — Call-to-Action-Banner (dunkelblau, kann mehrere Buttons nebeneinander enthalten via `.try-cta-buttons`)
- `.info-note` / `.tech-note` — Info-Hinweise am Seitenende
- `pre, code` — `user-select: text` erlaubt Textselektion/Kopieren trotz Kiosk-Modus (`body { user-select: none }`)

### CI/CD-Farben (Stadt Zürich Palette)

- `--blue: #0F05A0` — Züriblau / Mitternachtsblau 70 (Header, CTA, Steps)
- `--accent: #009ee0` — Ähnlich Cyan 50 (#0098C6) (Links, Hover, aktive Nav)
- `--blue-light: #e8e7f6` — Heller Blauton (Chips, Tags, Hintergründe)

### Zielauflösung

Laptops am Event: **1920×1200 bei 150% Skalierung** (effektiv 1280×800 CSS-Pixel). Die Startseite ist darauf optimiert (viewport-füllend, kein Scrollen).

### Katalog-Seite (fertig)

Aufbau:
1. Einführung: Was ist OGD? (mit Screenshot der OGD-Katalog-Startseite `startseite_ogd_katalog.png`, verlinkt auf data.stadt-zuerich.ch, Hover-Effekt)
2. So finden Sie offene Verwaltungsdaten der Stadt Zürich — 3 Schritte (mit Links zu Datensätzen und Kategorien)
3. CTA: Katalog durchsuchen (Link zu data.stadt-zuerich.ch)
4. 4 Merkmal-Boxen (ohne Nutzungseinschränkungen, kostenlos, laufend aktualisiert, ausführliche Beschreibungen)
5. Über 900 Datensätze in vielen Kategorien — 8 Kategorie-Kacheln (4×2 Grid) mit Icons von statistik.stadt-zuerich.ch (Umwelt, Bevölkerung, Bauen/Wohnen, Verwaltung, Basiskarten, Mobilität, Volkswirtschaft, Politik). Icons mit `object-fit: contain` damit sie bei jeder Fensterbreite sichtbar bleiben.
6. Datenformate als verlinkte Tags (je auf `data.stadt-zuerich.ch/dataset?res_format=...`), mit Tooltip (ausgeschriebener Name) und Hover-Effekt. Formate: CSV, JSON, GeoJSON, Parquet, XML, RDF, GPKG, SHP, WFS, WMS.
7. Info-Hinweis mit Link zur OGD-Hauptseite

### Starter-Code-Seite (fertig)

Aufbau:
1. Demo-Video (autoplay, Loop, links gefloated) + Einführungstext rechts
2. 4 Vorteile als Kacheln (kein Setup, sofortiger Einstieg, für alle, reproduzierbar)
3. So funktioniert es — 5 Schritte (unterhalb des Videos): Datensatz öffnen, Ressource auswählen, Renku starten (Python/R), SQL Workbench starten (DuckDB), Loslegen
4. CTA: Jetzt ausprobieren — zwei Optionen nebeneinander:
   - «Beispielauswertungen anzeigen» (Toggle-Button, klappt Beispielblöcke darunter auf)
   - «Datenkatalog öffnen» (Link zu data.stadt-zuerich.ch)
   - Jeweils mit kurzer Beschreibung unter dem Button
5. Beispielauswertungen (aufklappbar via `<details>`, standardmässig zugeklappt):
   - **Luftqualität** — Python/R als Tabs, IDE-ähnliche Blöcke (helles Grau), nummerierte Schritt-Chips, Code mit Syntax-Highlighting in `<pre><code>`
   - **Vornamensstatistik** — gleicher Aufbau, Namen anpassbar
   - **SQL Workbench** — Eigener Block mit shields.io DuckDB-Badge als Link, 5 Schritten (öffnen → Tabellenansicht → Zeile → SQL schreiben → Ctrl+Enter), Tipp-Hinweis, und 2 Beispiel-SQL-Abfragen mit Syntax-Highlighting und Schritt-Chips (kopieren → Ctrl+Enter)
   - Tab-Wechsel via `switchTab()` JS-Funktion (kein Framework)
   - Schritte als horizontale Chips mit farbigen Nummernkreisen:
     - Blau (`var(--blue)`) — Schritt 1: Link öffnen (Renku/SQL Workbench)
     - Grün (`#24b064`, `.renku`) — Schritte in RenkuLab
     - Gelb (`#e6a817`, `.sqlwb`) — Schritte in SQL Workbench
   - Alle Code-Snippets (Python, R, SQL) mit manuellem Syntax-Highlighting (Keywords blau/fett, Strings rot, Zahlen grün, Funktionen braun, Kommentare gedämpftes Grün)
   - Fragestellungen einheitlich gestylt via `.query-question` (1rem, fett, kursiv)
   - Copy-Button auf allen `<pre>`-Blöcken (`.lang-panel pre` und `.example-block pre`)
6. Notebook-Inhalt: Python und R nebeneinander (Karten mit feinem grauem Border, Kategorie-Titel uppercase)
7. Zielgruppen als Chips
8. Technischer Hintergrund (RenkuLab, GitHub-Repo, 2'300+ Notebooks, SQL Workbench/DuckDB)

Quelldaten: `\\szh.loc\ssz\users\sszsim\Bilder\0_some\2026\starter-code-komm\`

### MCP-Abfragen-Seite (fertig)

Aufbau:
1. Einführung in zwei Teilen: «KI + Daten — wie geht das?» (Problem: KI-Agenten können noch nicht auf externe Daten zugreifen) und «Was ist MCP?» (Lösung: offener Standard, MCP-Server lehren KI-Agenten neue Fähigkeiten). Ein `.intro`-Block mit Bild rechts.
2. 4 Vorteile als Kacheln
3. «MCP-Server einrichten» — Kurzanleitung in 4 Schritten, mit Untertitel «In 4 Schritten zum ersten Ergebnis»
4. CTA: Jetzt selber ausprobieren (Link zu claude.ai)
5. «Die MCP-Server im Detail» — 3 Server-Karten mit:
   - Beschreibung mit Hyperlinks zu den jeweiligen Datenquellen (Open-Data-Katalog, Geodaten-Service, Parlamentsinformationen, Zürich Tourismus, OpenERZ, tecdottir, data.stadt-zuerich.ch, opendata.swiss, data.gov, data.europa.eu)
   - Beispielabfragen als Chips direkt in den Karten (Label: «Beispielabfragen — klicken zum Ausprobieren»)
   - Klick auf Chip öffnet `claude.ai/new?q=...` mit unsichtbarem Prefix «Verwende den [server-name] Server: ...» (JS liest Server-Name aus `h3` der Karte)
   - JS-basierte Höhenangleichung: `min-height` auf `.server-card p` und `.example-queries` für einheitliche Ausrichtung
   - Meta-Zeile (Entwicklung, Sprache, Lizenz) und GitHub-Link am Ende jeder Karte

### Anwendungen-Seite (fertig)

6 Kacheln mit Bildern von stadt-zuerich.ch, jeweils als Link zur Detailseite:
1. Hanami Zürich (Kirschblüten-Karte)
2. OGD4All (ETH Zürich — Geodaten in natürlicher Sprache abfragen)
3. Velounfallrisiko-Rechner
4. Equal Street Names
5. Zürich, wer bist Du? (ZHdK/NZZ)
6. Wowoni (Mietpreis-Vergleich)

### Technische Hinweise

- Reine statische HTML/CSS/JS-Seiten, kein Build-System (JS: `switchTab()` für Python/R-Tabs auf Starter-Code, Höhenangleichung + Claude-Deep-Links auf MCP-Seite)
- Bilder der Anwendungen werden direkt von stadt-zuerich.ch (Scene7 CDN) geladen
- Kategorie-Bilder des Katalogs von statistik.stadt-zuerich.ch
- Auge-Bild: weisser Hintergrund wurde via Pillow entfernt (`eth_Auge1_transparent.png`)
- Video: `starterCode.mp4` funktioniert nur über HTTP-Server, nicht via `file:///`
- Lokaler Dev-Server: `python -m http.server 8080 --directory "G:\sszsim\_tmp\Scientifica"`
- Kiosk-Modus am Event: `chrome.exe --kiosk --noerrdialogs "http://localhost:8080"`
- Python (Anaconda) verfügbar unter: `C:\Users\sszsim\AppData\Local\anaconda3\python.exe`

### Sprache

Projektsprache und UI: **Deutsch**. Code, Commits und technische Dokumentation: Englisch oder Deutsch nach Kontext.
