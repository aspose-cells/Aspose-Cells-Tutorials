---
category: general
date: 2026-01-14
description: Wie man eine Pivot‑Tabelle mit Aspose.Cells kopiert und gleichzeitig
  lernt, Excel in PPTX zu konvertieren, einen Bereich in eine andere Arbeitsmappe
  zu kopieren und ein Textfeld in PPTX editierbar zu machen – alles in einem einzigen
  Tutorial.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: de
og_description: Wie man eine Pivot‑Tabelle kopiert und dann Excel in PPTX konvertiert,
  einen Bereich in eine andere Arbeitsmappe kopiert und ein Textfeld in PPTX editierbar
  macht – alles mit Aspose.Cells.
og_title: Wie man Pivot-Tabellen in C# kopiert – Vollständige Excel‑zu‑PPTX‑Anleitung
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Wie man eine Pivot‑Tabelle in C# kopiert – Excel in PPTX konvertieren, Bereich
  kopieren und Textfeld editierbar machen
url: /de/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Pivot-Tabellen in C# kopiert – Vollständiger Excel-zu-PPTX-Leitfaden

Wie man eine Pivot‑Tabelle von einer Arbeitsmappe in eine andere kopiert, ist eine häufige Frage, wenn Sie Excel‑basierte Berichte automatisieren. In diesem Tutorial gehen wir drei praxisnahe Szenarien mit **Aspose.Cells for .NET** durch: Kopieren eines Pivot‑Tabellen‑Bereichs, Exportieren eines Arbeitsblatts in eine PPTX‑Datei mit einem editierbaren Textfeld und Befüllen einer einzelnen Zelle mit einem JSON‑Array über Smart Markers.  

Sie sehen außerdem, wie man **Excel in PPTX konvertiert**, **Bereich in eine andere Arbeitsmappe kopiert** und **Textfeld in PPTX editierbar macht**, ohne die Formatierung zu zerstören. Am Ende haben Sie eine einsatzbereite Code‑Basis, die Sie in jedes .NET‑Projekt einbinden können.

> **Profi‑Tipp:** Alle Beispiele richten sich an Aspose.Cells 23.12, aber dieselben Konzepte gelten auch für frühere Versionen mit kleinen API‑Anpassungen.

![Diagramm, das zeigt, wie eine Pivot‑Tabelle kopiert, ein Arbeitsblatt nach PPTX exportiert und ein JSON‑Array eingefügt wird – Workflow zum Kopieren von Pivot‑Tabellen](how-to-copy-pivot-table-diagram.png)

---

## Was Sie benötigen

- Visual Studio 2022 (oder jede C#‑IDE)
- .NET 6.0 oder späteres Runtime
- Aspose.Cells for .NET NuGet-Paket  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Zwei Beispiel‑Excel‑Dateien (`source.xlsx`, `chartWithTextbox.xlsx`) in einem von Ihnen kontrollierten Ordner abgelegt (ersetzen Sie `YOUR_DIRECTORY` durch Ihren tatsächlichen Pfad).

Keine zusätzlichen Bibliotheken sind erforderlich; dieselbe `Aspose.Cells`‑Assembly verarbeitet Excel, PPTX und Smart Markers.

---

## Wie man Pivot‑Tabellen kopiert und deren Daten bewahrt

Wenn Sie einen Bereich kopieren, der eine Pivot‑Tabelle enthält, ist das Standardverhalten, nur die **Werte** einzufügen. Um die Pivot‑Definition intakt zu halten, müssen Sie das Flag `CopyPivotTable` aktivieren.

### Schritt‑für‑Schritt

1. **Laden Sie die Quell‑Arbeitsmappe**, die die Pivot‑Tabelle enthält.  
2. **Erstellen Sie eine leere Ziel‑Arbeitsmappe** – diese erhält den kopierten Bereich.  
3. **Verwenden Sie `CopyRange` mit `CopyPivotTable = true`**, damit die Pivot‑Definition mit den Daten mitkommt.  
4. **Speichern Sie die Zieldatei** an einem beliebigen Ort.

#### Vollständiges Code‑Beispiel

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Warum das funktioniert:**  
`CopyOptions.CopyPivotTable` weist Aspose.Cells an, das zugrunde liegende `PivotTable`‑Objekt zu klonen, anstatt nur dessen gerenderte Werte. Die Ziel‑Arbeitsmappe enthält nun eine voll funktionsfähige Pivot‑Tabelle, die Sie programmgesteuert aktualisieren oder ändern können.

**Randfall:** Wenn die Quell‑Arbeitsmappe externe Datenquellen verwendet, müssen Sie möglicherweise die Daten einbetten oder die Verbindungszeichenfolgen nach dem Kopieren anpassen, sonst zeigt die Pivot‑Tabelle “#REF!”.

---

## Excel nach PPTX konvertieren und Textfeld editierbar machen

Das Exportieren eines Arbeitsblatts nach PowerPoint ist praktisch, um Folienpräsentationen direkt aus Daten zu erstellen. Standardmäßig wird das exportierte Textfeld zu einer statischen Form, aber das Setzen von `IsTextBoxEditable` kehrt dieses Verhalten um.

### Schritt‑für‑Schritt

1. **Öffnen Sie die Arbeitsmappe**, die das Diagramm und das Textfeld enthält, das Sie exportieren möchten.  
2. **Konfigurieren Sie `ImageOrPrintOptions`** mit `SaveFormat = SaveFormat.Pptx`.  
3. **Definieren Sie einen Druckbereich**, der das Textfeld einschließt.  
4. **Aktivieren Sie `IsTextBoxEditable`**, damit der Text nach dem Öffnen der PPTX bearbeitet werden kann.  
5. **Speichern Sie die PPTX‑Datei**.

#### Vollständiges Code‑Beispiel

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Ergebnis:** Öffnen Sie `result.pptx` in PowerPoint – das in Excel platzierte Textfeld wird nun zu einem regulären Textfeld, in das Sie schreiben können. Keine manuelle Neuerstellung nötig.

**Häufiges Problem:** Wenn das Arbeitsblatt zusammengeführte Zellen enthält, die den Druckbereich überschneiden, kann die resultierende Folie verschoben werden. Passen Sie den Druckbereich an oder heben Sie die Zusammenführung der Zellen vor dem Export auf.

---

## Bereich in eine andere Arbeitsmappe kopieren mit Smart Markers (JSON → Einzelne Zelle)

Manchmal müssen Sie ein JSON‑Array in eine einzelne Excel‑Zelle einbetten, z. B. wenn Sie Daten an nachgelagerte Systeme übergeben, die einen JSON‑String erwarten. Die Smart Markers von Aspose.Cells können ein Array als einzelne Zelle serialisieren, wenn Sie `ArrayAsSingle = true` setzen.

### Schritt‑für‑Schritt

1. **Laden Sie eine Vorlagen‑Arbeitsmappe**, die einen Smart‑Marker‑Platzhalter enthält (z. B. `&=Items.Name`).  
2. **Bereiten Sie das Datenobjekt vor** – einen anonymen Typ mit einem `Items`‑Array.  
3. **Erstellen Sie einen `SmartMarkerProcessor`** und wenden Sie die Daten mit `ArrayAsSingle` an.  
4. **Speichern Sie die befüllte Arbeitsmappe**.

#### Vollständiges Code‑Beispiel

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Erklärung:**  
Wenn `ArrayAsSingle` true ist, verkettet Aspose.Cells jedes Element von `Items.Name` zu einem JSON‑ähnlichen String (`["A","B"]`) und schreibt ihn in die Zelle, die den Smart Marker enthielt. Dadurch wird vermieden, für jedes Array‑Element eine separate Zeile zu erzeugen.

**Wann zu verwenden:** Ideal zum Exportieren von Konfigurationstabellen, API‑Payloads oder jedem Szenario, bei dem der Empfänger einen kompakten JSON‑String statt eines tabellarischen Layouts erwartet.

---

## Zusätzliche Tipps & Umgang mit Randfällen

| Szenario | Worauf zu achten ist | Vorgeschlagene Lösung |
|----------|----------------------|-----------------------|
| **Große Pivot‑Tabellen** | Speicherauslastung steigt beim Kopieren riesiger Pivot‑Caches. | Verwenden Sie `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` vor dem Laden. |
| **Exportieren nach PPTX mit Bildern** | Bilder können bei niedriger DPI gerastert werden. | Setzen Sie `pptxOptions.ImageResolution = 300` für schärfere Folien. |
| **Smart‑Marker‑JSON‑Formatierung** | Sonderzeichen (`"` , `\`) brechen JSON. | Entkommen Sie ihnen manuell oder verwenden Sie `JsonSerializer`, um vor dem Einspeisen in Smart Markers vorzuseialisieren. |
| **Bereich über verschiedene Excel‑Versionen kopieren** | Ältere `.xls`‑Dateien können Formatierungen verlieren. | Speichern Sie das Ziel als `.xlsx`, um moderne Features zu erhalten. |

---

## Zusammenfassung – Wie man Pivot‑Tabellen kopiert und vieles mehr

Wir begannen mit der Beantwortung von **wie man Pivot‑Tabellen kopiert**, während deren Funktionalität erhalten bleibt, dann zeigten wir, wie man **Excel nach PPTX konvertiert**, **Textfeld in PPTX editierbar macht**, und schließlich, wie man **Bereich in eine andere Arbeitsmappe kopiert** mithilfe von Smart Markers, um ein JSON‑Array als einzelne Zelle einzubetten.  

Alle drei Snippets sind eigenständig; Sie können sie in eine neue Konsolen‑App einfügen, die Dateipfade anpassen und noch heute ausführen.

---

## Was kommt als Nächstes?

- **Andere Exportformate erkunden** – Aspose.Cells unterstützt außerdem PDF, XPS und HTML.  
- **Pivot‑Tabellen programmgesteuert aktualisieren** mit `PivotTable.RefreshData()` nach dem Kopieren.  
- **Smart Markers mit Diagrammen kombinieren**, um dynamische Dashboards zu erzeugen, die automatisch aktualisiert werden.  

Wenn Sie daran interessiert sind, **Arbeitsmappen als PPTX** mit benutzerdefinierten Folienlayouts zu speichern, werfen Sie einen Blick in die Aspose.Cells‑Dokumentation zu `SlideOptions`.  

Fühlen Sie sich frei zu experimentieren – ändern Sie den Druckbereich, probieren Sie verschiedene `CopyOptions` aus oder geben Sie ein komplexeres JSON‑Payload ein. Die API ist flexibel genug für die meisten Reporting‑Pipelines.

### Häufig gestellte Fragen

**F: Kopiert `CopyPivotTable` auch Slicer?**  
**A:** Nicht direkt. Slicer sind separate Objekte; nach dem Kopieren müssen Sie sie entweder neu erstellen oder über die `Worksheet.Shapes`‑Sammlung kopieren.

**F: Kann ich mehrere Arbeitsblätter in ein einziges PPTX‑Deck exportieren?**  
**A:** Ja. Durchlaufen Sie jedes Arbeitsblatt, rufen Sie `Save` mit denselben `ImageOrPrintOptions` auf und setzen Sie `pptxOptions.StartSlideNumber`, um die Nummerierung fortzusetzen.

**F: Was ist, wenn mein JSON‑Array verschachtelte Objekte enthält?**  
**A:** Setzen Sie `ArrayAsSingle = false` und verwenden Sie eine benutzerdefinierte Vorlage, die über 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}