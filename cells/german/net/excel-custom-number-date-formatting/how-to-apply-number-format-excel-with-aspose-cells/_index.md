---
category: general
date: 2026-10-10
description: Wenden Sie das Zahlenformat in Excel schnell an, indem Sie eine DataTable
  importieren, Datums‑ und Währungsformate festlegen und die Kopfzeile in Excel in
  einem einzigen Schritt beibehalten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: de
lastmod: 2026-10-10
og_description: Zahlenformat in Excel mit C# und Aspose.Cells anwenden. Erfahren Sie,
  wie Sie das Datumsformat in Excel festlegen, das Währungsformat in Excel setzen
  und die Kopfzeile in Excel beim Importieren einer DataTable beibehalten.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Zahlenformat in Excel mit C# anwenden – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Wie man das Zahlenformat in Excel mit Aspose.Cells anwendet
url: /de/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man das Zahlenformat in Excel mit Aspose.Cells anwendet

Wenn Sie **apply number format excel** beim Laden von Daten aus einer `DataTable` benötigen, zeigt Ihnen dieser Leitfaden genau, wie es geht. Sie lernen außerdem, wie man **set date format excel**, **set currency format excel** und **preserve header row excel** während des Imports einstellt, sodass das resultierende Arbeitsblatt professionell aussieht, ohne zusätzliche Nachbearbeitung.

Wir behandeln alles von der Installation der Bibliothek bis zum Schreiben eines vollständigen, ausführbaren Code‑Snippets. Am Ende können Sie jede `DataTable` in eine Excel-Arbeitsmappe importieren, numerische Spalten automatisch formatieren und die Kopfzeile unverändert lassen – alles in nur wenigen Zeilen C#.

## Voraussetzungen

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.6+)
* Visual Studio 2022 (oder jede C#‑IDE Ihrer Wahl)
* **Aspose.Cells for .NET** – Installation über NuGet:

```bash
dotnet add package Aspose.Cells
```

* Eine `DataTable`‑Quelle – das Beispiel verwendet eine Hilfsmethode `GetTable()`, die Beispieldaten zurückgibt.

> **Profi‑Tipp:** Aspose.Cells ist eine kommerzielle Bibliothek, bietet aber einen kostenlosen Evaluierungsmodus, der das Wasserzeichen für bis zu 30 Tage deaktiviert.

## Schritt 1: Erstellen einer Arbeitsmappe und Zugriff auf das erste Arbeitsblatt

Das Workbook‑Objekt ist der Einstiegspunkt für alle Excel‑Operationen. Durch das Erstellen einer neuen Arbeitsmappe erhalten Sie ein Standard‑Arbeitsblatt bei Index 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Warum dieser Schritt?*  
`Workbook` verwaltet Dateiformat, Berechnungs‑Engine und Stil‑Repository. Der frühe Zugriff auf `Worksheet` ermöglicht es uns, das Ziel‑Sheet später an die Import‑Methode zu übergeben.

## Schritt 2: Abrufen der Quelldaten als DataTable

In realen Projekten stammen die Daten häufig aus einer Datenbankabfrage, einem CSV‑Parser oder einer API‑Antwort. Zur Veranschaulichung erzeugen wir eine einfache `DataTable` mit drei Spalten: **Product**, **Price** und **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Warum dieser Schritt?*  
Eine `DataTable` liefert eine tabellarische In‑Memory‑Darstellung, die Aspose.Cells direkt importieren kann und dabei Spaltenreihenfolge sowie Datentypen beibehält.

## Schritt 3: Vorbereitung eines `Style`‑Arrays – ein Stil pro Spalte

Aspose.Cells ermöglicht es, während des Imports jedem Spalten ein eigenes Stil zuzuweisen, indem ein Array von `Style`‑Objekten übergeben wird. Die Array‑Länge muss der Anzahl der Spalten in der Quelltabelle entsprechen.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Warum dieser Schritt?*  
Wenn Sie die explizite Erstellung (`CreateStyle()`) überspringen, führt das Setzen von `Number` zu einer `NullReferenceException`. Das Initialisieren jedes `Style` stellt sicher, dass die späteren Zuweisungen erfolgreich sind.

## Schritt 4: Zuweisen von Zahlenformaten – Währung und Datum

Excel identifiziert integrierte Zahlenformate über IDs.  
* **14** – Währung (z. B. `$1,234.00`)  
* **22** – Kurzes Datum (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Hinweis:** Wenn Sie ein benutzerdefiniertes Format benötigen (z. B. `"¥#,##0.00"`), verwenden Sie `Style.Custom = "¥#,##0.00"` anstelle einer integrierten ID.

*Warum dieser Schritt?*  
Durch das Anwenden des richtigen **number format** beim Import entfällt ein zweiter Durchlauf, der Zellen durchläuft, um das Format zu ändern. Außerdem wird sichergestellt, dass **format excel cells date** und **set currency format excel** über alle Zeilen hinweg konsistent sind.

## Schritt 5: Importieren der DataTable unter Beibehaltung der Kopfzeile

Die Methode `ImportDataTable` kann Daten kopieren, die erste Zeile als Kopfzeile behalten und die vorbereiteten Spaltenstile anwenden.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Erwartete Ausgabe** – Öffnen Sie `FormattedReport.xlsx` und Sie sehen:

| Produkt | Preis (Währung) | Veröffentlichungsdatum (Datum) |
|---------|------------------|---------------------------------|
| Widget A| $12.99           | 05/01/2023                      |
| Widget B| $23.50           | 06/15/2023                      |
| Widget C| $7.75            | 07/30/2023                      |

Die Kopfzeile bleibt erhalten, die **Price**‑Spalte zeigt das Währungssymbol an und die **ReleaseDate**‑Spalte zeigt ein kurzes Datumsformat – alles ohne zusätzlichen Stil‑Code.

### Umgang mit häufigen Randfällen

| Situation                               | Lösung |
|----------------------------------------|----------|
| **Mehr Spalten als Stile**           | Stellen Sie sicher, dass `columnStyles.Length` gleich `sourceTable.Columns.Count` ist. Fehlende Einträge verwenden den Standardstil der Arbeitsmappe. |
| **Null‑Werte in numerischen Spalten**     | Excel behandelt `null` als leere Zelle; das Zahlenformat bleibt erhalten, wenn später ein Wert eingegeben wird. |
| **Benutzerdefinierte länderspezifische Währung**    | Verwenden Sie `columnStyles[i].Custom = \"\\\"€\\\"#,##0.00"` und setzen Sie `columnStyles[i].Number = -1`, um die integrierte ID zu deaktivieren. |
| **Große Tabellen ( > 100 000 Zeilen )**    | Erwägen Sie die Verwendung der Überladung von `ImportDataTable` mit `ImportTableOptions`, um Daten zu streamen und den Speicherverbrauch zu reduzieren. |
| **Anwenden desselben Stils auf mehrere Spalten** | Verwenden Sie dieselbe `Style`‑Instanz mehrfach im Array (z. B. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Verwendung einer benutzerdefinierten Formatzeichenfolge

Wenn die integrierten IDs nicht Ihren Anforderungen entsprechen, können Sie ein benutzerdefiniertes Zahlenformat definieren:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Dieser Ansatz gibt Ihnen die volle Kontrolle über **format excel cells date** und **set currency format excel** über die vordefinierten IDs hinaus.

## Fazit

Sie wissen jetzt, wie Sie **apply number format excel** effizient beim Import einer `DataTable` mit Aspose.Cells anwenden. Durch das Erstellen eines pro Spalte‑`Style`‑Arrays, das Zuweisen integrierter oder benutzerdefinierter Zahlen‑IDs und die Verwendung der `ImportDataTable`‑Überladung, die **preserve header row excel** unterstützt, können Sie in einem einzigen Vorgang veröffentlichungsfertige Arbeitsblätter erzeugen.

### Was kommt als Nächstes?

* Erkunden Sie **set date format excel** mit benutzerdefinierten Mustern wie `"dddd, mmmm dd, yyyy"`.
* Kombinieren Sie diese Technik mit **conditional formatting**, um Werte außerhalb des Bereichs hervorzuheben.
* Verwenden Sie **format excel cells date** in Pivot‑Tabellen oder Diagrammen für dynamische Berichte.

Fühlen Sie sich frei, mit verschiedenen Zahlen‑IDs oder benutzerdefinierten Zeichenfolgen zu experimentieren, um den Style‑Guide Ihrer Organisation zu erfüllen. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [apply number format excel – Schritt‑für‑Schritt‑Leitfaden zum Formatieren von Spalten](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Excel-Arbeitsmappe erstellen C# – Währungsformat anwenden und DataTable importieren](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Datumsformat in Excel mit C# festlegen – Vollständiger Import‑Formatierungsleitfaden](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}