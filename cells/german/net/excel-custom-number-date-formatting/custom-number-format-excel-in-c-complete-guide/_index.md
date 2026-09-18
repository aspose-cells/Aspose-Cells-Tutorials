---
category: general
date: 2026-03-22
description: Anleitung zum benutzerdefinierten Zahlenformat in Excel, die zeigt, wie
  man eine Datentabelle nach Excel importiert, die Hintergrundfarbe einer Spalte festlegt,
  die Spalte als Währung formatiert und die Arbeitsmappe als xlsx speichert.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: de
og_description: Excel‑Tutorial zum benutzerdefinierten Zahlenformat, das Sie Schritt
  für Schritt durch das Importieren einer DataTable, das Festlegen der Hintergrundfarbe
  einer Spalte, das Formatieren einer Spalte als Währung und das Speichern der Arbeitsmappe
  als xlsx führt.
og_title: Benutzerdefiniertes Zahlenformat in Excel mit C# – Schritt‑für‑Schritt‑Anleitung
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: Benutzerdefiniertes Zahlenformat in Excel mit C# – Vollständiger Leitfaden
url: /de/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzerdefiniertes Zahlenformat Excel – Full‑Stack C# Tutorial

Haben Sie sich jemals gefragt, wie man einen **custom number format excel** Stil direkt aus C# anwendet? Vielleicht haben Sie versucht, eine DataTable in ein Tabellenblatt zu exportieren, nur um reine Zahlen zu sehen, keine Farben und keine Währungsformatierung. Das ist ein häufiges Problem – besonders wenn Sie einen professionellen Bericht für Stakeholder benötigen.

In diesem Leitfaden werden wir dieses Problem gemeinsam lösen: Sie lernen, wie man **import datatable to excel**, **set column background color**, **format column as currency** und schließlich **save workbook as xlsx** mit einem benutzerdefinierten Zahlenformat, das Ihre Zahlen hervorhebt. Keine vagen Hinweise, nur eine vollständige, ausführbare Lösung, die Sie in Ihr Projekt kopieren‑und‑einfügen können.

---

## Was Sie bauen werden

Am Ende dieses Tutorials haben Sie eine eigenständige C# Konsolenanwendung, die:

1. Ruft eine `DataTable` ab (Sie können den Stub durch Ihre eigene Abfrage ersetzen).  
2. Erstellt ein neues Excel‑Arbeitsbuch mit Aspose.Cells (oder einer beliebigen kompatiblen Bibliothek).  
3. Wendet eine blaue, fette Schrift auf die erste Spalte an, einen hellgelben Hintergrund auf die zweite und ein Währungsformat (`$#,##0.00`) auf die dritte.  
4. Speichert die Datei als `DataTableWithStyleArray.xlsx` in einem von Ihnen gewählten Ordner.

Sie sehen genau, wie jede Zeile zur endgültigen Excel‑Datei beiträgt, und wir diskutieren, warum diese Entscheidungen für Wartbarkeit und Performance wichtig sind.

---

## Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+).  
- Aspose.Cells für .NET (Testversion oder lizenzierte Version). Installation über NuGet:

```bash
dotnet add package Aspose.Cells
```

- Grundlegende Kenntnisse von `DataTable` und C# Konsolenanwendungen.

---

## Schritt 1: Abrufen der Quelldaten als DataTable

Zuerst benötigen wir einige Daten zum Exportieren. In einem realen Szenario würden Sie wahrscheinlich ein Repository aufrufen oder eine SQL‑Abfrage ausführen. Zur Veranschaulichung erstellen wir eine einfache Tabelle im Speicher.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Warum das wichtig ist:** Die Verwendung einer `DataTable` liefert eine tabellarische, schema‑bewusste Quelle, die sauber auf Excel‑Zeilen und -Spalten abgebildet werden kann. Sie ermöglicht es Ihnen außerdem, dieselbe Exportlogik für jedes Dataset wiederzuverwenden, ohne den Code neu zu schreiben.

---

## Schritt 2: Erstellen eines neuen Arbeitsbuchs und Abrufen des ersten Arbeitsblatts

Jetzt erstellen wir ein Excel‑Arbeitsbuch. Die Klasse `Workbook` repräsentiert die gesamte Datei; ihr `Worksheets[0]` ist das Standard‑Blatt, in das wir unsere Daten einfügen werden.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro Tipp:** Wenn Sie mehrere Blätter benötigen, rufen Sie einfach `workbook.Worksheets.Add("SheetName")` auf und wiederholen die Formatierungsschritte für jedes.

---

## Schritt 3: Definieren von Spaltenstilen – Schrift, Hintergrund und Zahlenformat

Das Styling in Aspose.Cells erfolgt über `Style`‑Objekte. Wir erstellen ein Array, bei dem jedes Element einer Spalte in der DataTable entspricht.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Warum ein Stil‑Array?** Das Übergeben eines Arrays an `ImportDataTable` ermöglicht es, jedem Spalten in einem einzigen Aufruf einen eigenen Stil zuzuweisen, was sowohl kompakt als auch performant ist. Es stellt zudem sicher, dass die Formatierung mit der Datenreihenfolge synchron bleibt.

---

## Schritt 4: Importieren der DataTable unter Anwendung der Stile

Hier ist das Kernstück der Operation: Wir übergeben die `DataTable` an das Arbeitsblatt, weisen Aspose an, die Kopfzeile einzuschließen, und übergeben unser `columnStyles`‑Array.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Was im Hintergrund passiert:** Aspose iteriert durch jede Spalte, schreibt die Kopfzeile und anschließend jede Zeilenwert. Dabei wendet es den entsprechenden `Style` aus dem Array an, sodass Sie eine blaue Kopfzeile für „Product“, eine gelb schattierte „Quantity“ und eine schön formatierte „Revenue“-Spalte erhalten.

---

## Schritt 5: Speichern des Arbeitsbuchs als XLSX‑Datei

Abschließend speichern wir das Arbeitsbuch auf dem Datenträger. Die Methode `Save` wählt automatisch das XLSX‑Format basierend auf der Dateierweiterung.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **Tipp:** Wenn Sie die Datei streamen müssen (z. B. für eine Web‑API), verwenden Sie `workbook.Save(stream, SaveFormat.Xlsx)` anstelle eines Dateipfads.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette Programm, das Sie in ein neues Konsolenprojekt einfügen können. Es kompiliert und läuft unverändert und erzeugt eine formatierte Excel‑Datei.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Erwartetes Ergebnis

Wenn Sie `DataTableWithStyleArray.xlsx` öffnen, sehen Sie:

| **Product** (blau, fett) | **Quantity** (hellgelb) | **Revenue** (Währung) |
|--------------------------|--------------------------|------------------------|
| Widget A                 | 120                      | $3,450.75              |
| Widget B                 | 85                       | $2,190.00              |
| Widget C                 | 60                       | $1,580.40              |

Das **custom number format excel**, das Sie angegeben haben (`$#,##0.00`), sorgt dafür, dass jede Umsatzzelle ein Dollarzeichen, ein Tausendertrennzeichen und zwei Dezimalstellen anzeigt – genau das, was Finanzteams erwarten.

---

## Häufig gestellte Fragen & Sonderfälle

### Kann ich das mit einer anderen Excel‑Bibliothek verwenden?

Absolut. Das Konzept – für jede Spalte einen Stil zu erstellen und ihn beim Import anzuwenden – lässt sich auf EPPlus, ClosedXML oder NPOI übertragen. Die API‑Aufrufe unterscheiden sich, aber das Muster bleibt gleich.

### Was, wenn meine DataTable mehr Spalten als Stile hat?

Aspose wendet den Standardstil auf jede Spalte an, für die kein entsprechender Eintrag im `columnStyles`‑Array vorhanden ist. Um Überraschungen zu vermeiden, passen Sie die Größe des Arrays an `dataTable.Columns.Count` an oder erzeugen Sie Stile dynamisch in einer Schleife.

### Wie setze ich ein benutzerdefiniertes Zahlenformat für Datumsangaben?

Setzen Sie einfach `style.Custom = "dd‑mm‑yyyy"` (oder eine beliebige gültige Excel‑Formatzeichenfolge). Der gleiche array‑basierte Ansatz funktioniert für Datumsangaben, Prozentsätze oder wissenschaftliche Notation.

### Gibt es eine Möglichkeit, Spalten nach dem Import automatisch zu skalieren?

Ja – rufen Sie nach dem Import `worksheet.AutoFitColumns();` auf. Es führt eine schnelle Breitenberechnung basierend auf dem Zelleninhalt durch.

### Was ist mit großen Datensätzen (100 k+ Zeilen)?

`ImportDataTable` ist für Bulk‑Operationen optimiert, aber Sie könnten Speichergrenzen erreichen. In diesem Fall sollten Sie erwägen, Zeilen manuell mit `Cells[i, j].PutValue(...)` zu streamen und ein einzelnes `Style`‑Objekt wiederzuverwenden, um den Overhead zu reduzieren.

---

## Pro‑Tipps & häufige Fallstricke

- **Vermeiden Sie das Hard‑Coding von Pfaden** im Produktionscode; verwenden Sie `Environment.GetFolderPath` oder Konfigurationseinstellungen.  
- **Entsorgen Sie das Arbeitsbuch**, wenn Sie in einem langlaufenden Service sind – wickeln Sie es in einen `using`‑Block, um native Ressourcen freizugeben.  
- **Achten Sie auf kulturspezifische Trennzeichen**. Das benutzerdefinierte Format `$#,##0.00` erzwingt einen Punkt als Dezimaltrennzeichen, unabhängig von der OS‑Locale, was für Finanzberichte in der Regel gewünscht ist.  
- **Denken Sie daran, System.Drawing zu referenzieren** (oder `System.Drawing.Common` unter .NET Core) für die Farb‑Structs, die beim Styling verwendet werden.  
- **Testen Sie die Ausgabe in verschiedenen Excel‑Versionen**; ältere Versionen könnten einige benutzerdefinierte Formate leicht anders interpretieren.

---

## Fazit

Wir haben alles behandelt, was Sie benötigen, um **custom number format excel** Dateien aus C# zu erstellen: Daten aus einer `DataTable` holen, **import datatable to excel**, eine **set column background color** anwenden, **format column as currency** verwenden und schließlich **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}