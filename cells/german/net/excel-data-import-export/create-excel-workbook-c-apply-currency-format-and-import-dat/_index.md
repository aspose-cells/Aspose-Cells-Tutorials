---
category: general
date: 2026-03-30
description: Erstellen Sie eine Excel-Arbeitsmappe in C# mit Währungsformatierung.
  Erfahren Sie, wie Sie eine DataTable importieren, das Zahlenformat in Excel hinzufügen
  und in wenigen Minuten das Währungsformat für eine Spalte anwenden.
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: de
og_description: Erstelle ein Excel‑Arbeitsbuch mit C# und formatiere Zellen sofort
  als Währung. Dieses Schritt‑für‑Schritt‑Tutorial zeigt, wie man eine DataTable nach
  Excel importiert und das Zahlenformat für eine Spalte hinzufügt.
og_title: Excel-Arbeitsmappe mit C# erstellen – Leitfaden zur Währungsformatierung
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel-Arbeitsmappe in C# erstellen – Währungsformat anwenden und DataTable
  importieren
url: /de/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe erstellen C# – Währungsformat anwenden und DataTable importieren

Haben Sie schon einmal **Excel-Arbeitsmappe erstellen C#** benötigt, die bereits wie ein professioneller Bericht aussieht? Vielleicht ziehen Sie Verkaufszahlen aus einer Datenbank und möchten, dass die Preisspalte als Dollar angezeigt wird, ohne Excel manuell zu bearbeiten. Kommt Ihnen das bekannt vor? Sie sind nicht allein – die meisten Entwickler stoßen auf dieses Problem, wenn sie erstmals Excel-Exporte automatisieren.

In diesem Leitfaden führen wir Sie durch eine vollständige, sofort ausführbare Lösung, die **eine Excel-Arbeitsmappe erstellt C#**, einen `DataTable` importiert und **die Preisspalte als Währung formatiert**. Am Ende haben Sie eine Datei namens `StyledTable.xlsx`, die Sie öffnen können und die schön formatierte Zahlen enthält. Keine zusätzliche Nachbearbeitung erforderlich.

> **Was Sie lernen werden**
> - Wie man Aspose.Cells in einem .NET‑Projekt einrichtet  
> - Wie man **datatable nach excel importiert** mit einem Style‑Array  
> - Wie man **Zahlenformat zu excel hinzufügt** für eine bestimmte Spalte  
> - Tipps zum Umgang mit mehr Spalten oder verschiedenen Regionen  

> **Voraussetzungen**  
> - .NET 6+ (oder .NET Framework 4.6+) installiert  
> - Aspose.Cells für .NET NuGet‑Paket (`Install-Package Aspose.Cells`)  
> - Grundlegende Kenntnisse in C# und DataTables  

---

## Schritt 1: DataTable vorbereiten (datatable nach excel importieren)

Zuerst benötigen wir einige Beispieldaten. In einer realen Anwendung würden Sie diese Tabelle wahrscheinlich aus einer Datenbankabfrage füllen, aber ein fest codiertes Beispiel hält die Sache einfach.

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*Warum das wichtig ist*: Der `DataTable` ist die Brücke zwischen Ihren Geschäftsdaten und der Excel‑Datei. Aspose.Cells kann ihn direkt importieren und dabei Spaltennamen sowie Datentypen beibehalten.

---

## Schritt 2: Neues Workbook erstellen (excel workbook c# erstellen)

Jetzt erstellen wir das eigentliche Excel‑Datei‑Objekt. Denken Sie daran wie an eine leere Leinwand, auf der Sie malen werden.

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro‑Tipp:** Wenn Sie mehrere Arbeitsblätter benötigen, rufen Sie `workbook.Worksheets.Add()` auf und geben jedem einen aussagekräftigen Namen.

---

## Schritt 3: Währungsstil definieren (Zellenformat Währung)

Aspose.Cells ermöglicht es Ihnen, ein `Style`‑Objekt zu erstellen, das beschreibt, wie Zellen aussehen sollen. Für Währungen verwenden wir das integrierte Zahlenformat‑ID 164 (`"$#,##0.00"`).

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*Warum nicht einfach die Formatzeichenkette setzen?* Die Verwendung der integrierten ID gewährleistet Kompatibilität über verschiedene Excel‑Versionen hinweg und vermeidet lokalspezifische Eigenheiten.

---

## Schritt 4: Style‑Array erstellen (Währungsformat auf Spalte anwenden)

Beim Importieren eines `DataTable` können Sie ein Array von `Style`‑Objekten übergeben – eines pro Spalte. `null` bedeutet „Standardstil verwenden“. Hier wenden wir `priceStyle` nur auf die zweite Spalte an.

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

Wenn Sie später weitere Spalten hinzufügen, erweitern Sie das Array einfach entsprechend. Die Länge von `columnStyles` muss der Anzahl der zu importierenden Spalten entsprechen, sonst wirft Aspose eine Ausnahme.

---

## Schritt 5: DataTable mit Stilen importieren (datatable nach excel importieren)

Jetzt geschieht die Magie – unser `DataTable` wird im Arbeitsblatt platziert und die Preisspalte wird sofort als Währung angezeigt.

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*Was, wenn Sie mehr als zwei Spalten haben?* Erweitern Sie einfach `columnStyles`, sodass jede Spalte den passenden Stil erhält (oder `null` für den Standard). Dies ist der sauberste Weg, **Zahlenformat zu excel hinzuzufügen** selektiv.

---

## Schritt 6: Workbook speichern (excel workbook c# erstellen)

Abschließend schreiben wir die Datei auf die Festplatte. Wählen Sie einen beliebigen Ordner, in den Sie Schreibzugriff haben.

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

Öffnen Sie `StyledTable.xlsx` in Excel und Sie sollten sehen:

| Produkt | Preis |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

Die **Preis**‑Spalte ist bereits als Währung formatiert – keine zusätzlichen Schritte erforderlich.

---

## Sonderfälle & Variationen

### Mehr Spalten, unterschiedliche Formate

Wenn Sie **Zellen als Währung formatieren** für mehrere Spalten benötigen (z. B. Kosten, Steuer, Gesamt), erstellen Sie für jede einen separaten `Style` und füllen `columnStyles` entsprechend:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### Länderspezifische Währung

Für Euro oder Britisches Pfund verwenden Sie unterschiedliche integrierte IDs (z. B. 165 für `€#,##0.00`). Alternativ können Sie eine benutzerdefinierte Formatzeichenkette setzen:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### Große Datensätze

Aspose.Cells kann Millionen von Zeilen verarbeiten, aber der Speicherverbrauch steigt mit der Anzahl der Style‑Objekte. Verwenden Sie eine einzelne `Style`‑Instanz für alle Währungsspalten, um den Speicherbedarf gering zu halten.

### Fehlende Stile

Wenn `columnStyles` kürzer ist als die Anzahl der Spalten, wendet Aspose den Standardstil auf die verbleibenden Spalten an. Das ist praktisch, wenn Sie nur an wenigen Spalten interessiert sind.

---

## Vollständiges Beispiel (Alle Schritte kombiniert)

Unten finden Sie das vollständige Programm, das Sie in eine Konsolen‑App kopieren können. Es enthält alle besprochenen Teile sowie einige hilfreiche Kommentare.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Erwartetes Ergebnis:** Beim Öffnen von `StyledTable.xlsx` wird die `Price`‑Spalte mit einem Dollarzeichen und zwei Dezimalstellen angezeigt, genau wie die Anweisung `format cells currency` verlangt.

---

## Häufig gestellte Fragen

**F: Funktioniert das mit .NET Core?**  
A: Absolut. Aspose.Cells ist .NET‑standard‑konform, sodass Sie .NET 5, .NET 6 oder später ohne Änderungen anvisieren können.

**F: Was, wenn mein DataTable 10 Spalten hat, ich aber nur Spalte 5 formatieren möchte?**  
A: Erstellen Sie ein `Style[]` mit der Länge 10, füllen Sie die Positionen 0‑4 und 6‑9 mit `null` und setzen Sie Ihren benutzerdefinierten Stil an Index 4 (nullbasiert). Aspose respektiert jeden Eintrag.

**F: Kann ich die Kopfzeile ausblenden?**  
A: Nach dem Import setzen Sie `worksheet.Cells.Rows[0].Hidden = true;` oder übergeben einfach `false` für den Parameter `includeColumnNames` in `ImportDataTable`.

---

## Fazit

Wir haben gerade **eine Excel-Arbeitsmappe erstellt C#**, einen `DataTable` importiert und **eine Währungsformat‑Spalte** mit Aspose.Cells angewendet. Die wichtigsten Schritte – Daten vorbereiten, Stil definieren, Style‑Array erstellen, mit `ImportDataTable` importieren und speichern – decken das Kernstück der meisten Excel‑Automatisierungsaufgaben ab.

Von hier aus können Sie folgendes erkunden:

- **Zahlenformat zu excel hinzufügen** für Daten oder Prozentsätze  
- Export mehrerer Arbeitsblätter in einer einzigen Datei  
- Verwendung von **format cells currency** mit länderspezifischen Symbolen  
- Automatisierung der Diagrammerstellung basierend auf denselben Daten  

Probieren Sie diese aus, und Sie werden schnell zur Ansprechperson für Excel‑Reporting in Ihrem Team. Haben Sie eine Variante, die Sie teilen möchten? Hinterlassen Sie unten einen Kommentar – happy coding!

![Excel-Arbeitsmappe erstellen C# Screenshot](image.png "Excel-Arbeitsmappe erstellen C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}