---
category: general
date: 2026-11-19
description: Währungsformat in Excel mit C# festlegen – lernen Sie, wie Sie das Zahlenformat
  einstellen und Excel‑Spalten beim Import eines Excel‑Arbeitsblatts formatieren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: de
lastmod: 2026-11-19
og_description: Währungsformat in Excel mit C# festlegen und erfahren, wie man das
  Zahlenformat setzt, das Zahlenformat zuweist und Excel‑Spalten beim Import eines
  Arbeitsblatts formatiert.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: Währungsformat in Excel mit C# festlegen – vollständige Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: Währungsformat beim Importieren von Daten in Excel mit C# festlegen
url: /de/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Währungsformat festlegen beim Importieren von Daten in Excel mit C#

Wenn Sie **Währungsformat festlegen** in einem Excel-Arbeitsblatt benötigen, zeigt Ihnen dieser Leitfaden, wie Sie **Zahlenformat festlegen** und die Spalten formatieren, während Sie einen **excel worksheet import** durchführen. Sie sehen ein vollständiges, ausführbares Beispiel, das das korrekte Zahlenformat jeder Spalte einer `DataTable` zuweist und die Daten mit dem gewünschten Styling importiert.

Die Arbeit mit Excel aus C# erfordert oft mehr als nur das Dumpen roher Werte – Sie müssen auch steuern, wie Zahlen angezeigt werden. Egal, ob Sie Rechnungen, Finanzberichte oder Dashboards erstellen, das korrekte Formatieren von Währungen, Prozentsätzen oder Daten macht die Ausgabe sofort lesbar.

## Voraussetzungen

* .NET 6.0 (oder höher) installiert.
* Ein Verweis auf **Aspose.Cells for .NET** (oder eine Bibliothek, die eine `Style`‑Klasse mit einer `Number`‑Eigenschaft bereitstellt).  
  *NuGet*: `Install-Package Aspose.Cells`.
* Grundlegende Kenntnisse von `DataTable` und C#‑Sammlungen.
* Eine IDE wie Visual Studio 2022 oder VS Code.

## Schritt 1: Daten abrufen, die in das Arbeitsblatt geschrieben werden sollen

Zuerst erhalten Sie eine `DataTable`, die die Rohdaten enthält, die Sie exportieren möchten. In realen Projekten kann diese aus einer Datenbankabfrage, einem API‑Aufruf oder einem CSV‑Parser stammen.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Warum das wichtig ist:** Das Importieren einer vollständig gefüllten `DataTable` ermöglicht es Ihnen, die Datenabruf‑Logik von der Excel‑Erzeugungs‑Logik zu trennen, was die Testbarkeit und Wartbarkeit verbessert.

## Schritt 2: Ein Style‑Array erstellen – ein Eintrag pro Spalte in der DataTable

Aspose.Cells erwartet ein `Style[]`, dessen Länge der Anzahl der Spalten entspricht, die Sie importieren möchten. Jedes Element kann ein bestimmtes Zahlenformat enthalten.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Pro Tipp:** Auch wenn Sie nur für einen Teil der Spalten Formatierung benötigen, müssen Sie für jede Spalte eine `Style`‑Instanz erstellen; andernfalls erhalten Sie beim Import eine `NullReferenceException`.

## Schritt 3: Zahlenformat den gewünschten Spalten zuweisen

Die integrierten Style‑Nummern unterscheiden sich je nach Bibliothek. In Aspose.Cells:

* `0` → Allgemein (Ganzzahl)  
* `2` → Währung (z. B. `$#,##0.00`)  
* `3` → Datum, usw.

Hier **weisen wir das Zahlenformat** zwei Spalten zu: Die erste Spalte (Id) bleibt eine Ganzzahl, während die zweite Spalte (Amount) ein Währungsformat erhält.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Wie man das Zahlenformat festlegt:** Die Verwendung der `Number`‑Eigenschaft ist der schnellste Weg, ein integriertes Format auszuwählen. Für länderspezifische Währungen sollten Sie einen benutzerdefinierten Formatstring verwenden, der das passende Währungssymbol enthält.

## Schritt 4: Die DataTable in das Arbeitsblatt importieren und die Spaltenstile anwenden

Jetzt, wo das Style‑Array fertig ist, importieren Sie die Daten. Die Methode `ImportDataTable` berücksichtigt die übergebenen Stile.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Erwartetes Ergebnis

Wenn Sie **FinancialReport.xlsx** öffnen, sehen Sie:

| Id | Betrag      | Beschreibung      |
|----|------------|-------------------|
| 1  | $1,234.56  | Bürobedarf |
| 2  | $98,765.43 | Beratungsgebühren |
| 3  | $0.99      | Verschiedenes |

*Die **Betrag**‑Spalte wird mit dem von Ihnen festgelegten Währungsformat angezeigt, während **Id** eine Ganzzahl bleibt.*

## Wie man das Zahlenformat für weitere Szenarien festlegt

### Zahlenformat für Datumsspalten zuweisen

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Benutzerdefinierte Zahlenformate für Prozentsätze verwenden

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Styling über Zahlenformate hinaus

Sie können auch Schriftart, Hintergrundfarbe oder Ausrichtung im selben `Style`‑Objekt festlegen:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Warum das funktioniert:** Das `Style`‑Objekt fasst alle visuellen Eigenschaften einer Zelle zusammen. Wenn Sie das Array an `ImportDataTable` übergeben, erbt jede Zelle automatisch den definierten Stil.

## Häufige Fallstricke und wie man sie vermeidet

| Problem | Symptom | Lösung |
|---------|---------|--------|
| Vergessen, jede `Style`‑Instanz zu erstellen | `NullReferenceException` beim Import | Durchlaufen Sie das Array und rufen Sie `CreateStyle()` auf, bevor Sie Eigenschaften setzen. |
| Verwendung des falschen integrierten Zahlenindexes | Falsches Format (z. B. erscheinen Daten als Ganzzahlen) | Konsultieren Sie die Dokumentation der Bibliothek für die korrekten `Number`‑Konstanten. |
| Das Arbeitsbuch nicht speichern | Keine Ausgabedatei oder leere Datei | Rufen Sie nach Abschluss des Imports `workbook.Save(...)` auf. |
| Lokale Diskrepanz beim Währungssymbol | `$` erscheint sogar in Nicht‑US‑Lokalen | Verwenden Sie einen benutzerdefinierten Formatstring mit dem passenden Symbol (z. B. `"€#,##0.00"`). |

## Vollständiges, ausführbares Beispiel



## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel-Datei mit C# erstellen – Zellen formatieren und Währungsformat festlegen](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [Wie man Excel‑Spalten in C# formatiert – Vollständiger Leitfaden](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Excel‑Arbeitsmappe mit C# erstellen – Währungsformat anwenden und DataTable importieren](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}