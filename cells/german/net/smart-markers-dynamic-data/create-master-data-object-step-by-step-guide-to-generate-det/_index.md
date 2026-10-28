---
category: general
date: 2026-02-14
description: Erstellen Sie ein Master‑Datenobjekt in C# und generieren Sie mühelos
  ein Detailblatt. Lernen Sie den kompletten SmartMarker‑Workflow mit praktischen
  Codebeispielen.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: de
og_description: Erstellen Sie ein Master‑Datenobjekt in C# und generieren Sie ein
  Detailblatt mit SmartMarker. Folgen Sie unserem ausführlichen Tutorial für eine
  sofort einsatzbereite Lösung.
og_title: Master-Datenobjekt erstellen – Komplett‑Guide
tags:
- C#
- SmartMarker
- Excel Automation
title: Master‑Datenobjekt erstellen – Schritt‑für‑Schritt‑Anleitung zur Erstellung
  des Detailblatts
url: /de/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Masterdatenobjekt erstellen – Komplettes Tutorial

Haben Sie jemals ein **master data object** für ein Excel‑Arbeitsblatt erstellen müssen, waren sich aber nicht sicher, wie Sie es an ein SmartMarker‑Detailblatt anbinden? Sie sind nicht allein. In vielen Reporting‑Szenarien steuert das Master‑Objekt ein dynamisches Detailblatt, und die richtige Verkabelung kann sich anfühlen, als würde man ein Puzzle ohne Bild zusammensetzen.  

In diesem Leitfaden gehen wir den gesamten Prozess durch – das Erstellen des master data object, das Konfigurieren der SmartMarker‑Optionen zum **generate detail sheet** und schließlich das Ausführen des Prozessors. Am Ende haben Sie ein ausführbares Snippet, das Sie in jedes .NET‑Projekt einfügen können, das die GrapeCity Documents for Excel (GcExcel)‑Bibliothek verwendet.

## Was Sie benötigen

- .NET 6+ (oder .NET Framework 4.7.2) mit einem Verweis auf `GcExcel.dll`
- Grundlegende C#‑Kenntnisse (Variablen, anonyme Typen, Objektinitialisierer)
- Eine Excel‑Arbeitsmappe, die bereits SmartMarker‑Tags wie `{{OrderId}}` und eine Tabelle für Positionen enthält
- Visual Studio, Rider oder einen beliebigen Editor Ihrer Wahl

Das war’s – keine zusätzlichen NuGet‑Pakete über die Kern‑GcExcel‑Distribution hinaus.

## Schritt 1: Masterdatenobjekt erstellen

Das Erste, was Sie tun müssen, ist **create master data object**, das die von den SmartMarker‑Tags erwartete Struktur widerspiegelt. Betrachten Sie es als ein kleines In‑Memory‑Report‑Modell.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Warum hier einen anonymen Typ verwenden? Weil er Ihnen ermöglicht, einen leichten Container zu definieren, ohne eine vollwertige Klasse zu deklarieren – perfekt für schnelle Demos oder wenn sich die Struktur voraussichtlich nicht ändert. Wenn Sie später ein wiederverwendbares Modell benötigen, ersetzen Sie einfach `var` durch ein korrektes POCO.

> **Pro‑Tipp:** Halten Sie die Eigenschaftsnamen (`OrderId`, `Product`, `Quantity`) identisch zu den Platzhaltern in Ihrem Arbeitsblatt; SmartMarker vergleicht sie ohne Berücksichtigung der Groß‑/Kleinschreibung.

## Schritt 2: SmartMarker‑Optionen konfigurieren, um ein Detailblatt zu generieren

Jetzt teilen wir SmartMarker mit, dass wir ein separates Arbeitsblatt für die Zeilen‑Tabelle wünschen. Hier kommt das Schlüsselwort **generate detail sheet** zum Einsatz.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

Das Muster `DetailSheetNewName` verwendet geschweifte Platzhalter, die zur Laufzeit ersetzt werden. In unserem Beispiel heißt das Blatt `Order_1`. Wenn Sie später über mehrere Aufträge iterieren, erhält jeder sein eigenes Register – genau das, was die meisten Buchhalter erwarten.

## Schritt 3: SmartMarker‑Prozessor ausführen

Mit den Daten und Optionen bereit, ist der letzte Schritt, den Prozessor auf das Zielarbeitsblatt anzuwenden.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Im Hintergrund scannt SmartMarker das Arbeitsblatt nach Tags, fügt die Werte aus `orderData` ein, und weil `DetailSheet` auf `true` gesetzt ist, klont es die Vorlage in ein neues Blatt mit dem Namen `Order_1`. Alle Zeilenpositionen erscheinen im Detailbereich und erhalten die Formatierung, die Sie in der Vorlage angewendet haben.

### Vollständiges funktionierendes Beispiel

Unten finden Sie ein eigenständiges Konsolenprogramm, das eine Vorlagenarbeitsmappe (`Template.xlsx`) öffnet, die drei Schritte ausführt und das Ergebnis als `Result.xlsx` speichert. Sie können dies in ein neues Konsolenprojekt kopieren und **F5** drücken.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Erwartete Ausgabe

- **Result.xlsx** enthält ein Blatt namens `Order_1`.
- Zelle `A1` (oder wo immer Sie `{{OrderId}}` platziert haben) zeigt jetzt `1`.
- Eine Tabelle, die beim SmartMarker‑Block beginnt, listet zwei Zeilen auf:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Wenn Sie die Datei öffnen, sehen Sie, dass die Formatierung aus der Vorlage erhalten bleibt – Rahmen, Schriftarten, bedingte Formatierung – alles intakt.

## Häufige Fragen & Sonderfälle

### Was ist, wenn ich mehrere Aufträge habe?

Packen Sie das master object in eine Sammlung und lassen Sie SmartMarker automatisch iterieren:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Jeder Auftrag erzeugt ein eigenes Blatt (`Order_1`, `Order_2`, …). Der Prozessor behandelt das äußere Array als die Master‑Sammlung.

### Wie steuere ich die Position des Blatts?

Setzen Sie `smartMarkerOptions.DetailSheetInsertIndex = 2;`, um das neue Blatt nach dem zweiten Register zu platzieren, oder verwenden Sie `DetailSheetInsertAfter = "Summary"`, um es nach einem benannten Blatt einzufügen.

### Kann ich das Detailblatt für einen bestimmten Durchlauf deaktivieren?

Schalten Sie einfach `DetailSheet = false;`. SmartMarker schreibt dann die Zeilenpositionen in dasselbe Blatt, in dem die Master‑Tags liegen.

### Was ist mit großen Datensätzen?

SmartMarker streamt Daten effizient, aber wenn Sie einige hunderttausend Zeilen überschreiten, können Sie die Excel‑Grenze von 1.048.576 Zeilen erreichen. In diesem Fall teilen Sie die Daten in mehrere Master‑Datensätze auf oder erwägen Sie den Export nach CSV.

## Visuelle Übersicht

![Diagramm, das zeigt, wie man ein master data object erstellt und ein Detailblatt mit SmartMarker generiert](/images/smartmarker-flow.png)

*Die Abbildung zeigt den Ablauf vom C#‑master object → SmartMarker‑Optionen → Arbeitsblattverarbeitung → neues Detailblatt.*

## Fazit

Sie wissen jetzt, wie man in C# **create master data object** und SmartMarker so konfiguriert, dass es automatisch **generate detail sheet**. Das Drei‑Schritte‑Muster – Daten, Optionen, Prozessor – deckt die meisten Excel‑Automatisierungsszenarien mit GcExcel ab.  

Von hier aus können Sie folgendes erkunden:

- Hinzufügen von Kopf‑/Fußzeilendaten zu jedem Detailblatt
- Verwendung von bedingter Formatierung basierend auf dem Auftragsstatus
- Exportieren der erzeugten Arbeitsmappe nach PDF mit `workbook.SaveAsPdf(...)`

Fühlen Sie sich frei zu experimentieren, Dinge zu zerbrechen und dann wieder zusammenzufügen. Das ist der schnellste Weg, die Arbeitsblatt‑Automatisierung zu meistern. Viel Spaß beim Coden!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}