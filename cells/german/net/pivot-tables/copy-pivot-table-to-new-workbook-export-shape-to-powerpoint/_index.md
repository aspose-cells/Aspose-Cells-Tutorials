---
category: general
date: 2026-10-20
description: Kopieren Sie die Pivot‑Tabelle in eine neue Arbeitsmappe mit Aspose.Cells
  und lernen Sie, wie Sie eine editierbare Form in PowerPoint exportieren – alles
  in einem einzigen Leitfaden.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: de
lastmod: 2026-10-20
og_description: Kopieren Sie die Pivot‑Tabelle in eine neue Arbeitsmappe mit Aspose.Cells
  und exportieren Sie eine bearbeitbare Form nach PowerPoint – Schritt‑für‑Schritt‑Code,
  den Sie noch heute ausführen können.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Pivot‑Tabelle in neue Arbeitsmappe kopieren, Form nach PowerPoint exportieren
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Pivot‑Tabelle in neue Arbeitsmappe kopieren, Form in PowerPoint exportieren
url: /de/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot‑Tabelle in neue Arbeitsmappe kopieren, Shape nach PowerPoint exportieren

Wenn Sie **copy pivot table to new workbook** benötigen und dabei die Funktionalität erhalten wollen, zeigt Ihnen dieser Leitfaden genau, wie Sie das mit Aspose.Cells erledigen. Sie sehen außerdem den schnellsten Weg, **export an editable shape to PowerPoint** zu exportieren, sodass das Textfeld nach der Konvertierung editierbar bleibt.

Viele Entwickler gehen davon aus, dass das Kopieren eines Bereichs, der eine Pivot‑Tabelle enthält, die Pivot‑Logik verliert, oder dass Shapes zu statischen Bildern werden, wenn sie als PPTX gespeichert werden. Dieses Tutorial widerlegt diese Mythen und liefert Ihnen eine zuverlässige, produktionsreife Lösung.

In den folgenden Abschnitten werden Sie:

* Eine Quell‑Arbeitsmappe laden und einen Bereich kopieren, der eine Pivot‑Tabelle enthält.
* Eine Ziel‑Arbeitsmappe erstellen, die dieselbe Pivot‑Tabelle enthält.
* Ein Textfeld‑Shape hinzufügen, dessen Text ändern und die Arbeitsmappe als PowerPoint‑Präsentation speichern, wobei das Textfeld editierbar bleibt.
* Verstehen, warum jeder API‑Aufruf erforderlich ist und wie häufige Fallstricke vermieden werden können.

**Voraussetzungen**

* .NET 6.0 oder höher (der Code funktioniert auch mit .NET Framework 4.7+).
* Aspose.Cells für .NET installiert (`Install-Package Aspose.Cells`).
* Grundkenntnisse in C# und Visual Studio (oder einer anderen bevorzugten IDE).

---

## Pivot‑Tabelle in neue Arbeitsmappe kopieren

Dieser Schritt‑für‑Schritt‑Abschnitt demonstriert, wie ein Bereich, der eine Pivot‑Tabelle enthält, kopiert wird und die Pivot‑Definition in der neuen Datei erhalten bleibt.

### Schritt 1 – Quell‑Arbeitsmappe laden und erstes Arbeitsblatt auswählen

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Warum?*  
`Workbook` ist der Einstiegspunkt für jede Excel‑Manipulation in Aspose.Cells. Das korrekte Arbeitsblatt auszuwählen stellt sicher, dass wir genau an der Position der Pivot‑Tabelle arbeiten.

### Schritt 2 – Zellbereich definieren, der die Pivot‑Tabelle einschließt

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Warum?*  
Die Pivot‑Tabelle befindet sich in einem bestimmten Zellblock. Durch Angabe eines `CellArea`, das die Pivot‑Tabelle vollständig umschließt, weiß Aspose.Cells, dass es den zugrunde liegenden Pivot‑Cache ebenfalls kopieren muss.

### Schritt 3 – Ziel‑Arbeitsmappe erstellen und erstes Arbeitsblatt holen

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Warum?*  
Eine frische Arbeitsmappe garantiert, dass keine konfliktierenden benannten Bereiche oder vorhandenen Pivot‑Tabellen existieren, wodurch der Kopiervorgang sauber abläuft.

### Schritt 4 – Zeilen vom Quell‑Bereich in das Ziel‑Arbeitsblatt kopieren

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Warum?*  
`CopyRows` ist Teil der **Aspose.Cells copy rows**‑API. Es kopiert sowohl Zellwerte als auch den versteckten Pivot‑Cache, sodass die Pivot‑Tabelle nach dem Verschieben weiterhin funktional bleibt.

### Schritt 5 – Neue Arbeitsmappe speichern

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Ergebnis*  
Öffnen Sie `CopyWithPivot.xlsx` in Excel. Die Pivot‑Tabelle erscheint exakt wie in der Quell‑Datei, und Sie können sie normal aktualisieren oder bearbeiten.

---

## Editierbares Shape nach PowerPoint exportieren

Jetzt fügen wir ein Textfeld‑Shape hinzu, ändern dessen Inhalt und speichern die Arbeitsmappe als PPTX‑Datei. Das Shape bleibt vollständig editierbar, wenn es in PowerPoint geöffnet wird.

### Schritt 1 – Neue Arbeitsmappe erstellen und erstes Arbeitsblatt zugreifen

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Schritt 2 – Textfeld‑Shape zum Arbeitsblatt hinzufügen

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Warum?*  
`AddTextBox` erstellt ein **editable textbox in PowerPoint**‑kompatibles Shape. Die Koordinaten sind in Punkten angegeben; passen Sie sie an Ihr Layout an.

### Schritt 3 – Shape abrufen und Text ändern

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Warum?*  
Der direkte Zugriff auf das `Shape`‑Objekt ermöglicht das Ändern von Eigenschaften wie `Text`, `Font` oder `Fill`. Dieser Schritt zeigt, wie Sie programmgesteuert den Anfangsinhalt festlegen.

### Schritt 4 – Arbeitsmappe als PowerPoint‑Präsentation speichern

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Ergebnis*  
Öffnen Sie `Presentation.pptx` in Microsoft PowerPoint. Das Textfeld erscheint auf der ersten Folie, und Sie können es durch Doppelklick wie jedes native PowerPoint‑Shape bearbeiten.

---

## Erwartete Ausgabe

| Datei | Was Sie sehen werden |
|------|----------------------|
| `CopyWithPivot.xlsx` | Ein Arbeitsblatt mit der originalen Pivot‑Tabelle, voll funktionsfähig (Refresh funktioniert). |
| `Presentation.pptx` | Eine einzelne Folie mit einem editierbaren Textfeld, das “Change me in PowerPoint” anzeigt. |

---

## Häufige Fallstricke und bewährte Tipps

* **Verlust des Pivot‑Caches** – Wenn Sie nur Zellwerte kopieren (z. B. `CopyRows` mit dem `PasteOptions`‑Flag `PasteValues`), wird der Pivot‑Cache weggelassen und die Tabelle wird statisch. Verwenden Sie stets die Standard‑`CopyRows`‑Überladung wie gezeigt.
* **Shape‑Positionierung** – `AddTextBox` verwendet Punkt‑Einheiten, nicht Excel‑Zellindizes. Testen Sie die Koordinaten an einer Beispieldatei, um eine Platzierung außerhalb der Folie zu vermeiden.
* **Dateiformat‑Mismatch** – Das Speichern einer Arbeitsmappe als PPTX mit `SaveFormat.Pptx` konvertiert automatisch alle unterstützten Shapes. Ein Versuch, als `Pdf` zu speichern, rastert das Shape und macht es nicht editierbar.

---

## Fazit

Sie wissen jetzt, wie Sie **copy pivot table to new workbook** durchführen und wie Sie **export an editable shape to PowerPoint** mit Aspose.Cells für .NET umsetzen. Die vollständigen, ausführbaren Code‑Beispiele decken alle erforderlichen API‑Aufrufe ab, erklären, warum jeder Schritt wichtig ist, und zeigen die erwarteten Ergebnisse.

Als Nächstes könnten Sie Folgendes erkunden:

* **Arbeiten mit Diagrammen** – Diagramme zusammen mit Pivot‑Tabellen kopieren (`Aspose.Cells copy rows between worksheets`).
* 

## Was sollten Sie als Nächstes lernen?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Features zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Copy pivot table and export Excel to PPTX with Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}