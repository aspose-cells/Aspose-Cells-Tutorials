---
category: general
date: 2026-06-21
description: Erstellen Sie ein interaktives Datenraster mit Grid.js und lernen Sie,
  wie Sie eine JSON‑Datentabelle mit Sortierung, Paginierung und Suche anzeigen. Perfekt
  für Web‑Dashboards.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: de
og_description: Erstelle in wenigen Minuten ein interaktives Data‑Grid. Erfahre, wie
  du Grid.js nutzt, um eine JSON‑Datentabelle mit Pagination, Sortierung und Suche
  anzuzeigen.
og_title: Interaktives Datenraster mit Grid.js erstellen – Komplettes Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Interaktives Datenraster mit Grid.js – Vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Interaktives Datenraster mit Grid.js erstellen – Vollständige Schritt‑für‑Schritt‑Anleitung

Haben Sie sich jemals gefragt, wie man ein **interaktives Datenraster** erstellt, das Benutzern das Sortieren, Suchen und Durchblättern von Zeilen ermöglicht, ohne ein Backend zu schreiben? Sie sind nicht allein. In vielen Dashboards ist das größte Problem, einen statischen JSON‑Dump in eine elegante, durchsuchbare Tabelle zu verwandeln – etwas, das sich so geschmeidig anfühlt wie eine Tabellenkalkulation, aber vollständig im Browser läuft.

In diesem Tutorial führen wir Sie Schritt für Schritt durch **how to use Grid.js**, um **display JSON data table** auf einer einfachen HTML‑Seite anzuzeigen. Am Ende haben Sie ein funktionierendes Beispiel, das Sie in jedes Projekt einbinden können, sowie Tipps zur Anpassung der Symbolleiste, zum Umgang mit großen Datensätzen und zur Vermeidung häufiger Fallstricke.

## Was Sie lernen werden

- Wie man eine JSON‑Datei abruft, die Spalten und Zeilen definiert.
- Wie man **Grid.js** mit Pagination, Sortierung, Suche und einer benutzerdefinierten Symbolleiste initialisiert.
- Wie man das Raster in einen Ziel‑Container rendert.
- Optionale Anpassungen: benutzerdefinierte Zellformatierung, Themenwechsel und Fehlerbehandlung.
- Ein vollständiges, sofort kopier‑und‑einfügbares Code‑Beispiel.

### Voraussetzungen

Bevor wir loslegen, stellen Sie sicher, dass Sie Folgendes haben:

1. Ein moderner Browser (Chrome, Edge oder Firefox) – Grid.js nutzt ES6‑Funktionen.
2. Ein lokaler oder entfernter Ordner, der eine `grid_data.json`‑Datei enthält (wir zeigen das Format).
3. Grundlegende Kenntnisse in HTML und JavaScript – nichts Besonderes, nur die Fähigkeit, eine `.html`‑Datei im Browser zu öffnen.

Keine Build‑Tools, kein npm‑Install, kein serverseitiger Code. Das ist die Schönheit von **create interactive data grid** mit Grid.js: Es funktioniert direkt von einem CDN.

---

## Schritt 1: Bereiten Sie das JSON vor, das Ihre Tabelle definiert

Das Erste, was Sie benötigen, ist ein JSON‑Payload, das Grid.js mitteilt, welche Spalten existieren und welche Zeilen angezeigt werden sollen. Betrachten Sie es als den Bauplan für Ihre **display JSON data table**. Hier ein minimales Beispiel, das Sie als `grid_data.json` im selben Verzeichnis wie Ihre HTML‑Datei speichern können:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Warum dieses Format?* Grid.js erwartet `columns` als ein Array von Strings (oder Objekten für erweiterte Konfiguration) und `rows` als ein Array von Arrays, wobei jedes innere Array der Spaltenreihenfolge entspricht. Sie können natürlich weitere Spalten oder verschachtelte Objekte hinzufügen – Grid.js rendert sie, solange die Strukturen übereinstimmen.

> **Pro‑Tipp:** Wenn Sie Daten von einer API abrufen, ersetzen Sie einfach das statische `fetch('grid_data.json')` durch Ihre Endpunkt‑URL. Der Rest des Codes bleibt unverändert.

---

## Schritt 2: Initialisieren Sie Grid.js – Das Herz von **how to use gridjs**

Jetzt, wo die Datenquelle bereit ist, müssen wir Grid.js auf die Seite bringen und ihm mitteilen, wie es sich verhalten soll. Hier fügen wir tatsächlich die **create interactive data grid**‑Funktionalität wie Pagination, Sortierung und einen praktischen Symbolleisten‑Button hinzu.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

Das CDN liefert Ihnen die neueste stabile Version, und das Meri­maid‑Theme fügt sofort ein sauberes, modernes Aussehen hinzu. Sie können es gegen `gridjs.min.css` austauschen, wenn Sie das Standard‑Styling bevorzugen.

Als Nächstes, innerhalb eines `<script>`‑Tags, holen Sie das JSON und initialisieren das Raster:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Aufschlüsselung der Optionen

| Option | Was es tut | Warum es wichtig ist |
|--------|------------|----------------------|
| `pagination` | Teilt Zeilen in Seiten auf (standardmäßig 10 pro Seite) | Hält große Tabellen nutzbar, ohne die Benutzeroberfläche zu überladen. |
| `sort` | Klickbare Spaltenüberschriften schalten zwischen auf‑ und absteigender Reihenfolge | Benutzer können schnell die Zeilen mit den höchsten Werten finden. |
| `search` | Fügt ein Texteingabefeld hinzu, das Zeilen in Echtzeit filtert | Ideal für ad‑hoc‑Suchen, ohne Daten neu zu laden. |
| `toolbar` | Fügt über dem Raster benutzerdefinierte Buttons oder Dropdowns hinzu | Perfekt für Aktionen wie „Hilfe“, „Export“ oder „Aktualisieren“. |
| `formatter` | Ermöglicht das Zurückgeben von rohem HTML für eine Zelle | Hier verwandeln wir E‑Mail‑Strings in anklickbare mailto‑Links. |

> **Warum dieser Ansatz?** Durch die deklarative Konfiguration des Rasters können Sie das Verhalten leicht anpassen, ohne die Kern‑Render‑Logik zu verändern. Dies ist die empfohlene Methode, um **how to use Grid.js** in den meisten Projekten zu nutzen.

---

## Schritt 3: Rendern Sie das Raster in Ihre Seite

Die letzte Zeile des Skripts—`grid.render(document.getElementById('grid-container'))`—fügt die voll funktionsfähige Tabelle in ein `<div>` ein, das Sie irgendwo im HTML‑Body platziert haben:

```html
<div id="grid-container"></div>
```

Das war’s. Wenn die Seite geladen wird, holt der Browser das JSON, erstellt die Grid.js‑Instanz und zeichnet die interaktive Tabelle auf dem Bildschirm. Keine Aktualisierungen, keine Serveraufrufe nach dem ersten Laden.

---

## Optional: Styling‑ und Themen‑Anpassungen

Wenn Ihnen das Standard‑Meri­maid‑Theme nicht gefällt, können Sie es gegen eines der integrierten Themes (`gridjs.min.css`) austauschen oder Ihr eigenes CSS schreiben. Zum Beispiel, um den Header‑Hintergrund zu einem sanften Grau zu machen:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Fügen Sie das Snippet innerhalb eines `<style>`‑Tags oder einer externen Stylesheet‑Datei ein. Grid.js respektiert Standard‑CSS‑Selektoren, sodass Sie die volle Kontrolle über Schriftarten, Farben und Abstände haben.

---

## Häufige Fallstricke & wie man sie vermeidet

| Problem | Symptom | Lösung |
|---------|---------|--------|
| **CORS‑Fehler** beim Abrufen von JSON von einer anderen Domain | Browser‑Konsole zeigt „Blocked by CORS policy“ | Stellen Sie das JSON auf derselben Herkunft bereit oder aktivieren Sie CORS auf dem Server. |
| **Große Datensätze verursachen Verzögerungen** | Scrollen wird ruckelig, Pagination ist langsam | Verwenden Sie serverseitige Pagination (`pagination: { server: { url: (prev, page, limit) => … } }`) oder laden Sie Zeilen lazy‑load. |
| **Toolbar‑Button erscheint nicht** | Kein Button sichtbar trotz `toolbar.enabled: true` | Stellen Sie sicher, dass Sie Grid.js Version 2.0+ verwenden; ältere Versionen hatten eine andere Toolbar‑API. |
| **E‑Mail‑Links nicht anklickbar** | Formatter gibt reinen Text zurück | Geben Sie `gridjs.html(...)` zurück anstelle eines einfachen Strings, wie im Beispiel gezeigt. |

Das frühzeitige Beheben dieser Probleme spart Ihnen später Stunden an Fehlersuche.

---

## Vollständiges funktionierendes Beispiel (Kopieren‑und‑Einfügen bereit)

Unten finden Sie die komplette HTML‑Datei, die Sie als `index.html` speichern können. Öffnen Sie sie in einem Browser, und Sie sehen eine voll funktionsfähige **create interactive data grid**‑Demo, die **display JSON data table** mit Sortierung, Suche und einem Hilfeknopf zeigt.



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man eine Excel‑Datenvalidierungsliste mit Aspose.Cells für Java erstellt: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Wie man Kontrollkästchen in Excel mit Aspose.Cells für .NET erstellt | Datenvalidierungstutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [XML‑Daten in Excel erstellen & importieren mit Aspose.Cells für Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}