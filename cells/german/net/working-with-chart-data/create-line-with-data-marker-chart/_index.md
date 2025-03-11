---
title: Erstellen eines Liniendiagramms mit Datenmarkierungen
linktitle: Erstellen eines Liniendiagramms mit Datenmarkierungen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET ein Liniendiagramm mit Datenmarkierungen in Excel erstellen. Folgen Sie dieser Schritt-für-Schritt-Anleitung, um Diagramme einfach zu erstellen und anzupassen.
weight: 10
url: /de/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen eines Liniendiagramms mit Datenmarkierungen

## Einführung

Haben Sie sich schon einmal gefragt, wie Sie in Excel programmgesteuert beeindruckende Diagramme erstellen können? Nun, schnallen Sie sich an, denn heute tauchen wir in die Erstellung eines Liniendiagramms mit Datenmarkierungen mithilfe von Aspose.Cells für .NET ein. Dieses Tutorial führt Sie durch jeden Schritt und stellt sicher, dass Sie die Diagrammerstellung gut beherrschen, auch wenn Sie gerade erst mit Aspose.Cells beginnen.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie alles bereit haben, um nahtlos mitmachen zu können.

1. Aspose.Cells für .NET-Bibliothek – Sie müssen dies installieren. Sie können es herunterladen[Hier](https://releases.aspose.com/cells/net/).
2. .NET Framework – Stellen Sie sicher, dass Ihre Entwicklungsumgebung mit der neuesten Version von .NET eingerichtet ist.
3. IDE (Integrated Development Environment) – Visual Studio wird empfohlen.
4.  Eine gültige Aspose.Cells-Lizenz – Wenn Sie keine haben, können Sie eine anfordern[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder schauen Sie sich ihre[Kostenlose Testversion](https://releases.aspose.com/).

Bereit loszulegen? Dann lass es uns aufschlüsseln!

## Erforderliche Pakete importieren

Stellen Sie zunächst sicher, dass Sie die folgenden Namespaces in Ihr Projekt importieren. Diese stellen die erforderlichen Klassen und Methoden zum Erstellen Ihres Diagramms bereit.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Sobald Sie das geschafft haben, können wir mit dem Programmieren beginnen!

## Schritt 1: Richten Sie Ihre Arbeitsmappe und Ihr Arbeitsblatt ein

Als Erstes müssen Sie eine neue Arbeitsmappe erstellen und auf das erste Arbeitsblatt zugreifen.

```csharp
//Ausgabeverzeichnis
static string outputDir = "Your Document Directory";
		
// Instanziieren einer Arbeitsmappe
Workbook workbook = new Workbook();

// Greifen Sie auf das erste Arbeitsblatt zu
Worksheet worksheet = workbook.Worksheets[0];
```

Stellen Sie sich die Arbeitsmappe als Ihre Excel-Datei und das Arbeitsblatt als das darin enthaltene spezifische Blatt vor. In diesem Fall arbeiten wir mit dem ersten Blatt.

## Schritt 2: Füllen Sie das Arbeitsblatt mit Daten

Jetzt, da wir unser Arbeitsblatt haben, füllen wir es mit einigen Daten. Wir erstellen zufällige Datenpunkte für zwei Wertereihen.

```csharp
// Spaltentitel festlegen
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Zufällige Daten zur Erstellung des Diagramms
Random R = new Random();

// Zufällige Daten erstellen und in den Zellen speichern
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Hier verwenden wir Zufallszahlen, um Daten zu simulieren, aber in realen Anwendungen können Sie sie mit tatsächlichen Werten aus Ihrem Datensatz füllen.

## Schritt 3: Fügen Sie das Diagramm zum Arbeitsblatt hinzu

Als Nächstes fügen wir das Diagramm zum Arbeitsblatt hinzu und wählen den Typ aus – in diesem Fall ein Liniendiagramm mit Datenmarkierungen.

```csharp
// Hinzufügen eines Diagramms zum Arbeitsblatt
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Greifen Sie auf das neu erstellte Diagramm zu
Chart chart = worksheet.Charts[idx];
```

Dieses Snippet fügt dem Arbeitsblatt ein Liniendiagramm mit Datenmarkierungen hinzu und platziert es in einem bestimmten Bereich (1,3 bis 20,20). Ziemlich einfach, oder?

## Schritt 4: Das Erscheinungsbild des Diagramms anpassen

Sobald das Diagramm erstellt ist, können Sie es nach Ihren Wünschen gestalten. Lassen Sie uns den Hintergrund, den Titel und den Diagrammstil ändern.

```csharp
// Diagrammstil festlegen
chart.Style = 3;

// Setzen Sie den Autoscaling-Wert auf „true“.
chart.AutoScaling = true;

// Vordergrundfarbe auf Weiß setzen
chart.PlotArea.Area.ForegroundColor = Color.White;

//Festlegen der Eigenschaften des Diagrammtitels
chart.Title.Text = "Sample Chart";

// Diagrammtyp festlegen
chart.Type = ChartType.LineWithDataMarkers;
```

Hier verleihen wir dem Diagramm ein klares Aussehen, indem wir einen weißen Hintergrund festlegen, eine automatische Skalierung vornehmen und ihm einen aussagekräftigen Titel geben.

## Schritt 5: Serien definieren und Datenpunkte darstellen

Nachdem unser Diagramm nun gut aussieht, müssen wir die Datenreihen definieren, die dargestellt werden sollen.

```csharp
// Eigenschaften des Kategorieachsentitels festlegen
chart.CategoryAxis.Title.Text = "Units";

// Definieren Sie zwei Reihen für das Diagramm
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Diese Reihen entsprechen den Datenpunktbereichen, die wir zuvor ausgefüllt haben.

## Schritt 6: Farben hinzufügen und Serienmarkierungen anpassen

Lassen Sie uns dieses Diagramm noch ansprechender gestalten, indem Sie unseren Datenmarkierungen benutzerdefinierte Farben hinzufügen.

```csharp
// Erste Serie anpassen
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Zweite Serie anpassen
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Durch die Anpassung der Farben machen Sie das Diagramm nicht nur funktional, sondern auch optisch ansprechend!

## Schritt 7: X- und Y-Werte für jede Serie festlegen

Lassen Sie uns abschließend für jede unserer Reihen die X- und Y-Werte zuweisen.

```csharp
// Legen Sie die X- und Y-Werte der ersten Reihe fest
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// X- und Y-Werte der zweiten Reihe festlegen
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Die Werte basieren auf den Daten, die wir in Schritt 2 eingegeben haben.

## Schritt 8: Speichern Sie die Arbeitsmappe

Nachdem nun alles eingestellt ist, speichern wir die Arbeitsmappe, damit wir das Diagramm in Aktion sehen können.

```csharp
// Speichern der Arbeitsmappe
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Und das ist es! Sie haben gerade mit Aspose.Cells für .NET ein Liniendiagramm mit Datenmarkierungen erstellt.

## Abschluss

Das programmgesteuerte Erstellen von Diagrammen in Excel kann entmutigend erscheinen, aber mit Aspose.Cells für .NET ist es so einfach wie das Befolgen einer Schritt-für-Schritt-Anleitung. Vom Einrichten Ihrer Arbeitsmappe bis zum Anpassen des Diagrammaussehens erledigt diese leistungsstarke Bibliothek alles. Egal, ob Sie Berichte, Dashboards oder Datenvisualisierungen erstellen, mit Aspose.Cells ist das ein Kinderspiel.

## Häufig gestellte Fragen

### Kann ich das Diagramm weiter anpassen?  
Auf jeden Fall! Aspose.Cells bietet jede Menge Anpassungsoptionen, von Schriftarten bis zu Gitternetzlinien und mehr.

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?  
 Ja, für die volle Funktionalität ist eine Lizenz erforderlich. Sie erhalten eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) oder beginnen Sie mit einem[Kostenlose Testversion](https://releases.aspose.com/).

### Wie kann ich weitere Datenreihen hinzufügen?  
 Fügen Sie einfach weitere Serien hinzu mit dem`NSeries.Add` Methode, um die Zellbereiche für die neuen Daten anzugeben.

### Kann ich das Diagramm als Bild exportieren?  
 Ja, Sie können Diagramme direkt als Bilder exportieren mit dem`Chart.ToImage` Verfahren.

### Unterstützt Aspose.Cells 3D-Diagramme?  
Ja, Aspose.Cells unterstützt eine breite Palette von Diagrammtypen, einschließlich 3D-Diagrammen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
