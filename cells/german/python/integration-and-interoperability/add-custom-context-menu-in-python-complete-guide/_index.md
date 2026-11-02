---
category: general
date: 2026-06-30
description: Fügen Sie ein benutzerdefiniertes Kontextmenü zu einem Python‑Excel‑Raster
  hinzu und schreiben Sie einen Wert in eine Excel‑Zelle, während Sie die aktualisierte
  Datei speichern. Lernen Sie, ein Rechtsklick‑Menü zu erstellen und den Zellenwert
  im Python‑Stil zu aktualisieren.
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: de
og_description: Fügen Sie ein benutzerdefiniertes Kontextmenü in Python hinzu, um
  einen Wert in eine Excel‑Zelle zu schreiben und die aktualisierte Excel‑Datei zu
  speichern. Diese Anleitung führt Sie durch die Erstellung eines Rechtsklick‑Menüs
  mit GridJs.
og_title: Benutzerdefiniertes Kontextmenü in Python hinzufügen – Schritt‑für‑Schritt‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Benutzerdefiniertes Kontextmenü in Python hinzufügen – Komplettanleitung
url: /de/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefiniertes Kontextmenü in Python – Komplettanleitung

Haben Sie sich jemals gefragt, wie man **benutzerdefinierte Kontextmenü**‑Einträge zu einem Spreadsheet‑Raster hinzufügt, das Sie aus Python bereitstellen? Vielleicht benötigen Sie einen schnellen „Mark as Reviewed“-Button, der erscheint, wenn ein Benutzer mit der rechten Maustaste auf eine Zelle klickt, einen Wert in die Excel‑Zelle schreibt und dann die aktualisierte Arbeitsmappe speichert – alles, ohne die Web‑UI zu verlassen.  

In diesem Tutorial bauen wir genau das: ein **benutzerdefiniertes Rechtsklick‑Menü**, das von GridJs betrieben wird, einen serverseitigen Handler, der **Wert in Excel‑Zelle schreibt**, und einen abschließenden Schritt, der **die aktualisierte Excel‑Datei** auf der Festplatte **speichert**. Am Ende haben Sie ein wiederverwendbares Muster, das Sie in jedes Flask-, FastAPI- oder Django‑Projekt einbinden können.

> **Warum das wichtig ist?**  
> Das Hinzufügen eines benutzerdefinierten Kontextmenüs rationalisiert Daten‑Review‑Workflows, reduziert manuelles Kopieren‑Einfügen und bietet End‑Benutzern ein nativeres Erlebnis direkt im Raster. Außerdem sehen Sie, wie man **Zellwert python‑artig aktualisiert**, was eine Kernkompetenz für jede Excel‑Automatisierungsaufgabe ist.

## Voraussetzungen

- Python 3.9+ (der Code funktioniert auch mit 3.10)  
- `openpyxl` für die Excel‑Dateiverarbeitung  
- `gridjs` Python‑Wrapper (oder die JS‑Bibliothek, wenn Sie das Front‑End bevorzugen)  
- Ein einfaches Web‑Framework (gezeigtes Beispiel mit Flask)  
- Eine Arbeitsmappendatei namens `sample.xlsx` in Ihrem Projektordner  

Falls Ihnen etwas davon fehlt, führen Sie aus:

```bash
pip install openpyxl flask gridjs
```

Jetzt tauchen wir ein.

---

## Schritt 1 – Benutzerdefiniertes Kontextmenü hinzufügen: GridJs initialisieren und Arbeitsblatt binden

Das allererste, was Sie tun müssen, ist eine `GridJs`‑Instanz zu starten und sie auf das Arbeitsblatt zu verweisen, mit dem Sie arbeiten möchten. Hier erscheint zum ersten Mal der Ausdruck **add custom context menu** in unserem Code und legt die Grundlage für alles Weitere.

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**Was passiert?**  
`grid.set_worksheet(ws)` teilt GridJs mit, die Daten aus `ws` als Datenquelle zu verwenden. Von nun an werden alle Kontextmenü‑Modifikationen, die wir hinzufügen, automatisch das gleiche Arbeitsblatt ansprechen und UI sowie Datei synchron halten.

> **Pro‑Tipp:** Öffnen Sie Ihre Arbeitsmappe im Lese‑/Schreibmodus nur einmal. Das wiederholte Öffnen innerhalb eines Request‑Handlers kann unter Windows zu Datei‑Lock‑Problemen führen.

## Schritt 2 – Wert in Excel‑Zelle schreiben: Aktion für das Menüelement definieren

Jetzt, wo das Raster bereit ist, müssen wir **write value to excel cell** ausführen, wenn der Benutzer unseren benutzerdefinierten Befehl auswählt. Wir fügen einen Menüeintrag namens „Mark as Reviewed“ hinzu und geben ihm den Bezeichner `markReviewed`. Der Bezeichner ist das, was das clientseitige JavaScript an den Server zurücksendet.

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**Warum einen benutzerdefinierten Bezeichner verwenden?**  
Der Bezeichner entkoppelt den UI‑Text von der Server‑Logik, sodass Sie die Beschriftung ändern können, ohne den Backend‑Code zu berühren. Außerdem macht er die **create right‑click menu**‑Operation explizit und wiederverwendbar.

---

## Schritt 3 – Rechtsklick‑Menü erstellen: Server‑seitigen Handler registrieren

Mit dem Menüeintrag an Ort und Stelle müssen wir GridJs mitteilen, was zu tun ist, wenn der Benutzer darauf klickt. Hier kommt die **create right‑click menu**‑Funktionalität zum Einsatz, die tatsächlich eine Anfrage zurück an Python sendet.

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

Ein paar Dinge zu beachten:

1. **`ws[cell_address] = "Reviewed"`** ist der einfachste Weg, **update cell value python** auszuführen. Im Hintergrund übersetzt `openpyxl` die A1‑Adresse in Zeilen‑/Spalten‑Indizes.  
2. Der Handler gibt ein kleines JSON‑Payload zurück. GridJs erwartet einen Status‑Indikator; Sie könnten dies bei Bedarf erweitern, um Fehlermeldungen einzuschließen.

Jetzt binden wir den Bezeichner an den Handler:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**Was, wenn die Zelle leer oder geschützt ist?**  
- Leere Zellen sind in Ordnung – `openpyxl` erstellt sie bei Bedarf.  
- Bei geschützten Blättern müssen Sie zuerst den Schutz aufheben (`ws.protection.sheet = False`) oder einen `PermissionError` abfangen.

## Schritt 4 – Zellwert Python aktualisieren: Änderung durch Speichern der Arbeitsmappe persistieren

Einen Wert zu schreiben ist nur die halbe Geschichte; Sie müssen **save updated excel file**, damit die Änderung über die aktuelle Sitzung hinaus erhalten bleibt. Hier schließen wir den Rundweg von UI zu Festplatte ab.

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**Warum ein separates Verzeichnis?**  
Das Speichern in einem `output/`‑Verzeichnis lässt die ursprüngliche Vorlage unverändert, was für Prüfpfade nützlich ist. Passen Sie den Pfad an Ihre Bereitstellungsumgebung an.

> **Achtung:** Wenn Sie vielen gleichzeitigen Benutzern dienen, sollten Sie einen thread‑sicheren Lock (`threading.Lock`) um `wb.save()` verwenden, um Race‑Conditions zu vermeiden.

## Schritt 5 – Client‑Konfigurations‑JSON erzeugen und alles verbinden

Schließlich müssen wir das JSON erzeugen, das die Front‑End‑GridJs‑Instanz konsumiert. Dieses JSON enthält die Arbeitsblattdaten **und** die Definition des benutzerdefinierten Menüs.

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

Wenn Sie `config_json` in Ihre HTML‑Seite einbetten, rendert GridJs das Raster mit dem rechtsklickbaren Eintrag „Mark as Reviewed“ in jeder Zelle.

### Vollständiges Flask‑Beispiel

Unten finden Sie eine minimale Flask‑App, die alle Bausteine zusammenfügt. Führen Sie sie aus, öffnen Sie `http://localhost:5000` und klicken Sie mit der rechten Maustaste auf eine beliebige Zelle, um das benutzerdefinierte Menü in Aktion zu sehen.

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**Erwartetes Ergebnis:**  
- Rechtsklick auf eine Zelle → „Mark as Reviewed“ erscheint.  
- Klick darauf → der Zelleninhalt ändert sich zu „Reviewed“.  
- Die Arbeitsmappe `output/sample-updated.xlsx` enthält nun den neuen Wert.

---

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| *Was, wenn ich mehrere benutzerdefinierte Aktionen benötige?* | Fügen Sie einfach weitere Objekte zu `grid.settings.context_menu.custom_items` hinzu und registrieren Sie jedes mit einem eigenen Bezeichner. |
| *Kann ich zusätzliche Daten (z. B. Zeilen‑ID) an den Handler übergeben?* | Ja. Fügen Sie zusätzliche Schlüssel im JSON‑Payload auf der Client‑Seite ein und lesen Sie sie aus `request` in `on_custom_command`. |
| *Ist dieser Ansatz mit asynchronen Frameworks kompatibel?* | Absolut – machen Sie `on_custom_command` einfach zu einer async‑Funktion und verwenden Sie `await wb.save(...)`, wenn Sie zu `aiofiles` oder Ähnlichem wechseln. |
| *Wie style ich das Menüsymbol?* | Geben Sie einen beliebigen Material‑Icons‑Namen an (`"icon": "edit"`). Das Front‑End lädt die Symbolschrift automatisch. |
| *Wie gehe ich mit großen Arbeitsmappen um?* | Laden Sie nur das benötigte Blatt und erwägen Sie, Zeilen mit `openpyxl.iter_rows()` zu streamen, um den Speicherverbrauch gering zu halten. |

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Einzelnes Anführungszeichen‑Präfix des Zellwerts oder Bereichs in Excel erhalten](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Einzelnes Anführungszeichen‑Präfix des Zellwerts oder Bereichs in Excel erhalten](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Einzelnes Anführungszeichen‑Präfix des Zellwerts oder Bereichs in Excel erhalten](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}