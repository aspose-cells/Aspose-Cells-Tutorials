---
category: general
date: 2026-09-15
description: Erstelle eine Excel‑Arbeitsmappe in C# und lerne, wie du die Arbeitsmappe
  als PDF speicherst, während du dynamische Arrays mit der EXPAND‑Funktion ausgibst.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: de
lastmod: 2026-09-15
og_description: Erstelle eine Excel‑Arbeitsmappe in C# und speichere sie schnell als
  PDF, während du die EXPAND‑Funktion zum Ausgeben eines dynamischen Arrays nutzt.
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: Excel-Arbeitsmappe erstellen und als PDF mit dynamischen Arrays speichern
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: Excel-Arbeitsmappe erstellen und als PDF mit dynamischen Arrays speichern
url: /de/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Arbeitsmappe erstellen und als PDF speichern mit dynamischen Arrays

Wenn Sie programmgesteuert **Excel-Arbeitsmappe** erstellen und anschließend **Arbeitsmappe als PDF speichern** müssen, zeigt Ihnen dieser Leitfaden eine vollständige End‑to‑End‑Lösung in C#. Außerdem sehen Sie, wie Sie **dynamische Array‑Ergebnisse** mit der **EXPAND‑Funktion** ausgeben können, die moderne Methode zur Erzeugung von Arrays ohne VBA.  

Egal, ob Sie einen Reporting‑Dienst, eine Export‑Funktion für ein ERP‑System oder ein datengetriebenes Dashboard erstellen, die nachfolgenden Schritte ermöglichen es Ihnen, eine Arbeitsmappe zu erzeugen, sie mit Smart‑Marker‑Daten zu füllen und ein PDF zu erzeugen, das erweiterte Schriftmerkmale bewahrt.

## Voraussetzungen

Bevor Sie beginnen, stellen Sie sicher, dass Sie folgendes haben:

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.8)
* Eine aktuelle Version von **Aspose.Cells for .NET** (v25.8 oder neuer) – sie stellt `Workbook`, `PdfSaveOptions` und `SmartMarkerProcessor` bereit.
* Eine IDE wie Visual Studio 2022 (jeder Editor, der C# kompilieren kann, funktioniert).

Fügen Sie das NuGet‑Paket zu Ihrem Projekt hinzu:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Schritt 1: Excel‑Arbeitsmappe erstellen und das erste Arbeitsblatt einrichten

Die erste Aufgabe besteht darin, **Excel‑Arbeitsmappe** zu **erstellen** und eine Referenz auf das Standard‑Arbeitsblatt zu erhalten. Dieses Arbeitsblatt wird das dynamische Array und die Smart‑Marker‑Vorlage beherbergen.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Warum das wichtig ist*: Durch das Instanziieren von `Workbook` wird die interne Arbeitsmappenstruktur zugewiesen, während der Zugriff auf `Worksheets[0]` Ihnen ein sofort einsatzbereites Blatt liefert, ohne dass Sie eines manuell hinzufügen müssen.

## Schritt 2: Dynamisches Array mit der EXPAND‑Funktion ausgeben

Die **EXPAND‑Funktion** von Excel kann ein statisches Array‑Literal in einen Spill‑Bereich beliebiger Größe umwandeln. Hier lassen wir Excel `{1,2,3}` in einen 5‑Zeilen × 1‑Spalten‑Bereich ausgehend von `A1` expandieren.

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Warum das wichtig ist*: Durch die Verwendung von `EXPAND` entfallen manuelle Schleifen in C#. Die Engine berechnet den Spill‑Bereich und speichert die Werte direkt im Arbeitsblatt, die später im PDF erscheinen.

## Schritt 3: Arbeitsmappe als PDF speichern und dabei Schrift‑Variationsselektoren bewahren

Wenn Sie **Arbeitsmappe als PDF speichern** müssen, können Sie zudem erweiterte typografische Funktionen wie Schrift‑Variationsselektoren aktivieren (verfügbar ab Aspose.Cells v25.8). Dies stellt sicher, dass PDFs komplexe Schriftsysteme korrekt darstellen.

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Warum das wichtig ist*: Das Setzen von `FontVariationSelectors` auf `true` ist entscheidend für Sprachen, die auf Glyphen‑Variationen angewiesen sind (z. B. Chinesisch, Japanisch, Emoji). Das erzeugte PDF spiegelt die Excel‑Ansicht auf dem Bildschirm wider.

## Schritt 4: Smart‑Marker‑Vorlage einfügen, die auf eine verschachtelte Datenquelle verweist

Smart Markers ermöglichen das Einbetten von Platzhaltern direkt im Arbeitsblatt. Die nachstehende Vorlage erzeugt eine Liste von Bestellungen und deren Artikeln.

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Warum das wichtig ist*: Durch das Platzieren der Vorlage in `A1` teilen Sie Aspose.Cells mit, wo die Datenexpansion beginnen soll. Die `:`‑Syntax (`Items:ItemName`) weist den Prozessor an, über eine verschachtelte Sammlung zu iterieren.

## Schritt 5: Verschachtelte Datenquelle definieren (Bestellungen mit Artikeln)

Wir erstellen ein anonymes Array von Bestellungen, von denen jede ihre eigene Sammlung von Artikelobjekten enthält. Dies spiegelt ein typisches Master‑Detail‑Szenario wider.

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Warum das wichtig ist*: Die verschachtelte Struktur demonstriert **wie man dynamische Arrays in Excel** über Smart Markers erstellt, ohne VBA oder manuelle Zellschleifen zu schreiben.

## Schritt 6: Smart Markers verarbeiten und die endgültige Excel‑Datei speichern

Jetzt übergeben wir die Arbeitsmappe und die Datenquelle an `SmartMarkerProcessor`. Nach der Verarbeitung werden die Platzhalter durch tatsächliche Zeilen ersetzt, und wir speichern das Ergebnis als reguläre `.xlsx`‑Datei.

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Warum das wichtig ist*: `SmartMarkerProcessor` expandiert die Vorlage automatisch, erstellt die erforderlichen Zeilen und füllt sie mit Daten. Die endgültige Arbeitsmappe kann in Excel geöffnet werden, um zu prüfen, dass jede Bestellung und ihre Artikel korrekt angezeigt werden.

## Erwartete Ausgabe

* **VarSelector.pdf** – eine PDF‑Datei, die die Zahlen 1‑3 über fünf Zeilen hinweg ausgibt, gerendert mit den von Ihnen aktivierten OpenType‑Schriftvariationen.
* **NestedSmartMarker.xlsx** – eine Excel‑Datei mit den folgenden Zeilen (beginnend bei `A1`):

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

Die PDF‑Version behält denselben numerischen Spill bei, da der Arbeitsblattzustand vor der Smart‑Marker‑Verarbeitung gespeichert wurde; Sie können das PDF‑Speichern nach der Verarbeitung wiederholen, falls Sie die endgültigen Daten ebenfalls im PDF benötigen.

## Profi‑Tipps und häufige Fallstricke

| Tipp | Erklärung |
|------|-----------|
| **Verwenden Sie dieselben `PdfSaveOptions` erneut** | Das Erstellen des Options‑Objekts einmal und dessen Wiederverwendung verhindert subtile Unterschiede beim Rendern (z. B. fehlende Variationsselektoren). |
| **Rufen Sie `ws.Calculate()` nach dem Setzen von Formeln auf** | Ohne explizite Berechnung kann der Spill‑Bereich leer bleiben, wenn Sie die Arbeitsmappe programmgesteuert inspizieren. |
| **Platzieren Sie Smart Marker‑Vorlagen auf einem leeren Blatt** | Das Mischen von Vorlagen mit vorhandenen Daten kann zu unerwarteten Zeileneinfügungen führen. Verwenden Sie nach Möglichkeit ein dediziertes Blatt. |
| **Achten Sie auf die Dateipfade** | Verwenden Sie `Path.Combine(Environment.CurrentDirectory, "output.pdf")`, um hartkodierte Verzeichnisse auf verschiedenen Rechnern zu vermeiden. |
| **Versionsprüfung** | `FontVariationSelectors` ist nur ab Version 25.8 verfügbar; ältere Versionen ignorieren die Eigenschaft, ohne einen Fehler zu werfen. |

## Nächste Schritte

Jetzt, da Sie wissen, wie man **Excel‑Arbeitsmappe** erstellt, **dynamische Arrays ausgibt** und **Arbeitsmappe als PDF speichert**, können Sie Folgendes erkunden:

* Diagramme oder Bilder vor der PDF‑Konvertierung hinzufügen.
* Die gleiche Arbeitsmappe in andere Formate exportieren (z. B. HTML, CSV) mittels `Save`‑Überladungen.
* Verwendung von **Smart Marker‑Ausdrücken** (`${Orders.Total:SUM(Items.Price)}`) zur Berechnung von Aggregaten in Echtzeit.
* Integration dieses Codes in eine ASP.NET Core‑API, sodass Benutzer das erzeugte PDF direkt von einem Web‑Endpunkt herunterladen können.

---

**Zusammenfassung** – Dieses Tutorial zeigte Ihnen, wie Sie **Excel‑Arbeitsmappe** erstellen, die **EXPAND‑Funktion** verwenden, um **dynamische Arrays auszugeben**, einen **Smart Marker** einbetten, der mit einer verschachtelten Datenquelle arbeitet, und schließlich **Arbeitsmappe als PDF speichern**, wobei erweiterte Schriftmerkmale erhalten bleiben. Das vollständige, ausführbare Beispiel kann in jedes C#‑Projekt kopiert und an Ihre eigenen Datenstrukturen angepasst werden. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel‑Arbeitsmappe erstellen und als PDF in ASP.NET mit Aspose.Cells speichern](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Wie man eine Excel‑Arbeitsmappe als ODS mit Aspose.Cells für .NET erstellt und speichert](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Wie man eine Excel‑Arbeitsmappe als SVG mit Aspose.Cells für Java erstellt und speichert](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}