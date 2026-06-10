# Scientifica 2026: Open Government Data — Stadt Zürich

Statistik Stadt Zürich (SSZ) nimmt an der [Scientifica 2026](https://scientifica.ch) teil. Dieses Repository enthält die OGD-Station: eine interaktive Web-Anwendung, an der Besucher*innen Open Government Data der Stadt Zürich entdecken können.

## Kontext

- **Event:** Scientifica 2026, 22.–30. August 2026
- **Ort:** Napfgasse 6, 8001 Zürich
- **Format:** Selbstbestimmter Rundgang, 5–10 Laptops im Kiosk-Modus

## Stationen

| # | Station | Beschreibung |
|---|---------|--------------|
| 1 | OGD-Katalog | Über 900 Datensätze durchsuchen und entdecken |
| 2 | Starter Code | Code-Beispiele in Python und R ausprobieren |
| 3 | MCP-Abfragen | Datenabfragen in natürlicher Sprache via MCP-Server |
| 4 | Anwendungen | Sechs bestehende OGD-Anwendungen erkunden |

## Lokal starten

```bash
python -m http.server 8080
```

Dann im Browser [http://localhost:8080](http://localhost:8080) öffnen.

## Kiosk-Modus (Event)

```bash
chrome.exe --kiosk --noerrdialogs "http://localhost:8080"
```

Nach 3 Minuten Inaktivität erscheint automatisch ein Reset-Overlay.

## Technologie

Rein statische HTML/CSS/JS-Seiten ohne Build-System oder Abhängigkeiten.

## Lizenz

Inhalte und Code: Stadt Zürich, Statistik Stadt Zürich.
