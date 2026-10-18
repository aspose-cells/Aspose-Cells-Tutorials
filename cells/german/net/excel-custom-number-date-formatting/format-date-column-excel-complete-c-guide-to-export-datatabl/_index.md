---
category: general
date: 2026-07-13
description: Datums‑Spalte in Excel formatieren, während eine DataTable aus C# exportiert
  wird. Lernen Sie, wie Sie DataTables in Excel exportieren und DataTables mit Formatierung
  in Excel importieren – in wenigen Minuten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: de
lastmod: 2026-07-13
og_description: Datums‑Spalte in Excel mühelos formatieren. Dieser Leitfaden zeigt
  Ihnen, wie Sie eine DataTable in C# nach Excel exportieren und eine DataTable mit
  benutzerdefinierten Stilen nach Excel importieren.
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: Datums‑Spalte in Excel formatieren – Schritt‑für‑Schritt C#‑Export‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Datums‑Spalte in Excel formatieren – Vollständiger C#‑Leitfaden zum Export
  einer DataTable
url: /de/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datums‑Spalte in Excel formatieren – Vollständige C#‑Anleitung zum Exportieren von DataTable

Haben Sie jemals die **format date column Excel** benötigt, wenn Sie Daten aus einer Datenbank ziehen, aber die Zellen zeigten nur rohe Zeitstempel? Sie sind nicht der Einzige. In vielen Business‑Apps gibt der Standard‑Export einen `DateTime`‑Wert wie `2024‑03‑15 00:00:00` aus und niemand will dieses Durcheinander.  

Die gute Nachricht ist, dass Sie das genaue Aussehen jeder Spalte direkt aus C# steuern können. In diesem Tutorial führen wir Sie durch eine End‑to‑End‑Lösung, die **excel export datatable c#** verwendet, einen Datumsstil auf die erste Spalte anwendet, einen Währungsstil auf die zweite und schließlich **import datatable to excel** mit müheloser Formatierung.

Am Ende haben Sie eine wiederverwendbare Methode, die Sie in jedes .NET‑Projekt einbinden können, egal ob Sie .NET 6, .NET Framework 4.8 oder eine neuere Version verwenden.

---

## Was Sie benötigen

- **Aspose.Cells for .NET** (oder jede Bibliothek, die `CreateStyle` und `ImportDataTable` bereitstellt). Die Code‑Snippets verwenden Aspose, weil seine API sauber und weit verbreitet ist.
- Eine **DataTable**, die Sie bereits aus SQL, CSV oder einer anderen Quelle befüllen.
- Visual Studio (oder Ihre bevorzugte IDE).  
- .NET‑Runtime 5.0+ (das Beispiel zielt auf .NET 6, aber ältere Frameworks funktionieren genauso).

Falls Sie Aspose.Cells noch nicht haben, holen Sie sich eine kostenlose Testversion von der offiziellen Website – keine Kreditkarte erforderlich.

---

## Schritt 1: Die Quelldaten als DataTable abrufen

Zuerst benötigen Sie eine `DataTable`. In realen Szenarien kommt diese normalerweise von `SqlDataAdapter.Fill`, aber zur Veranschaulichung erstellen wir eine einfache Tabelle:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **Pro‑Tipp:** Wenn Sie Daten direkt aus einer Stored Procedure holen, stellen Sie sicher, dass die Spaltentypen den beabsichtigten Excel‑Formaten entsprechen. Eine `datetime`‑Spalte wird später das Ziel für unseren **format date column excel**‑Stil sein.

## Schritt 2: Ein Excel‑Workbook erstellen und Spaltenstile definieren

Jetzt erstellen wir ein neues Workbook. Der Trick für **format date column excel** besteht darin, ein `Style`‑Objekt zu erzeugen, dessen `Number`‑Eigenschaft auf das integrierte Excel‑Datumsformat (Code 14) zu setzen und diesen Stil dem entsprechenden Spaltenindex zuzuweisen.

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

Warum `Number = 14`? Excel speichert Daten als Seriennummern; Format 14 weist das Programm an, diese Zahlen mit dem kurzen Datumsformat der jeweiligen Locale darzustellen. Wenn Sie ein benutzerdefiniertes Muster benötigen (z. B. `dd‑MMM‑yyyy`), könnten Sie stattdessen `columnStyles[0].Custom = "dd-MMM-yyyy"` setzen.

## Schritt 3: Die DataTable mit Stilen in das Arbeitsblatt importieren

Mit dem fertiggestellten Stil‑Array ist der Importaufruf eine einzige Zeile. Das ist das Herzstück von **excel export datatable c#** und zugleich die Stelle, an der wir **import datatable to excel** durchführen und dabei unsere Formatierung beibehalten.

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

Die von uns verwendete Überladung von `ImportDataTable` akzeptiert das Stil‑Array und wendet jeden Stil auf die entsprechende Spalte an, während die Daten geschrieben werden. Keine nachträgliche Schleife nötig – Ihre Datumsspalte ist bereits schön formatiert.

## Schritt 4: Das Workbook speichern (oder direkt an den Browser streamen)

Je nach Szenario können Sie das Workbook auf Festplatte, in einen Memory‑Stream oder als HTTP‑Antwort zurückgeben. Hier sind drei gängige Muster:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **Achtung:** Wenn Sie `FileResult` in ASP.NET Core verwenden, stellen Sie sicher, dass Sie `Response.Headers["Cache-Control"] = "no-cache"` setzen, wenn die Datei on‑the‑fly erzeugt wird. Das verhindert, dass der Browser eine veraltete Version ausliefert.

## Schritt 5: Ergebnis überprüfen – Wie das Excel‑Blatt aussieht

Nachdem Sie den Code ausgeführt haben, öffnen Sie `ExportedReport.xlsx`. Sie sollten folgendes sehen:

| Bestelldatum (formatiert) | Gesamtbetrag (Währung) | Kunde |
|---------------------------|------------------------|-------|
| 03/13/2024                | $1,245.67              | Acme Corp|
| 03/14/2024                | $980.00                | Beta Ltd |
| 03/15/2024                | $1,500.25              | Gamma Inc|

Beachten Sie, dass **format date column excel** ein sauberes Kurzdatum anzeigt, während die Währungsspalte sich automatisch an Ihre regionalen Einstellungen anpasst. Keine manuelle Zell‑für‑Zell‑Formatierung nötig.

![format date column excel example](/images/format-date-column-excel.png)

*Bildbeschreibung: format date column excel – ein Screenshot des Excel‑Blatts mit einer korrekt formatierten Datumsspalte.*

---

## Häufige Fragen & Sonderfälle

### Was, wenn meine DataTable mehr als drei Spalten hat?

Erweitern Sie einfach das `columnStyles`‑Array. Für jede Spalte, die Sie nicht explizit formatieren, lassen Sie den Eintrag `null`; Excel verwendet dann das Standard‑General‑Format.

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### Wie wende ich ein benutzerdefiniertes Datumsformat an (z. B. „dd‑MMM‑yyyy“) ?

Ersetzen Sie die integrierte Nummer durch einen benutzerdefinierten String:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### Kann ich diesen Ansatz mit EPPlus oder ClosedXML verwenden?

Ja, das Konzept ist identisch: ein Stil‑Objekt erstellen, es einer Spalte zuweisen und dann die `DataTable` laden. Die API unterscheidet sich, aber das **excel export datatable c#**‑Muster bleibt gleich.

### Wie sieht es mit großen Datensätzen (100 k+ Zeilen) aus?

`ImportDataTable` ist für Massenschreibvorgänge optimiert, aber Sie könnten an Speichergrenzen stoßen. In diesem Fall sollten Sie in Erwägung ziehen, Zeilen in Stücke zu streamen mit `Cells.ImportDataTable`, oder `Worksheet.Cells["A1"].PutValue` in einer Schleife zu verwenden und dabei die Stil‑Objekte wiederzuverwenden.

---

## Vollständiges funktionierendes Beispiel (alle Schritte in einer Methode)

Unten finden Sie eine eigenständige Methode, die Sie in jede Konsolen‑App oder jeden ASP.NET‑Controller kopieren können. Sie demonstriert den gesamten Ablauf – von der Datenabfrage bis zum formatierten Excel‑Export.

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

Führen Sie das Programm aus, öffnen Sie `StyledExport.xlsx` und Sie werden sehen, dass **format date column excel** perfekt angewendet wurde.

---

## Zusammenfassung & nächste Schritte

Wir haben gerade behandelt, wie man **format date column excel** beim **excel export datatable c#** anwendet und wie man **import datatable to excel** mit spaltenbezogener Formatierung in einem einzigen Aufruf durchführt. Die wichtigsten Erkenntnisse:

1. Erstellen Sie für jede zu formatierende Spalte ein `Style`.
2. Verwenden Sie `Number = 14` für Daten, `Number = 2` für Währungen oder jedes gewünschte benutzerdefinierte Format.
3. Übergeben Sie das Stil‑Array an `ImportDataTable` – die Bibliothek übernimmt die schwere Arbeit.

Was könnten Sie als Nächstes erkunden?

- **Conditional formatting** zum Hervorheben überfälliger Daten.  
- **

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man DataTable in Excel mit Aspose.Cells für .NET importiert (Schritt‑für‑Schritt‑Anleitung)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Excel‑Daten mit Aspose.Cells für .NET in DataTable exportieren: Ein vollständiger Leitfaden](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [HTML‑Strings aus Excel in DataTable exportieren mit Aspose.Cells für .NET: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}