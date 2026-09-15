---
category: general
date: 2026-09-15
description: Erfahren Sie, wie Sie Schriftarten in SVG einbetten und Excel‑Diagramme
  nach PowerPoint exportieren, einschließlich der Umwandlung von XLSX zu SVG und von
  XLSX zu PPTX mit vollständigen Codebeispielen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: de
lastmod: 2026-09-15
og_description: Schriften in SVG einbetten und Excel‑Diagramm mit Schritt‑für‑Schritt‑C#‑Code
  nach PowerPoint exportieren. XLSX schnell und zuverlässig in SVG und PPTX konvertieren.
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: Schriftarten in SVG einbetten und Excel‑Diagramm nach PowerPoint exportieren
  – vollständige Anleitung
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Wie man Schriftarten in SVG einbettet, wenn Excel‑Dateien in SVG und PowerPoint
  konvertiert werden
url: /de/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man Schriftarten in SVG einbettet, wenn Excel‑Dateien in SVG und PowerPoint konvertiert werden  

Wenn Sie **Schriftarten in SVG einbetten** müssen, während Sie eine Excel‑Arbeitsmappe konvertieren, zeigt Ihnen diese Anleitung genau, wie das geht. Sie erfahren außerdem, wie Sie **Excel‑Diagramm nach PowerPoint exportieren** und wie Sie **XLSX nach SVG** sowie **XLSX nach PPTX** mit editierbaren Diagrammen konvertieren.  

Die programmgesteuerte Arbeit mit Excel‑Daten bedeutet häufig, dass derselbe visuelle Inhalt zwischen verschiedenen Dateiformaten verschoben werden muss. Das manuelle Neuerstellen eines Diagramms in PowerPoint oder das erneute Anwenden von Schriftarten in einem SVG ist fehleranfällig und zeitaufwändig. Am Ende dieses Tutorials besitzen Sie ein einzelnes, wiederverwendbares C#‑Snippet, das:

* Eine Arbeitsmappe als SVG‑Datei mit eingebetteten Schriftarten und Font‑Variation‑Selectors speichert.  
* Dieselbe Arbeitsmappe als PPTX‑Datei exportiert, wobei das Diagramm editierbar bleibt.  

Voraussetzung ist lediglich eine aktuelle Version von **Aspose.Cells for .NET** (2024‑x oder neuer) und eine .NET‑Entwicklungsumgebung wie Visual Studio 2022.

---

## Was Sie benötigen  

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.8).  
* Aspose.Cells for .NET NuGet‑Paket (`Install-Package Aspose.Cells`).  
* Eine Excel‑Datei (`input.xlsx`), die mindestens ein Diagramm enthält.  
* Schreibrechte für das Ausgabeverzeichnis.  

---

## Schriftarten in SVG einbetten beim Konvertieren von XLSX nach SVG  

Das Einbetten von Schriftarten stellt sicher, dass das SVG auf jedem Gerät korrekt dargestellt wird, selbst wenn das Zielsystem die ursprünglichen Schriftarten nicht installiert hat. Die Klasse `SvgSaveOptions` bietet zwei Flags, die dies ermöglichen: `EmbedFonts` und `FontVariationSelectors`.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**Warum das funktioniert:**  
* `EmbedFonts = true` kopiert die Schriftdateien in den `<defs>`‑Abschnitt des SVGs und eliminiert externe Abhängigkeiten.  
* `FontVariationSelectors = true` fügt die notwendigen Selektoren für Schriftarten hinzu, die OpenType‑Features unterstützen, und bewahrt Glyphen‑Variationen wie Ligaturen.  

**Erwartetes Ergebnis:** Öffnen Sie `WithFonts.svg` in einem modernen Browser; der Text im Diagramm oder in den Zellen erscheint mit exakt derselben Schriftart wie in Excel, selbst auf Rechnern, auf denen diese Schriftart nicht installiert ist.

---

## Excel‑Diagramm nach PowerPoint exportieren mit editierbaren Diagrammen  

Wenn Sie ein Diagramm in eine PowerPoint‑Folie einbetten möchten, das der Empfänger jedoch noch bearbeiten können soll, bietet Aspose.Cells `PptxSaveOptions` das Flag `ExportEditableChart`.

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**Warum das wichtig ist:**  
Durch Setzen von `ExportEditableChart` auf `true` wird das Diagramm als Office‑Open‑XML‑Diagrammobjekt statt als statisches Bild gespeichert. Öffnen Sie `EditableChart.pptx` in PowerPoint, klicken Sie mit der rechten Maustaste auf das Diagramm → **Edit Data** und ändern Sie die Datenreihen wie bei einem nativen PowerPoint‑Diagramm.

**Verifizierungsschritte:**  

1. Öffnen Sie `EditableChart.pptx` in PowerPoint.  
2. Suchen Sie die Folie, die das Diagramm enthält.  
3. Wählen Sie **Chart Tools → Design → Edit Data**.  
4. Bestätigen Sie, dass das Excel‑ähnliche Datenraster erscheint und Sie Werte ändern können.

---

## XLSX nach SVG – vollständige Workflow‑Zusammenfassung  

Unten finden Sie eine kompakte Version, die das Laden, optionale Datenmanipulationen und das Speichern als SVG kombiniert. Verwenden Sie diese, wenn Sie ausschließlich die SVG‑Ausgabe benötigen.

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

Aufruf der Methode erfolgt wie folgt:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**Tipp für Sonderfälle:** Enthält Ihre Arbeitsmappe benutzerdefinierte Schriftarten, die nicht auf dem Server installiert sind, betten Sie diese manuell ein, bevor Sie `Save` aufrufen. Nutzen Sie `FontInfoCollection`, um die Schriftdateien über die Eigenschaft `CustomFonts` zu `SvgSaveOptions` hinzuzufügen (verfügbar in neueren Aspose.Cells‑Versionen).

---

## XLSX nach PPTX – Diagrammbearbeitung erhalten  

Die folgende Hilfsmethode demonstriert den **XLSX‑nach‑PPTX**‑Pfad, wobei das Diagramm editierbar bleibt.

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

Verwendung:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**Häufige Frage:** *Was, wenn meine Arbeitsmappe mehrere Arbeitsblätter mit Diagrammen enthält?*  
**Antwort:** Aspose.Cells exportiert standardmäßig das erste Arbeitsblatt. Um weitere Blätter zu berücksichtigen, iterieren Sie über `workbook.Worksheets`, kopieren jedes Diagramm auf eine neue Folie und speichern jede Folie einzeln mit `Presentation`‑Objekten von Aspose.Slides. Dieses erweiterte Szenario geht über den Basis‑„Arbeitsmappe als SVG speichern“‑ und „Excel‑Diagramm nach PowerPoint exportieren“‑Ablauf hinaus, aber die Kern‑Flags bleiben gleich.

---

## Praktische Tipps und Fallstricke  

* **Performance:** Das Einbetten von Schriftarten erhöht die SVG‑Dateigröße. Bei Platzproblemen setzen Sie `EmbedFonts = false` und nutzen web‑sichere Schriftarten.  
* **Schriftlizenzierung:** Stellen Sie sicher, dass Sie das Recht haben, die verwendeten Schriftarten einzubetten; einige kommerzielle Schriften schränken das Einbetten ein.  
* **Diagramm‑Kompatibilität:** Editierbare Diagramme werden als `chart.xml`‑Teile innerhalb der PPTX gespeichert. Sehr komplexe Diagramme (z. B. 3‑D‑ oder Kombidiagramme) können beim Bearbeiten in PowerPoint Styling‑Verluste erleiden. Testen Sie die gängigsten Diagrammtypen, die Sie benötigen.  
* **Versionskonflikte:** Das Flag `ExportEditableChart` erfordert Aspose.Cells 20.10 oder neuer. Ältere Versionen fallen stillschweigend auf ein Rasterbild zurück.  
* **Thread‑Safety:** Workbook‑Objekte sind nicht thread‑sicher. Erzeugen Sie in einem Web‑Service‑Szenario pro Anfrage eine neue `Workbook`‑Instanz.  

---

## Vollständiges End‑zu‑End‑Beispiel  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

Beim Ausführen dieses Programms entstehen zwei Dateien:

* **WithFonts.svg** – ein SVG, das exakt wie die Excel‑Ansicht gerendert wird, inklusive Schriftarten.  
* **EditableChart.pptx** – eine PowerPoint‑Präsentation, in der das Diagramm direkt bearbeitet werden kann.

---

## Fazit  

Sie wissen nun, wie Sie **Schriftarten in SVG einbetten**, wenn Sie **XLSX nach SVG** konvertieren, und wie Sie **Excel‑Diagramm nach PowerPoint exportieren**, wobei das Diagramm editierbar bleibt. Der gleiche Code demonstriert zudem eine saubere Methode, **Arbeitsmappe als SVG zu speichern** und **XLSX nach PPTX** mit minimalem Aufwand zu konvertieren.  

Von hier aus können Sie weitere Themen erkunden, etwa:

* Benutzerdefinierte Schriftarten programmgesteuert hinzufügen (`svgOptions.CustomFonts`).  
* Batch‑Verarbeitung mehrerer Arbeitsmappen in einem Hintergrunddienst.  
* Verwendung von Aspose.Slides zum Erstellen von mehrseitigen PPTX‑Dateien, die mehrere Excel‑Diagramme kombinieren.  

Probieren Sie die Optionen aus, passen Sie die Snippets an Ihr Projekt an und genießen Sie zuverlässige Excel‑zu‑SVG/PPTX‑Konvertierungen ohne manuelle Nachbearbeitung. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?  

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, damit Sie weitere API‑Funktionen meistern und alternative Implementierungsansätze in Ihren eigenen Projekten erkunden können.

- [Wie man Excel‑Diagramme mit Aspose.Cells für .NET in SVG konvertiert (Schritt‑für‑Schritt‑Anleitung)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Excel‑Diagramm nach SVG konvertieren Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}