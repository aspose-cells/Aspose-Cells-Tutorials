---
category: general
date: 2026-02-28
description: Erstellen Sie einen Master‑Detail‑Bericht in C# und lernen Sie, wie Sie
  eine Excel‑Vorlage befüllen, Daten in Excel zusammenführen und eine Excel‑Arbeitsmappe
  in C# laden – alles in wenigen Schritten.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: de
og_description: Erstellen Sie einen Master‑Detail‑Bericht in C# mit Aspose.Cells SmartMarker.
  Lernen Sie, eine Excel‑Arbeitsmappe in C# zu laden, Daten in Excel zu mergen und
  eine Excel‑Vorlage zu befüllen.
og_title: Master‑Detail‑Bericht in C# erstellen – Excel‑Vorlage ausfüllen
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Master‑Detail‑Bericht in C# erstellen – Excel‑Vorlage mit SmartMarker befüllen
url: /de/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Master‑Detail‑Bericht in C# erstellen – Excel‑Vorlage mit SmartMarker füllen

Haben Sie jemals einen **master detail report** in C# erstellen müssen, waren sich aber nicht sicher, wie Sie die Daten in eine Excel‑Datei bekommen? Sie sind nicht allein. In diesem Leitfaden gehen wir die genauen Schritte durch, um **Excel‑Vorlage zu füllen**, **Daten in Excel zu mergen** und **Excel‑Arbeitsmappe C#‑style zu laden**, sodass Sie am Ende einen professionellen Master‑Detail‑Bericht zur Verteilung haben.

Wir verwenden Aspose.Cells SmartMarker, eine leistungsstarke Engine, die Master‑Detail‑Beziehungen sofort versteht. Am Ende des Tutorials haben Sie ein vollständiges, ausführbares Beispiel, das Sie in jedes .NET‑Projekt einbinden können. Keine vagen „siehe die Dokumentation“-Abkürzungen – nur eine eigenständige Lösung, die Sie copy‑paste‑bereit haben.

## Was Sie lernen werden

- Wie Sie **master detail**‑Datenstrukturen in C# erstellen, die direkt auf eine Excel‑Vorlage abgebildet werden können.  
- Der genaue Weg, **Excel‑Arbeitsmappe C#**‑Code zu laden, der eine `.xlsx`‑Datei mit SmartMarker‑Tags öffnet.  
- Der Prozess, **Excel‑Vorlage zu füllen**, indem Sie `SmartMarkerProcessor` ausführen.  
- Tipps zum Umgang mit Sonderfällen, wie fehlenden Tags oder großen Datenmengen.  
- Wie Sie das Ergebnis überprüfen und wie der finale **master detail report** aussieht.

### Voraussetzungen

- .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.8).  
- Aspose.Cells für .NET (Sie können das kostenlose Test‑NuGet‑Paket holen: `Install-Package Aspose.Cells`).  
- Eine einfache Excel‑Datei (`template.xlsx`), die SmartMarker‑Tags enthält (wir zeigen das minimale Markup, das Sie benötigen).

Wenn Sie das alles bereit haben, legen wir los.

## Schritt 1 – Datenquelle für Master‑Detail erstellen *(wie man master detail erstellt)*

Das Erste, was Sie benötigen, ist ein C#‑Objekt, das die Master‑Zeilen (Bestellungen) und deren Kind‑Zeilen (Bestellpositionen) repräsentiert. SmartMarker liest diese Hierarchie automatisch, wenn `MasterDetail` auf `true` gesetzt ist.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Warum das wichtig ist:**  
SmartMarker sucht nach einer Eigenschaft namens `Orders` (der Master) und anschließend für jede Bestellung nach einer Sammlung namens `Items`. Durch das Angleichen dieser Namen erhalten Sie automatisch einen **master‑detail report**, ohne selbst Schleifen schreiben zu müssen.

> **Pro‑Tipp:** Halten Sie die Eigenschaftsnamen kurz und aussagekräftig; sie werden zu den Platzhaltern in Ihrer Excel‑Vorlage.

## Schritt 2 – SmartMarker‑Optionen für Master‑Detail‑Verarbeitung konfigurieren

Teilen Sie der Engine mit, dass Sie ein Master‑Detail‑Szenario haben, und geben Sie den Namen des Detail‑Sheets an, das die Kind‑Zeilen erhalten soll.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Warum das wichtig ist:**  
Wenn Sie `MasterDetail = true` weglassen, behandelt SmartMarker die Daten als flache Liste und die Detail‑Zeilen erscheinen nie. `DetailSheetName` muss exakt dem Blattnamen entsprechen, den Sie in der Vorlage erstellt haben (Groß‑/Kleinschreibung beachten).

## Schritt 3 – Excel‑Arbeitsmappe C#‑style laden

Jetzt öffnen wir die Vorlage, die die SmartMarker‑Tags enthält. Das ist der **load Excel workbook C#**‑Schritt, bei dem viele Entwickler scheitern, weil sie den korrekten Dateipfad vergessen oder die Arbeitsmappe nicht ordnungsgemäß freigeben.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Warum das wichtig ist:**  
Aspose.Cells liest die gesamte Arbeitsmappe in den Speicher, sodass die Datei auf der Festplatte, als eingebettete Ressource oder sogar gestreamt von einem Web‑Service liegen kann. Stellen Sie einfach sicher, dass der Pfad auf eine gültige `.xlsx`‑Datei mit den Tags zeigt, die wir gleich besprechen.

## Schritt 4 – SmartMarker‑Tags in die Vorlage einfügen (Excel‑Vorlage füllen)

Wenn Sie jetzt `template.xlsx` öffnen, sehen Sie zwei Blätter:

- **Orders** – das Master‑Blatt mit einer Zeile wie `&=Orders.Id`.  
- **OrderDetail** – das Detail‑Blatt mit Zeilen wie `&=Items.Sku` und `&=Items.Qty`.

Ein minimales Beispiel des Markups:

| Sheet | Cell A1 | Cell B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Sie müssen keinen Code für die Tags schreiben – sie leben in der Excel‑Datei. Der **populate Excel template**‑Schritt besteht einfach darin, den Prozessor aufzurufen:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Warum das wichtig ist:**  
Der Prozessor scannt jedes Blatt, ersetzt die `&=`‑Platzhalter durch die tatsächlichen Werte und erweitert Zeilen für jeden Master‑ und Detail‑Datensatz. Da `MasterDetail` aktiviert ist, wird automatisch für jedes Element unter der jeweiligen Bestellung eine neue Zeile erzeugt.

## Schritt 5 – Master‑Detail‑Bericht speichern

Zum Schluss schreiben wir die gefüllte Arbeitsmappe auf die Festplatte. Jetzt erhalten Sie einen sofort teilbaren **master detail report**.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Erwartete Ausgabe:**  

- **Orders**‑Blatt zeigt zwei Zeilen: `1` und `2` (Bestell‑IDs).  
- **OrderDetail**‑Blatt zeigt drei Zeilen:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Damit haben Sie einen voll funktionsfähigen **create master detail report**, den Sie per E‑Mail verschicken, drucken oder in ein anderes System einspeisen können.

## Sonderfälle & häufige Fragen

### Was, wenn in der Vorlage ein Tag fehlt?
SmartMarker ignoriert unbekannte Tags stillschweigend, sodass leere Zellen entstehen. Überprüfen Sie die Schreibweise der Tags und stellen Sie sicher, dass die Eigenschaftsnamen in Ihrem C#‑Objekt exakt übereinstimmen.

### Wie geht es mit großen Datenmengen um?
Der Prozessor streamt Zeilen, sodass selbst tausende Detail‑Datensätze den Speicher nicht sprengen. Bei extrem großen Dateien sollten Sie jedoch die `MemorySetting` in `LoadOptions` erhöhen.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Kann ich einen anderen Blattnamen für den Master verwenden?
Ja – benennen Sie das Blatt in der Vorlage einfach um und passen Sie `DetailSheetName` an, falls Sie ein Detail‑Blatt haben. Der Master‑Blattname wird aus dem Platzhalter (`&=Orders.Id`) abgeleitet.

### Was, wenn ich eine Summenzeile hinzufügen muss?
Fügen Sie in der Vorlage eine reguläre Excel‑Formel ein (z. B. `=SUM(B2:B{#})`). SmartMarker bewahrt die Formel nach dem Einfügen der Daten.

## Vollständiges ausführbares Beispiel

Unten finden Sie das komplette Programm, das Sie in eine Konsolen‑App copy‑pasten können. Es enthält alle `using`‑Direktiven, das Datenmodell, die Optionen und die Dateiverarbeitung.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Führen Sie das Programm aus, öffnen Sie `output.xlsx`, und Sie sehen die Master‑Detail‑Daten wunderschön gefüllt.

## Visuelle Referenz

![Create master detail report output screenshot](https://example.com/images/master-detail-report.png "Create master detail report example")

*Das Bild zeigt das Orders‑Blatt mit den IDs 1 und 2 sowie das OrderDetail‑Blatt mit den drei SKU‑Qty‑Zeilen.*

## Fazit

Sie wissen jetzt **wie man master detail report** in C# mit Aspose.Cells SmartMarker erstellt – vom Aufbau der Datenquelle über das **loading Excel workbook C#**, das **populating Excel template** bis hin zum finalen Schritt.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}