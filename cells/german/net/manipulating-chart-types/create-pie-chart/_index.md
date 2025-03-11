---
title: Kreisdiagramm erstellen
linktitle: Kreisdiagramm erstellen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET ein Kreisdiagramm in Excel erstellen. Visualisieren Sie Ihre Daten mühelos.
weight: 12
url: /de/net/manipulating-chart-types/create-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kreisdiagramm erstellen

## Einführung

Das Erstellen von Diagrammen ist für die visuelle Darstellung von Daten unerlässlich, und Kreisdiagramme sind eine der beliebtesten Möglichkeiten, um zu veranschaulichen, wie Teile ein Ganzes bilden. Mit Aspose.Cells für .NET können Sie die Generierung von Kreisdiagrammen in Excel-Dateien ganz einfach automatisieren. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells für .NET ein Kreisdiagramm von Grund auf erstellen. Eine Schritt-für-Schritt-Anleitung sorgt dafür, dass der Vorgang reibungslos und unkompliziert abläuft. Egal, ob Sie das Tool noch nicht kennen oder Ihre Excel-Automatisierungskenntnisse verbessern möchten, in diesem Handbuch finden Sie alles!

## Voraussetzungen

Bevor Sie sich in den Code vertiefen, stellen Sie sicher, dass Sie Folgendes eingerichtet haben:

1.  Aspose.Cells für .NET-Bibliothek: Stellen Sie sicher, dass Sie Aspose.Cells in Ihrem Projekt installiert haben. Wenn Sie es noch nicht installiert haben, können Sie es hier herunterladen:[Hier](https://releases.aspose.com/cells/net/).
2. .NET-Entwicklungsumgebung: Stellen Sie sicher, dass Ihr Projekt für die Verwendung von .NET Framework oder .NET Core eingerichtet ist.
3. Grundkenntnisse in C#: Sie sollten mit der C#-Programmierung vertraut sein, insbesondere mit der objektorientierten Programmierung (OOP).

 Für fortgeschrittene Benutzer kann eine temporäre Lizenz beantragt werden, um alle Funktionen von Aspose.Cells freizuschalten. Sie können eine anfordern bei[Hier](https://purchase.aspose.com/temporary-license/).

## Pakete importieren

Importieren Sie zunächst die für dieses Tutorial erforderlichen Namespaces und Pakete. Dazu gehören grundlegende E/A-Vorgänge und das Aspose.Cells-Paket.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Schritt 1: Erstellen Sie eine neue Arbeitsmappe

 Zuerst müssen wir eine Instanz des`Workbook` Klasse, die die Excel-Datei darstellt. Eine Arbeitsmappe enthält mehrere Blätter, und in unserem Beispiel arbeiten wir mit zwei Blättern – einem für Daten und einem für das Kreisdiagramm.

```csharp
Workbook workbook = new Workbook();
```

Damit wird eine neue Excel-Arbeitsmappe initialisiert. Doch wohin gehen die Daten? Darum kümmern wir uns im nächsten Schritt.

## Schritt 2: Daten zum Arbeitsblatt hinzufügen

Sobald die Arbeitsmappe erstellt ist, müssen wir auf das erste Arbeitsblatt zugreifen und ihm einen Namen geben. Hier geben wir die für das Kreisdiagramm erforderlichen Daten ein.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Jetzt können wir einige Dummy-Verkaufsdaten eingeben, die verschiedene Regionen repräsentieren:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Hier fügen wir zwei Spalten hinzu: eine für Regionen und eine für Verkaufszahlen. Diese Daten werden im Kreisdiagramm dargestellt.

## Schritt 3: Fügen Sie ein Diagrammblatt hinzu

Als Nächstes fügen wir ein separates Arbeitsblatt hinzu, das das Kreisdiagramm enthält.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Dieses neue Blatt enthält das Kreisdiagramm. Wenn Sie ihm einen Namen wie „Diagramm“ geben, wissen Benutzer, was sie erwartet, wenn sie die Datei öffnen.

## Schritt 4: Erstellen Sie das Kreisdiagramm

Jetzt ist es an der Zeit, das eigentliche Diagramm zu erstellen. Wir geben an, dass wir ein Kreisdiagramm möchten, und definieren seine Position auf dem Blatt.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

 Die Methode`Add()`akzeptiert Parameter für den Diagrammtyp (in diesem Fall`ChartType.Pie`) und seine Position auf dem Arbeitsblatt. Die Zahlen repräsentieren Zeilen- und Spaltenpositionen.

## Schritt 5: Anpassen des Diagrammaussehens

Ein Kreisdiagramm wäre ohne Anpassungen unvollständig! Lassen Sie uns unser Diagramm optisch ansprechend gestalten, indem wir Farben, Beschriftungen und Titel optimieren.

### Diagrammtitel festlegen
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Plotbereich anpassen
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Wir legen die Verlaufsfüllung für den Plotbereich fest und verbergen den Rand für ein saubereres Erscheinungsbild.

## Schritt 6: Diagrammdaten definieren

 Es ist Zeit, das Diagramm mit unseren Daten zu verknüpfen.`NSeries` Eigenschaft des Diagramms bindet die Umsatzzahlen und Regionen an das Kreisdiagramm.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

 Die erste Zeile gibt an, dass wir die Verkaufsdaten aus Zellen verwenden`B2:B8` . Wir sagen dem Diagramm auch, dass es die Regionsnamen verwenden soll aus`A2:A8` als Kategoriebeschriftungen.

## Schritt 7: Datenbeschriftungen hinzufügen

Das direkte Hinzufügen von Beschriftungen zu den Diagrammsegmenten kann das Verständnis erleichtern. Lassen Sie uns die Regionsnamen und Verkaufswerte in die Kreisdiagrammsegmente aufnehmen.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Schritt 8: Diagrammbereich und Legende anpassen

Zum Schluss geben wir dem Diagrammbereich und der Legende noch den letzten Schliff. Dadurch wird die Gesamtdarstellung des Diagramms verbessert.

### Diagrammbereich
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legende
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Schritt 9: Speichern der Arbeitsmappe

Zum Schluss speichern wir die Arbeitsmappe in einer Excel-Datei. Das Ausgabeverzeichnis und den Dateinamen können Sie nach Bedarf angeben.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Abschluss

Das Erstellen eines Kreisdiagramms mit Aspose.Cells für .NET ist ein unkomplizierter und anpassbarer Prozess. Wenn Sie dieser Anleitung folgen, können Sie in nur wenigen Schritten ein professionell aussehendes Diagramm erstellen, das wertvolle Erkenntnisse vermittelt. Ob für Geschäftsberichte oder Bildungszwecke – die Beherrschung der Diagrammerstellung wird Ihre Excel-Automatisierungsfähigkeiten verbessern. Denken Sie daran, Aspose.Cells bietet die Flexibilität, die Sie benötigen, um mühelos beeindruckende, datengesteuerte Excel-Dateien zu erstellen.

## Häufig gestellte Fragen

### Kann ich mit Aspose.Cells für .NET andere Diagrammtypen erstellen?
Ja! Aspose.Cells unterstützt verschiedene Diagrammtypen, darunter Balkendiagramme, Liniendiagramme und Streudiagramme.

### Benötige ich eine kostenpflichtige Lizenz, um Aspose.Cells für .NET zu verwenden?
Sie können die kostenlose Version mit einigen Einschränkungen nutzen. Für den vollen Funktionsumfang benötigen Sie eine Lizenz, die Sie kaufen können[Hier](https://purchase.aspose.com/buy).

### Kann ich das Diagramm in Formate wie PDF oder Bilder exportieren?
Auf jeden Fall! Mit Aspose.Cells können Sie Diagramme in verschiedene Formate exportieren, darunter PDF und PNG.

### Ist es möglich, jedes Tortenstück mit einer anderen Farbe zu gestalten?
 Ja, Sie können jedem Slice eine andere Farbe zuweisen, indem Sie die`IsColorVaried` Eigentum an`true`, wie im Tutorial gezeigt.

### Kann ich die Generierung mehrerer Diagramme in einer einzigen Arbeitsmappe automatisieren?
Ja, Sie können in einer einzigen Excel-Datei beliebig viele Diagramme erstellen und anpassen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
