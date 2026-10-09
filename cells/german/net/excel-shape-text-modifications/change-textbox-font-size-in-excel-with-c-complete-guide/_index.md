---
category: general
date: 2026-05-30
description: Ändern Sie die Schriftgröße von Textfeldern in Excel mit C#. Erfahren
  Sie, wie Sie die Schrift von Excel‑Textfeldern schnell mit Schritt‑für‑Schritt‑Code
  anpassen.
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: de
og_description: Ändern Sie die Schriftgröße von Textfeldern in Excel mit C#. Dieser
  Leitfaden zeigt, wie man die Schrift von Excel‑Textfeldern sicher und effizient
  anpasst.
og_title: Textbox‑Schriftgröße in Excel mit C# ändern – Vollständiges Tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: Textbox‑Schriftgröße in Excel mit C# ändern – Komplettanleitung
url: /de/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Textfeld‑Schriftgröße in Excel mit C# ändern – Vollständige Anleitung

Möchten Sie **die Schriftgröße eines Textfelds** in einem Excel-Arbeitsblatt aus C# ändern? Sie sind hier genau richtig. Egal, ob Sie Berichte erstellen, ein Dashboard bauen oder einfach eine Vorlage anpassen, das Anpassen des Aussehens eines Textfelds kann Ihre Tabelle deutlich professioneller wirken lassen.

In diesem Tutorial werden wir außerdem **die Excel‑Textfeld‑Schrift** über die reine Größe hinaus anpassen – denken Sie an Schriftfamilie, Fettdruck und sogar die Handhabung mehrerer Formen. Am Ende haben Sie ein sofort einsatzbereites Snippet, das jeden Aspekt des Prozesses abdeckt, vom Öffnen der Arbeitsmappe bis zum Aufräumen der COM‑Objekte. Kein Schnickschnack, nur praktischer Code, den Sie noch heute in Ihr Projekt einbinden können.

## Voraussetzungen — Was Sie benötigen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes auf Ihrem Rechner haben:

| Anforderung | Warum es wichtig ist |
|-------------|----------------------|
| **.NET 6+** (oder .NET Framework 4.7.2+) | Stellt den C#‑Compiler und die Laufzeit bereit. |
| **Microsoft.Office.Interop.Excel** NuGet‑Paket | Liefert die COM‑Interop‑Typen, die zum Kommunizieren mit Excel benötigt werden. |
| **Excel installiert** (beliebige aktuelle Version) | Die Interop‑Schicht funktioniert nur, wenn die Office‑Anwendung vorhanden ist. |
| **Grundkenntnisse in C#** | Sie können leicht folgen, aber wir erklären jede Zeile. |

Falls etwas fehlt, halten Sie jetzt an und installieren Sie es; der Rest der Anleitung geht davon aus, dass alles vorhanden ist.

## Schritt 1: Projekt einrichten und Namespaces importieren

Zuerst einmal – erstellen Sie eine neue Konsolenanwendung (oder integrieren Sie sie in ein bestehendes Projekt) und binden Sie den Interop‑Namespace ein.

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Pro‑Tipp:** Wenn Sie .NET 6+ anvisieren, fügen Sie das `Microsoft.Office.Interop.Excel`‑Paket via `dotnet add package Microsoft.Office.Interop.Excel` hinzu. Das stellt sicher, dass das `Excel`‑Alias korrekt aufgelöst wird.

## Schritt 2: Arbeitsmappe öffnen und Ziel‑Arbeitsblatt auswählen

Jetzt müssen wir Excel starten, die Datei öffnen und das Blatt ansteuern, das das Textfeld enthält. Das Einbetten in einen `try/finally`‑Block stellt sicher, dass die COM‑Objekte freigegeben werden, selbst wenn etwas schiefgeht.

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### Warum das wichtig ist

Das Öffnen der Arbeitsmappe über COM liefert uns ein Live‑Objektmodell – jede Änderung wird sofort in der Datei wirksam. Das Setzen von `Visible = false` beschleunigt den Vorgang und verhindert das Aufpoppen von Fenstern während der Automatisierung.

## Schritt 3: Textfeld‑Shape abrufen

Excel behandelt Textfelder als `Shape`‑Objekte in der `Shapes`‑Sammlung, nicht als eigene `TextBox`‑Sammlung. Deshalb sieht der nachfolgende Code etwas anders aus als das Snippet, das Sie vielleicht online gesehen haben.

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Achtung:** Die `Shapes`‑Sammlung ist 1‑basiert, daher addieren wir `+1` zum nullbasierten `textboxIndex`, das Sie übergeben. Wird das vergessen, führt das zu „Index außerhalb des Bereichs“-Fehlern, die beim Debuggen frustrierend sein können.

## Schritt 4: Textfeld‑Schriftgröße (und Name) ändern

Hier ändern wir schließlich **die Schriftgröße des Textfelds**. Die Eigenschaft `TextFrame2` gibt uns Zugriff auf die Rich‑Text‑Formatierungsoptionen, darunter `Font.Name` und `Font.Size`.

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### Warum wir `TextFrame2` verwenden

`TextFrame2` ist das neuere Objektmodell, das mit Office 2007 eingeführt wurde. Es unterstützt erweiterte typografische Funktionen und ist im Allgemeinen zuverlässiger als das ältere `TextFrame`. Durch die Verwendung wird sichergestellt, dass unsere **Änderung der Textfeld‑Schriftgröße** in modernen Excel‑Versionen funktioniert.

## Schritt 5: Speichern, Aufräumen und Verifizieren

Nachdem die Schrift angepasst wurde, müssen wir die Änderungen speichern und jede COM‑Referenz freigeben. Das Auslassen des Aufräumens kann verwaiste Excel‑Prozesse im Hintergrund zurücklassen.

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Pro‑Tipp:** Wenn Sie **die Excel‑Textfeld‑Schrift** auf vielen Arbeitsblättern ändern müssen, verpacken Sie die innere Logik in eine Schleife, die über `Workbook.Worksheets` iteriert. Denken Sie nur daran, `textboxIndex` für jedes Blatt zurückzusetzen.

## Umgang mit Sonderfällen — Mehrere Textfelder und fehlende Shapes

In der Praxis enthalten Tabellen selten nur ein Textfeld. Im Folgenden finden Sie zwei schnelle Strategien, die Sie übernehmen können, ohne die gesamte Methode neu zu schreiben.

### 1. *Alle* Textfelder auf einem Blatt ändern

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. Ein Textfeld über seinen **Namen** statt über den Index identifizieren

Wenn Sie Ihrem Textfeld einen aussagekräftigen Namen gegeben haben (z. B. „TitleBox“), können Sie es direkt abrufen:

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

Beide Ansätze ermöglichen es Ihnen, **die Excel‑Textfeld‑Schrift** präzise zu ändern, unabhängig davon, wie die Arbeitsmappe strukturiert ist.

## Visuelle Übersicht (Optional)

Wenn Sie lieber einen schnellen visuellen Hinweis bevorzugen, stellen Sie sich das folgende Diagramm vor:

![Screenshot, der ein Excel-Arbeitsblatt mit einem hervorgehobenen Textfeld zeigt – demonstriert, wie man die Textfeld‑Schriftgröße ändert](change-textbox-font-size.png)

*Alt‑Text:* *Schriftgröße des Textfelds in Excel ändern – hervorgehobenes Textfeld bereit für die Schriftanpassung.*

## Vollständiges funktionierendes Beispiel

Wenn wir alles zusammenfügen, erhalten Sie eine einzelne Datei, die Sie in ein Konsolenprojekt kopieren‑und‑einfügen können und sofort ausführen (nur Pfad und Blattnamen anpassen).



## Was sollten Sie als Nächstes lernen?

- [Schriftgröße in Excel ändern](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Wie man die Schriftgröße in Excel‑Zellen mit Aspose.Cells .NET anpasst | Vollständige Anleitung](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Wie man Schriftstile in Excel mit Aspose.Cells für .NET festlegt (Schritt‑für‑Schritt‑Anleitung)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}