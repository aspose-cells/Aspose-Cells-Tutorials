---
title: Konvertieren eines Arbeitsblatts in SVG in .NET
linktitle: Konvertieren eines Arbeitsblatts in SVG in .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET ein Excel-Arbeitsblatt in SVG konvertieren. Perfekt für .NET-Entwickler, die Excel in SVG rendern möchten.
weight: 11
url: /de/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertieren eines Arbeitsblatts in SVG in .NET

## Einführung

Wenn Sie ein Excel-Arbeitsblatt in das SVG-Format konvertieren möchten, sind Sie hier richtig! Aspose.Cells für .NET ist ein leistungsstarkes Tool, mit dem Entwickler Excel-Dateien bearbeiten und in verschiedene Formate konvertieren können, darunter das weithin unterstützte SVG (Scalable Vector Graphics). Dieses Tutorial führt Sie Schritt für Schritt durch den Prozess der Konvertierung eines Arbeitsblatts in ein SVG in .NET, sodass selbst Anfänger problemlos folgen können.

## Voraussetzungen

Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:

1.  Aspose.Cells für .NET: Laden Sie die neueste Version von Aspose.Cells für .NET herunter und installieren Sie sie von[Aspose.Cells für .NET](https://releases.aspose.com/cells/net/).
2. .NET-Entwicklungsumgebung: Sie müssen Visual Studio oder eine andere .NET-IDE installiert haben.
3. Grundkenntnisse in C#: Kenntnisse in C# sind erforderlich, aber keine Sorge, wir erklären alles klar und deutlich.
4. Excel-Datei: Halten Sie eine Excel-Datei bereit, die Sie in das SVG-Format konvertieren möchten.

## Erforderliche Pakete importieren

Bevor Sie mit dem Codieren beginnen, achten Sie darauf, die erforderlichen Namespaces oben in Ihrer C#-Datei einzuschließen.

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

Diese Pakete sind für die Arbeit mit Aspose.Cells und die Handhabung von Rendering-Optionen wie dem SVG-Export erforderlich.

Nachdem wir nun die Grundlagen behandelt haben, gehen wir nun zu den eigentlichen Schritten der Konvertierung eines Excel-Arbeitsblatts in ein SVG-Bild über.

## Schritt 1: Legen Sie den Pfad zu Ihrem Dokumentverzeichnis fest

Als Erstes müssen wir den Pfad zum Ordner definieren, in dem sich Ihre Excel-Datei befindet. Dies ist wichtig, da Ihr Code zum Laden und Speichern von Dateien auf das Verzeichnis verweist.

```csharp
// Der Pfad zum Dokumentenverzeichnis
string dataDir = "Your Document Directory";
```

 Ersetzen Sie unbedingt`"Your Document Directory"`durch den tatsächlichen Pfad, in dem sich Ihre Excel-Datei befindet.

##  Schritt 2: Laden Sie die Excel-Datei mit`Workbook`

 Als nächstes müssen wir die Excel-Datei in eine Instanz des`Workbook` Klasse. Die`Workbook` Klasse stellt die gesamte Excel-Datei dar, einschließlich aller darin enthaltenen Arbeitsblätter.

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

 Hier,`"Template.xlsx"` ist der Name der Excel-Datei, mit der Sie arbeiten. Stellen Sie sicher, dass diese Datei im angegebenen Verzeichnis vorhanden ist, da sonst Fehler auftreten.

## Schritt 3: Bild- oder Druckoptionen für die SVG-Konvertierung festlegen

 Bevor wir das Arbeitsblatt in das SVG-Format konvertieren können, müssen wir die Bildoptionen angeben.`ImageOrPrintOptions` Klasse können Sie steuern, wie das Arbeitsblatt konvertiert wird. Insbesondere müssen wir die`SaveFormat` Zu`SVG` und stellen Sie sicher, dass jedes Arbeitsblatt in eine einzelne Seite umgewandelt wird.

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

 Der`SaveFormat.Svg` Die Option stellt sicher, dass das Ausgabeformat SVG ist, während`OnePagePerSheet` stellt sicher, dass jedes Arbeitsblatt auf einer einzelnen Seite gerendert wird.

## Schritt 4: Durchlaufen Sie jedes Arbeitsblatt in der Arbeitsmappe

Nun müssen wir alle Arbeitsblätter in der Excel-Datei durchlaufen. Jedes Arbeitsblatt wird einzeln konvertiert.

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    // Wir werden jedes Arbeitsblatt einzeln bearbeiten
}
```

Diese Schleife stellt sicher, dass jedes Arbeitsblatt verarbeitet wird, unabhängig davon, wie viele Arbeitsblätter in Ihrer Arbeitsmappe vorhanden sind.

##  Schritt 5: Erstellen Sie eine`SheetRender` Object for Rendering

 Für jedes Arbeitsblatt erstellen wir ein`SheetRender` Objekt. Dieses Objekt ist für die Konvertierung des Arbeitsblatts in das gewünschte Bildformat verantwortlich, in diesem Fall SVG.

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

 Der`SheetRender` Das Objekt benötigt zwei Argumente: das Arbeitsblatt, das Sie konvertieren, und die Bildoptionen, die Sie zuvor definiert haben.

## Schritt 6: Konvertieren Sie das Arbeitsblatt in SVG

 Schließlich konvertieren wir innerhalb der Schleife jedes Arbeitsblatt in das SVG-Format. Wir verwenden eine verschachtelte Schleife, um durch die Seiten zu iterieren (obwohl es in diesem Fall nur eine Seite pro Arbeitsblatt gibt, dank der`OnePagePerSheet` Option).

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    // Geben Sie das Arbeitsblatt im SVG-Bildformat aus
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

Dieser Code speichert das Arbeitsblatt als SVG-Datei im selben Verzeichnis wie die Excel-Datei. Jede SVG-Datei wird entsprechend dem Arbeitsblattnamen und einer Indexnummer benannt, um Namenskonflikte zu vermeiden.

## Abschluss

Und das war’s! Sie haben ein Excel-Arbeitsblatt erfolgreich mit Aspose.Cells für .NET in das SVG-Format konvertiert. Mit diesem Vorgang können Sie das Layout und Design Ihres Arbeitsblatts beibehalten und es gleichzeitig in jedem Browser oder Gerät anzeigen, das SVG unterstützt, was so ziemlich alle sind. Egal, ob Sie mit komplexen Excel-Dateien oder nur einer einfachen Tabelle arbeiten, diese Methode stellt sicher, dass Ihre Daten in einem webfreundlichen Format schön dargestellt werden.

## Häufig gestellte Fragen

### Was ist SVG und warum sollte ich es verwenden?
SVG (Scalable Vector Graphics) ist ein webfreundliches Format, das sich ohne Qualitätsverlust unendlich skalieren lässt. Es eignet sich perfekt für Diagramme, Grafiken und Bilder, die in verschiedenen Größen angezeigt werden müssen.

### Kann Aspose.Cells große Excel-Dateien zur Konvertierung verarbeiten?
Ja, Aspose.Cells kann große Excel-Dateien effizient verarbeiten und sie ohne nennenswerte Leistungsprobleme in SVG konvertieren.

### Gibt es eine Begrenzung für die Anzahl der Arbeitsblätter, die ich in SVG konvertieren kann?
Nein, es gibt in Aspose.Cells keine inhärente Beschränkung für die Konvertierung mehrerer Arbeitsblätter. Die einzige Einschränkung wäre der Speicher und die Leistung Ihres Systems.

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
 Ja, Aspose.Cells erfordert eine Lizenz für den Produktionseinsatz. Sie können eine temporäre Lizenz erhalten[Hier](https://purchase.aspose.com/temporary-license/) oder erkunden Sie die[Kostenlose Testversion](https://releases.aspose.com/).

### Kann ich die SVG-Ausgabe anpassen?
 Ja, Sie können die`ImageOrPrintOptions` um verschiedene Aspekte der SVG-Ausgabe anzupassen, beispielsweise Auflösung und Skalierung.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
