---
category: general
date: 2026-11-19
description: Wie man ein Arbeitsblatt wiederholt, während man Excel mit Array‑Daten
  füllt. Lernen Sie, in wenigen Schritten mehrere Arbeitsblätter zu erzeugen und ein
  Arbeitsblatt aus einer Liste zu füllen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: de
lastmod: 2026-11-19
og_description: Wie man ein Arbeitsblatt mit SmartMarkerProcessor wiederholt. Folgen
  Sie dieser Anleitung, um Excel mit Array‑Daten zu füllen, mehrere Arbeitsblätter
  zu erzeugen und ein Arbeitsblatt aus einer Liste zu befüllen.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Wie man ein Arbeitsblatt in Excel wiederholt – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Wie man ein Arbeitsblatt in Excel mit SmartMarkerProcessor wiederholt
url: /de/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Arbeitsblatt in Excel mit SmartMarkerProcessor wiederholt

Wenn Sie **wie man ein Arbeitsblatt wiederholt** beim Erstellen von Excel‑Berichten benötigen, zeigt Ihnen dieser Leitfaden eine vollständige, ausführbare Lösung. Am Ende des Tutorials können Sie **Excel mit Array‑Daten füllen**, **mehrere Arbeitsblätter erzeugen** und **ein Arbeitsblatt aus einer Liste füllen** mithilfe der SmartMarkerProcessor‑Bibliothek.

Das Wiederholen eines Arbeitsblatts ist ein häufiges Bedürfnis, wenn jede Abteilung, Region oder Zeitperiode ihren eigenen Reiter benötigt. Das untenstehende Beispiel zeigt die genauen Schritte, erklärt, warum jede Einstellung wichtig ist, und behandelt Sonderfälle wie leere Listen oder benutzerdefinierte Benennungen.

## Voraussetzungen

- .NET 6.0 oder höher installiert
- Ein Verweis auf das **GroupDocs.Viewer** (oder ein äquivalentes) NuGet‑Paket, das `SmartMarkerProcessor` enthält
- Eine Excel‑Vorlagendatei (`.xlsx`) mit einem Marker wie `${repeat:Dept}`, der in einer Zeile platziert ist, die Sie wiederholen möchten
- Grundlegende Kenntnisse in C# und LINQ (optional, aber hilfreich)

Es werden keine zusätzlichen Drittanbieter‑Bibliotheken benötigt.

## Schritt 1: Erstellen der SmartMarkerProcessor‑Instanz

Der Prozessor koordiniert den Marker‑Ersetzungsvorgang und die Duplizierung von Arbeitsblättern. Die Instanziierung ohne Argumente verwendet die Standardoptionen.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Das frühe Erstellen des Prozessors ermöglicht es Ihnen, globale Optionen zu konfigurieren, bevor Daten angewendet werden. Dies ist die Grundlage, um **wie man ein Arbeitsblatt korrekt wiederholt**.

## Schritt 2: Aktivieren der Arbeitsblatt‑Wiederholung

Standardmäßig ersetzt der Prozessor Marker nur im aktuellen Blatt. Das Setzen von `RepeatWorksheet` auf `true` weist die Engine an, das gesamte Arbeitsblatt für jedes Element in der Datensammlung zu duplizieren.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Das Aktivieren dieser Option ist der Schlüssel, um **mehrere Arbeitsblätter zu erzeugen** – der Prozessor erstellt einen neuen Reiter für jedes Element im `Dept`‑Array und behält die ursprüngliche Formatierung bei.

## Schritt 3: Vorbereitung der Datenquelle als Array oder Liste

SmartMarkerProcessor arbeitet mit jedem aufzählbaren Typ, aber die Verwendung eines Arrays macht die Absicht klar, wenn Sie **ein Arbeitsblatt aus einer Liste füllen** möchten. Hier erstellen wir ein anonymes Objekt, das eine `Dept`‑Eigenschaft enthält, die ein String‑Array hält.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Wenn Sie bereits eine `List<string>` haben, können Sie diese direkt übergeben; der Prozessor behandelt sie auf dieselbe Weise. Wichtig ist, dass der Property‑Name (`Dept`) mit dem Marker `${repeat:Dept}` in der Vorlage übereinstimmt.

## Schritt 4: Laden des Vorlagen‑Arbeitsblatts

Angenommen, Sie haben ein `ExcelPackage` (von EPPlus) oder ein `Workbook`‑Objekt, rufen Sie das Arbeitsblatt ab, das Sie wiederholen möchten. Die Variable `ws` repräsentiert dieses Blatt.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Wenn Sie eine andere Bibliothek bevorzugen (z. B. ClosedXML), gilt dasselbe Prinzip: Sie erhalten ein Arbeitsblatt‑Objekt, das die erforderliche Schnittstelle implementiert.

## Schritt 5: Verarbeiten des Arbeitsblatts mit den Daten

Wenden Sie nun die Daten auf die Vorlage an. Der Prozessor dupliziert das Arbeitsblatt für jede Abteilung, ersetzt den `${repeat:Dept}`‑Marker durch den tatsächlichen Abteilungsnamen und lässt den Rest des Blatts unverändert.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

Nachdem `Process` abgeschlossen ist, wird `ws` zum ersten von mehreren Arbeitsblättern – eines pro Abteilung. Der Name des Originalblatts bleibt erhalten, während die Duplikate inkrementelle Suffixe erhalten (z. B. „Sheet1 (1)“, „Sheet1 (2)“). Sie können sie anschließend umbenennen, wenn Sie ein benutzerdefiniertes Benennungsschema benötigen.

### Erwartete Ausgabe

Wenn Sie die resultierende Arbeitsmappe öffnen, sollten Sie folgendes sehen:

- **Sheet1** – die Originalvorlage (oft leer oder als Master verwendet)
- **Sheet1 (1)** – gefüllt mit „HR“
- **Sheet1 (2)** – gefüllt mit „IT“
- **Sheet1 (3)** – gefüllt mit „Finance“

Jedes Blatt enthält das gleiche Layout, jedoch mit dem Abteilungsnamen anstelle des `${repeat:Dept}`‑Markers.

## Umgang mit Sonderfällen

### Leere oder null‑Arrays

Wenn `Dept` null oder leer ist, erstellt der Prozessor keine zusätzlichen Arbeitsblätter. Um eine völlig leere Arbeitsmappe zu vermeiden, können Sie eine Prüfung hinzufügen:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Benutzerdefinierte Arbeitsblattnamen

Das Standard‑Benennungsschema passt möglicherweise nicht zu allen Berichtsanfordernissen. Nach der Verarbeitung können Sie jedes Blatt mit einer Schleife umbenennen:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Zusätzliche Spalten füllen

Wenn Sie **Excel mit Array‑Werten** über einen einzelnen Marker hinaus füllen müssen, erweitern Sie das Datenobjekt:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Passen Sie dann die Vorlagen‑Marker zu `${repeat:Dept.Name}` und `${repeat:Dept.Headcount}` an. Der Prozessor wiederholt die Zeile für jede Abteilung und füllt beide Spalten.

## Vollständiges funktionierendes Beispiel

Unten finden Sie eine eigenständige Konsolenanwendung, die den gesamten Ablauf vom Laden der Vorlage bis zum Speichern der finalen Arbeitsmappe demonstriert.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Erklärung der wichtigsten Abschnitte**

- **Processor creation** – legt die Engine fest, die Marker interpretiert.
- **RepeatWorksheet option** – aktiviert die Kernfunktion, die *wie man ein Arbeitsblatt wiederholt* beantwortet.
- **Data source** – verwendet ein Array (`new[]`), um **Excel mit Array zu füllen** zu erfüllen.
- **Template loading** – zeigt eine gängige Methode, ein Arbeitsblatt‑Objekt zu erhalten.
- **Processing** – führt die Duplizierung und Dateneinfügung in einem Aufruf aus.
- **Renaming** – zeigt, wie die generischen Namen „(1)“, „(2)“ in sinnvolle Titel umgewandelt werden, ein typisches Erfordernis nach **mehrere Arbeitsblätter zu erzeugen**.

Das Ausführen dieses Programms erzeugt `Result.xlsx` mit drei abteilungsspezifischen Reitern, die jeweils aus dem Array gefüllt werden.

## Häufige Fallstricke und Profi‑Tipps

- **Marker spelling** – der Marker muss exakt dem Property‑Namen entsprechen (`${repeat:Dept}`). Ein Tippfehler verhindert die Wiederholung.
- **Worksheet index** – nach der Verarbeitung bleibt das Originalblatt bei Index 0; erzeugte Blätter folgen sequenziell. Falsche Indizierung kann dazu führen, dass der falsche Reiter umbenannt wird.
- **Large data sets** – das Erzeugen von Hunderten von Arbeitsblättern kann die Dateigröße stark erhöhen. Erwägen Sie, Berichte aufzuteilen oder ein einzelnes Blatt mit gruppierten Abschnitten zu verwenden, falls die Leistung ein Problem darstellt.
- **Thread safety** – `SmartMarkerProcessor` ist nicht thread‑sicher. Erstellen Sie pro Thread eine separate Instanz, wenn Sie mehrere Arbeitsmappen parallel verarbeiten.

## Fazit

Sie wissen jetzt, **wie man ein Arbeitsblatt** in Excel mit SmartMarkerProcessor wiederholt, wie man **Excel mit Array‑Daten** füllt, wie man **mehrere Arbeitsblätter erzeugt** und wie man **ein Arbeitsblatt aus einer Liste füllen** effizient. Das vollständige Beispiel verbindet alle Konzepte, und der optionale Umbenennungsschritt ermöglicht es Ihnen, saubere, benutzerfreundliche Reiternamen zu erzeugen.

Als Nächstes könnten Sie erkunden:

- Verwendung von **ein Arbeitsblatt aus einer Liste füllen** mit komplexen Objekten (verschachtelte Sammlungen)
- Anwenden von bedingter Formatierung nach der Duplizierung von Arbeitsblättern
- Exportieren der erzeugten Arbeitsmappe nach PDF oder CSV für die Weiterverarbeitung

Passen Sie den Code gern an Ihre eigenen Berichtsszenarien an und freuen Sie sich über die sichere Automatisierung von Excel‑Arbeitsmappen!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu beherrschen und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Wie man Arbeitsblätter wiederholt – Komplett‑Leitfaden für Excel‑Automatisierung](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Arbeitsblatt pro Element erstellen – Wie man ein Arbeitsblatt in C# wiederholt](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Wie man ein Array in Excel erweitert und eine Vorlage füllt](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}