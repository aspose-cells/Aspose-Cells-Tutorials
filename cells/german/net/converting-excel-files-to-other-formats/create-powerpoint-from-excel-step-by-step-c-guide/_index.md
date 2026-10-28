---
category: general
date: 2026-03-30
description: Erstellen Sie schnell PowerPoint-Präsentationen aus Excel mit Aspose.Cells
  und Aspose.Slides. Erfahren Sie, wie Sie ein Arbeitsblatt als Bild exportieren und
  die Präsentation als PPTX in C# speichern.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: de
og_description: Erstellen Sie PowerPoint aus Excel in C# mit Aspose. Exportieren Sie
  das Arbeitsblatt als Bild, behalten Sie die Formen bearbeitbar und speichern Sie
  das Ergebnis als PPTX.
og_title: PowerPoint aus Excel erstellen – Vollständiges C#‑Tutorial
tags:
- Aspose
- C#
- Office Automation
title: PowerPoint aus Excel erstellen – Schritt‑für‑Schritt C#‑Leitfaden
url: /de/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint aus Excel erstellen – Vollständiges C#‑Tutorial

Hatten Sie schon einmal das Bedürfnis, **PowerPoint aus Excel zu erstellen**, wussten aber nicht, welche Bibliothek Ihre Diagramme editierbar hält? Sie sind nicht allein. In vielen Reporting‑Szenarien möchten Sie eine Kalkulationstabelle in ein Folien‑Deck verwandeln, ohne die Möglichkeit zu verlieren, Textfelder später anzupassen. Dieser Leitfaden zeigt Ihnen genau, wie Sie **Excel nach PowerPoint konvertieren** mit Aspose.Cells und Aspose.Slides, und behandelt zudem, wie Sie **ein Arbeitsblatt als Bild exportieren** und schließlich **die Präsentation als PPTX speichern**.

Wir gehen jede Code‑Zeile durch, erklären *warum* jede Einstellung wichtig ist und diskutieren, was zu tun ist, wenn Ihre Arbeitsmappe komplexe Diagramme enthält, die Sie lieber als Bild exportieren möchten. Am Ende haben Sie eine sofort einsatzbereite C#‑Konsolen‑App, die `ShapesDemo.xlsx` nimmt und `Result.pptx` ausgibt – alles mit editierbaren Textfeldern und scharfen Bildern.

## Was Sie benötigen

- .NET 6.0 oder höher (die API funktioniert auch mit dem .NET Framework, aber .NET 6 ist der optimale Punkt).  
- **Aspose.Cells**‑ und **Aspose.Slides**‑NuGet‑Pakete (Kostenlose Testlizenzen funktionieren zum Ausprobieren).  
- Grundlegende Kenntnisse der C#‑Syntax – wenn Sie `Console.WriteLine` schreiben können, sind Sie startklar.  

Keine zusätzliche COM‑Interop, kein Office auf dem Server installiert und kein manuelles Kopieren‑Einfügen von Bildern. Alles wird programmgesteuert erledigt.

---

## PowerPoint aus Excel erstellen – Arbeitsmappe laden und Export‑Optionen festlegen

Als erstes öffnen wir die Excel‑Datei und teilen Aspose.Cells mit, wie das Blatt gerendert werden soll. Das Objekt `ImageOrPrintOptions` ist dabei der Ort, an dem die Magie passiert: Wir aktivieren `ExportShapes` und `ExportEditableTextBoxes`, sodass alle Formen (einschließlich Diagramme) Teil der Folie **werden** und nach der Konvertierung editierbar bleiben.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Warum diese Flags?**  
- `OnePagePerSheet` verhindert, dass das Blatt auf mehrere Folien aufgeteilt wird – Sie erhalten ein einzelnes, großformatiges Bild.  
- `ExportShapes` weist Aspose.Cells an, Diagramme *und* Vektorformen zu rasterisieren und ihr Aussehen zu bewahren.  
- `ExportEditableTextBoxes` ist das Geheimrezept, das Ihnen erlaubt, in PowerPoint per Doppelklick ein Textfeld zu öffnen und den Text zu bearbeiten, ohne Excel erneut zu öffnen.

> **Pro‑Tipp:** Wenn Sie nur ein statisches Bild eines Diagramms benötigen, setzen Sie `ExportShapes = false` und verwenden Sie später die Methode `ExportExcelChartAsPicture` (siehe den abschließenden Abschnitt).

---

## Excel nach PowerPoint konvertieren – Bild aus Arbeitsblatt erzeugen

Mit den vorbereiteten Optionen wandeln wir nun das Arbeitsblatt in ein `System.Drawing.Image` um. Der `WorksheetToImageConverter` übernimmt die schwere Arbeit und wendet die gerade definierten Einstellungen an.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

Das Argument `0` bezeichnet die erste Seite (wir haben nur eine, weil `OnePagePerSheet` aktiv ist). Das resultierende `sheetImage` behält die ursprüngliche DPI bei, sodass Ihre Folie selbst auf hochauflösenden Displays nicht pixelig wirkt.

---

## Präsentation als PPTX speichern – Bild in eine Folie einfügen

Jetzt erstellen wir eine neue PowerPoint‑Datei, fügen eine Folie hinzu und platzieren das Bitmap darauf. Aspose.Slides behandelt das Bild als *Picture Frame*‑Form, die Sie später wie jedes native PowerPoint‑Objekt skalieren oder verschieben können.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Was, wenn das Bild größer als die Foliengröße ist?**  
> PowerPoint schneidet automatisch alles ab, was die Folienabmessungen überschreitet. Eine schnelle Lösung besteht darin, das Bild vor dem Einfügen zu skalieren:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Anschließend übergeben Sie `newWidth` und `newHeight` an `AddPictureFrame`.

---

## Arbeitsblatt als Bild exportieren – PPTX‑Datei speichern

Zum Schluss schreiben wir die Präsentation auf die Festplatte. Der Flag `SaveFormat.Pptx` garantiert das moderne OpenXML‑Format, das in allen aktuellen PowerPoint‑Versionen funktioniert.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

Wenn Sie `Result.pptx` öffnen, sehen Sie eine einzelne Folie, die exakt wie Ihr Excel‑Blatt aussieht, Sie können jedoch weiterhin jedes Textfeld anklicken und den Inhalt direkt in PowerPoint bearbeiten.

---

## Excel‑Diagramm als Bild exportieren – Wenn Raster‑Bilder bevorzugt werden

Manchmal benötigen Sie keine editierbaren Formen; ein hochwertiges PNG‑Diagramm reicht aus. Aspose.Cells kann ein bestimmtes Diagramm als Bild exportieren, ohne das gesamte Blatt zu konvertieren:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Sie können dann `chart.png` auf dieselbe Weise in eine Folie einbetten, wie wir `sheetImage` hinzugefügt haben. Dieser Ansatz reduziert die PPTX‑Dateigröße und ist nützlich, wenn die umgebenden Daten nicht auf der Folie benötigt werden.

---

## Häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Text sieht unscharf aus** | Exportiert mit niedriger DPI (Standard 96). | Setzen Sie `imageOptions.Dpi = 300;` vor der Konvertierung. |
| **Formen verschwinden** | `ExportShapes` war auf `false` gesetzt. | Stellen Sie sicher, dass `ExportShapes = true` ist, wenn Sie editierbare Grafiken benötigen. |
| **Foliengröße stimmt nicht überein** | Bild ist größer als die Folienabmessungen. | Skalieren Sie das Bild (siehe Code‑Snippet) oder ändern Sie die Foliengröße über `presentation.SlideSize`. |
| **Lizenzausnahme** | Verwendung der Testversion ohne ordnungsgemäße Aktivierung. | Rufen Sie `License license = new License(); license.SetLicense("Aspose.Total.lic");` früh im `Main` auf. |

---

## Vollständiges funktionierendes Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das gesamte Programm, das Sie in ein neues Konsolen‑Projekt einfügen können. Ersetzen Sie `YOUR_DIRECTORY` durch den Ordner, der Ihre Excel‑Datei enthält.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Erwartete Ausgabe:**  
Beim Ausführen des Programms wird `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx` ausgegeben. Öffnen Sie die PPTX‑Datei, Sie sehen eine einzelne Folie, die das ursprüngliche Excel‑Blatt widerspiegelt, mit editierbaren Textfeldern.

---

## Zusammenfassung & nächste Schritte

Sie wissen jetzt, wie Sie **PowerPoint aus Excel erstellen** mit den leistungsstarken APIs von Aspose, wie Sie **ein Arbeitsblatt als Bild exportieren** und wie Sie **die Präsentation als PPTX speichern**, wobei die Editierbarkeit erhalten bleibt. Das gleiche Muster funktioniert für Arbeitsmappen mit mehreren Blättern – einfach über `workbook.Worksheets` iterieren und für jedes Blatt eine neue Folie hinzufügen.

**Was Sie als Nächstes erkunden können?**  

- **Batch‑Konvertierung:** Durchlaufen Sie einen Ordner mit Excel‑Dateien und erzeugen Sie für jede Datei ein Folien‑Deck.  
- **Dynamische Layouts:** Verwenden Sie `slide.LayoutSlide`, um vordesignte PowerPoint‑Vorlagen anzuwenden.  
- **Nur‑Diagramm‑Export:** Kombinieren Sie das Snippet „Export Excel chart as picture“ mit Folien‑Platzhaltern für ein schlankeres Deck.  
- **Erweiterte Gestaltung:** Anwenden benutzerdefinierter Folien‑Hintergründe, Übergänge oder Animationen via Aspose.Slides.

Experimentieren Sie gern – ändern Sie die DPI, tauschen Sie `ShapeType.Ellipse` gegen einen runden Bildrahmen aus, oder betten Sie mehrere Bilder pro Folie ein. Der Himmel ist die Grenze, wenn Sie programmgesteuerte Kontrolle über

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}