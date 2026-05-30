---
category: general
date: 2026-05-30
description: Füllen Sie Excel-Vorlagen schnell aus und lernen Sie, wie Sie Excel mit
  Daten mithilfe von Aspose.Cells SmartMarker befüllen. Vollständige C#‑Anleitung
  mit ausführbarem Code.
draft: false
keywords:
- populate excel template
- fill excel with data
- Aspose.Cells SmartMarker
- automate Excel reporting
- C# Excel automation
language: de
og_description: Füllen Sie die Excel‑Vorlage aus und befüllen Sie Excel mit Daten
  mithilfe von Aspose.Cells SmartMarker. Folgen Sie diesem Schritt‑für‑Schritt‑C#‑Tutorial
  für sofortige Ergebnisse.
og_title: Excel-Vorlage befüllen – Excel-Daten mit SmartMarker füllen
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  headline: Populate Excel Template – Fill Excel Data via SmartMarker
  type: TechArticle
- description: Populate Excel template quickly and learn how to fill Excel with data
    using Aspose.Cells SmartMarker. Complete C# guide with runnable code.
  name: Populate Excel Template – Fill Excel Data via SmartMarker
  steps:
  - name: Empty Collections
    text: 'If `Items` is empty, SmartMarker will leave the table header intact but
      won’t insert any rows. To avoid a blank space, you can add a conditional block:'
  - name: Custom Number Formats
    text: 'Sometimes you need currency symbols or thousands separators. After processing,
      you can apply a style programmatically:'
  - name: Large Data Sets
    text: 'For thousands of rows, enable the `UseFastMode` option to improve performance:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Excel-Vorlage befüllen – Excel-Daten über SmartMarker ausfüllen
url: /de/net/smart-markers-dynamic-data/populate-excel-template-fill-excel-data-via-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel-Vorlage ausfüllen – Excel-Daten über SmartMarker füllen

Haben Sie jemals eine **Excel-Vorlage ausfüllen** müssen, waren sich aber nicht sicher, wie Sie den Prozess automatisieren können? In diesem Tutorial zeigen wir Ihnen, wie Sie **Excel mit Daten füllen** können, indem Sie Aspose.Cells SmartMarker verwenden – ein Tool, das eine statische Arbeitsmappe in einen dynamischen Berichtsgenerator verwandelt.

Stellen Sie sich vor, Sie haben ein vorgefertigtes Rechnungblatt, ein Vertriebs‑Dashboard oder ein beliebiges wiederholbares Formular. Anstatt Werte manuell einzugeben, können Sie ein C#‑Objekt übergeben und SmartMarker die schwere Arbeit erledigen lassen. Am Ende dieses Leitfadens haben Sie ein vollständig ausführbares Projekt, das eine Vorlage nimmt, Zeilen, Summen und sogar bedingte Formatierungen einfügt – ganz ohne UI‑Interaktion.

## Was Sie lernen werden

- Wie Sie eine Datenquelle vorbereiten, die zu den Markern in Ihrer Excel‑Vorlage passt.  
- Wie Sie **SmartMarkerProcessor** instanziieren und die Bereichsunterstützung aktivieren.  
- Wie Sie **Excel‑Vorlage ausfüllen** mit verschachtelten Sammlungen, z. B. Bestellpositionen.  
- Tipps zum Umgang mit Sonderfällen wie leeren Sammlungen oder benutzerdefinierten Zahlenformaten.  

Keine externen Dienste, keine VBA‑Makros – nur reines C# und Aspose.Cells. Alles, was Sie benötigen, ist .NET 6 (oder höher) und das Aspose.Cells‑NuGet‑Paket.

## Voraussetzungen

- Visual Studio 2022 (oder jede andere IDE Ihrer Wahl).  
- .NET 6 SDK installiert.  
- Aspose.Cells für .NET (Sie können eine kostenlose Testversion von der Aspose‑Website herunterladen).  
- Eine einfache Excel‑Vorlage mit SmartMarker‑Tags (wir erstellen gleich eine).

Wenn Ihnen irgendeiner dieser Punkte unbekannt ist, keine Panik; die nachfolgenden Schritte führen Sie durch jede Anforderung.

## Schritt 1: Entwerfen Sie die Excel‑Vorlage mit SmartMarker‑Tags

Öffnen Sie zunächst eine neue Arbeitsmappe und legen Sie die statischen Teile fest – Firmenlogo, Überschriften usw. Fügen Sie dann SmartMarker‑Platzhalter dort ein, wo dynamische Daten erscheinen sollen.

| Zelle | Inhalt |
|------|--------|
| A1   | **Rechnung** |
| A3   | `{{CompanyName}}` |
| A5   | **Bestelldetails** |
| A7   | `{{Orders.Items.Name}}` |
| B7   | `{{Orders.Items.Qty}}` |
| C7   | `{{Orders.Items.Price}}` |
| D7   | `{{Orders.Items.Price * Orders.Items.Qty}}` |

**Warum das wichtig ist:** SmartMarker liest die doppelten geschweiften Klammern und ordnet sie den Eigenschaften des Objekts zu, das Sie später übergeben. Die Sammlung `Orders.Items` weist die Engine an, die Zeile für jedes Element in der Liste zu wiederholen.

> **Pro‑Tipp:** Verwenden Sie die Option `RangeSmartMarker` (wir aktivieren sie später), wenn die Engine den Bereich automatisch erweitern soll – ideal für Tabellen, die wachsen oder schrumpfen.

Speichern Sie die Datei als `InvoiceTemplate.xlsx` im `Resources`‑Ordner Ihres Projekts.

## Schritt 2: Bereiten Sie die Datenquelle vor, die zu den Vorlagen‑Markern passt

Jetzt erstellen wir ein anonymes C#‑Objekt (oder eine stark typisierte Klasse), dessen Eigenschaftsnamen exakt mit den Markern übereinstimmen. Der Schlüssel ist, die Hierarchie exakt zu spiegeln.

```csharp
// Step 2: Prepare the data source that matches the template markers
var data = new
{
    CompanyName = "Acme Corp.",
    Orders = new[]
    {
        new
        {
            Items = new[]
            {
                new { Name = "Pen",   Qty = 2, Price = 1.5m },
                new { Name = "Notebook", Qty = 1, Price = 3.75m },
                new { Name = "Stapler",  Qty = 1, Price = 5.0m }
            }
        }
    }
};
```

**Warum das wichtig ist:** Das `Orders`‑Array enthält eine einzelne Bestellung, und jede Bestellung hat ein `Items`‑Array. SmartMarker iteriert über `Items` und klont die Zeile für jedes Element. Wenn Sie später mehrere Bestellungen benötigen, fügen Sie einfach weitere Objekte zum `Orders`‑Array hinzu – ohne Code‑Änderungen.

## Schritt 3: Laden Sie die Vorlage und erstellen Sie eine SmartMarkerProcessor‑Instanz

Mit den vorbereiteten Daten laden wir die Arbeitsmappe, erstellen den Processor und weisen ihn an, Bereichs‑Marker zu berücksichtigen.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook
Workbook workbook = new Workbook("Resources/InvoiceTemplate.xlsx");

// Get the first worksheet (where our markers live)
Worksheet ws = workbook.Worksheets[0];

// Step 3: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Warum das wichtig ist:** `SmartMarkerProcessor` ist die Engine, die die Marker analysiert, Bereiche erweitert und Werte schreibt. Durch die Trennung von Processor und Arbeitsmappe bleibt der Code sauber und wiederverwendbar.

## Schritt 4: Verarbeiten Sie das Arbeitsblatt mit aktiviertem RangeSmartMarker

Die Magie passiert, wenn wir `Process` aufrufen. Durch Setzen von `RangeSmartMarker = true` wird SmartMarker angewiesen, den gesamten Zeilenbereich als wiederholbaren Block zu behandeln und bei Bedarf Zeilen automatisch einzufügen oder zu löschen.

```csharp
// Step 4: Process the worksheet using SmartMarker with range support enabled
processor.Process(ws, data, new SmartMarkerOptions { RangeSmartMarker = true });
```

Zu diesem Zeitpunkt hat die Engine:

1. Das Arbeitsblatt nach `{{...}}`‑Tags durchsucht.  
2. Jeden Tag einer Eigenschaft von `data` zugeordnet.  
3. Den Tabellenbereich (A7:D7) erkannt und dreimal dupliziert – einmal pro Element.  
4. Den Ausdruck `Price * Qty` für die Gesamtsumme berechnet.

## Schritt 5: Speichern Sie die resultierende Arbeitsmappe

Schließlich schreiben wir die ausgefüllte Arbeitsmappe auf die Festplatte (oder streamen sie zurück an einen Web‑Client).

```csharp
// Step 5: Save the populated workbook
workbook.Save("Output/InvoicePopulated.xlsx");
```

Öffnen Sie `InvoicePopulated.xlsx` und Sie sehen eine ordentlich gefüllte Tabelle:

| Name      | Menge | Preis | Gesamt |
|-----------|-------|-------|--------|
| Pen       | 2     | 1.5   | 3.00 |
| Notebook  | 1     | 3.75  | 3.75 |
| Stapler   | 1     | 5.00  | 5.00 |

Der Schritt **Excel‑Vorlage ausfüllen** ist nun abgeschlossen, und Sie haben erfolgreich **Excel mit Daten gefüllt** für beliebig viele Zeilen.

## Umgang mit häufigen Sonderfällen

### Leere Sammlungen

Ist `Items` leer, lässt SmartMarker die Tabellenüberschrift erhalten, fügt jedoch keine Zeilen ein. Um einen leeren Raum zu vermeiden, können Sie einen bedingten Block hinzufügen:

```csharp
{{#if Orders.Items.Length > 0}}
    ... table rows ...
{{else}}
    No items were ordered.
{{/if}}
```

### Benutzerdefinierte Zahlenformate

Manchmal benötigen Sie Währungssymbole oder Tausendertrennzeichen. Nach der Verarbeitung können Sie einen Stil programmgesteuert anwenden:

```csharp
Style style = workbook.CreateStyle();
style.Number = 164; // Built‑in currency format
StyleFlag flag = new StyleFlag { NumberFormat = true };

foreach (Cell cell in ws.Cells["C8:D12"])
{
    cell.SetStyle(style, flag);
}
```

### Große Datenmengen

Für tausende Zeilen aktivieren Sie die Option `UseFastMode`, um die Leistung zu verbessern:

```csharp
processor.Process(ws, data, new SmartMarkerOptions { 
    RangeSmartMarker = true,
    UseFastMode = true
});
```

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, eigenständige Programm, das Sie in eine Konsolen‑App kopieren‑und‑einfügen können. Es enthält alle using‑Direktiven, Datenvorbereitung, Verarbeitung und das Speichern.



## Was sollten Sie als Nächstes lernen?

- [Excel mit Daten über Aspose.Cells und Smart Markers ausfüllen](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Wie man Excel‑Zellen mit Aspose.Cells für .NET füllt: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/cell-operations/aspose-cells-dotnet-populate-excel-data/)
- [Excel‑Datenexport automatisieren mit Aspose.Cells für .NET: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}