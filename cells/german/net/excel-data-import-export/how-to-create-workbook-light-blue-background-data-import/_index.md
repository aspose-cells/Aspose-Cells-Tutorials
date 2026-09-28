---
category: general
date: 2026-02-09
description: Wie man ein Arbeitsbuch in C# mit einem hellblauen Hintergrund erstellt
  und Daten mit Überschriften importiert. Lernen Sie, einen hellblauen Hintergrund
  hinzuzufügen, den Standard‑Excel‑Stil zu verwenden und eine DataTable zu importieren.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: de
og_description: Wie man in C# eine Arbeitsmappe mit hellblauem Hintergrund erstellt,
  Daten mit Überschriften importiert und den Standard‑Excel‑Stil anwendet – alles
  in einem kurzen Leitfaden.
og_title: Wie man ein Arbeitsbuch erstellt – Hellblauer Hintergrund, Datenimport
tags:
- C#
- Excel
- Aspose.Cells
title: Wie man ein Arbeitsbuch erstellt – Hellblauer Hintergrund, Datenimport
url: /de/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Workbook erstellt – Hellblauer Hintergrund, Datenimport

Haben Sie sich jemals gefragt, **how to create workbook** in C#, das gleich nach dem Erstellen etwas ansprechender aussieht? Vielleicht haben Sie eine `DataTable` aus einer Datenbank gezogen und sind die fade, standard‑weißen Zellen leid. In diesem Tutorial führen wir Sie durch das Erstellen eines neuen Workbooks, das Hinzufügen eines hellblauen Hintergrunds zu einer Spalte und das Importieren von Daten mit Überschriften – alles unter Verwendung des von Excel bereitgestellten Standardstils.

Wir werden auch ein paar „what‑if“-Szenarien einstreuen, wie das Handhaben von Nullwerten oder das Anpassen von mehr als einer Spalte. Am Ende haben Sie eine vollständig formatierte Excel‑Datei, die Sie ohne Nachbearbeitung an Stakeholder senden können.

## Voraussetzungen

* **.NET 6+** (der Code funktioniert auch auf .NET Framework 4.6+)
* **Aspose.Cells for .NET** – die Bibliothek, die die Aufrufe `Workbook`, `Style` und `ImportDataTable` bereitstellt. Installieren Sie sie über NuGet:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* Eine `DataTable`‑Quelle – wir erzeugen im Beispiel eine künstliche, Sie können sie jedoch durch jede ADO.NET‑Abfrage ersetzen.

Haben Sie das? Großartig, dann legen wir los.

## Schritt 1: Ein neues Workbook initialisieren (Primäres Schlüsselwort)

Das Erste, was Sie tun müssen, ist **how to create workbook** – buchstäblich. Die Klasse `Workbook` repräsentiert die gesamte Excel‑Datei, und ihr Konstruktor liefert Ihnen ein leeres Blatt.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Warum das wichtig ist:** Das Beginnen mit einem frischen `Workbook` stellt sicher, dass Sie von Anfang an jede Formatierung kontrollieren. Wenn Sie eine bestehende Datei öffnen, übernehmen Sie die Stilvorlagen des ursprünglichen Autors, was zu inkonsistenter Formatierung führen kann.

## Schritt 2: Die zu importierende DataTable vorbereiten

Zur Veranschaulichung erstellen wir eine einfache `DataTable`. In realen Szenarien würden Sie wahrscheinlich eine Stored Procedure oder eine ORM‑Methode aufrufen.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tipp:** Wenn Sie die Spaltenreihenfolge exakt so beibehalten müssen, wie sie in der Datenbank erscheint, setzen Sie den Parameter `importColumnNames` von `ImportDataTable` auf `true`. Dadurch schreibt Aspose.Cells die Spaltenüberschriften für Sie.

## Schritt 3: Spaltenstile definieren – Standard + hellblauer Hintergrund

Jetzt beantworten wir den **add light blue background**‑Teil des Puzzles. Aspose.Cells ermöglicht es Ihnen, ein Array von `Style`‑Objekten zu übergeben, das jeder zu importierenden Spalte entspricht. Der erste Eintrag ist der Stil für Spalte 0, der zweite für Spalte 1 usw. Haben Sie weniger Stile als Spalten, erhalten die übrigen Spalten den Standardstil.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Warum nur zwei Stile?** In unserem Beispiel haben wir vier Spalten, aber wir möchten nur die zweite Spalte (Name) hervorheben. Die Array‑Länge muss nicht der Spaltenanzahl entsprechen; fehlende Einträge erben automatisch den Standardstil des Workbooks.

## Schritt 4: Die DataTable mit Überschriften und Stilen importieren

Hier verbinden wir **excel import datatable c#** und **import data with headers**. Die Methode `ImportDataTable` übernimmt die Hauptarbeit: Sie schreibt die Spaltennamen, Zeilen und wendet das gerade erstellte Stil‑Array an.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Erwartetes Ergebnis

Nach dem Ausführen des Programms enthält `workbook` ein einzelnes Arbeitsblatt, das wie folgt aussieht:

| **ID** | **Name** (hellblau) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* Die **Name**‑Spalte hat einen hellblauen Hintergrund, was zeigt, dass das Stil‑Array funktioniert.
* Spaltenüberschriften werden automatisch erzeugt, weil wir `true` für `importColumnNames` übergeben haben.
* Null‑Werte erscheinen als leere Zellen, was das Standardverhalten von Aspose.Cells ist.

## Schritt 5: Das Workbook speichern (optional aber nützlich)

Wahrscheinlich möchten Sie die Datei auf die Festplatte schreiben oder sie an einen Web‑Client streamen. Das Speichern ist unkompliziert:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro‑Tipp:** Wenn Sie ältere Excel‑Versionen ansprechen, ändern Sie `SaveFormat.Xlsx` zu `SaveFormat.Xls`. Die API übernimmt die Konvertierung für Sie.

## Randfälle & Variationen

### Mehrere formatierte Spalten

Wenn Sie mehr als eine formatierte Spalte benötigen, erweitern Sie einfach das `columnStyles`‑Array:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Jetzt werden sowohl **Name** als auch **Salary** hellblau sein.

### Bedingte Formatierung statt fester Stile

Manchmal soll eine Spalte rot werden, wenn ein Wert einen Schwellenwert überschreitet. Dort kommt **use default style excel** zusammen mit bedingter Formatierung zum Einsatz:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Import ohne Überschriften

Wenn Ihr nachgelagertes System bereits eigene Überschriften bereitstellt, übergeben Sie einfach `false` für das Argument `importColumnNames`. Die Daten beginnen dann bei `A1` und Sie können anschließend eigene Überschriften schreiben.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Vollständiges funktionierendes Beispiel (Alle

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}