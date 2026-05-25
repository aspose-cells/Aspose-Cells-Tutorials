---
category: general
date: 2026-05-23
description: Wie man Marker mit Aspose.Cells verwendet, um dynamische Blattnamen in
  der Excel‑Automatisierung zu erreichen. Lernen Sie Smart Markers, JSON‑Datenbindung
  und die Erstellung von Blättern in Minuten.
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: de
og_description: Wie man Marker in Aspose.Cells verwendet, um Excel‑Dateien mit dynamischer
  Blattbenennung zu erzeugen. Vollständige Schritt‑für‑Schritt‑Anleitung mit vollständigem
  C#‑Beispiel.
og_title: Wie man Marker verwendet – Dynamische Blattbenennung in Excel mit Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man Marker in Aspose.Cells für dynamische Blattbenennung in Excel verwendet
url: /de/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Marker in Aspose.Cells für dynamische Blattnamen in Excel verwendet

Haben Sie sich jemals gefragt, **wie man Marker** verwendet, um eine statische Excel‑Vorlage in ein vollwertiges Master‑Detail‑Arbeitsbuch zu verwandeln? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie *dynamic sheet naming excel* benötigen, insbesondere wenn die Blattnamen Datenwerte aus JSON oder einer Datenbank widerspiegeln müssen.  

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, sofort ausführbares C#‑Beispiel, das **zeigt, wie man Marker** mit **Aspose.Cells** Smart Markers verwendet, JSON‑Daten bindet und den Prozessor Blätter erstellen lässt, deren Namen zur Laufzeit geändert werden. Kein Schnickschnack, nur der exakte Code, den Sie in Visual Studio einfügen und sofort Ergebnisse sehen können.

## Was Sie lernen werden

- Das Konzept der **smart markers** und warum sie sich perfekt für Master‑Detail‑Szenarien eignen.  
- Wie man Marker‑Tags in ein Arbeitsbuch einbettet, die später durch echte Blattnamen ersetzt werden.  
- Einrichtung von **dynamic sheet naming excel** über die Option `DetailSheetNewName`.  
- Ausführen des `SmartMarkerProcessor` mit JSON‑Daten, um automatisch mehrere Blätter zu erzeugen.  
- Überprüfung der Ausgabe und ein paar nützliche Tipps, um häufige Fallstricke zu vermeiden.

> **Voraussetzungen** – Sie benötigen ein aktuelles .NET‑Runtime (≥ .NET 6 ist in Ordnung), die Aspose.Cells für .NET‑Bibliothek (Sie können eine kostenlose Testversion von Aspose herunterladen) und Grundkenntnisse in C#.  

---

![Beispiel zur Verwendung von Markern in Aspose.Cells](example.png "how to use markers example in Aspose.Cells")

## Wie man Marker verwendet, um dynamische Blattnamen zu erstellen (Schritt 1)

Das Erste, was wir benötigen, ist ein leeres Arbeitsbuch, das als Vorlage dient. In einem echten Projekt würden Sie wahrscheinlich von einer bestehenden `.xlsx`‑Datei ausgehen, die bereits Layout, Formatierung und Platzhalterzellen enthält. Der Übersicht halber erstellen wir alles programmgesteuert.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Warum das wichtig ist*: Das `Worksheet`‑Objekt ist dort, wo wir unsere **smart marker**‑Tags ablegen. Stellen Sie sich die Tags als winzige Platzhalter vor, die der Prozessor später durch echte Werte aus JSON ersetzt.  

## Smart‑Marker‑Tags einfügen (Schritt 2)

Jetzt platzieren wir die Marker‑Tags direkt in Zellen. Die Syntax `${...}` sagt Aspose.Cells „das ist ein Marker“. In unserem Beispiel benötigen wir zwei Marker: einen für den Namen des Master‑Blatts und einen für den Namen des Detail‑Blatts.

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro‑Tipp** – Halten Sie Markernamen kurz und aussagekräftig; sie werden zu den Schlüsseln, die Sie in Ihrem JSON‑Payload verwenden.

## JSON‑Daten vorbereiten (Schritt 3)

Der Prozessor arbeitet mit jeder Datenquelle, die als JSON, `DataSet` oder sogar als einfaches Objekt dargestellt werden kann. Hier ein minimaler JSON‑String, der eine Master‑Detail‑Sammlung enthält. Beachten Sie, dass jede Bestellung sowohl ein `MasterSheetName` als auch ein `DetailSheetName` trägt.

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Warum JSON?* Es ist leichtgewichtig, menschenlesbar und funktioniert hervorragend mit Web‑APIs. Sie könnten dieselben Daten genauso gut aus einer SQL‑Abfrage holen und mit `Newtonsoft.Json` serialisieren.

## SmartMarkerProcessor initialisieren (Schritt 4)

Der `SmartMarkerProcessor` ist die Engine, die das Arbeitsbuch scannt, Marker findet und die Datenbindung durchführt. Die Instanziierung erfolgt in einer einzigen Zeile.

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## Dynamische Blattnamen definieren (Schritt 5)

Hier kommt **dynamic sheet naming excel** richtig zur Geltung. Durch Setzen von `DetailSheetNewName` teilen wir dem Prozessor mit, für jede Bestellung ein neues Detail‑Blatt zu erzeugen und es anhand der `OrderId` zu benennen. Der Platzhalter `${OrderId}` wird aus dem aktuellen Datensatz während der Verarbeitung aufgelöst.

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Achtung** – Wenn Sie die `${}`‑Syntax weglassen, wird das Blatt wörtlich „Detail_${OrderId}“ genannt, anstatt „Detail_1“, „Detail_2“ usw.

## JSON anwenden und Blätter erzeugen (Schritt 6)

Jetzt lässt wir den Prozessor die schwere Arbeit übernehmen. Er liest das JSON, ersetzt die Marker und erstellt bei Bedarf neue Arbeitsblätter.

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### Was passiert im Hintergrund?

1. Der Prozessor liest das `Orders`‑Array.  
2. Für jede Bestellung erstellt er ein **Master‑Blatt** (mit `${Orders.MasterSheetName}`) und ein **Detail‑Blatt** (nach dem Muster `DetailSheetNewName`).  
3. Zellwerte werden durch die entsprechenden JSON‑Felder ersetzt, sodass die erste Zelle des Master‑Blatts „Master_1“, „Master_2“ usw. enthält.  

## Ergebnis speichern und prüfen (optional)

Zum Schluss schreiben wir das Arbeitsbuch auf die Festplatte. Öffnen Sie die Datei in Excel – Sie sollten zwei Master‑Blätter (`Master_1`, `Master_2`) und zwei dynamisch benannte Detail‑Blätter (`Detail_1`, `Detail_2`) sehen.  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Erwartete Ausgabe** – Nach dem Öffnen von `output.xlsx` sehen Sie:

- Blatt **Master_1** mit Zelle A1 = „Master_1“.  
- Blatt **Detail_1** mit Zelle A1 = „Detail_1“.  
- Blatt **Master_2** mit Zelle A1 = „Master_2“.  
- Blatt **Detail_2** mit Zelle A1 = „Detail_2“.  

Damit ist der komplette Zyklus von **wie man Marker verwendet** zur Erreichung von **dynamic sheet naming excel** mit **Aspose.Cells smart markers** abgeschlossen.

---

## Häufige Fragen & Sonderfälle

### Was, wenn ich mehr als zwei Ebenen Hierarchie benötige?

Sie können Marker in den neu erstellten Detail‑Blättern verschachteln. Platzieren Sie einfach zusätzliche `${...}`‑Tags im Vorlagenblatt, bevor Sie die Verarbeitung starten. Der Prozessor durchläuft jede Ebene automatisch.

### Kann ich anstelle von JSON ein DataTable verwenden?

Absolut. `SmartMarkerProcessor` bietet Überladungen für `DataSet`, `DataTable` und sogar benutzerdefinierte Objekte. Der einzige Unterschied ist der Aufruf von `ApplyJson` – stattdessen würden Sie `ApplyDataSet(myDataSet)` verwenden.

### Wie steuere ich die Reihenfolge der Blatt-Erstellung?

Die Reihenfolge folgt der Sequenz der Quell‑Sammlung. Wenn Sie eine benutzerdefinierte Sortierung benötigen, sortieren Sie einfach das JSON‑Array (oder die DataTable), bevor Sie es dem Prozessor übergeben.

### Gibt es eine Möglichkeit, das Vorlagenblatt nach der Verarbeitung zu verbergen?

Ja. Setzen Sie `sm.Options.RemoveTemplateSheets = true;` bevor Sie `ApplyJson` aufrufen. Das ursprüngliche Blatt (Index 0) wird dann aus dem finalen Arbeitsbuch entfernt.

---

## Vollständiges Beispiel (Alle Schritte kombiniert)

Unten finden Sie das komplette Programm, das Sie in ein neues C#‑Konsolenprojekt kopieren‑und‑einfügen können. Stellen Sie sicher, dass Sie das `Aspose.Cells`‑NuGet‑Paket referenzieren.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

Führen Sie das Programm aus, öffnen Sie `output.xlsx` und Sie sehen die dynamischen Blätter exakt wie oben beschrieben.

---

## Fazit

Wir haben gerade **wie man Marker** in Aspose.Cells verwendet, um ein einfaches Arbeitsbuch in eine Master‑Detail‑Lösung mit **dynamic sheet naming excel** zu verwandeln. Die wichtigsten Erkenntnisse:

1. Platzieren Sie `${...}`‑Smart‑Marker dort, wo Daten erscheinen sollen.  
2. Übergeben Sie JSON (oder eine andere unterstützte Datenquelle) an den `SmartMarkerProcessor`.  
3. Nutzen Sie `DetailSheetNewName`, damit der Prozessor neue Blätter zur Laufzeit benennt.  

Ab hier können Sie weiterführende Szenarien erkunden – Tabellen hinzufügen, Zellen formatieren oder sogar Diagramme einbetten, alles gesteuert durch Smart Markers.

## Verwandte Tutorials

- [Wie man Aspose.Cells Smart Markers in C# für dynamisches Excel‑Reporting implementiert](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Dynamische Excel‑Berichte mit Aspose.Cells .NET Smart Markers generieren](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose.Cells .NET meistern: Smart Markers und benutzerdefinierte Labels für dynamische Excel‑Reports implementieren](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}