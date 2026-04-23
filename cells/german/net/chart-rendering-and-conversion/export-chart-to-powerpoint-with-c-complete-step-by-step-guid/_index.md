---
category: general
date: 2026-02-26
description: Diagramm aus Excel mit C# nach PowerPoint exportieren. Erfahren Sie,
  wie Sie Excel nach PowerPoint konvertieren, Excel als PowerPoint speichern und die
  Formen bearbeitbar halten.
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: de
og_description: Diagram aus Excel mit C# nach PowerPoint exportieren. Dieser Leitfaden
  zeigt, wie man Excel nach PowerPoint konvertiert, die Arbeitsmappe als PPTX speichert
  und die Formen editierbar hält.
og_title: Diagramm mit C# nach PowerPoint exportieren – Vollständiges Programmier‑Tutorial
tags:
- Aspose.Cells
- C#
- Office Automation
title: Diagramm nach PowerPoint mit C# exportieren – vollständige Schritt‑für‑Schritt‑Anleitung
url: /de/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm nach PowerPoint exportieren – Vollständiges Programmier‑Tutorial

Haben Sie sich jemals gefragt, wie man **export chart to PowerPoint** ohne Verlust der Bearbeitbarkeit exportiert? In vielen Reporting‑Szenarien benötigen Sie ein Live‑Diagramm innerhalb einer Präsentation, doch manuelles Kopieren und Einfügen ist mühsam. Die gute Nachricht: Sie können dies programmgesteuert mit wenigen Zeilen C# erledigen.

In diesem Leitfaden gehen wir den gesamten Prozess durch: vom Laden einer Excel‑Arbeitsmappe, die ein Diagramm mit einem Textfeld enthält, über die Konfiguration des Exports, sodass Textfelder und Formen editierbar bleiben, bis hin zum Speichern des Ergebnisses als **PowerPoint**‑Datei. Am Ende wissen Sie außerdem, wie man **convert Excel to PowerPoint**, **save Excel as PowerPoint** durchführt und sogar die Optionen für Rand‑Fall‑Szenarien anpasst.

## Was Sie benötigen

- **Aspose.Cells for .NET** (Version 23.10 oder neuer). Das ist die Bibliothek, die die Konvertierung mühelos macht.
- **.NET 6+** Runtime – jedes aktuelle SDK funktioniert.
- Eine einfache Excel‑Datei (`ChartWithTextbox.xlsx`), die mindestens ein Diagramm und ein Textfeld enthält.
- Visual Studio oder Ihre bevorzugte IDE.

Zusätzliche NuGet‑Pakete sind über Aspose.Cells hinaus nicht erforderlich, doch ein grundlegendes Verständnis von C#‑Syntax hilft selbstverständlich.

## Export Chart to PowerPoint – Schritt‑für‑Schritt

Im Folgenden zerlegen wir die Lösung in übersichtliche, leicht nachvollziehbare Schritte. Jeder Schritt enthält den exakt benötigten Code sowie einen kurzen „Warum‑Absatz“, der die dahinterstehende Logik erklärt.

### Schritt 1: Laden der Excel‑Arbeitsmappe, die das Diagramm enthält

Zuerst müssen wir die Quelldatei in den Speicher einlesen. Mit `Workbook` von Aspose.Cells wird die gesamte Tabelle gelesen, inklusive Diagrammen, Bildern und eingebetteten Objekten.

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*Warum das wichtig ist:* Wird die Arbeitsmappe ohne korrekte Pfadangabe geöffnet, erhalten Sie eine `FileNotFoundException`. Der schnelle Plausibilitäts‑Check verhindert, dass Sie später eine leere Folie exportieren.

### Schritt 2: Präsentationsoptionen vorbereiten, damit Formen editierbar bleiben

Aspose.Cells lässt Sie entscheiden, ob Textfelder, Formen und sogar das Diagramm selbst **editierbar** bleiben sollen nach dem Export. Durch Setzen von `ExportTextBoxes` und `ExportShapes` auf `true` werden diese Objekte als native PowerPoint‑Elemente erhalten, anstatt zu einem statischen Bild zu werden.

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*Warum das wichtig ist:* Bleiben diese Flags bei den Standardwerten (`false`), enthält die resultierende Folie ein Bitmap‑Diagramm, das nicht mehr bearbeitet werden kann (z. B. Serien ändern oder Beschriftungen anpassen). Durch Aktivieren beider Optionen erhalten Sie ein echtes PowerPoint‑Diagramm, das sich exakt wie ein manuell erstelltes verhält.

### Schritt 3: Excel nach PowerPoint konvertieren und Datei speichern

Jetzt rufen wir die `Save`‑Methode auf, übergeben das `SaveFormat.Pptx`‑Enum und die zuvor konfigurierten Optionen. Die Bibliothek übernimmt die Übersetzung des Excel‑Diagrammobjekts in ein PowerPoint‑Diagramm‑Shape.

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*Warum das wichtig ist:* Der Aufruf von `Save` erledigt die schwere Arbeit – Zuordnung von Excel‑Serien zu PowerPoint‑Serien, Erhaltung der Achsenformatierung und Kopieren aller verknüpften Textfelder. Nach dieser Zeile besitzen Sie eine vollständig editierbare `.pptx`‑Datei, die in Microsoft PowerPoint geöffnet werden kann.

### Ergebnis überprüfen

Öffnen Sie `Result.pptx` in PowerPoint. Sie sollten eine Folie sehen, die enthält:

- Das ursprüngliche Diagramm, weiterhin mit seinen Daten verknüpft (Doppelklick zum Bearbeiten der Serien).
- Jedes Textfeld, das in der Excel‑Tabelle war, jetzt ein natives PowerPoint‑Textfeld.
- Das Folienlayout wird automatisch gewählt (in der Regel eine leere Folie).

Falls Elemente fehlen, prüfen Sie, ob die Quell‑Arbeitsmappe tatsächlich sichtbare Objekte enthielt und ob `ExportTextBoxes` / `ExportShapes` auf `true` gesetzt waren.

### Excel nach PowerPoint konvertieren: Mehrere Arbeitsblätter behandeln

Oft enthält eine Arbeitsmappe mehr als ein Blatt, jedes mit eigenem Diagramm. Standardmäßig exportiert Aspose.Cells **alle** Diagramme aus **allen** Arbeitsblättern in separate Folien. Wenn Sie nur einen Teil benötigen, können Sie sie vor dem Speichern filtern:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*Pro‑Tipp:* Das Setzen von `chart.IsVisible = false` ist günstiger als das Diagramm komplett zu entfernen und ermöglicht ein einfaches Ein‑ bzw. Ausschalten ohne Änderung der Quelldatei.

### Excel als PowerPoint speichern – Foliengröße anpassen

PowerPoint verwendet standardmäßig eine Folie von 10 inch × 5,63 inch. Wenn Ihr Diagramm zu gedrängt wirkt, können Sie die Folienabmessungen über das `PresentationOptions`‑Objekt ändern:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

Jetzt hat das exportierte Diagramm mehr Spielraum, und Textfelder behalten ihr ursprüngliches Layout bei.

### Excel nach PPT konvertieren: Versteckte Objekte behandeln

Versteckte Zeilen, Spalten oder Formen können manchmal in den Export gelangen. Um sie zu entfernen, führen Sie vor dem Speichern eine kurze Aufräum‑Routine aus:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

Dieser Schritt ist nicht immer nötig, verhindert jedoch unerwartete Lücken im finalen Foliensatz.

### Arbeitsmappe als PPTX speichern – Vollständiges Beispiel

Alles zusammengeführt, hier ein lauffähiges Konsolenprogramm, das den gesamten Ablauf demonstriert:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

Wenn Sie dieses Programm ausführen, wird `Result.pptx` mit einem editierbaren Diagramm und Textfeld erstellt – genau das, was Sie erwarten, wenn Sie **save workbook as pptx** manuell durchführen.

![Export chart to PowerPoint example](/images/export-chart-to-powerpoint.png "Export chart to PowerPoint – editable slide")

## Häufige Fragen & Randfälle

**Was passiert, wenn die Excel‑Datei ein Diagramm mit einer externen Datenquelle enthält?**  
Aspose.Cells kopiert die *aktuellen* Datenwerte in das PowerPoint‑Diagramm. Es wird **keine** externe Verknüpfung erhalten, da PowerPoint keine Excel‑Datenverbindung in derselben Weise referenzieren kann. Für Live‑Updates sollten Sie die ursprüngliche Excel‑Datei stattdessen als OLE‑Objekt in die PPTX einbetten.

**Kann ich ein Diagramm exportieren, das ein benutzerdefiniertes Theme verwendet?**  
Ja. Die Bibliothek versucht, Excel‑Theme‑Farben den PowerPoint‑Theme‑Slots zuzuordnen. Bei sehr individuellen Paletten müssen Sie die Farben nach dem Export eventuell über die PowerPoint‑API (z. B. Aspose.Slides) anpassen.

**Gibt es ein Limit für die Anzahl der Diagramme?**  
Praktisch kein – Aspose.Cells streamt die Daten, sodass selbst Arbeitsmappen mit Dutzenden von Diagrammen exportiert werden können, wobei die resultierende PPTX‑Dateigröße linear wächst.

**Benötige ich eine Lizenz für Aspose.Cells?**  
Eine kostenlose Evaluation funktioniert, fügt jedoch ein Wasserzeichen auf der ersten Folie ein. Für den Produktionseinsatz sollten Sie eine gültige Lizenz erwerben, um das Wasserzeichen zu entfernen und die volle Performance freizuschalten.

## Zusammenfassung

Wir haben gezeigt, wie man **export chart to PowerPoint** mit C# durchführt, den genauen Code zum Laden einer Excel‑Arbeitsmappe, zur Konfiguration von `PresentationOptions` für editierbare Textfelder und Formen und schließlich zum Speichern als `.pptx` demonstriert. Außerdem haben Sie gelernt, wie man **convert Excel to PowerPoint**, **save Excel as PowerPoint** ausführt und die Frage „**how to convert Excel to ppt**“ mit einem vollständigen, ausführbaren Beispiel beantwortet.

## Was kommt als Nächstes?

- **Save workbook as PPTX** mit mehreren Folien: Durchlaufen Sie jedes Arbeitsblatt und rufen Sie `Save` mit `PresentationOptions` für jedes auf.
- Erkunden Sie **Aspose.Slides**, wenn Sie das erzeugte PPTX programmgesteuert weiter bearbeiten möchten (Übergänge, Sprecher‑Notizen usw.).
- Probieren Sie das Exportieren von **Pivot‑Diagrammen** oder **3‑D‑Diagrammen** – dieselben Optionen gelten, jedoch müssen Sie ggf. die Achsenformatierung nachträglich anpassen.

Wenn Sie auf Probleme stoßen, hinterlassen Sie einen Kommentar unten oder schauen Sie in die offizielle Aspose.Cells‑Dokumentation für die neuesten API‑Änderungen. Viel Spaß beim Coden und beim Umwandeln Ihrer Excel‑Diagramme in professionelle PowerPoint‑Präsentationen mit nur wenigen Zeilen C#!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}