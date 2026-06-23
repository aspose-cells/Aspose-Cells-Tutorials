---
category: general
date: 2026-02-21
description: Erstellen Sie schnell Zellstile in C#. Lernen Sie, wie Sie einen Stil
  auf eine Zelle anwenden, Text in einer Zelle zentrieren, die Ausrichtung der Zelle
  festlegen und die Zellformatierung meistern.
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: de
og_description: Erstellen Sie Zellformat in C# und lernen Sie, wie Sie das Format
  auf eine Zelle anwenden, Text in der Zelle zentrieren und die Zellenausrichtung
  mit einer klaren Schritt‑für‑Schritt‑Anleitung festlegen.
og_title: Zellstil in C# erstellen – Stil auf eine Zelle anwenden und Text zentrieren
tags:
- C#
- Aspose.Cells
- Excel automation
title: Zellstil in C# erstellen – Wie man einen Stil auf eine Zelle anwendet und den
  Text zentriert
url: /de/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

remain unchanged.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zellstil in C# erstellen – Vollständiger Leitfaden zum Anwenden von Stilen und Zentrieren von Text

Haben Sie schon einmal **einen Zellstil** in einem Excel‑Arbeitsblatt erstellen müssen, wussten aber nicht, wo Sie anfangen sollten? Sie sind nicht allein. In vielen Automatisierungsprojekten ist die Fähigkeit, **Stil auf Zelle**‑Objekte **anzuwenden**, der Unterschied zwischen einer langweiligen Tabelle und einem professionellen Bericht.

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, ausführbares Beispiel, das zeigt, **wie man Text** in einer Zelle **zentriert**, die Ausrichtung festlegt und einen dünnen Rahmen hinzufügt – alles in nur wenigen Zeilen C#. Am Ende wissen Sie genau, warum jedes Element wichtig ist und wie Sie es für Ihre eigenen Szenarien anpassen können.

## Was Sie am Ende wissen werden

- Ein klares Verständnis des **create cell style**‑Workflows mit Aspose.Cells (oder einer ähnlichen Bibliothek).
- Den genauen Code, den Sie in eine Konsolen‑App kopieren‑und‑einfügen können, um **style to cell** anzuwenden.
- Einblick in **center text in cell**, **set cell alignment** und den Umgang mit Sonderfällen wie zusammengeführten Zellen oder benutzerdefinierten Zahlenformaten.
- Tipps zum Erweitern des Stils – andere Schriftarten, Hintergrundfarben oder bedingte Formatierung.

> **Voraussetzung:** Visual Studio 2022 (oder jede C#‑IDE) und das Aspose.Cells for .NET NuGet‑Paket. Keine weiteren Abhängigkeiten sind erforderlich.

---

## Schritt 1: Projekt einrichten und Namespaces importieren

Bevor wir **create cell style** ausführen können, benötigen wir ein Projekt, das die Excel‑Bibliothek referenziert.

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Warum das wichtig ist:* Durch das Importieren von `Aspose.Cells` erhalten wir Zugriff auf die Klassen `Workbook`, `Worksheet`, `Style` und `Border`. Wenn Sie eine andere Bibliothek verwenden (z. B. EPPlus), ändern sich die Klassennamen, aber das Konzept bleibt gleich.

---

## Schritt 2: Arbeitsmappe erstellen und die erste Zelle holen

Jetzt **create cell style**, indem wir zuerst eine Referenz auf die zu formatierende Zelle erhalten.

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

Beachten Sie, dass wir `Cell` anstelle von `var` verwendet haben – explizite Typisierung macht den Code für Einsteiger klarer. Der Aufruf von `PutValue` schreibt einen String, sodass wir die Stil‑Auswirkung später sehen können.

---

## Schritt 3: Stil definieren – Text zentrieren, dünnen Rahmen hinzufügen

Hier liegt das Herz der **create cell style**‑Operation. Wir setzen die horizontale Ausrichtung, einen dünnen Rahmen und ein paar optionale Feinheiten.

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Warum wir das tun:*  
- **HorizontalAlignment** und **VerticalAlignment** beantworten gemeinsam die Frage „**how to center text** in a cell?“.  
- Das Hinzufügen aller vier Rahmen sorgt dafür, dass die Zelle wie ein umrandetes Etikett aussieht – nützlich für Überschriften.  
- Die Hintergrundfarbe ist nicht zwingend erforderlich, demonstriert aber, wie Sie den Stil später erweitern können.

---

## Schritt 4: Definierten Stil auf die ausgewählte Zelle anwenden

Jetzt, wo der Stil existiert, **apply style to cell** mit einem einzigen Methodenaufruf.

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

Das war’s – Aspose.Cells übernimmt das Kopieren des Stils in die interne Stil‑Sammlung der Zelle. Wenn Sie dieselbe Formatierung auf einen Bereich anwenden möchten, können Sie `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });` verwenden.

---

## Schritt 5: Arbeitsmappe speichern und Ergebnis prüfen

Ein kurzer Save‑Aufruf ermöglicht es Ihnen, die Datei in Excel zu öffnen und zu bestätigen, dass der Text wirklich zentriert ist und der Rahmen angezeigt wird.

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Erwartete Ausgabe:* Wenn Sie **StyledCell.xlsx** öffnen, enthält Zelle **A1** den Text „Hello, styled world!“ sowohl horizontal als auch vertikal zentriert, umgeben von einem dünnen grauen Rahmen und mit einem hellgrauen Hintergrund.

---

## Häufige Varianten & Sonderfälle

### 1. Text in einem zusammengeführten Bereich zentrieren

Wenn Sie die Zellen **A1:C1** zusammenführen und den Text weiterhin zentriert haben möchten, müssen Sie den Stil nach dem Zusammenführen auf die obere linke Zelle **anwenden**:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Numerisches Format verwenden

Manchmal müssen Sie **set cell alignment** *und* Zahlen mit einem bestimmten Format anzeigen:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

Die Ausrichtung bleibt zentriert, während die Zahl als `12,345.68` erscheint.

### 3. Stile effizient wiederverwenden

Für jede Zelle einen neuen `Style` zu erstellen, kann die Leistung beeinträchtigen. Erstellen Sie stattdessen ein Stil‑Objekt und verwenden Sie es für viele Zellen oder Bereiche. Die Klasse `StyleFlag` ermöglicht es Ihnen, nur die Teile anzuwenden, die Sie benötigen, und spart Speicher.

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Pro‑Tipps & Stolperfallen

- **Vergessen Sie nicht die vertikale Ausrichtung** – nur horizontal zu zentrieren wirkt oft unpassend, besonders bei hohen Zeilen.
- **Rahmentypen**: `CellBorderType.Thin` reicht für die meisten Berichte, Sie können aber zu `Medium` oder `Dashed` wechseln, um visuelle Hierarchien zu erzeugen.
- **Farbbehandlung**: Beim Ziel .NET Core verwenden Sie `System.Drawing.Color` aus dem Paket `System.Drawing.Common`; sonst erhalten Sie einen Laufzeitfehler.
- **Speicherformat**: Wenn Sie Kompatibilität zu älteren Excel‑Versionen benötigen, ändern Sie `SaveFormat.Xlsx` zu `SaveFormat.Xls`.

---

![Create cell style example](https://example.com/images/create-cell-style.png "Create cell style in C#")

*Alt‑Text: Screenshot, der eine Zelle mit zentriertem Text und dünnem Rahmen zeigt, erstellt durch das create cell style‑Tutorial.*

---

## Vollständiges, lauffähiges Beispiel (Copy‑Paste‑bereit)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

Führen Sie dieses Programm aus, öffnen Sie **StyledCell.xlsx** und Sie sehen das exakt beschriebene Ergebnis. Ändern Sie gern den Text, den Rahmenstil oder die Hintergrundfarbe, um sie an Ihr Corporate Design anzupassen.

---

## Fazit

Wir haben gerade **cell style** von Grund auf **erstellt**, **style to cell** **angewendet** und **wie man Text** sowohl horizontal als auch vertikal **zentriert**. Durch das Beherrschen dieser Bausteine können Sie jetzt Überschriften formatieren, Summen hervorheben oder komplette Berichtsvorlagen bauen, ohne C# zu verlassen.

Wenn Sie neugierig auf die nächsten Schritte sind, probieren Sie:

- **Den gleichen Stil auf eine ganze Zeile anwenden** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`).
- **Bedingte Formatierung hinzufügen**, um den Hintergrund basierend auf Zellwerten zu ändern.
- **Export nach PDF**, wobei der Stil erhalten bleibt.

Denken Sie daran: Styling ist genauso wichtig für die Lesbarkeit wie für die Ästhetik. Experimentieren, iterieren und bald sehen Ihre Tabellen genauso professionell aus wie Ihr Code.

*Viel Spaß beim Coden!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}