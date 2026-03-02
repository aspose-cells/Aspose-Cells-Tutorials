---
category: general
date: 2026-03-01
description: Importieren Sie Daten mit Formatierung in Excel mithilfe von C#. Erfahren
  Sie, wie Sie eine DataTable in Excel importieren und Zellen eine Hintergrundfarbe
  hinzufügen – in nur wenigen Schritten.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: de
og_description: Daten mit Formatierung in Excel importieren mit C#. Schritt‑für‑Schritt‑Anleitung,
  die zeigt, wie man eine DataTable importiert und Zellen eine Hintergrundfarbe hinzufügt.
og_title: Daten mit Formatierung in Excel importieren – C#‑Leitfaden
tags:
- C#
- Excel
- DataTable
- Formatting
title: Daten mit Formatierung in Excel importieren mit C#
url: /de/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Daten mit Formatierung in Excel importieren mit C#

Haben Sie jemals **Daten mit Formatierung** in eine Excel‑Arbeitsmappe importieren müssen, aber nur ein schlichtes, langweiliges Blatt erhalten? Sie sind nicht allein. Die meisten Entwickler stoßen auf dieses Problem, wenn sie feststellen, dass der Standard‑Import alle Farben und Stile, die sie mühsam in den Quelldaten eingerichtet haben, entfernt.

In diesem Tutorial führen wir Sie durch eine komplette, sofort ausführbare Lösung, die **eine DataTable in Excel importiert** und **Hintergrundfarbe zu Excel‑Zellen hinzufügt**. Keine zusätzliche Nachbearbeitung nötig – Ihre Tabelle sieht genau so aus, wie Sie es sich wünschen, sofort nach dem Erstellen.

## Was Sie lernen werden

- Wie man Daten in eine `DataTable` lädt.
- Wie man ein Array von `Style`‑Objekten definiert, die Hintergrundfarben enthalten.
- Wie man `ImportDataTable` mit diesen Stilen aufruft, sodass der Import die Formatierung beibehält.
- Ein vollständiges, ausführbares Beispiel, das Sie in eine Konsolen‑App einfügen können und das Ergebnis sofort sehen.
- Tipps, Fallstricke und Varianten für reale Projekte.

### Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+).
- Die **GemBox.Spreadsheet**‑Bibliothek (die kostenlose Version reicht für die Demo).
- Grundlegende Kenntnisse in C# und Excel‑Konzepten.

Falls Sie sich fragen *warum GemBox?* weil es eine einzeilige `ImportDataTable`‑Methode bietet, die Stil‑Arrays akzeptiert – genau das, was wir benötigen, um **Daten mit Formatierung** zu importieren, ohne eine Schleife zu schreiben.

---

## Schritt 1: Projekt einrichten und GemBox.Spreadsheet hinzufügen

Um zu beginnen, erstellen Sie eine neue Konsolen‑App:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Profi‑Tipp:** Die kostenlose Version begrenzt Arbeitsblätter auf 150 k Zellen, was für Demos mehr als genug ist. Wenn Sie das Limit erreichen, aktualisieren Sie oder wechseln Sie zu EPPlus, aber die API sieht dann leicht anders aus.

## Schritt 2: Quellendaten als `DataTable` abrufen

Das Erste, was wir benötigen, ist eine `DataTable`, die die Daten nachahmt, die Sie normalerweise aus einer Datenbank holen würden. Hier ist ein kleiner Helfer, der eine im Speicher erstellt:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Warum das wichtig ist:** Durch das Trennen der Datenabfrage in eine eigene Methode können Sie jede Quelle – SQL, CSV, Web‑Service – austauschen, ohne die Import‑Logik zu berühren. Das hält den Code sauber und macht das Tutorial **wie man DataTable in Excel importiert** wiederverwendbar.

## Schritt 3: Definieren Sie die anzuwendenden Stile

Jetzt kommt der spaßige Teil: Wir erstellen ein Array von `Style`‑Objekten, jedes mit einer eigenen `ForegroundColor`. GemBox ermöglicht das Setzen von `BackgroundPatternColor` (die Zellfüllung) und `ForegroundColor` (die Textfarbe). Für diese Demo färben wir die ersten beiden Spalten unterschiedlich.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Erklärung:**  
- `Style`‑Objekte sind leichte Container; Sie müssen nicht für jede Zelle ein neues erstellen.  
- Durch die Angleichung der Reihenfolge des Arrays an die Spaltenreihenfolge wendet GemBox automatisch den passenden Stil beim Import an.  
- Das ist der Schlüssel zu **Daten mit Formatierung importieren** – die Formatierung reist mit den Daten, nicht nachträglich.

## Schritt 4: Importieren Sie die `DataTable` mit Stilen in das Arbeitsblatt

Mit den Daten und Stilen bereit, können wir nun eine Arbeitsmappe erstellen, das erste Arbeitsblatt auswählen und `ImportDataTable` aufrufen. Die Methodensignatur sieht so aus:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

So verwenden wir es:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Was passiert im Hintergrund?**  
- `true` weist GemBox an, die Spaltennamen in der ersten Zeile zu schreiben.  
- `0, 0` positioniert den Import bei Zelle A1.  
- `importStyles` verknüpft jede Spalte mit den zuvor definierten Farben.

Wenn Sie *Report.xlsx* öffnen, sehen Sie die **ID**‑Spalte hellblau schattiert, die **Name**‑Spalte hellgrün und die **Score**‑Spalte unverändert. Das ist **Daten mit Formatierung importieren** in einem einzigen Aufruf.

## Schritt 5: Ergebnis überprüfen (erwartete Ausgabe)

Öffnen Sie die erzeugte `Report.xlsx`. Sie sollten etwas Ähnliches sehen:

| ID (light blue) | Name (light green) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- Die Zellen der **ID**‑Spalte haben einen hellblauen Hintergrund.  
- Die Zellen der **Name**‑Spalte haben einen hellgrünen Hintergrund.  
- Die **Score**‑Spalte behält den standardmäßigen weißen Hintergrund bei.

Dieser visuelle Hinweis macht den Bericht sofort scanbar – ein kleiner Touch, der die Benutzererfahrung deutlich verbessern kann.

![Excel‑Tabelle, die Datenimport mit Formatierung zeigt – ID‑Spalte hellblau, Name‑Spalte hellgrün](excel-screenshot.png "Beispiel für Datenimport mit Formatierung")

*Der Alt‑Text des Bildes enthält das Haupt‑Keyword für SEO.*

---

## Häufige Fragen & Sonderfälle

### Kann ich mehr als nur Hintergrundfarben anwenden?

Absolut. `Style` ermöglicht das Setzen von Schriftarten, Rahmen, Zahlenformaten und sogar bedingter Formatierung. Zum Beispiel, um Werte über 90 fett und rot darzustellen:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### Was passiert, wenn meine DataTable mehr Spalten als Stile hat?

GemBox wendet Stile nur auf die Spalten an, die einen passenden Eintrag im Array haben. Zusätzliche Spalten erhalten den Standardstil – es wird kein Fehler ausgelöst.

### Funktioniert das mit großen Datensätzen?

Ja, aber achten Sie auf das Zell‑Limit der kostenlosen Version (150 k Zellen). Für sehr große Berichte sollten Sie die kostenpflichtige Lizenz in Betracht ziehen oder die Daten zeilenweise mit `worksheet.Cells[row, col].Value = …` streamen – dabei verlieren Sie jedoch die Einzeiler‑Bequemlichkeit.

### Wie importiere ich Daten mit Formatierung aus einer bestehenden Excel‑Vorlage?

Sie können zuerst eine Vorlagen‑Arbeitsmappe laden:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Damit können Sie Header‑Logos, Fußzeilen und bereits vorhandene Stile beibehalten, während Sie dennoch **Daten mit Formatierung importieren** für den dynamischen Teil.

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Führen Sie das Programm (`dotnet run`) aus und öffnen Sie die erzeugte *Report.xlsx*, um die Farben sofort angewendet zu sehen.

---

## Fazit

Sie haben jetzt eine solide, vollständige Lösung.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}