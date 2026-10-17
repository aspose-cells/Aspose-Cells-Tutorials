---
category: general
date: 2026-02-15
description: Erstelle ein Arbeitsbuch in C# und exportiere eine DataTable nach Excel
  mit Zeilenformatierung, setze den Zeilenhintergrund und automatisiere Excel‑Aufgaben
  in Minuten.
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: de
og_description: Erstellen Sie schnell ein C#‑Arbeitsbuch, wenden Sie Zeilenstile an
  und automatisieren Sie den Excel‑Export mit vollständigen Codebeispielen und Best‑Practice‑Tipps.
og_title: Arbeitsmappe erstellen in C# – DataTable nach Excel mit Formatierung exportieren
tags:
- C#
- Excel
- DataExport
title: Arbeitsmappe erstellen in C# – DataTable mit Formatierung nach Excel exportieren
url: /de/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Arbeitsmappe erstellen C# – DataTable nach Excel exportieren mit Formatierung

Haben Sie jemals **eine Arbeitsmappe in C# erstellen** und eine `DataTable` mit benutzerdefiniertem Styling nach Excel exportieren müssen? Sie sind nicht allein. In vielen Business‑Anwendungen besteht die Anforderung, ein schön formatiertes Tabellenblatt auszugeben, das ein nicht‑technischer Benutzer sofort öffnen und verstehen kann.  

In diesem Leitfaden gehen wir Schritt für Schritt durch eine vollständige, sofort ausführbare Lösung, die Ihnen zeigt, **wie man eine Arbeitsmappe in C# erstellt**, **Excel‑Export‑Formatierung** anwendet, einen **Zeilenhintergrund** festlegt und **Excel‑Automation C#** nutzt, um eine professionell aussehende Datei zu erzeugen. Keine vagen „Siehe die Dokumentation“-Abkürzungen – nur der komplette Code, Erklärungen, warum jede Zeile wichtig ist, und Tipps, die Sie bereits morgen einsetzen können.

---

## Voraussetzungen

- .NET 6 (oder .NET Framework 4.6+).  
- Visual Studio 2022 oder jede C#‑kompatible IDE.  
- Das **Aspose.Cells for .NET** NuGet‑Paket (oder jede Bibliothek, die `Workbook`, `Worksheet`, `Style` bereitstellt).  
- Grundlegende Kenntnisse von `DataTable`.  

Falls Sie Aspose.Cells noch nicht haben, führen Sie aus:

```bash
dotnet add package Aspose.Cells
```

> **Pro Tipp:** Die kostenlose Testversion funktioniert für die meisten Entwicklungsszenarien; denken Sie nur daran, den Lizenzschlüssel vor dem Ausliefern zu ersetzen.

![Beispiel für das Erstellen einer Arbeitsmappe C# mit formatierten Zeilen in Excel]( "Beispiel für das Erstellen einer Arbeitsmappe C# mit Zeilenhintergrundfarben")

---

## Schritt 1: Initialisieren der Arbeitsmappe und des Arbeitsblatts (Arbeitsmappe erstellen C#)

Das erste, was Sie tun müssen, ist ein `Workbook` zu instanziieren. Stellen Sie sich das vor wie das Öffnen einer brandneuen Excel‑Datei im Speicher.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Warum?**  
`Workbook` enthält das gesamte Excel‑Dokument, während `Worksheet` ein einzelnes Tabellenblatt darstellt. Mit einer leeren Arbeitsmappe zu beginnen, stellt sicher, dass Sie jeden Aspekt der Ausgabe kontrollieren – keine versteckten Standardstile, die sich einschleichen.

---

## Schritt 2: Erstellen einer Beispiel‑DataTable (DataTable nach Excel exportieren)

In einem echten Projekt würden Sie Daten aus einer Datenbank holen, aber zur Veranschaulichung erstellen wir eine kleine `DataTable` im laufenden Betrieb.

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Warum das wichtig ist:**  
Der Export einer `DataTable` ist die gängigste Methode, tabellarische Daten aus einer Anwendung nach Excel zu übertragen. Die oben gezeigte Methode ist vollständig eigenständig, sodass Sie sie in jedes Projekt kopieren‑und‑einfügen können und sie funktioniert.

---

## Schritt 3: Erstellen eines Stils pro Zeile (Excel‑Export‑Formatierung)

Um jeder Zeile eine eigene Hintergrundfarbe zu geben, erzeugen wir für jede Zeile der `DataTable` ein `Style`‑Objekt. Hier kommt die **Excel‑Export‑Formatierung** zum Einsatz.

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Warum Styling pro Zeile?**  
Wenn Sie bestimmte Datensätze hervorheben müssen (z. B. überfällige Rechnungen), können Sie den einfachen Farbzirkus durch bedingte Logik ersetzen – setzen Sie einfach `style.ForegroundColor` basierend auf den Daten der Zeile.

---

## Schritt 4: Importieren der DataTable mit Zeilenstilen (Zeilenhintergrund festlegen)

Jetzt fügen wir alles zusammen: die Daten, die Arbeitsmappe und die Stile.

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**Was Sie sehen werden:**  
Beim Öffnen von `EmployeesReport.xlsx` sehen Sie eine Kopfzeile mit Standardformatierung, gefolgt von vier Datenzeilen, die jeweils mit einer hellen Hintergrundfarbe versehen sind. Das Ergebnis sieht aus wie ein handgefertigter Bericht, nicht wie ein fade Dump.

---

## Schritt 5: Fortgeschrittene Excel‑Automation‑C#‑Tipps (Excel Automation C#)

Im Folgenden finden Sie einige schnelle Tricks, die Sie auf das Grundbeispiel anwenden können:

| Tipp | Code‑Snippet | Wann zu verwenden |
|-----|--------------|-------------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | Nach dem Importieren der Daten, um abgeschnittenen Text zu vermeiden. |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | Wenn die Tabelle über den Bildschirm hinaus scrollen kann. |
| **Conditional Formatting** | <details><summary>Anzeigen</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | Gehälter über einem Schwellenwert hervorheben. |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | Wenn Sie schreibgeschützte Berichte benötigen. |

Diese Snippets zeigen die Bandbreite von **excel automation c#** – Sie können die Arbeitsmappe weiter ausbauen, ohne die Kern‑Import‑Logik neu zu schreiben.

---

## Häufige Fragen & Sonderfälle

**Was, wenn die DataTable tausende Zeilen enthält?**  
Aspose.Cells streamt Daten effizient, aber Sie könnten die Erstellung von Stilen für jede Zeile deaktivieren, um Speicher zu sparen. Stattdessen wenden Sie einen einzigen Stil auf einen Bereich an:

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**Kann ich stattdessen nach .csv exportieren statt .xlsx?**  
Natürlich – ändern Sie einfach das Speicherformat:

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

Das Styling geht dabei verloren (CSV unterstützt kein Styling), aber der Datenexport bleibt gleich.

**Funktioniert das unter .NET Core?**  
Ja. Aspose.Cells unterstützt .NET Standard 2.0 und höher, sodass derselbe Code unter .NET 6, .NET 7 oder .NET Framework läuft.

---

## Vollständiges funktionierendes Beispiel (Kopieren‑Einfügen bereit)

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}