---
title: Hauptgitternetzlinien im Diagramm ändern
linktitle: Hauptgitternetzlinien im Diagramm ändern
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in unserer ausführlichen Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET die Hauptgitternetzlinien in Excel-Diagrammen ändern.
weight: 11
url: /de/net/setting-chart-appearance/change-major-gridlines-in-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hauptgitternetzlinien im Diagramm ändern

## Einführung

Das Erstellen optisch ansprechender Diagramme in Excel ist für eine effektive Datenpräsentation unerlässlich. Egal, ob Sie Datenanalyst, Projektmanager oder einfach nur an Datenvisualisierung interessiert sind, das Wissen, wie man Diagramme anpasst, kann Ihre Berichte erheblich verbessern. In diesem Artikel erfahren Sie, wie Sie die wichtigsten Gitternetzlinien in einem Excel-Diagramm mithilfe der Aspose.Cells-Bibliothek für .NET ändern.

## Voraussetzungen

Bevor wir beginnen, müssen Sie einige Dinge vorbereitet haben, um eine reibungslose Arbeit mit Aspose.Cells zu gewährleisten:

- Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Hier schreiben und führen Sie Ihren Code aus.
-  Aspose.Cells für .NET: Sie können die neueste Version von Aspose.Cells herunterladen von der[Webseite](https://releases.aspose.com/cells/net/) Wenn Sie vor dem Kauf experimentieren möchten, sollten Sie sich für ein[Kostenlose Testversion](https://releases.aspose.com/).
- Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie den Beispielen in diesem Tutorial leichter folgen.

Sobald Sie alles eingerichtet haben, können wir mit dem Schreiben unseres Codes beginnen!

## Pakete importieren

Um mit Aspose.Cells zu arbeiten, müssen Sie zunächst die erforderlichen Pakete in Ihr C#-Projekt importieren. Öffnen Sie Ihr Visual Studio-Projekt und fügen Sie die folgenden using-Direktiven oben in Ihre C#-Datei ein:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

Diese Pakete ermöglichen Ihnen den Zugriff auf die Klassen und Methoden, die Sie zum Erstellen und Ändern von Excel-Arbeitsmappen und -Diagrammen benötigen.

Lassen Sie uns den Prozess nun in detaillierte und leicht verständliche Schritte unterteilen. Wir erstellen ein einfaches Diagramm mit einigen Daten und ändern dann die Farbe der wichtigsten Gitternetzlinien.

## Schritt 1: Legen Sie Ihr Ausgabeverzeichnis fest

Als Erstes müssen Sie festlegen, wo die Excel-Ausgabedatei gespeichert werden soll. Geben Sie dazu in Ihrem Code einen Verzeichnispfad an:

```csharp
// Ausgabeverzeichnis
string outputDir = "Your Output Directory"; // Aktualisieren Sie mit dem gewünschten Pfad
```

 Ersetzen`"Your Output Directory"` durch den tatsächlichen Pfad, in dem Sie Ihre Datei speichern möchten.

## Schritt 2: Instanziieren eines Arbeitsmappenobjekts

 Als nächstes müssen Sie eine neue Instanz des`Workbook` Klasse. Dieses Objekt stellt Ihre Excel-Datei dar und ermöglicht Ihnen, deren Inhalt zu bearbeiten.

```csharp
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
```

Diese Codezeile initialisiert eine neue Arbeitsmappe, die eine leere Leinwand für unser Arbeitsblatt und Diagramm bereitstellt.

## Schritt 3: Zugriff auf das Arbeitsblatt

 Nachdem Sie die Arbeitsmappe erstellt haben, können Sie auf das Standardarbeitsblatt zugreifen. Arbeitsblätter in Aspose.Cells sind indiziert. Wenn Sie also das erste Arbeitsblatt möchten, verweisen Sie über den Index darauf.`0`.

```csharp
// Abrufen der Referenz des neu hinzugefügten Arbeitsblatts durch Übergeben seines Blattindex
Worksheet worksheet = workbook.Worksheets[0];
```

## Schritt 4: Füllen Sie das Arbeitsblatt mit Beispieldaten

Fügen wir den Arbeitsblattzellen einige Beispielwerte hinzu, die als Daten für unser Diagramm dienen. Dies ist wichtig, da das Diagramm auf diese Daten verweist.

```csharp
// Hinzufügen von Beispielwerten zu Zellen
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(60);
worksheet.Cells["B2"].PutValue(32);
worksheet.Cells["B3"].PutValue(50);
```

Hier geben wir mehrere numerische Werte in bestimmte Zellen ein. Die Spalten „A“ und „B“ enthalten die Datenpunkte, die wir visualisieren werden.

## Schritt 5: Dem Arbeitsblatt ein Diagramm hinzufügen

Nachdem wir unsere Daten haben, ist es an der Zeit, ein Diagramm zu erstellen. Wir fügen ein Säulendiagramm hinzu, das unseren Datensatz visualisiert.

```csharp
// Hinzufügen eines Diagramms zum Arbeitsblatt
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 25, 10);
```

In diesem Code geben wir den Diagrammtyp (in diesem Fall ein Säulendiagramm) und die Position an, an der wir es platzieren möchten.

## Schritt 6: Zugriff auf die Diagramminstanz

 Sobald wir das Diagramm erstellt haben, müssen wir auf seine Instanz zugreifen, um seine Eigenschaften zu ändern. Dies geschieht, indem wir es über den`Charts`Sammlung.

```csharp
// Zugriff auf die Instanz des neu hinzugefügten Diagramms
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

## Schritt 7: Datenreihen zum Diagramm hinzufügen

Jetzt müssen wir unsere Daten an das Diagramm binden. Dazu müssen wir die Zellen als Datenquelle für das Diagramm angeben.

```csharp
// Hinzufügen einer SeriesCollection (Diagrammdatenquelle) zum Diagramm im Bereich von Zelle „A1“ bis Zelle „B3“
chart.NSeries.Add("A1:B3", true);
```

In diesem Schritt teilen wir dem Diagramm mit, welchen Datenbereich es visualisieren soll.

## Schritt 8: Anpassen des Diagrammaussehens

Lassen Sie uns unser Diagramm ein wenig aufpeppen, indem wir die Farben des Plotbereichs, des Diagrammbereichs und der Seriensammlungen ändern. Dadurch fällt unser Diagramm besser auf und wird optisch ansprechender.

```csharp
// Festlegen der Vordergrundfarbe des Plotbereichs
chart.PlotArea.Area.ForegroundColor = Color.Blue;

// Festlegen der Vordergrundfarbe des Diagrammbereichs
chart.ChartArea.Area.ForegroundColor = Color.Yellow;

// Festlegen der Vordergrundfarbe des 1. SeriesCollection-Bereichs
chart.NSeries[0].Area.ForegroundColor = Color.Red;

// Festlegen der Vordergrundfarbe für den Bereich des 1. SeriesCollection-Punkts
chart.NSeries[0].Points[0].Area.ForegroundColor = Color.Cyan;

// Füllen des Bereichs der 2. Serienkollektion mit einem Farbverlauf
chart.NSeries[1].Area.FillFormat.SetOneColorGradient(Color.Lime, 1, Aspose.Cells.Drawing.GradientStyleType.Horizontal, 1);
```

In diesem Code legen wir verschiedene Farben für verschiedene Teile des Diagramms fest. Durch Anpassen des Erscheinungsbilds können Sie Ihre Daten viel ansprechender gestalten!

## Schritt 9: Hauptfarben der Gitternetzlinien ändern

Kommen wir nun zum Hauptereignis! Um die Lesbarkeit zu verbessern, ändern wir die Farbe der Hauptgitternetzlinien entlang beider Achsen unseres Diagramms.

```csharp
// Festlegen der Farbe der Hauptgitterlinien der Kategorieachse auf Silber
chart.CategoryAxis.MajorGridLines.Color = Color.Silver;

// Festlegen der Farbe der Hauptgitterlinien der Werteachse auf Rot
chart.ValueAxis.MajorGridLines.Color = Color.Red;
```

Diese Befehle setzen die Hauptgitternetzlinien für die Kategorie- und Werteachsen auf Silber bzw. Rot. Diese Unterscheidung stellt sicher, dass Ihre Betrachter den Gitternetzlinien im Diagramm problemlos folgen können.

## Schritt 10: Speichern der Arbeitsmappe

Nachdem Sie alle Änderungen vorgenommen haben, ist es an der Zeit, die Arbeitsmappe zu speichern. Dies ist der letzte Schritt, der Ihre Bemühungen zum Erfolg führt.

```csharp
// Speichern der Excel-Datei
workbook.Save(outputDir + "outputChangingMajorGridlinesInChart.xlsx");
```

Diese Zeile speichert Ihre neu erstellte Excel-Datei unter einem Namen, der ihren Zweck widerspiegelt, im angegebenen Ausgabeverzeichnis.

## Schritt 11: Bestätigungsnachricht

Fügen wir abschließend eine Nachricht hinzu, um zu bestätigen, dass unsere Aufgabe erfolgreich war:

```csharp
Console.WriteLine("Changing Major Gridlines in Chart executed successfully.");
```

Diese einfache Konsolenausgabe informiert Sie darüber, dass Ihr Programm ohne Probleme ordnungsgemäß ausgeführt wurde.

## Abschluss

Und da haben Sie es! Sie haben erfolgreich gelernt, wie Sie die Hauptgitternetzlinien in einem Diagramm mit Aspose.Cells für .NET ändern. Indem Sie dieser Schritt-für-Schritt-Anleitung folgen, haben Sie Excel-Dateien nicht nur programmgesteuert bearbeitet, sondern auch ihre visuelle Attraktivität durch Farbanpassungen verbessert. Experimentieren Sie ruhig weiter mit Aspose.Cells, um Ihre Fähigkeiten zur Datenpräsentation zu vertiefen und Ihre Diagramme noch dynamischer zu gestalten!

## Häufig gestellte Fragen

### Was ist Aspose.Cells?  
Aspose.Cells ist eine .NET-Bibliothek zum programmgesteuerten Erstellen, Bearbeiten und Verwalten von Excel-Dateien.

### Kann ich Aspose.Cells kostenlos testen?  
 Ja, Sie können sich für eine kostenlose Testversion anmelden[Hier](https://releases.aspose.com/).

### Wie kann ich mit Aspose.Cells andere Elemente in einem Diagramm ändern?  
 Sie können verschiedene Diagrammeigenschaften auf ähnliche Weise anpassen, indem Sie auf Diagrammelemente über das`Chart` Klasse, wie Titel, Legenden und Datenbeschriftungen.

### Welche Dateiformate unterstützt Aspose.Cells?  
Aspose.Cells unterstützt mehrere Dateiformate, darunter XLSX, XLS, CSV und andere.

### Wo finde ich Dokumentation für Aspose.Cells?  
 Eine ausführliche Dokumentation finden Sie unter[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
