---
category: general
date: 2026-02-21
description: Erstellen Sie schnell PowerPoint-Präsentationen aus Excel. Erfahren Sie,
  wie Sie Excel mit Aspose.Cells in nur wenigen C#‑Zeilen nach PowerPoint exportieren,
  wobei Text und Diagramme editierbar bleiben.
draft: false
keywords:
- create powerpoint from excel
- export excel to powerpoint
- export editable text
- export excel chart powerpoint
- convert excel chart powerpoint
language: de
og_description: Erstellen Sie PowerPoint aus Excel mit editierbarem Text und Diagrammen.
  Folgen Sie dieser ausführlichen Anleitung, um Excel mit Aspose.Cells nach PowerPoint
  zu exportieren.
og_title: PowerPoint aus Excel erstellen – Schritt‑für‑Schritt C#‑Leitfaden
tags:
- C#
- Aspose.Cells
- PowerPoint
- Excel Automation
title: PowerPoint aus Excel erstellen – Komplettes C#‑Tutorial
url: /de/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-complete-c-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint aus Excel erstellen – Komplettes C#‑Tutorial

Haben Sie schon einmal **PowerPoint aus Excel erstellen** müssen, wussten aber nicht, welche API Sie dafür verwenden sollen? Sie sind nicht allein. Viele Entwickler stoßen an Grenzen, wenn sie ein datenreiches Arbeitsblatt in ein professionelles Folienset umwandeln wollen, besonders wenn die Textfelder nach der Konvertierung editierbar bleiben sollen.  

In diesem Leitfaden zeigen wir Ihnen, wie Sie **Excel nach PowerPoint exportieren** und dabei editierbaren Text, Diagrammtreue und Layout beibehalten – und das mit nur wenigen Zeilen C#. Am Ende haben Sie eine einsatzbereite PPTX‑Datei, die Sie in PowerPoint genauso anpassen können wie jede manuell erstellte Folie.

## Was Sie lernen werden

- Wie Sie eine Excel‑Arbeitsmappe laden, die Diagramme und Formen enthält.  
- Wie Sie `PresentationExportOptions` konfigurieren, damit Textfelder editierbar bleiben (`export editable text`).  
- Wie Sie **Excel‑Diagramm nach PowerPoint exportieren** und ein sauberes Folienset erhalten.  
- Kleine Variationen, die Sie anwenden können, wenn Sie **Excel‑Diagramm nach PowerPoint konvertieren** für unterschiedliche Seiteneinstellungen oder mehrere Arbeitsblätter.

### Voraussetzungen

- Eine .NET‑Entwicklungsumgebung (Visual Studio 2022 oder neuer).  
- Aspose.Cells für .NET (Testversion oder lizenziert).  
- Eine Excel‑Datei (`ChartWithShape.xlsx`), die mindestens ein Diagramm und eine Form enthält, die Sie editierbar behalten möchten.  

Wenn Sie das haben, legen wir los – ohne Umschweife, nur eine praxisnahe, ausführbare Lösung.

## PowerPoint aus Excel erstellen – Schritt für Schritt

Unter jedem Schritt geben wir ein kompaktes Code‑Snippet, erklären **warum** wir es tun, und weisen auf häufige Stolperfallen hin. Sie können das vollständige Beispiel am Seitenende einfach kopieren und einfügen.

### Schritt 1: Laden der Excel‑Arbeitsmappe

Zuerst müssen wir die Quellarbeitsmappe in den Speicher laden. Aspose.Cells liest die Datei und baut ein reichhaltiges Objektmodell auf, das wir manipulieren können.

```csharp
// Step 1: Load the Excel workbook that contains the chart and shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");

// Quick sanity check – make sure the workbook actually loaded
if (workbook.Worksheets.Count == 0)
    throw new InvalidOperationException("The workbook appears to be empty.");
```

**Warum das wichtig ist:**  
Das Laden der Arbeitsmappe ist die Basis. Wenn der Dateipfad falsch ist oder die Arbeitsmappe beschädigt ist, schlagen alle nachfolgenden `export excel to powerpoint`‑Schritte fehl. Der Sanity‑Check gibt Ihnen frühzeitig Feedback statt einer vagen „Datei nicht gefunden“-Meldung später.

### Schritt 2: Export‑Optionen vorbereiten

Aspose.Cells stellt ein `PresentationExportOptions`‑Objekt bereit, das steuert, wie die PPTX aussehen wird. Hier entscheiden Sie, ob der Text editierbar bleiben soll.

```csharp
// Step 2: Create export options for PowerPoint conversion
PresentationExportOptions exportOptions = new PresentationExportOptions();

// Optional: tweak the slide size (default is 10in x 7.5in)
exportOptions.SlideSize = new SizeF(10, 7.5f);
```

**Warum das wichtig ist:**  
Ohne Konfiguration von `PresentationExportOptions` verwendet die Bibliothek ihre Vorgaben, die möglicherweise nicht zu Ihrer Unternehmens‑Slide‑Vorlage passen. Die Foliengröße gleich zu Beginn anzupassen verhindert manuelles Nachgrößen später.

### Schritt 3: Editierbare Textfelder aktivieren

Das magische Flag `ExportEditableTextBoxes` weist Aspose.Cells an, alle Textformen als PowerPoint‑Textfelder und nicht als statische Bilder zu übernehmen.

```csharp
// Step 3: Enable editability of text boxes in the resulting presentation
exportOptions.ExportEditableTextBoxes = true;
```

**Warum das wichtig ist:**  
Wenn Sie diese Zeile weglassen, enthält die resultierende PPTX gerasterten Text – Sie können die Beschriftung oder Caption in PowerPoint nicht mehr bearbeiten. Das Setzen von `export editable text` ist der Schlüssel zu einer wirklich wiederverwendbaren Folie.

### Schritt 4: Arbeitsblatt nach PPTX exportieren

Jetzt schreiben wir die PPTX‑Datei. Sie können jedes Arbeitsblatt wählen; hier verwenden wir das erste (`Worksheets[0]`).

```csharp
// Step 4: Export the first worksheet's page setup to a PPTX file
workbook.Worksheets[0].PageSetup.SaveToPptx("YOUR_DIRECTORY/Result.pptx", exportOptions);
```

**Warum das wichtig ist:**  
`SaveToPptx` respektiert die Seiteneinrichtung (Ränder, Ausrichtung), die Sie in Excel definiert haben, sodass die Folie das von Ihnen entworfene Layout widerspiegelt. Das ist das Kernstück von **export excel chart powerpoint**.

### Schritt 5: Ausgabe prüfen (optional, aber empfohlen)

Nach der Konvertierung öffnen Sie die erzeugte `Result.pptx` in PowerPoint und prüfen:

1. Diagramme erscheinen scharf und behalten die Datenreihen.  
2. Textfelder sind auswähl‑ und editierbar.  
3. Die Foliengröße entspricht Ihren Erwartungen.

Falls etwas nicht stimmt, überprüfen Sie `exportOptions` – zum Beispiel könnten Sie `exportOptions.IncludePrintArea = true` setzen, um einen benannten Druckbereich zu berücksichtigen.

```csharp
// Optional: open the PPTX automatically (requires System.Diagnostics)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = "YOUR_DIRECTORY/Result.pptx",
    UseShellExecute = true
});
```

### Schritt 6: Erweiterte Varianten (mehrere Blätter exportieren)

Oft möchten Sie **excel chart powerpoint konvertieren** für mehrere Arbeitsblätter gleichzeitig. Durchlaufen Sie die Sammlung und geben Sie jeder Folie einen eindeutigen Namen:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    string outputPath = $"YOUR_DIRECTORY/Result_Sheet{i + 1}.pptx";
    workbook.Worksheets[i].PageSetup.SaveToPptx(outputPath, exportOptions);
}
```

**Pro‑Tipp:** Wenn Sie alle Blätter in einer *einzigen* PPTX haben wollen, erstellen Sie ein neues `Presentation`‑Objekt, importieren jede Folie und speichern einmal. Das ist etwas aufwändiger, spart aber das Jonglieren mit vielen Dateien.

## Vollständiges funktionierendes Beispiel

Hier das komplette Programm, das Sie in eine Konsolen‑App einfügen und sofort ausführen können.

```csharp
using System;
using System.Drawing;
using Aspose.Cells;
using Aspose.Cells.Export;

class Program
{
    static void Main()
    {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWithShape.xlsx");
        if (workbook.Worksheets.Count == 0)
        {
            Console.WriteLine("Workbook is empty – aborting.");
            return;
        }

        // 2️⃣ Set up export options
        PresentationExportOptions exportOptions = new PresentationExportOptions
        {
            SlideSize = new SizeF(10, 7.5f),          // optional custom size
            ExportEditableTextBoxes = true           // <‑‑ keep text boxes editable
        };

        // 3️⃣ Export first worksheet
        string outputPath = "YOUR_DIRECTORY/Result.pptx";
        workbook.Worksheets[0].PageSetup.SaveToPptx(outputPath, exportOptions);
        Console.WriteLine($"PowerPoint created at: {outputPath}");

        // 4️⃣ Open the result automatically (Windows only)
        try
        {
            System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
            {
                FileName = outputPath,
                UseShellExecute = true
            });
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Could not open PPTX automatically: {ex.Message}");
        }
    }
}
```

**Erwartetes Ergebnis:**  
Wenn Sie `Result.pptx` öffnen, sehen Sie eine Folie, die das Layout des Excel‑Arbeitsblatts widerspiegelt. Jedes Diagramm, das Sie in Excel platziert haben, erscheint als nativer PowerPoint‑Chart, und die als Form hinzugefügte Beschriftung ist nun ein vollständig editierbares Textfeld.

## Häufige Fragen & Sonderfälle

- **Funktioniert das mit makrofähigen Arbeitsmappen (`.xlsm`)?**  
  Ja. Aspose.Cells liest Makros, führt sie aber nicht aus. Der Konvertierungsprozess ignoriert VBA, sodass Sie trotzdem die visuelle Darstellung erhalten.

- **Was, wenn mein Arbeitsblatt mehrere Diagramme enthält?**  
  Alle sichtbaren Diagramme werden auf dieselbe Folie übertragen. Wenn Sie jedes Diagramm auf einer eigenen Folie benötigen, teilen Sie das Arbeitsblatt oder nutzen Sie die Schleife aus Schritt 6.

- **Kann ich benutzerdefinierte PowerPoint‑Designs beibehalten?**  
  Nicht direkt während des Exports. Nach der Konvertierung können Sie in PowerPoint ein Design anwenden oder programmgesteuert über Aspose.Slides hinzufügen.

- **Gibt es eine Möglichkeit, nur einen ausgewählten Bereich zu exportieren?**  
  Definieren Sie einen benannten Druckbereich in Excel (`Seitenlayout → Druckbereich`) und aktivieren Sie `exportOptions.IncludePrintArea = true`.

## Fazit

Sie wissen jetzt, wie Sie **PowerPoint aus Excel erstellen** mit Aspose.Cells, wobei Sie die volle Kontrolle über editierbaren Text, Diagrammtreue und Foliengröße haben. Das kurze Code‑Snippet deckt das gängigste Szenario ab, und die zusätzlichen Tipps geben Ihnen Flexibilität, wenn Sie **excel to powerpoint exportieren** für mehrere Blätter oder benutzerdefinierte Layouts benötigen.  

Bereit für die nächste Herausforderung? Kombinieren Sie diesen Ansatz mit **Aspose.Slides**, um programmgesteuert Übergänge, Referenten‑Notizen oder sogar die erzeugten Folien in eine größere Präsentation einzubetten. Oder experimentieren Sie mit der Umwandlung einer kompletten Arbeitsmappe in ein mehrseitiges Deck – ideal für automatisierte Reporting‑Pipelines.

Haben Sie Fragen oder einen cleveren Trick entdeckt? Hinterlassen Sie einen Kommentar unten, und happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}