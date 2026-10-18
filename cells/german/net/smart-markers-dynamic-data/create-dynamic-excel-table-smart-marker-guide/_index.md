---
category: general
date: 2026-05-23
description: Erstelle eine dynamische Excel‑Tabelle mit einer Vorlage und JSON‑Daten.
  Erfahre, wie du eine Excel‑Vorlage lädst, Excel‑Berichte automatisierst und Excel
  schnell aus JSON befüllst.
draft: false
keywords:
- create dynamic excel table
- load excel template
- automate excel report
- populate excel from json
- generate excel report json
language: de
og_description: Erstellen Sie in wenigen Minuten dynamische Excel-Tabellen mit einer
  Vorlage und JSON. Dieses Tutorial zeigt, wie man eine Excel-Vorlage lädt, Excel-Berichte
  automatisiert und Excel aus JSON befüllt.
og_title: Dynamische Excel‑Tabelle erstellen – Smart Marker Leitfaden
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create dynamic excel table using a template and JSON data. Learn how
    to load excel template, automate excel report, and populate excel from json quickly.
  headline: Create Dynamic Excel Table – Smart Marker Guide
  type: TechArticle
tags:
- Excel
- Smart Markers
- JSON
- .NET
title: Dynamische Excel‑Tabelle erstellen – Smart‑Marker‑Leitfaden
url: /de/net/smart-markers-dynamic-data/create-dynamic-excel-table-smart-marker-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dynamische Excel-Tabelle erstellen – Smart Marker Anleitung

Haben Sie schon einmal eine **create dynamic excel table** benötigt, die sich automatisch für jeden Datensatz in Ihrem Datensatz erweitert? Sie sind nicht allein. Egal, ob Sie ein monatliches Verkaufs‑Dashboard oder ein kundenbezogenes Rechnungspaket erstellen, die Möglichkeit, **populate excel from json** zu nutzen, ohne endlose Schleifen zu schreiben, kann Stunden sparen.

In diesem Tutorial führen wir Sie durch eine vollständige, praxisnahe Lösung, die zeigt, wie man **load excel template**, einen Smart Marker einbettet, ihn mit JSON füttert und schließlich die **automate excel report**‑Erstellung durchführt. Am Ende haben Sie ein sofort ausführbares .NET‑Projekt, das aus einer einzigen JSON‑Payload eine professionell formatierte Excel‑Arbeitsmappe erzeugt.

---

## Was Sie benötigen

- **Aspose.Cells for .NET** (oder jede Bibliothek, die Smart Markers unterstützt). Das Beispiel verwendet Version 24.5, aber jede aktuelle Version funktioniert.
- Visual Studio 2022 (oder Ihre bevorzugte C#‑IDE).
- Eine einfache Excel‑Vorlagendatei (`template.xlsx`), die in einem von Ihnen kontrollierten Ordner liegt.
- Ein JSON‑String, der eine Sammlung namens `Customers` enthält.

Das war's – keine zusätzlichen Dienste, keine Datenbankverbindungen, nur reiner Code.

---

## Schritt 1: Vorlage-Arbeitsmappe erstellen – Load Excel Template

Das Erste, was wir tun, ist **load excel template** in den Speicher zu laden. Betrachten Sie die Vorlage als Leinwand, auf der ein spezieller Platzhalter dem Prozessor sagt, wo Zeilen wiederholt werden sollen.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

// Load the template workbook (make sure the path is correct)
Workbook workbook = new Workbook(@"C:\Reports\template.xlsx");

// Grab the first worksheet – this is where our Smart Marker lives
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** Das einmalige Laden der Vorlage minimiert die Dateiein-/-ausgabe und ermöglicht die Wiederverwendung desselben Layouts für viele Berichte. Außerdem isoliert es die Smart‑Marker‑Logik vom Rest Ihres Codes, was eine saubere Trennung der Verantwortlichkeiten darstellt.

---

## Schritt 2: Smart Marker einfügen – Create Dynamic Excel Table

Jetzt betten wir einen **Smart Marker** ein, der für jeden Eintrag in der `Customers`‑Sammlung eine Tabelle wiederholt. Die Syntax `${Customers.RepeatWorksheet}` weist Aspose.Cells an, das gesamte Arbeitsblatt für jeden Kunden zu duplizieren.

```csharp
// Place the Smart Marker in cell A1 (top‑left corner)
worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");
```

> **Pro tip:** Wenn Sie nur Zeilen statt ganzer Arbeitsblätter wiederholen müssen, verwenden Sie `${Customers.Repeat}` in der ersten Zeile der Tabelle. Das Wiederholen auf Arbeitsblattebene ist praktisch, wenn jeder Kunde sein eigenes Registerblatt erhält.

---

## Schritt 3: SmartMarkerProcessor vorbereiten – Automate Excel Report

Mit dem Marker an Ort und Stelle erstellen wir einen `SmartMarkerProcessor`. Dieses Objekt steuert die Datenbindung zwischen JSON und der Excel‑Vorlage.

```csharp
// Initialize the processor with the workbook that contains the marker
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

Der Prozessor ist leichtgewichtig; Sie können ihn bei Bedarf für mehrere JSON‑Payloads wiederverwenden.

---

## Schritt 4: JSON‑Daten zuführen – Populate Excel from JSON

Hier geschieht die Magie. Wir übergeben einen JSON‑String, der ein Array von Kunden enthält. Jeder Kunde kann Felder wie `Name`, `Email` und `Total` besitzen.

```csharp
// Sample JSON data – in a real scenario you might read this from a file or API
string customersJson = @"
{
  ""Customers"": [
    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
  ]
}";

// Apply the JSON to the processor – this populates the workbook
processor.ApplyJson(customersJson);
```

> **Why JSON?** JSON ist sprachunabhängig und lässt sich leicht aus APIs, Datenbanken oder sogar manueller Eingabe erzeugen. Die Verwendung von `ApplyJson` bedeutet, dass Sie Objekte nicht manuell zuordnen müssen; der Prozessor übernimmt die schwere Arbeit.

---

## Schritt 5: Ergebnis speichern – Generate Excel Report JSON

Abschließend schreiben wir die gefüllte Arbeitsmappe auf die Festplatte. Die Ausgabedatei enthält nun ein separates Arbeitsblatt für jeden Kunden, das jeweils mit den Daten aus unserem JSON gefüllt ist.

```csharp
// Save the filled workbook – choose a path that makes sense for your app
workbook.Save(@"C:\Reports\output.xlsx");
```

### Erwartete Ausgabe

- **output.xlsx** wird drei Arbeitsblätter mit den Namen `Sheet1`, `Sheet2`, `Sheet3` (oder welcher Namenskonvention Ihre Vorlage auch folgt) enthalten.
- Jedes Blatt zeigt die Werte `Name`, `Email` und `Total` für einen einzelnen Kunden an.
- Das Layout, das Sie in `template.xlsx` entworfen haben (Kopfzeilen, Formatierung, Formeln), bleibt in allen erzeugten Blättern erhalten.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das komplette, sofort ausführbare Programm. Kopieren Sie es in eine Konsolenanwendung, passen Sie die Dateipfade an und drücken Sie **F5**.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace DynamicExcelDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the template workbook
            string templatePath = @"C:\Reports\template.xlsx";
            Workbook workbook = new Workbook(templatePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Insert the Smart Marker that repeats the worksheet per customer
            worksheet.Cells[0, 0].PutValue("${Customers.RepeatWorksheet}");

            // 3️⃣ Create the SmartMarkerProcessor
            SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

            // 4️⃣ JSON data containing a collection of customers
            string customersJson = @"
            {
                ""Customers"": [
                    { ""Name"": ""Acme Corp"", ""Email"": ""contact@acme.com"", ""Total"": 12500 },
                    { ""Name"": ""Globex"", ""Email"": ""sales@globex.com"", ""Total"": 9800 },
                    { ""Name"": ""Initech"", ""Email"": ""info@initech.com"", ""Total"": 15400 }
                ]
            }";

            // Apply the JSON – this populates the workbook dynamically
            processor.ApplyJson(customersJson);

            // 5️⃣ Save the generated report
            string outputPath = @"C:\Reports\output.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"✅ Dynamic Excel report generated at: {outputPath}");
        }
    }
}
```

Führen Sie das Programm aus, öffnen Sie `output.xlsx`, und Sie sehen eine **create dynamic excel table** in Aktion – jeder Kunde erhält ein eigenes Blatt, vollständig formatiert nach Ihrem Entwurf.

---

## Häufige Fragen & Sonderfälle

| Frage | Antwort |
|----------|--------|
| *Was ist, wenn mein JSON verschachtelte Objekte enthält?* | Smart Markers unterstützen die Punktnotation (`${Customers.Address.City}`), solange die JSON‑Hierarchie übereinstimmt. |
| *Kann ich die erzeugten Arbeitsblätter nach dem Kunden benennen?* | Ja – fügen Sie einen Marker wie `${Customers.Name}` in die Zelle für den Arbeitsblattnamen ein oder verwenden Sie `processor.ApplyJson(customersJson, \"Customers\")` mit einem Namensmuster. |
| *Wie sieht es mit großen Datensätzen (10 k+ Zeilen) aus?* | Der Prozessor streamt Daten effizient, aber achten Sie auf den Speicherverbrauch. Erwägen Sie, den Bericht in mehrere Dateien aufzuteilen, wenn Sie Leistungsgrenzen erreichen. |
| *Benötige ich eine Lizenz für Aspose.Cells?* | Eine kostenlose Evaluation reicht für Tests, aber eine lizenzierte Version entfernt Wasserzeichen und bietet alle Funktionen. |
| *Kann ich diesen Ansatz mit .NET Core verwenden?* | Absolut – Aspose.Cells unterstützt .NET 6/7/8. Verweisen Sie einfach auf das NuGet‑Paket und der Code bleibt unverändert. |

---

## Tipps für produktionsreife Implementierungen

- **Validate JSON** bevor Sie es an `ApplyJson` übergeben. Ein fehlerhaftes Payload wirft eine `JsonParseException`.
- **Cache the template**, wenn Sie in kurzer Zeit viele Berichte erzeugen; wiederholtes Laden von der Festplatte ist unnötiger I/O.
- **Lock the workbook** während der Verarbeitung, wenn Sie dies in einem mehrthreadigen Web‑Service ausführen, um Rennbedingungen zu vermeiden.
- **Add error handling** um `workbook.Save`, um Berechtigungsprobleme oder gesperrte Dateien elegant zu behandeln.
- **Customize styling** in der Vorlage (bedingte Formatierung, Formeln), damit die erzeugten Blätter die Geschäftslogik ohne zusätzlichen Code beibehalten.

---

## Fazit

Sie haben nun ein solides End‑zu‑Ende‑Muster, wie Sie **create dynamic excel table** mit einer Vorlage, Smart Markern und JSON‑Daten erstellen. Durch **loading excel template**, das Einfügen eines Wiederholungsmarkers und **populate excel from json** können Sie die **automate excel report**‑Erstellung mit nur wenigen Zeilen C# automatisieren.

Nächste Schritte? Versuchen Sie, Diagramme hinzuzufügen, die auf die dynamischen Tabellen verweisen, oder exportieren Sie dasselbe JSON mit Aspose.Words in ein PDF. Sie könnten auch mit **generate excel report json** aus einer Datenbankabfrage experimentieren, um den Kreislauf zu schließen.

## Verwandte Tutorials

- [Pivot-Tabelle in Excel mit Aspose.Cells für .NET erstellen](/cells/english/net/pivot-tables/create-pivot-table/)
- [Dynamische Liniendiagramme in Excel mit Aspose.Cells für .NET: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/charts-graphs/create-line-charts-excel-aspose-cells-dotnet/)
- [Wie man Kontrollkästchen in Excel mit Aspose.Cells für .NET erstellt | Datenvalidierung‑Tutorial](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}