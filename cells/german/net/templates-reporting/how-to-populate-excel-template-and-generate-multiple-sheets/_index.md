---
category: general
date: 2026-11-22
description: Excel‑Vorlage mit Aspose.Cells füllen, um mehrere Tabellenblätter zu
  erzeugen, das Aspose‑Arbeitsbuch speichern und einen Master‑Detail‑Bericht in C#
  erstellen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- populate excel template
- generate multiple sheets
- save aspose workbook
- generate master detail report
language: de
lastmod: 2026-11-22
og_description: Excel-Vorlage mit Aspose.Cells füllen, mehrere Arbeitsblätter erzeugen,
  Aspose-Arbeitsmappe speichern und einen Master‑Detail-Bericht in einem einzigen
  C#‑Programm erstellen.
og_image_alt: Screenshot showing a populated Excel workbook with multiple detail sheets
og_title: Excel-Vorlage ausfüllen & mehrere Arbeitsblätter mit Aspose.Cells generieren
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  headline: How to populate Excel template and generate multiple sheets with Aspose.Cells
  type: TechArticle
- description: populate excel template using Aspose.Cells to generate multiple sheets,
    save aspose workbook, and create a master‑detail report in C#.
  name: How to populate Excel template and generate multiple sheets with Aspose.Cells
  steps:
  - name: What the resulting workbook looks like
    text: '| Sheet name | Content | |------------|----------| | **Master** | Header
      row with order summary (OrderId, Customer) | | **Details_1** | All `OrderLines`
      where `OrderId = 1` (Pen, Notebook) | | **Details_2** | All `OrderLines` where
      `OrderId = 2` (Pencil) |'
  - name: Expected output
    text: 'Open `MasterDetailResult.xlsx` and you will see:'
  - name: Next steps
    text: '* Explore **SmartMarkerOptions** such as `EnableFormulaCalculation` to
      evaluate formulas after data insertion. * Add charts to the master sheet and
      let the processor update series ranges automatically. * Combine this approach
      with **Aspose.Slides** to export the same data to PowerPoint presentations'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man eine Excel‑Vorlage ausfüllt und mehrere Arbeitsblätter mit Aspose.Cells
  erzeugt
url: /de/net/templates-reporting/how-to-populate-excel-template-and-generate-multiple-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Excel‑Vorlage füllt und mehrere Arbeitsblätter mit Aspose.Cells erzeugt

Wenn Sie eine Excel‑Vorlage mit dynamischen Daten **befüllen** müssen, zeigt Ihnen dieser Leitfaden eine vollständige, sofort ausführbare Lösung. Mit der Smart‑Marker‑Engine von Aspose.Cells können Sie **mehrere Arbeitsblätter erzeugen**, das **Aspose‑Arbeitsbuch** speichern und einen vollständigen **Master‑Detail‑Bericht** ohne manuelles Kopieren oder VBA‑Makros erstellen.

Das Tutorial führt Sie durch jeden Schritt – von der Vorbereitung der Master‑Detail‑Sammlungen bis zum Speichern der endgültigen Datei – sodass Sie den Code in Ihr eigenes Projekt übernehmen und sofortige Ergebnisse sehen können.

## Voraussetzungen

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+)
* Aspose.Cells für .NET installiert (`dotnet add package Aspose.Cells`)
* Eine grundlegende C#‑Entwicklungsumgebung (Visual Studio, VS Code, Rider usw.)
* Eine Excel‑Vorlage (`MasterDetailTemplate.xlsx`), die Smart‑Marker‑Tags wie `&=Orders.OrderId` und eine Detail‑Tabelle mit `&=OrderLines` enthält.

> **Pro‑Tipp:** Bewahren Sie die Vorlage im selben Ordner wie das Projekt auf oder verwenden Sie einen absoluten Pfad, um `FileNotFoundException` zu vermeiden.

## Überblick über die Lösung

1. **Master‑Detail‑Datenkollektionen vorbereiten** – die Quellobjekte, die den Bericht speisen.  
2. **Die Excel‑Vorlage laden**, die bereits Smart‑Marker‑Platzhalter enthält.  
3. **Einen `SmartMarkerProcessor` erstellen**, um die Marker zu interpretieren.  
4. **Die Daten anwenden** und Aspose.Cells **automatisch mehrere Arbeitsblätter erzeugen** lassen.  
5. **Das Aspose‑Arbeitsbuch** auf die Festplatte speichern.

Jeder Schritt wird unten erklärt, inklusive vollständigem Code und erwarteter Ausgabe.

![Beispiel für das Befüllen einer Excel‑Vorlage](https://example.com/images/populate-excel-template.png "Beispiel für das Befüllen einer Excel‑Vorlage")

## Schritt 1: Master‑Detail‑Datenkollektionen vorbereiten

Master‑Detail‑Berichte basieren auf zwei verwandten Sammlungen: einer Liste von Bestellungen (Master) und einer Liste von Bestellpositionen (Detail). Die Smart‑Marker‑Engine ordnet Zeilen anhand des Feldes `OrderId` zu.

```csharp
using System.Collections.Generic;

// Master collection – one record per order
var orders = new List<object>
{
    new { OrderId = 1, Customer = "Alice" },
    new { OrderId = 2, Customer = "Bob" }
};

// Detail collection – multiple rows per order
var orderLines = new List<object>
{
    new { OrderId = 1, Item = "Pen",      Qty = 10 },
    new { OrderId = 1, Item = "Notebook", Qty = 5  },
    new { OrderId = 2, Item = "Pencil",   Qty = 20 }
};
```

**Warum das wichtig ist:**  
Der `SmartMarkerProcessor` durchsucht die Vorlage nach Markern wie `&=Orders.OrderId` und `&=OrderLines.Item`. Durch die Bereitstellung zweier separater Sammlungen erzeugt Aspose.Cells automatisch ein neues Arbeitsblatt für jeden Master‑Datensatz und füllt die Detail‑Zeilen entsprechend.

## Schritt 2: Die Excel‑Vorlage laden, die Smart‑Marker enthält

Die Vorlage enthält das Layout, die Formatierung und die Platzhalter‑Tags. Achten Sie darauf, dass Dateiname und Pfad korrekt sind.

```csharp
using Aspose.Cells;

// Adjust the path to where you stored the template
string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
Workbook workbook = new Workbook(templatePath);
```

**Warum das wichtig ist:**  
Das Laden der Vorlage liefert dem Prozessor ein Arbeitsbuch‑Objekt, das bereits weiß, wo Daten eingefügt werden sollen. Alle Formatierungen (Schriftarten, Rahmen, Formeln) bleiben erhalten, sodass der erzeugte Bericht professionell aussieht, ohne zusätzlichen Styling‑Code.

## Schritt 3: Einen SmartMarkerProcessor erstellen

Der Prozessor ist die Engine, die Marker durch tatsächliche Werte ersetzt.

```csharp
// Initialise the processor with the loaded workbook
var processor = new SmartMarkerProcessor(workbook);
```

**Warum das wichtig ist:**  
`SmartMarkerProcessor` isoliert die Smart‑Marker‑Logik vom Rest des Arbeitsbuchs, sodass Sie dasselbe Arbeitsbuch nach dem Anwenden der Daten für andere Vorgänge (z. B. Diagramme) wiederverwenden können.

## Schritt 4: Master‑Detail‑Daten anwenden und mehrere Arbeitsblätter erzeugen

Hier binden wir die beiden Sammlungen an den Prozessor und teilen Aspose.Cells mit, wie jedes erzeugte Arbeitsblatt benannt werden soll.

```csharp
using Aspose.Cells.SmartMarkers;

// Combine the collections into an anonymous object matching the marker names
var data = new { Orders = orders, OrderLines = orderLines };

// Options let you control sheet naming and other behaviours
var options = new SmartMarkerOptions
{
    // {0} will be replaced by the master record index (1‑based)
    DetailSheetNewName = "Details_{0}"
};

// Apply the data – this step creates a new sheet for each order
processor.ApplyTemplate(data, options);
```

**Warum das wichtig ist:**  
Das Muster `DetailSheetNewName` erzeugt Arbeitsblätter mit Namen wie `Details_1`, `Details_2` usw., die jeweils einer Bestellung in der Master‑Sammlung entsprechen. Diese automatische Blattgenerierung ist das Kernstück des **Erzeugens mehrerer Arbeitsblätter**, ohne das Arbeitsbuch manuell zu durchlaufen.

### Wie das resultierende Arbeitsbuch aussieht

| Blattname | Inhalt |
|------------|----------|
| **Master** | Kopfzeile mit Bestellübersicht (OrderId, Customer) |
| **Details_1** | Alle `OrderLines`, bei denen `OrderId = 1` (Pen, Notebook) |
| **Details_2** | Alle `OrderLines`, bei denen `OrderId = 2` (Pencil) |

Das Master‑Blatt kann ebenfalls befüllt werden, indem man eine Smart‑Marker‑Tabelle hinzufügt, die über `Orders` iteriert. Die Detail‑Blätter werden automatisch vom Prozessor erstellt.

## Schritt 5: Das Aspose‑Arbeitsbuch speichern

Schließlich schreiben Sie das befüllte Arbeitsbuch in eine neue Datei.

```csharp
// Choose the output path – ensure the folder exists
string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
workbook.Save(resultPath);
```

**Warum das wichtig ist:**  
Der Aufruf von `Save` schreibt das im Speicher befindliche Arbeitsbuch in eine physische `.xlsx`‑Datei und schließt damit den Schritt **Aspose‑Arbeitsbuch speichern** ab. Die Datei kann in Excel, Google Sheets oder jedem Viewer, der das OpenXML‑Format unterstützt, geöffnet werden.

### Erwartete Ausgabe

Öffnen Sie `MasterDetailResult.xlsx` und Sie sehen:

* **Blatt “Master”** – eine Tabelle mit Order 1 (Alice) und Order 2 (Bob).  
* **Blatt “Details_1”** – zwei Zeilen: Pen (10) und Notebook (5).  
* **Blatt “Details_2”** – eine Zeile: Pencil (20).

Alle Formatierungen aus der ursprünglichen Vorlage (Kopfzeilen‑Farben, Spaltenbreiten, Zahlenformate) bleiben erhalten.

## Umgang mit gängigen Sonderfällen

| Situation | Empfohlener Ansatz |
|-----------|----------------------|
| **Vorlage nicht gefunden** | Umwickeln Sie den Aufruf `new Workbook(...)` mit einem `try/catch` und protokollieren Sie `FileNotFoundException`. |
| **Große Datensätze (10 000+ Zeilen)** | Erhöhen Sie `SmartMarkerOptions.MaxRowsPerSheet`, falls Sie mehr Zeilen pro Blatt benötigen, oder paginieren Sie manuell. |
| **Benutzerdefinierte Blattbenennung** | Verwenden Sie einen Format‑String wie `DetailSheetNewName = \"Order_{0}_{1}\"`, wobei `{1}` eine Eigenschaft des Master‑Datensatzes sein kann (z. B. `Customer`). |
| **Bedingte Formatierung pro Bestellung** | Fügen Sie der Vorlage eine Regel für bedingte Formatierung hinzu, die auf einen Marker verweist (z. B. `&=Orders.Status`), und lassen Sie den Prozessor diese auswerten. |

## Vollständiges ausführbares Programm

Unten finden Sie die vollständige C#‑Konsolenanwendung, die alle Teile zusammenfügt. Ersetzen Sie `YOUR_DIRECTORY` durch einen tatsächlichen Ordnerpfad auf Ihrem Rechner.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class SmartMarkerDetailSheetDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Prepare master‑detail data collections
        // -------------------------------------------------
        var orders = new List<object>
        {
            new { OrderId = 1, Customer = "Alice" },
            new { OrderId = 2, Customer = "Bob" }
        };

        var orderLines = new List<object>
        {
            new { OrderId = 1, Item = "Pen",      Qty = 10 },
            new { OrderId = 1, Item = "Notebook", Qty = 5  },
            new { OrderId = 2, Item = "Pencil",   Qty = 20 }
        };

        // -------------------------------------------------
        // Step 2: Load the template workbook that contains smart markers
        // -------------------------------------------------
        string templatePath = @"YOUR_DIRECTORY\MasterDetailTemplate.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor to handle the template
        // -------------------------------------------------
        var processor = new SmartMarkerProcessor(workbook);

        // -------------------------------------------------
        // Step 4: Apply the master‑detail data and generate multiple sheets
        // -------------------------------------------------
        var data = new { Orders = orders, OrderLines = orderLines };
        var options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Details_{0}"
        };

        processor.ApplyTemplate(data, options);

        // -------------------------------------------------
        // Step 5: Save the populated Aspose workbook
        // -------------------------------------------------
        string resultPath = @"YOUR_DIRECTORY\MasterDetailResult.xlsx";
        workbook.Save(resultPath);

        Console.WriteLine($"Report generated successfully: {resultPath}");
    }
}
```

Führen Sie das Programm aus (`dotnet run` oder `Ctrl+F5` in Visual Studio). Wenn es fertig ist, öffnen Sie `MasterDetailResult.xlsx`, um zu überprüfen, dass das **Befüllen der Excel‑Vorlage** den erwarteten Master‑Detail‑Bericht mit **mehreren Arbeitsblättern** erzeugt hat.

## Fazit

Sie wissen jetzt, wie Sie mit Aspose.Cells **Excel‑Vorlagen befüllen**, **mehrere Arbeitsblätter erzeugen**, **Aspose‑Arbeitsbuch speichern** und in nur wenigen C#‑Zeilen einen robusten **Master‑Detail‑Bericht** erstellen können. Die Smart‑Marker‑Engine eliminiert die Notwendigkeit manueller Schleifen, bewahrt Ihre Formatierung und skaliert problemlos auf größere Datensätze.

### Nächste Schritte

* Erkunden Sie **SmartMarkerOptions**, z. B. `EnableFormulaCalculation`, um Formeln nach dem Einfügen von Daten auszuwerten.  
* Fügen Sie dem Master‑Blatt Diagramme hinzu und lassen Sie den Prozessor die Serienbereiche automatisch aktualisieren.  
* Kombinieren Sie diesen Ansatz mit **Aspose.Slides**, um dieselben Daten in PowerPoint‑Präsentationen zu exportieren.

Probieren Sie gerne verschiedene Vorlagen‑Layouts, benutzerdefinierte Blattbenennungs‑Muster oder zusätzliche Detail‑Sammlungen aus. Viel Spaß beim Programmieren!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Master‑Detail‑Bericht in C# erstellen – Excel‑Vorlage mit SmartMarker befüllen](/cells/english/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/)
- [Wie man Excel aus einer Vorlage mit C# und Aspose.Cells erzeugt](/cells/english/net/templates-reporting/how-to-generate-excel-from-template-with-c-and-aspose-cells/)
- [Aspose Cells Smart Markers – Excel‑Vorlage befüllen](/cells/english/java/templates-reporting/aspose-cells-smart-markers-populate-excel-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}