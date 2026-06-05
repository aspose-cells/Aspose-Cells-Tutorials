---
category: general
date: 2026-06-05
description: Wenden Sie Zellstile beim Import mit Aspose.Cells an. Erfahren Sie, wie
  Sie DataTable mit Formatierung importieren, Zeilen formatieren und Arbeitsblätter
  ordentlich halten.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: de
og_description: Wenden Sie Zellstile an, während Sie eine DataTable in ein Aspose.Cells-Arbeitsblatt
  importieren. Schritt‑für‑Schritt‑Anleitung mit vollständigem Code und Tipps.
og_title: Zellstile mit Aspose.Cells anwenden – DataTable importieren
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Zellstile mit Aspose.Cells anwenden – DataTable mit Formatierung importieren
url: /de/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zellstile mit Aspose.Cells anwenden – DataTable mit Formatierung importieren

Haben Sie sich jemals gefragt, wie man **Zellstile** anwendet, wenn man eine `DataTable` in ein Excel‑Blatt einfügt? Sie sind nicht allein. In vielen Reporting‑Szenarien muss die Daten sofort gut aussehen – ohne nachträgliche manuelle Formatierung. Die gute Nachricht ist, dass Aspose.Cells das **Importieren mit Formatierung** mühelos macht, sodass Ihre Zeilen rot oder blau, fett oder beliebig formatiert sein können.

In diesem Tutorial führen wir Sie durch ein vollständiges, ausführbares Beispiel, das zeigt, **wie man eine DataTable** in ein Arbeitsblatt **mit angewendeten Zellstilen** importiert. Am Ende haben Sie eine sofort ausführbare C#‑Konsolen‑App, die eine Arbeitsmappe erstellt, die ersten beiden Spalten formatiert und die Datei speichert – alles mit der `aspose cells import`‑API.

## Was Sie lernen werden

- Aspose.Cells in einem .NET‑Projekt einrichten  
- Ein Beispiel‑`DataTable` erstellen, das reale Daten nachahmt  
- `Style`‑Objekte für rote und blaue Schriftarten definieren  
- `Worksheet.Cells.ImportDataTable` verwenden, um **DataTable‑Arbeitsblatt zu importieren** und dabei die Stile anzuwenden  
- Das Ergebnis überprüfen und die Arbeitsmappe speichern  

Kein externes Werkzeug, nur reines C# und Aspose.Cells. Lassen Sie uns beginnen.

## Voraussetzungen

Bevor wir in den Code eintauchen, stellen Sie sicher, dass Sie Folgendes haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| .NET 6.0 or later | Aspose.Cells 23.x zielt auf .NET Standard 2.0+ ab, daher bietet .NET 6 die neuesten Laufzeit‑Features. |
| Aspose.Cells for .NET (NuGet) | Die Bibliothek stellt die benötigten Methoden `Workbook`, `Worksheet`, `Style` und `ImportDataTable` bereit. |
| Basic C# knowledge | Sie verstehen Klassen, Arrays und `using`‑Anweisungen. |
| An IDE (Visual Studio, VS Code, Rider) | Jeder Editor funktioniert, aber Sie müssen NuGet‑Pakete wiederherstellen. |

Sie können das Paket über die Befehlszeile installieren:

```bash
dotnet add package Aspose.Cells
```

## Schritt 1: Eine neue Arbeitsmappe erstellen und das erste Arbeitsblatt öffnen

Zuerst einmal – wir erzeugen ein `Workbook` und holen das erste Blatt. Stellen Sie sich die Arbeitsmappe als leeres Notizbuch vor; das erste Arbeitsblatt ist die Seite, auf die wir schreiben.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Pro‑Tipp:** Wenn Sie mehrere Blätter benötigen, fügen Sie sie einfach mit `wb.Worksheets.Add()` hinzu und referenzieren Sie sie per Name oder Index.

## Schritt 2: Ein Beispiel‑DataTable vorbereiten (Wie man DataTable importiert)

Jetzt benötigen wir etwas zum Importieren. In realen Projekten würden Sie eine Datenbank abfragen, aber zur Veranschaulichung erstellen wir ein `DataTable` im Speicher.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Warum das wichtig ist:** Ein `DataTable` ermöglicht es uns, den **aspose cells import**‑Ablauf ohne externe Abhängigkeiten zu testen.

## Schritt 3: Die Stile definieren, die auf die importierten Zellen angewendet werden

Hier passiert die Magie. Wir erstellen zwei `Style`‑Objekte: eines mit roter Schrift, ein anderes mit blauer Schrift. Diese werden beim Import spaltenweise angewendet.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Achtung:** Die Länge von `importStyles` muss der Anzahl der zu importierenden Spalten entsprechen, sonst wirft Aspose eine `ArgumentException`.

## Schritt 4: Das DataTable in das Arbeitsblatt **mit Formatierung** importieren

Jetzt fügen wir alles zusammen. Die von uns verwendete Überladung von `ImportDataTable` akzeptiert das `Style[]`‑Array, sodass wir **Zellstile** anwenden können, sobald die Daten im Blatt landen.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Wie es funktioniert

1. **Kopfzeilen** – Da wir `true` übergeben haben, schreibt Aspose „Name“ und „Score“ in die erste Zeile.  
2. **Datenzeilen** – Jede nachfolgende Zeile erhält den entsprechenden Stil aus `importStyles`.  
3. **Performance** – Die Methode streamt die Daten direkt in das Arbeitsblatt, was schneller ist als das zeilenweise Durchlaufen jeder Zelle.

## Schritt 5: Das Ergebnis überprüfen und die Arbeitsmappe speichern

Werfen wir einen Blick auf die ersten paar Zellen, um sicherzustellen, dass die Stile übernommen wurden, und schreiben dann die Datei auf die Festplatte.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Wenn Sie **StyledImport.xlsx** öffnen, sehen Sie:

- Die Spalte „Name“ in **rotem** Text.  
- Die Spalte „Score“ in **blauem** Text.  
- Spaltenüberschriften im Standardstil (Sie könnten sie ebenfalls formatieren, aber das ist ein weiteres Tutorial).

![Apply cell styles example](https://example.com/images/apply-cell-styles.png "Apply cell styles in Aspose.Cells")

> **Hinweis:** Das obige Bild zeigt das endgültige Aussehen. Das `alt`‑Attribut enthält das Haupt‑Keyword und erfüllt die SEO‑Anforderungen.

## Häufige Fragen & Sonderfälle

### Was, wenn mein DataTable mehr Spalten als Stile hat?

Aspose wendet den letzten Stil im Array auf alle zusätzlichen Spalten an. Um unerwartete Farben zu vermeiden, sollten Sie stets die Array‑Länge an die Spaltenanzahl anpassen oder `null` für Spalten übergeben, die Sie nicht formatieren möchten.

### Kann ich unterschiedliche Stile auf bestimmte Zeilen anwenden?

Absolut. Nach dem Import können Sie über die Zeilen iterieren und neue `Style`‑Objekte basierend auf Bedingungen zuweisen (z. B. Scores > 90 in Grün hervorheben). Hier ein kurzer Ausschnitt:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Funktioniert das mit großen Datensätzen?

Ja. `ImportDataTable` streamt Daten effizient, und das Anwenden eines statischen Stil‑Arrays verursacht nur geringen Overhead. Bei Millionen von Zeilen sollten Sie `ImportDataTable` in Teilen verwenden oder `Cells.ImportDataTable` mit einem `DataReader` nutzen, um den Speicherverbrauch weiter zu reduzieren.

### Wie bewahre ich vorhandene Formatierungen im Arbeitsblatt?

Wenn der Zielbereich bereits Formatierungen enthält, die Sie behalten möchten, setzen Sie den Parameter `importOptions` der `ImportDataTable`‑Überladung (`ImportTableOptions`) und passen `ImportDataTableOptions.PreserveCellFormatting` an. Das Standardverhalten überschreibt Stile mit den von Ihnen bereitgestellten.

## Zusammenfassung: Was wir erreicht haben

- **Zellstile angewendet** während einer **aspose cells import**‑Operation.  
- **Import mit Formatierung** demonstriert, indem ein `Style[]`‑Array übergeben wurde.  
- **Wie man eine DataTable** in ein Arbeitsblatt importiert und das Ergebnis speichert, gezeigt.  
- Sonderfälle behandelt, wie nicht übereinstimmende Stil‑Anzahlen und bedingte Zeilenformatierung.

All dies wurde in einer einzigen, eigenständigen Konsolen‑App umgesetzt – ohne externe Skripte, ohne manuelles Excel‑Herumfummeln. Sie haben nun eine solide Basis für jedes Reporting‑ oder Daten‑Export‑Feature, das ein professionell formatiertes Excel‑Ergebnis benötigt.

## Nächste Schritte

Bereit für den nächsten Schritt? Hier sind einige Ideen, die auf dem Gelernten aufbauen:

- **Die Kopfzeile formatieren** (z. B. fett, Hintergrundfarbe).  
- **Bedingte Formatierung anwenden** mit `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **In andere Formate exportieren** wie CSV oder PDF mit `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Mehrere DataTables** zu einer einzigen Arbeitsmappe kombinieren, jeweils auf einem eigenen Blatt, mit demselben Stil‑Ansatz.

Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar oder prüfen Sie die offizielle Aspose‑Dokumentation zu `ImportDataTable`. Viel Spaß beim Programmieren und genießen Sie die wunderschön formatierten Excel‑Dateien!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren Projekten zu erkunden.

- [Wie man DataTable in Excel mit Aspose.Cells für .NET importiert (Schritt‑für‑Schritt‑Anleitung)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Wie man Schriftarten in Excel mit Aspose.Cells für .NET festlegt (Schritt‑für‑Schritt‑Anleitung)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [Wie man Textschatten in Excel mit Aspose.Cells .NET anwendet: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}