---
category: general
date: 2026-02-15
description: Wie man Schriftart kopiert und Zellstil in C# mit einem einfachen Beispiel
  anwendet. Lernen Sie, wie man den Zellstil abruft und die Zellformatierung verwendet,
  um die Schriftgröße eines Textfelds festzulegen.
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: de
og_description: Wie man die Schriftart aus einer Tabellenzelle kopiert und den Zellenstil
  auf ein Textfeld anwendet. Dieser Leitfaden zeigt, wie man den Zellenstil abruft,
  die Zellformatierung verwendet und die Schriftgröße des Textfelds festlegt.
og_title: Wie man die Schriftart aus einer Excel‑Zelle kopiert – Vollständiges C#‑Tutorial
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Wie man die Schriftart aus einer Excel‑Zelle in ein Textfeld kopiert – Schritt‑für‑Schritt‑Anleitung
url: /de/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

ubehalten."

Next:

The good news is that with just a few lines of C# you can **get cell style**, read its font properties, and **apply cell style** to any text‑box control. In this tutorial we’ll walk through a complete, runnable example that shows how to **use cell formatting** and even **set textbox font size** programmatically.

Translate.

...

Continue.

We must translate bullet lists etc.

Also keep code block placeholders.

Proceed step by step.

Will produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Schriftart aus einer Excel‑Zelle in ein TextBox‑Steuerelement kopieren – Vollständiges C#‑Tutorial

Haben Sie jemals die **Schriftart** aus einer Tabellenzelle kopieren müssen, damit ein UI‑Textfeld exakt gleich aussieht? Sie sind nicht allein. In vielen Reporting‑Tools oder benutzerdefinierten Dashboards ziehen Sie Daten aus Excel und versuchen dann, die visuelle Treue – Schriftfamilie, Größe und Farbe – beizubehalten.  

Die gute Nachricht: Mit nur wenigen Zeilen C# können Sie **Zellstil abrufen**, die Schrift‑Eigenschaften auslesen und **Zellstil anwenden** auf jedes Text‑Box‑Steuerelement. In diesem Tutorial führen wir Sie durch ein komplettes, ausführbares Beispiel, das zeigt, wie man **Zellenformatierung verwendet** und sogar **Textbox‑Schriftgröße programmgesteuert setzt**.

---

## Was Sie lernen werden

- Wie man ein `TextBox`‑Objekt aus einer Grid‑Komponente (`gridJs` in unserem Beispiel) abruft  
- Wie man die Schriftfamilie, Größe und Farbe aus einer bestimmten Excel‑Zelle (`B2`) liest  
- Wie man diese Schrift‑Attribute auf das Textfeld überträgt, sodass die UI die Tabelle widerspiegelt  
- Häufige Stolperfallen (z. B. Farbkonvertierung) und ein paar **Pro‑Tipps**, um Ihren Code robust zu halten  
- Ein sofort einsatzbereites Code‑Snippet, das Sie in eine Konsolen‑App oder ein WinForms‑Projekt einfügen können  

**Voraussetzungen**  
Sie sollten haben:

1. .NET 6+ (oder .NET Framework 4.8) installiert  
2. Das EPPlus‑NuGet‑Paket (für die Excel‑Verarbeitung)  
3. Ein Grid‑Steuerelement, das ein `TextBoxes`‑Dictionary bereitstellt (das Beispiel verwendet ein fiktives `gridJs`, aber das Prinzip funktioniert mit jeder UI‑Bibliothek)

Jetzt legen wir los.

---

## Schritt 1: Projekt einrichten und Arbeitsblatt laden

Erstellen Sie zunächst ein neues Konsolen‑ oder WinForms‑Projekt und fügen Sie EPPlus hinzu:

```bash
dotnet add package EPPlus --version 6.*
```

Laden Sie dann die Arbeitsmappe und holen Sie die Zelle, deren Stil Sie kopieren möchten.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**Warum das wichtig ist:** EPPlus gibt Ihnen direkten Zugriff auf das `Style`‑Objekt, das das Unter‑Objekt `Font` enthält. Von dort aus können Sie `Name`, `Size` und `Color` auslesen. Das ist das Kernstück der **Zellstil‑Abruf**‑Operation.

---

## Schritt 2: Ziel‑TextBox aus Ihrem Grid holen

Angenommen, Ihr UI‑Grid (`gridJs`) speichert TextBoxen in einem Dictionary, das mit dem Spaltennamen indiziert ist, dann können Sie die gewünschte wie folgt abrufen:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

Verwenden Sie WinForms, könnte `notesTextBox` ein `TextBox`‑Steuerelement sein; für WPF ein `TextBox`‑Element, und für ein web‑basiertes Grid ein JavaScript‑Interop‑Objekt. Wichtig ist, dass Sie eine Referenz haben, die Sie manipulieren können.

---

## Schritt 3: Schriftfamilie übertragen

Jetzt, wo wir sowohl den Quell‑Stil als auch das Ziel‑Steuerelement haben, kopieren wir die Schriftfamilie.

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**Pro‑Tipp:** Nicht alle UI‑Frameworks besitzen eine `FontFamily`‑Eigenschaft, die einen einfachen String akzeptiert. In WinForms würden Sie `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);` setzen. Passen Sie es entsprechend an.

---

## Schritt 4: Schriftgröße übertragen

Die Schriftgröße wird in EPPlus als `float` gespeichert. Direkt zuweisen:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

Verwendet Ihr Steuerelement Punkte (wie die meisten), können Sie den Wert ohne Umrechnung zuweisen. Für CSS‑basierte Grids müssen Sie eventuell `"pt"` anhängen.

---

## Schritt 5: Schriftfarbe übertragen

Die Farbkonvertierung ist der kniffligste Teil, weil EPPlus Farben als ARGB‑Integer speichert, während viele UI‑Frameworks ein `System.Drawing.Color` oder einen CSS‑Hex‑String erwarten.

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **Warum das funktioniert:** `GetColor()` löst themenbasierte Farben auf und liefert ein konkretes `System.Drawing.Color`. Wenn die Zelle die Standardfarbe verwendet (keine explizite Einstellung), greifen wir auf Schwarz zurück, um Null‑Referenz‑Ausnahmen zu vermeiden.

---

## Vollständiges Beispiel

Alles zusammengeführt, hier ein minimales Konsolen‑Programm, das eine Excel‑Datei liest, die Schrift aus **B2** extrahiert und sie auf eine Mock‑TextBox anwendet.

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Erwartete Ausgabe (angenommen B2 verwendet Arial, 12 pt, blau):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

Starten Sie das Programm, öffnen Sie Ihre UI, und Sie sehen, dass das „Notes“-Textfeld nun exakt die Schriftformatierung der Zelle **B2** widerspiegelt. Kein manuelles Nachjustieren nötig.

---

## Häufig gestellte Fragen & Sonderfälle

### Was, wenn die Zelle eine Themenfarbe statt eines expliziten RGB‑Werts verwendet?

`GetColor()` von EPPlus löst Themenfarben automatisch zu einem konkreten `System.Drawing.Color` auf. Verwenden Sie jedoch eine ältere Bibliothek, die nur den Themen‑Index zurückgibt, müssen Sie diesen Index selbst einer Farbpalette zuordnen.

### Kann ich weitere Stil‑Attribute kopieren (z. B. fett, kursiv)?

Natürlich. Das `ExcelStyle.Font`‑Objekt stellt auch `Bold`, `Italic`, `Underline` und `Strike` bereit. Setzen Sie einfach die entsprechenden Eigenschaften Ihres UI‑Steuerelements:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### Was, wenn das Grid‑Steuerelement keine `FontColor`‑Eigenschaft hat?

Die meisten modernen UI‑Frameworks besitzen sie, aber falls Ihr Framework nur einen CSS‑String akzeptiert, konvertieren Sie das `Color`‑Objekt zu Hex:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### Wie gehe ich mit mehreren Zellen gleichzeitig um?

Iterieren Sie über den gewünschten Bereich, holen Sie den Stil jeder Zelle und wenden Sie ihn auf die entsprechende TextBox an. Denken Sie daran, die Stil‑Objekte zu cachen, wenn Sie viele Zeilen verarbeiten, um Performance‑Einbußen zu vermeiden.

---

## Pro‑Tipps & häufige Stolperfallen

- **ExcelPackage cachen** – das Öffnen und Schließen der Datei für jede Zelle ist teuer. Laden Sie die Arbeitsmappe einmal und verwenden Sie das `ExcelWorksheet`‑Objekt mehrfach.  
- **Null‑Farben beachten** – eine Zelle, die die Standardfarbe erbt, liefert `null`. Immer einen Fallback (schwarz oder den Standardwert des Steuerelements) bereitstellen.  
- **DPI‑Skalierung im Blick behalten** – bei High‑DPI‑Monitoren können Schriftgrößen leicht größer erscheinen. Bei Bedarf mit `Graphics.DpiX` nachjustieren.  
- **Thread‑Safety** – EPPlus ist nicht thread‑sicher. Wenn Sie viele Blätter parallel verarbeiten, erzeugen Sie für jeden Thread ein separates `ExcelPackage`.

---

## Fazit

Sie wissen jetzt, **wie man die Schriftart** aus einer Excel‑Zelle kopiert und **den Zellstil** auf jedes TextBox‑Steuerelement mit C# anwendet. Durch das Abrufen des Zell‑`Style`, das Extrahieren der `Font`‑Eigenschaften und das Zuweisen an das UI‑Element erhalten Sie visuelle Konsistenz ohne manuelles Nacharbeiten.  

Die komplette Lösung – Laden der Arbeitsmappe, Abrufen des Zellstils und Setzen von Schriftfamilie, Größe und Farbe der TextBox – deckt das Kernstück von **Zellenformatierung verwenden** ab und demonstriert, wie man **Textbox‑Schriftgröße** korrekt setzt.  

Versuchen Sie jetzt, das Beispiel zu erweitern, um Hintergrundfarben, Rahmen oder sogar den gesamten Zellinhalt zu übernehmen. Arbeiten Sie mit einer Data‑Grid‑Bibliothek, die reichhaltiges Zell‑Rendering unterstützt, können Sie nun exakt dieselben Stil‑Informationen aus Excel übernehmen und Ihre UI sowie Berichte perfekt synchronisieren.

Noch Fragen? Hinterlassen Sie einen Kommentar oder schauen Sie sich verwandte Themen wie „dynamisches Excel‑zu‑UI‑Binding“ und „themenbewusste Farbkonvertierung“ an. Viel Spaß beim Coden!

---

![how to copy font example](placeholder-image.jpg "how to copy font from Excel cell to TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}