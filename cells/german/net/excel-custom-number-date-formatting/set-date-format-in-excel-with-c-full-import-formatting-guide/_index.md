---
category: general
date: 2026-06-17
description: Datumsformat in Excel mit C# festlegen und außerdem den Zellenhintergrund
  setzen, Vordergrundfarbe anwenden und Excel‑Spalte beim Import färben. Schritt für
  Schritt lernen.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: de
og_description: Datumsformat in Excel mit C# festlegen, dabei Zellhintergrund setzen,
  Vordergrundfarbe anwenden und Excel‑Spalte beim Import einfärben. Vollständiges
  Tutorial.
og_title: Datumsformat in Excel mit C# festlegen – Vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: Datumsformat in Excel mit C# festlegen – Vollständiger Leitfaden zur Importformatierung
url: /de/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Datumformat in Excel mit C# – Vollständige Importformatierungsanleitung

Haben Sie jemals **das Datumsformat** in einem aus C#‑Code generierten Excel‑Blatt festlegen müssen, wollten aber gleichzeitig, dass die Spalte einen benutzerdefinierten Hintergrund oder Textfarbe hat? Sie sind nicht allein. In vielen Reporting‑Szenarien holen Sie eine `DataTable` aus einer Datenbank, fügen sie in ein Arbeitsblatt ein und kämpfen dann darum, die Daten richtig darzustellen und die Spalten mit den richtigen Farben hervorzuheben.

In diesem Tutorial führen wir Sie durch eine saubere, End‑to‑End‑Lösung, die **das Datumsformat festlegt**, **den Zellhintergrund setzt**, **die Vordergrundfarbe anwendet** und sogar **eine Excel‑Spalte färbt**, während Daten importiert werden. Am Ende haben Sie ein wiederverwendbares Muster, das **Excel‑Importformatierung** ohne das übliche Ausprobieren ermöglicht.

> **Was Sie benötigen**  
> * .NET 6+ (oder .NET Framework 4.7+)  
> * Aspose.Cells für .NET (kostenlose Testversion zum Testen)  
> * Eine `DataTable`‑Quelle – jede ADO.NET‑Abfrage reicht aus  
> * Visual Studio oder Ihre bevorzugte IDE  

Los geht's.

---

## Überblick über die Lösung

Wir teilen das Problem in drei logische Abschnitte auf:

1. **Quellendaten abrufen** – eine `DataTable` mit den Zeilen, die Sie exportieren möchten.  
2. **Spaltenspezifische Stile erstellen** – ein Stil für die Datumsspalte, ein weiterer für eine Textspalte, plus jede zusätzliche Formatierung, die Sie wünschen.  
3. **Tabelle mit Stilen importieren** – verwenden Sie `Worksheet.Cells.ImportDataTable`, sodass jede Spalte den vorbereiteten Stil erbt.

Warum dieser Ansatz? Weil Aspose.Cells es Ihnen ermöglicht, ein `Style`‑Array direkt an den Aufruf von `ImportDataTable` anzuhängen, sodass Sie keinen zweiten Durchlauf benötigen, um die Formatierung erneut anzuwenden. Es ist schneller, weniger fehleranfällig und hält Ihren Code übersichtlich.

## Schritt 1: Daten für den Export abrufen

Zuerst benötigen Sie eine `DataTable`. In einem realen Projekt würden Sie wahrscheinlich eine Stored Procedure aufrufen oder Entity Framework verwenden, um sie zu füllen, aber zur Veranschaulichung erstellen wir eine einfache Tabelle mit einer Datums‑ und einer Textspalte.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro‑Tipp:** Wenn Ihre Quelle nullable Datumswerte verwendet, stellen Sie sicher, dass der Spaltentyp `typeof(DateTime?)` ist – Aspose wird das von Ihnen später zugewiesene Format weiterhin berücksichtigen.

## Schritt 2: Ein Array von Stilen vorbereiten – eins pro Spalte

Jetzt erstellen wir ein `Style[]`, dessen Länge der Anzahl der Spalten in der `DataTable` entspricht. Jeder Eintrag enthält die Formatierung für die jeweilige Spalte.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 Datumsformat für die erste Spalte festlegen

Die erste Spalte (`OrderDate`) sollte als „MM/dd/yyyy“ angezeigt werden. Aspose verwendet den integrierten Zahlenformat‑Index 14 für das Kurzdatum, Sie können jedoch auch einen benutzerdefinierten Formatstring angeben, wenn Sie möchten.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Warum das wichtig ist:** Excel speichert Daten als Seriennummern. Durch das Zuweisen eines Zahlenformats teilen Sie Excel mit, diese Seriennummern als lesbare Daten und nicht als Rohzahlen darzustellen.

### 2.2 Zellhintergrund für die zweite Spalte festlegen

Geben wir der Spalte `CustomerName` einen hellblauen Hintergrund. Hier kommt **set cell background** zum Einsatz.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Hinweis:** Ohne das Setzen von `Pattern` auf `Solid` wird die Vordergrundfarbe nicht angezeigt, da das Standardmuster „None“ ist.

### 2.3 Vordergrundfarbe (Text) anwenden – optionales Extra

Wenn Sie möchten, dass der Text selbst eine kontrastierende Farbe hat, können Sie denselben Stil anpassen:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Damit wird die Anforderung **apply foreground color** erfüllt, während der Hintergrund der Spalte erhalten bleibt.

## Schritt 3: DataTable mit den definierten Stilen importieren

Mit den Stilen bereit, besteht der letzte Schritt aus einer einzigen Zeile, die die Daten importiert und die Stile spaltenweise anwendet.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Wie es funktioniert:** Aspose liest das `columnStyles`‑Array und ordnet jedes `Style` dem entsprechenden Spaltenindex zu. Die Kopfzeile erbt den Standardstil, es sei denn, Sie stellen einen separaten Stil für Zeile 0 bereit.

### 3.1 Arbeitsmappe speichern

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Führen Sie das Programm aus, öffnen Sie *FormattedReport.xlsx*, und Sie sollten sehen:

- **OrderDate**‑Spalte wird als Datum angezeigt (z. B. `06/15/2026`).  
- **CustomerName**‑Spalte mit hellblauer Füllung und dunkelblauem Text.  

Das ist der gesamte **excel import formatting**‑Arbeitsablauf in weniger als 30 Zeilen C#.

## Schritt‑für‑Schritt‑Zusammenfassung (mit Warum)

| Schritt | Was Sie tun | Warum es wichtig ist |
|---------|-------------|----------------------|
| **Daten abrufen** | Rufen Sie `GetData()` auf, um eine `DataTable` zu füllen. | Stellt eine strukturierte Quelle bereit, die Aspose direkt einlesen kann. |
| **Stil‑Array erstellen** | Allozieren Sie `Style[]`, passend zur Spaltenanzahl. | Ermöglicht spaltenweise Formatierung in einem einzigen Importaufruf. |
| **Datumsformat festlegen** | `columnStyles[0].Number = 14;` | Stellt sicher, dass Daten in Excel korrekt dargestellt werden. |
| **Hintergrundfarbe festlegen** | `ForegroundColor = LightBlue; Pattern = Solid;` | Hebt die Spalte hervor und erfüllt **set cell background**. |
| **Vordergrundfarbe anwenden** | `Font.Color = DarkBlue;` | Verbessert die Lesbarkeit und erfüllt **apply foreground color**. |
| **Import mit Stilen** | `ImportDataTable(..., columnStyles);` | Ein‑Durchlauf‑Import, der alle Formatierungen berücksichtigt. |
| **Arbeitsmappe speichern** | `wb.Save(...);` | Speichert das Ergebnis für nachgelagerte Benutzer. |

## Umgang mit Sonderfällen & häufigen Fragen

### Was ist, wenn ich mehr als zwei Spalten habe?

Erweitern Sie einfach das `columnStyles`‑Array und weisen Sie jedem Index, den Sie benötigen, einen `Style` zu. Nicht zugewiesene Indizes fallen auf den Standardstil zurück, was völlig in Ordnung ist.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Wie formatiere ich eine Spalte als Währung?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Kann ich den Stil der Kopfzeile separat ändern?

Ja. Nach dem Import können Sie die erste Zeile holen und einen eigenen Stil anwenden:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### Was ist, wenn die DataTable null‑Datumswerte enthält?

Aspose lässt diese Zellen leer. Wenn Sie einen Platzhalter wie „N/A“ bevorzugen, können Sie die Tabelle vorverarbeiten:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Dann passen Sie den Stil an, um ein benutzerdefiniertes Format anzuzeigen, das „N/A“ für den Sentinel‑Wert darstellt.

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige, sofort kopier‑fertige Programm. Führen Sie es als Konsolenanwendung aus, und Sie erhalten eine schön formatierte Excel‑Datei.

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelExportDemo
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook & style array
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 2a️⃣ Date column – set date format
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date (MM/dd/yyyy)

        // 2b️⃣ Text column – set background & foreground colors
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].ForegroundColor = Color.LightBlue;
        columnStyles[1].Pattern = BackgroundType.Solid;
        columnStyles[1].Font.Color = Color.DarkBlue; // apply foreground color

        // 3️⃣ Import with formatting
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Optional: style header row
        Style headerStyle = wb.CreateStyle();
        headerStyle.Font.IsBold = true;
        headerStyle.ForegroundColor = Color.Gold;
        headerStyle.Pattern = BackgroundType.Solid;
        ws.Cells


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Schriftfarbe in Excel‑Zellen mit Aspose.Cells für .NET festlegen](/cells/english/net/formatting/setting-font-color/)
- [Schriftfarbe in .NET‑Excel mit Aspose.Cells festlegen](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Excel‑Spaltenbreiten in Pixeln mit Aspose.Cells für .NET festlegen | Schritt‑für‑Schritt‑Anleitung](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}