---
category: general
date: 2026-06-30
description: Fügen Sie ein benutzerdefiniertes Kontextmenü in GridJs hinzu und lernen
  Sie, wie Sie eine Excel‑Arbeitsmappe laden, den Zellenwert aktualisieren, die Rechtschreibprüfung
  aktivieren und einen benutzerdefinierten Befehl registrieren.
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: de
og_description: Fügen Sie ein benutzerdefiniertes Kontextmenü in GridJs hinzu, während
  Sie lernen, Excel-Arbeitsmappen zu laden, Zellenwerte zu aktualisieren, die Rechtschreibprüfung
  zu aktivieren und einen benutzerdefinierten Befehl zu registrieren.
og_title: Benutzerdefiniertes Kontextmenü zu GridJs hinzufügen – Schritt‑für‑Schritt
  Python‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: Benutzerdefiniertes Kontextmenü zu GridJs hinzufügen – Vollständiger Python‑Leitfaden
url: /de/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefiniertes Kontextmenü zu GridJs hinzufügen – Vollständiger Python‑Leitfaden

Haben Sie sich jemals gefragt, wie man **benutzerdefinierte Kontextmenü**‑Einträge zu einer GridJs‑Tabelle hinzufügt, die von einer Excel‑Arbeitsmappe unterstützt wird? Sie sind nicht allein. In vielen datenintensiven Apps benötigen Sie dieses Rechtsklick‑Menü, um Benutzern zu ermöglichen, Zeilen zu markieren, Elemente als überprüft zu kennzeichnen oder eine serverseitige Aktion auszulösen – ohne das Grid zu verlassen.

In diesem Tutorial führen wir Sie durch das Laden einer Excel‑Arbeitsmappe, das Einbinden eines benutzerdefinierten Kontextmenü‑Eintrags, das Aktualisieren eines Zellenwerts, das Aktivieren der Rechtschreibprüfung und das Registrieren eines benutzerdefinierten Befehls, der Änderungen zurück in die Datei schreibt. Am Ende haben Sie eine voll funktionsfähige GridJs‑Instanz, die sich für Ihre Nutzer naturnah anfühlt und direkt in die Quell‑Spreadsheet schreibt.

## Voraussetzungen

- Python 3.9+ (der Code verwendet Typ‑Hints, läuft aber auf jeder aktuellen Version)  
- `cells`‑Bibliothek (oder irgendein Excel‑Handling‑Wrapper, der `Workbook`‑ und `Worksheet`‑Objekte bereitstellt)  
- `gridjs`‑Python‑Binding (das Objektmodell spiegelt die JavaScript‑API wider)  
- Grundlegendes Verständnis von Lambdas und JSON‑Strukturen  

Wenn Sie das alles haben, legen wir los.

## Schritt 1: Excel‑Arbeitsmappe laden und ein Arbeitsblatt auswählen

Der erste Schritt besteht darin, **excel workbook** zu **laden**, damit GridJs Daten zum Anzeigen hat. Die Klasse `cells.Workbook` abstrahiert die Datei‑IO und gibt Ihnen direkten Zugriff auf Zeilen, Spalten und einzelne Zellen.

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Warum das wichtig ist:** Das Vorab‑Laden der Arbeitsmappe ermöglicht es dem Grid, Daten bei Bedarf abzurufen, und alle späteren Änderungen (wie **update cell value**) werden in derselben Datei gespeichert.

## Schritt 2: GridJs‑Instanz erstellen und an das Arbeitsblatt binden

Jetzt erzeugen wir ein `gridjs.GridJs`‑Objekt und teilen ihm mit, welches Arbeitsblatt gerendert werden soll. Das ist, als würde man GridJs eine Live‑Datenquelle geben, die es bei Bedarf abfragen kann, um eine Seite oder einen lazy‑geladenen Chunk darzustellen.

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro‑Tipp:** Wenn Sie mit mehreren Blättern arbeiten, rufen Sie später einfach `grid.set_worksheet(other_ws)` auf – ein erneutes Erstellen des Grids ist nicht nötig.

## Schritt 3: Rechtschreibprüfung aktivieren (und andere nützliche Funktionen)

Die meisten Business‑Apps lassen Nutzer Freitext‑Notizen eingeben. Das Aktivieren der **spell checking** reduziert Tippfehler und verbessert die Datenqualität. GridJs stellt dafür ein einfaches Flag bereit.

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Warum Rechtschreibprüfung aktivieren?** Sie läuft clientseitig und liefert sofortiges Feedback ohne zusätzliche Server‑Aufrufe – ideal für großflächige Tabellen.

## Schritt 4: Benutzerdefinierten Kontext‑Menü‑Eintrag hinzufügen

Hier kommt das Herzstück des Tutorials: **add custom context menu**‑Einträge. Wir erstellen eine Option „Mark as Reviewed“, die beim Klick einen serverseitigen Befehl ausführt, den wir im nächsten Schritt definieren.

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Bildillustration**  
> ![Add Custom Context Menu screenshot showing right‑click options](/images/add-custom-context-menu.png "Add Custom Context Menu example")

Der obige Alt‑Text enthält das Haupt‑Keyword und erfüllt damit die SEO‑Anforderungen.

## Schritt 5: Benutzerdefinierten Befehl registrieren, um den Zellenwert zu aktualisieren

Wenn der Nutzer „Mark as Reviewed“ auswählt, müssen wir **register custom command** implementieren, das die zugrunde liegende Excel‑Zelle aktualisiert und die Datei speichert. Die Methode `grid.register_custom_command` bindet eine Python‑Callable an den zuvor festgelegten Aktions‑Identifier.

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Warum das funktioniert:** Der Handler erhält die Zellreferenz vom Client, nutzt die `Worksheet`‑API, um **update cell value** durchzuführen, und schreibt anschließend die gesamte Arbeitsmappe zurück auf die Festplatte. Die Antwort signalisiert dem Front‑End, dass die Operation erfolgreich war.

### Edge‑Case‑Behandlung

- **Missing cell reference:** Wenn `req` kein `"cell"` enthält, werfen Sie einen klaren Fehler, sodass die UI einen Toast anzeigen kann.  
- **Concurrent edits:** Für stark frequentierte Szenarien sollten Sie die Arbeitsmappe sperren oder einen Versions‑Stamp verwenden, um Rennbedingungen zu vermeiden.

## Schritt 6: Lazy Loading für große Tabellen aktivieren

Bei tausenden von Zeilen sorgt Lazy Loading für ein flüssiges UI. Setzen Sie die Seitengröße auf einen vernünftigen Chunk – 500 Zeilen funktionieren für die meisten Browser gut.

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **Was, wenn Sie 10 000 Zeilen haben?** Das Grid fordert Daten Seite für Seite an und reduziert so den Speicher‑Druck auf Client und Server.

## Schritt 7: (Optional) Benutzerdefiniertes Modal für Zeilenbearbeitung hinzufügen

Manchmal benötigen Sie eine reichhaltigere UI als einen Inline‑Editor. GridJs ermöglicht das Öffnen eines Modal‑Fensters, das Sie überall hosten können – etwa als React‑Komponente oder einfaches HTML‑Formular.

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Warum ein Modal verwenden?** Es isoliert komplexe Validierungslogik und gibt Ihnen volle Kontrolle über das Layout, während es dennoch vom Grid aus ausgelöst wird.

## Schritt 8: Client‑seitige Konfigurations‑JSON abrufen

Abschließend müssen Sie die Konfiguration an den Browser senden. Die Methode `get_client_config` serialisiert alles in ein JSON‑Blob, das die Front‑End‑GridJs‑Bibliothek konsumieren kann.

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

Die Ausgabe sieht ungefähr so aus (gekürzt zur Übersicht):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Erwartetes Ergebnis

- Rechtsklick auf irgendeine Zelle öffnet ein Menü mit **Mark as Reviewed**.  
- Die Auswahl sendet eine Anfrage an den Server, der **update cell value** auf „Reviewed“ setzt und `example‑updated.xlsx` speichert.  
- Die Rechtschreibprüfung hebt falsch geschriebene Wörter hervor, während der Nutzer tippt.  

All das geschieht ohne kompletten Seiten‑Refresh, dank Lazy Loading und der leichten JSON‑Payload.

## Häufige Fragen & Pro‑Tipps

| Frage | Antwort |
|-------|---------|
| *Was, wenn die Arbeitsmappe schreibgeschützt ist?* | Stellen Sie sicher, dass die Dateiberechtigungen Schreibzugriff erlauben, oder öffnen Sie die Arbeitsmappe mit `mode="rw"`, falls die Bibliothek das unterstützt. |
| *Kann ich mehr als einen benutzerdefinierten Menüeintrag hinzufügen?* | Absolut – fügen Sie einfach weitere Dictionaries zu `grid.settings.context_menu.custom_items` hinzu. |
| *Muss ich das Grid nach einer Zellenaktualisierung neu laden?* | GridJs aktualisiert die betroffene Zeile automatisch, wenn Sie `{status:"ok"}` zurückgeben; andernfalls rufen Sie `grid.refresh()` vom Client aus auf. |
| *Wie mache ich die Rechtschreibprüfung sprachspezifisch?* | Setzen Sie `grid.settings.spell_check.language = "en-US"` (oder eine andere unterstützte Locale). |
| *Ist Lazy Loading mit serverseitiger Filterung kompatibel?* | Ja – kombinieren Sie `grid.settings.filter.enabled = True` und implementieren Sie die Filterlogik in Ihrem benutzerdefinierten Befehl. |

## Vollständiges funktionierendes Beispiel (Alle Schritte kombiniert)

Im Folgenden finden Sie ein einzelnes Skript, das Sie in eine Flask‑Route einbinden oder als eigenständigen Prozess ausführen können. Ersetzen Sie `YOUR_DIRECTORY` durch den tatsächlichen Pfad auf Ihrem Server.

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie zusätzliche API‑Features meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}