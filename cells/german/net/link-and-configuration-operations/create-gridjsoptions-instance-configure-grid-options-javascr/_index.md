---
category: general
date: 2026-05-30
description: Erfahren Sie, wie Sie eine GridJsOptions‑Instanz erstellen und die Grid‑Optionen
  in JavaScript für dynamische Tabellen konfigurieren. Schritt‑für‑Schritt‑Anleitung
  mit vollständigem Code.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: de
og_description: Erstellen Sie eine GridJsOptions‑Instanz und konfigurieren Sie die
  Grid‑Optionen in JavaScript in wenigen Minuten. Vollständiges Beispiel, Erklärungen
  und Tipps zu bewährten Methoden.
og_title: GridJsOptions‑Instanz erstellen – Grid‑Optionen in JavaScript konfigurieren
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: GridJsOptions‑Instanz erstellen – Grid‑Optionen in JavaScript konfigurieren
url: /de/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJsOptions‑Instanz erstellen – Grid‑Optionen in JavaScript konfigurieren

Haben Sie sich jemals gefragt, wie man **create GridJsOptions instance** erstellt, ohne durch verstreute Dokumente zu suchen? Sie sind nicht allein. Wenn Sie eine elegante, sortierbare Tabelle auf einer Webseite benötigen, ist das Beherrschen der Konfiguration von grid options JavaScript der erste Schritt zu einer polierten Benutzeroberfläche.

In diesem Tutorial gehen wir den genauen Code durch, den Sie benötigen, erklären, warum jede Einstellung wichtig ist, und zeigen Ihnen ein vollständiges, ausführbares Beispiel. Am Ende können Sie problemlos GridJsOptions‑Instanzen erstellen, die Ausrichtung, Paginierung und sogar benutzerdefinierte Zell‑Renderer anpassen – alles mit reinem JavaScript.

## Was Sie lernen werden

- Wie man **create GridJsOptions instance** von Grund auf **erstellt**.
- Die wichtigsten Eigenschaften, mit denen Sie **configure grid options JavaScript** (Sortierung, Paginierung, Zahlenformatierung usw.) steuern können.
- Häufige Stolperfallen (z. B. das Mischen von Zeichenketten‑ und Zahlentypen) und wie man sie vermeidet.
- Eine komplette HTML‑Seite, die Sie in jedes Projekt kopieren‑und‑einfügen können, um sofort Ergebnisse zu sehen.

### Voraussetzungen

- Ein moderner Browser (Chrome, Edge, Firefox) – keine Build‑Tools erforderlich.
- Grundlegende Kenntnisse in JavaScript (Variablen, Objekte, DOM).
- Die Grid.js‑Bibliothek (wir holen sie von einem CDN).

Falls Ihnen einer dieser Punkte unbekannt ist, keine Panik – jeder Schritt enthält eine kurze Auffrischung.

---

## Schritt 1: Grid.js laden und das HTML‑Gerüst vorbereiten

Bevor wir **create GridJsOptions instance** ausführen können, benötigen wir die Bibliothek selbst. Der einfachste Weg ist die offizielle CDN‑Version. Unten finden Sie ein minimales HTML‑Gerüst, das zudem ein `<div>` reserviert, in dem das Grid gerendert wird.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Pro Tipp:** Platzieren Sie den CSS‑Link vor Ihren eigenen Styles, damit das Standard‑Theme des Grids korrekt geladen wird.

### Warum das wichtig ist

Das Laden der Bibliothek von einem CDN stellt sicher, dass Sie stets die neueste stabile Version erhalten, ohne eine lokale Installation. Das `<div id="grid-wrapper">` ist der Platzhalter, den der Grid.js‑Konstruktor anvisiert, sobald wir **configure grid options JavaScript**.

---

## Schritt 2: Eine neue GridJsOptions‑Instanz erstellen

Jetzt kommt das Herzstück des Tutorials: die Zeile, die tatsächlich **creates GridJsOptions instance**. In einer separaten Datei namens `grid-config.js` (im HTML oben referenziert) schreiben wir:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Diese einzelne Zeile liefert Ihnen ein sauberes Objekt, das Sie mit Einstellungen füllen können. Denken Sie an `gridOptions` als das Bedienfeld für jede Funktion, die Sie später aktivieren werden.

### Was Sie konfigurieren

- **NumberFormatAlignment** – richtet numerische Zeichenketten automatisch aus.
- **Pagination** – steuert Seitengröße und Navigation.
- **Sorting** – schaltet die Spaltensortierung ein/aus.
- **Columns** – definiert Überschriften, Datentypen und benutzerdefinierte Renderer.

Sie können jede dieser Eigenschaften hinzufügen, bevor Sie schließlich das Grid selbst instanziieren.

---

## Schritt 3: Zahlen‑Ausrichtung aktivieren (ein häufiges Anliegen)

Die meisten Tabellen enthalten eine Mischung aus Text und Zahlen. Standardmäßig richtet Grid.js alles linksbündig aus, was bei Geldbeträgen unästhetisch wirkt. Um **configure grid options JavaScript** für die korrekte Ausrichtung zu nutzen, setzen Sie das Flag `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Warum das aktivieren? Wenn das Flag wahr ist, prüft Grid.js jede Zelle; sieht sie wie eine Zahl aus (z. B. „1234“, „12.34%“), wird sie automatisch rechtsbündig ausgerichtet. Diese kleine Anpassung macht Berichte deutlich lesbarer.

---

## Schritt 4: Paginierung und Sortierung hinzufügen

Ein Grid in der Praxis passt selten auf einen einzigen Bildschirm. Aktivieren wir die Paginierung (10 Zeilen pro Seite) und erlauben dem Nutzer, jede Spalte zu sortieren.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Hinweis zu Randfällen

Wenn Sie später eine benutzerdefinierte Datenquelle bereitstellen, die bereits paginierte Ergebnisse liefert, sollten Sie die eingebaute Paginierung von Grid.js deaktivieren, um Doppel‑Paging zu vermeiden. Setzen Sie einfach `gridOptions.Pagination.enabled = false;`.

---

## Schritt 5: Spalten und Beispieldaten definieren

Jetzt füttern wir das Grid mit Mock‑Daten und geben an, was jede Spalte bedeutet. Hier kommt das **create gridjsoptions instance**‑Muster richtig zur Geltung – alles lebt in einem übersichtlichen Objekt.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Beachten Sie, dass wir die Spalten‑`id`‑Werte identisch zu den Schlüsseln in jedem Datenobjekt halten. Diese Konvention lässt Grid.js die Werte automatisch zuordnen und spart Ihnen das Schreiben eines eigenen Formatters für jede Spalte.

---

## Schritt 6: Das Grid mit unseren Optionen instanziieren

Wir **configure grid options javascript** schließlich, indem wir das `gridOptions`‑Objekt an den Grid‑Konstruktor übergeben. Das Grid wird innerhalb des zuvor vorbereiteten `<div id="grid-wrapper">` gerendert.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

Das war’s. Der gesamte Prozess – vom **create gridjsoptions instance** bis zum Rendern – dauert weniger als eine Minute Code.

### Erwartete Ausgabe

Wenn Sie die HTML‑Datei in einem Browser öffnen, sollten Sie sehen:

- Eine Kopfzeile mit „ID“, „Employee“, „Salary ($)“, „Dept.“.
- Rechtsbündig ausgerichtete Gehaltszahlen (dank `NumberFormatAlignment`).
- Paginierungs‑Steuerelemente am unteren Rand (wenn Sie mehr als zehn Zeilen hinzugefügt haben).
- Anklickbare Spaltenüberschriften, die auf‑ und absteigend sortieren.

Falls etwas nicht stimmt, öffnen Sie die Browser‑Konsole (F12) und suchen Sie nach Fehlermeldungen – die meisten Bugs entstehen durch nicht übereinstimmende Spalten‑IDs oder fehlende Bibliotheksskripte.

---

## Schritt 7: Erweiterte Anpassungen (optional)

Im Folgenden finden Sie ein paar schnelle Ideen, die Sie ausprobieren können, sobald das Grund‑Grid funktioniert.

| Feature | Wie aktivieren | Warum es hilft |
|---------|----------------|----------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Hebt Gehälter fett hervor. |
| **Search bar** | `gridOptions.Search = true;` | Ermöglicht dem Nutzer, Zeilen sofort zu filtern. |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Skalierbar auf tausende Zeilen. |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Passt zu Dark‑Mode‑Designs. |

Fühlen Sie sich frei, zu kombinieren – Grid.js ist bewusst flexibel. Denken Sie nur daran, die ursprüngliche **create gridjsoptions instance**‑Zeile oben beizubehalten; alle späteren Anpassungen basieren auf diesem einen Objekt.

---

## Fazit

Wir haben gerade einen vollständigen Workflow durchlaufen, um **create GridJsOptions instance** und **configure grid options JavaScript** für eine funktionale, sortierbare und paginierte Datentabelle zu erstellen. Ausgehend von einer einfachen HTML‑Seite haben wir die Bibliothek geladen, ein Options‑Objekt gebaut, die Zahlen‑Ausrichtung aktiviert, die Paginierung hinzugefügt, Spalten definiert und schließlich das Grid gerendert.

Ab hier können Sie:

- Die statischen `sampleData` durch einen AJAX‑Aufruf ersetzen.
- Benutzerdefinierte Formatter für Daten, Währungen oder Icons hinzufügen.
- Das Grid in ein Framework wie React oder Vue integrieren (das gleiche `gridOptions`‑Objekt funktioniert dort ebenfalls).

Die Möglichkeiten sind praktisch unbegrenzt, und das von uns genutzte Muster – das Zentralisieren aller Einstellungen in einer einzigen `GridJsOptions`‑Instanz – hält Ihren Code sauber und wartbar.

Haben Sie einen Anwendungsfall, bei dem Sie unsicher sind? Hinterlassen Sie einen Kommentar, und wir erkunden ihn gemeinsam. Viel Spaß beim Coden und beim Erstellen dynamischer Tabellen mit Grid.js!

## Was sollten Sie als Nächstes lernen?

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step‑By‑Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}