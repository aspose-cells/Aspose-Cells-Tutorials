---
category: general
date: 2026-08-14
description: Exportieren Sie Excel nach PowerPoint mit Aspose.Cells und lernen Sie,
  wie Sie Excel‑Formeln im Code berechnen. Schritt‑für‑Schritt C#‑Beispiel mit vollständigem
  Quellcode.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: de
lastmod: 2026-08-14
og_description: Exportieren Sie Excel nach PowerPoint mit Aspose.Cells und berechnen
  Sie Excel‑Formeln im Code. Folgen Sie diesem vollständigen Leitfaden, um bearbeitbare
  PPTX‑Dateien aus Arbeitsmappen zu erstellen.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Excel nach PowerPoint exportieren mit Aspose.Cells – vollständiges C#‑Tutorial
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Excel nach PowerPoint exportieren mit Aspose.Cells – vollständiger Programmierleitfaden
url: /de/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel nach PowerPoint mit Aspose.Cells exportieren – vollständiger Programmierleitfaden

Wenn Sie **Excel nach PowerPoint** programmgesteuert exportieren müssen, zeigt Ihnen dieses Handbuch genau, wie Sie dies mit Aspose.Cells für .NET erledigen. Sie lernen außerdem, wie Sie **Excel‑Formeln im Code berechnen**, Pivot‑Tabellen kopieren, ohne Definitionen zu verlieren, und die neue Office‑365 EXPAND‑Funktion für dynamische Arrays verwenden.

In den folgenden Abschnitten gehen wir ein real‑world C#‑Beispiel durch, erklären, warum jede Zeile wichtig ist, und behandeln gängige Fallstricke, damit Sie die Lösung an Ihre eigenen Projekte anpassen können.

## Was dieses Tutorial abdeckt

* Laden einer bestehenden Arbeitsmappe (`input.xlsx`)  
* Kopieren eines Bereichs, der eine Pivot‑Tabelle enthält, wobei die Definition erhalten bleibt  
* Exportieren der Arbeitsmappe in eine PowerPoint‑Datei (`.pptx`) mit editierbaren Textfeldern und Formen  
* Exportieren eines Zellbereichs als Zeichenketten mittels benutzerdefinierter Logik  
* Berechnen von Excel‑Formeln im Code, einschließlich der Office‑365 EXPAND‑Funktion  
* Speichern der finalen Arbeitsmappe mit allen angewendeten Änderungen  

**Voraussetzungen**  
* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7.2+)  
* Aspose.Cells für .NET v25.11 oder neuer (die Option `CopyPivotTable` wurde in v25.11 eingeführt)  
* Grundlegendes Verständnis von C# und Excel‑Konzepten wie Bereichen, Pivot‑Tabellen und Formeln  

> **Profi‑Tipp:** Installieren Sie Aspose.Cells über NuGet (`Install-Package Aspose.Cells`), um Ihr Projekt mit den neuesten Funktionen auf dem neuesten Stand zu halten.

## Excel mit Aspose.Cells nach PowerPoint exportieren

Die erste Hauptaufgabe besteht darin, die Arbeitsmappe in eine PowerPoint‑Präsentation zu konvertieren und dabei alle visuellen Elemente editierbar zu erhalten. Dies ist unverzichtbar, wenn Sie automatisch Folienpräsentationen aus Finanzberichten oder Dashboards erzeugen möchten.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Warum das funktioniert

* **`Workbook`** lädt die gesamte Excel‑Datei in den Speicher und gibt Ihnen vollen API‑Zugriff.  
* **`CopyRange`** mit `CopyPivotTable = true` stellt sicher, dass Datenquelle, Cache und Layout der Pivot‑Tabelle exakt dupliziert werden – etwas, das ältere Versionen von Aspose.Cells nicht konnten.  
* Das Hinzufügen eines neuen Arbeitsblatts (`Copy`) ermöglicht es, das Originalblatt unverändert zu lassen, was für Prüfpfade nützlich ist.

## Exportieren der Arbeitsmappe nach PowerPoint mit editierbaren Objekten

Jetzt verwandeln wir die Arbeitsmappe in eine PowerPoint‑Datei. Durch Aktivieren von `ExportEditableObjects` wird jedes Diagramm, jede Form oder jedes Textfeld zu einem nativen PowerPoint‑Objekt, das Benutzer nach dem Export direkt bearbeiten können.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Erklärung

* **`WorkbookDesigner`** ist ein High‑Level‑Hilfswerkzeug, das die Arbeitsmappe für den Export vorbereitet und Smart Markers, benannte Bereiche und Layout‑Anpassungen verarbeitet.  
* Durch Setzen von `ExportEditableObjects = true` wird Aspose.Cells angewiesen, Excel‑Zeichnungen in PowerPoint‑Formen zu übersetzen, anstatt sie zu Bildern zu flachzulegen. Das ergibt ein **vollständig editierbares** Folienset.

> **Sonderfall:** Wenn Ihre Arbeitsmappe komplexe Diagramme enthält, die aus externen Datenverbindungen erstellt wurden, stellen Sie sicher, dass diese Verbindungen vor dem Aufruf von `ExportToPptx` aufgelöst sind, sonst kann das Diagramm leer erscheinen.

## Exportieren eines Bereichs als Zeichenketten mit benutzerdefinierter Logik

Manchmal benötigen Sie rohe Zeichenkettenwerte für die nachgelagerte Verarbeitung (z. B. für einen CSV‑Parser). Die Klasse `ExportTableOptions` ermöglicht Ihnen die Kontrolle darüber, wie jede Zelle konvertiert wird.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Warum Sie das verwenden könnten

* **Einheitlicher Datentyp:** Der Export als Zeichenketten vermeidet Typ‑Mismatches, wenn der Empfänger Text erwartet.  
* **Benutzerdefinierte Formatierung:** Ersetzen Sie `value.ToString()` durch einen beliebigen benutzerdefinierten Formatter (z. B. `value.ToString("yyyy-MM-dd")` für Datumsangaben).  

## Excel‑Formeln im Code berechnen

Eine häufige Anforderung besteht darin, **Excel‑Formeln im Code zu berechnen**, ohne Excel zu öffnen. Aspose.Cells stellt eine integrierte Berechnungs‑Engine bereit, die offline arbeitet und die neuesten Office‑365‑Funktionen, einschließlich `EXPAND`, unterstützt.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Wie die Berechnungs‑Engine funktioniert

* Die Eigenschaft `Formula` speichert den Ausdruck exakt so, wie Sie ihn in Excel eingeben würden.  
* `CalculateFormula()` löst eine vollständige Neuberechnung der Arbeitsmappe aus und berücksichtigt Abhängigkeiten zwischen Zellen.  
* Die Funktion `EXPAND` (verfügbar in Excel 365) gibt einen Spill‑Bereich zurück, basierend auf der Quellzelle (`B1`) und den angegebenen Zeilen (`5`) und Spalten (`3`).  

> **Tipp:** Wenn Sie nur einen Teil der Arbeitsmappe berechnen müssen, verwenden Sie `Worksheet.CalculateFormula()`, um den Umfang zu begrenzen und die Leistung zu verbessern.

## Speichern der Arbeitsmappe mit allen angewendeten Änderungen

Abschließend schreiben Sie die modifizierte Arbeitsmappe zurück auf die Festplatte. Sie können in jedem der unterstützten Formate (`.xlsx`, `.xls`, `.csv` usw.) speichern, indem Sie die Dateierweiterung ändern.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Was zu überprüfen ist

* Öffnen Sie `result.xlsx` in Excel, um die Kopie der Pivot‑Tabelle, das Ergebnis der `EXPAND`‑Formel und alle benutzerdefiniert exportierten Zeichenketten zu bestätigen.  
* Öffnen Sie `output.pptx` in PowerPoint; Sie sollten eine Folie sehen, die das Excel‑Layout widerspiegelt, und alle Diagramme/Textfelder sollten editierbar sein.

## Häufige Fragen und Fehlersuche

| Frage | Antwort |
|----------|--------|
| **Muss ich eine Lizenz für die Nutzung von Aspose.Cells besitzen?** | Ja. Eine Testversion funktioniert für die Evaluierung, aber eine Vollversion entfernt Wasserzeichen und schaltet die `CopyPivotTable`‑Funktion frei. |
| **Was ist, wenn die exportierte PPTX leere Formen zeigt?** | Stellen Sie sicher, dass die Zeichenobjekte der Arbeitsmappe nicht ausgeblendet sind (`Visible = true`) und dass externe Bildverknüpfungen vor dem Export eingebettet werden. |
| **Kann ich mehrere Arbeitsblätter in separate PPTX‑Folien exportieren?** | Verwenden Sie `WorkbookDesigner.ExportToPptx` in einer Schleife und geben Sie für jedes Arbeitsblatt unterschiedliche `ExportOptions` an, oder kombinieren Sie sie zu einer einzigen Präsentation, indem Sie Folien manuell über Aspose.Slides hinzufügen. |
| **Ist `CalculateFormula` thread‑sicher?** | Nein. Führen Sie Berechnungen in einem einzelnen Thread aus oder klonen Sie die Arbeitsmappe pro Thread, um Race‑Conditions zu vermeiden. |

## Fazit

Sie haben nun eine **vollständige End‑zu‑End‑Lösung für den Export von Excel nach PowerPoint** mit Aspose.Cells und verstehen, wie Sie **Excel‑Formeln im Code berechnen** – einschließlich der modernen `EXPAND`‑Funktion. Das Tutorial behandelte das Laden einer Arbeitsmappe, das Kopieren von Pivot‑Tabellen, den Export in editierbares PowerPoint, den benutzerdefinierten Zeichenketten‑Export, die Formelb berechnung und das abschließende Speichern.

Von hier aus können Sie:

* Den Export erweitern, um mehrere Folien pro Arbeitsblatt einzuschließen (sekundäres Stichwort: *calculate Excel formulas in code* kann beim Erzeugen von Diagrammdaten wiederverwendet werden).  
* Aspose.Slides integrieren, um Animationen oder Master‑Folien‑Layouts hinzuzufügen.  
* Den einfachen `CustomExport`‑Delegate durch lokalisierungs‑aware Formatierung für internationale Projekte ersetzen.  

Probieren Sie gern verschiedene Bereiche aus, erkunden Sie weitere Office‑365‑Funktionen (z. B. `FILTER`, `SORT`) und kombinieren Sie diesen Workflow mit automatisierter E‑Mail‑Zustellung für vollständig automatisierte Reporting‑Pipelines.

---


## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel-Datenexport automatisieren mit Aspose.Cells für .NET: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Wie man Excel‑Diagramme mit Aspose.Cells für .NET nach PDF exportiert: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Excel‑Zellen mit Aspose.Cells .NET in ein Bild exportieren: Eine Schritt‑für‑Schritt‑Anleitung](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}