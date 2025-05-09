---
"description": "Erfahren Sie, wie Sie die von MS Excel gewählte Farbe mit Aspose.Cells für .NET berechnen. Folgen Sie dieser Schritt-für-Schritt-Anleitung, um programmgesteuert auf die bedingte Formatierungsfarbe von Excel zuzugreifen."
"linktitle": "Berechnen Sie die von MS Excel gewählte Farbe programmgesteuert"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Berechnen Sie die von MS Excel gewählte Farbe programmgesteuert"
"url": "/de/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Berechnen Sie die von MS Excel gewählte Farbe programmgesteuert

## Einführung
Haben Sie schon einmal mit Excel-Dateien gearbeitet und sich gefragt, wie bestimmte Farben automatisch für die Formatierung ausgewählt werden? Damit sind Sie nicht allein. Die bedingte Formatierung von Excel kann ein kleines Rätsel sein, insbesondere wenn Sie versuchen, die exakte Farbe zu ermitteln, die Excel zuweist. Aber keine Sorge, wir haben das Problem! In diesem Tutorial erfahren Sie ausführlich, wie Sie die von MS Excel gewählte Farbe mit Aspose.Cells für .NET programmgesteuert berechnen. Wir erklären es Schritt für Schritt, damit Sie es problemlos nachvollziehen und in Ihren eigenen Projekten anwenden können. Los geht's!
## Voraussetzungen
Bevor wir uns in den Code vertiefen, wollen wir besprechen, was Sie benötigen, um diesem Tutorial folgen zu können:
- Aspose.Cells für .NET installiert. Falls Sie es noch nicht haben, können Sie [Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
- Praktische Kenntnisse in C# und .NET Framework.
- Eine Beispiel-Excel-Datei (Book1.xlsx) mit angewendeter bedingter Formatierung.
Sie können auch die kostenlose Testversion von Aspose.Cells für .NET ausprobieren, wenn Sie noch keine Lizenz besitzen. Holen Sie sich die Testversion [Hier](https://releases.aspose.com/).
## Pakete importieren
Bevor wir mit dem Programmieren beginnen, müssen wir die notwendigen Pakete importieren, um einen reibungslosen Ablauf zu gewährleisten. Stellen Sie sicher, dass Sie die folgenden Namespaces in Ihr Projekt einbinden:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Diese Importe bieten Zugriff auf die wichtigsten Aspose.Cells-Klassen und die native Systemzeichnungsbibliothek von .NET zur Farbverarbeitung.

Nachdem wir nun alles vorbereitet haben, können wir diese Aufgabe in überschaubare Schritte unterteilen:
## Schritt 1: Einrichten des Arbeitsmappenobjekts
Als erstes müssen wir eine `Workbook` Objekt und laden Sie die Excel-Datei, mit der wir arbeiten möchten. Hier beginnt die Reise!
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
// Instanziieren Sie ein Arbeitsmappenobjekt und öffnen Sie die Vorlagendatei
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
In diesem Schritt erstellen wir eine neue Instanz des `Workbook` Klasse von Aspose.Cells. Die `Workbook` Die Klasse stellt eine Excel-Datei dar. Indem wir den Pfad zu unserer Datei angeben, können wir sie problemlos zur weiteren Bearbeitung laden.
## Schritt 2: Zugriff auf das erste Arbeitsblatt
Sobald die Arbeitsmappe geladen ist, müssen wir auf das Arbeitsblatt zugreifen, aus dem wir die Farbe extrahieren möchten. In diesem Beispiel arbeiten wir mit dem ersten Blatt.
```csharp
// Holen Sie sich das erste Arbeitsblatt
Worksheet worksheet = workbook.Worksheets[0];
```
Hier holen wir das erste Arbeitsblatt in der Arbeitsmappe mit dem `Worksheets[0]` Index. Mit Aspose.Cells können Sie über den Index oder Namen auf jedes Arbeitsblatt in der Excel-Datei zugreifen.
## Schritt 3: Wählen Sie die gewünschte Zelle aus
Als Nächstes wählen wir eine bestimmte Zelle im Arbeitsblatt aus. In diesem Tutorial konzentrieren wir uns auf Zelle „A1“, Sie können jedoch jede Zelle mit angewendeter bedingter Formatierung auswählen.
```csharp
// Holen Sie sich die A1-Zelle
Cell a1 = worksheet.Cells["A1"];
```
Wir verwenden die `Cells` Eigenschaft, um eine bestimmte Zelle über ihre Adresse zu referenzieren. In diesem Fall wählen wir Zelle „A1“ aus, da wir die auf diese Zelle angewendeten Ergebnisse der bedingten Formatierung extrahieren möchten.
## Schritt 4: Abrufen des Ergebnisses der bedingten Formatierung
Und jetzt kommt der Zauber! Wir verwenden Aspose.Cells, um das Ergebnis der bedingten Formatierung für die ausgewählte Zelle abzurufen. So berechnet Excel die Formatierung dynamisch, einschließlich der Farben.
```csharp
// Holen Sie sich das Ergebnisobjekt der bedingten Formatierung
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
Der `GetConditionalFormattingResult()` Die Methode ist in diesem Schritt entscheidend. Sie gibt ein Objekt zurück, das die Ergebnisse der auf die Zelle angewendeten bedingten Formatierung enthält. Hier beginnen wir, die von Excel verwendeten Farbinformationen abzurufen.
## Schritt 5: Zugriff auf das ColorScaleResult
Sobald wir das Ergebnis der bedingten Formatierung haben, können wir tiefer graben und auf die Farbskala zugreifen, die Excel für diese bestimmte Zelle verwendet hat.
```csharp
// Holen Sie sich das resultierende Farbobjekt von ColorScale
Color c = cfr1.ColorScaleResult;
```
Bedingte Formatierung in Excel basiert häufig auf Farbskalen. Diese Zeile ermöglicht es uns, die resultierende Farbe zu extrahieren, die basierend auf den Regeln der bedingten Formatierung angewendet wurde.
## Schritt 6: Ausgabe der Farbinformationen
Abschließend möchten wir die in Excel angewendete Farbe sehen. Drucken wir die Farbdetails in einem leicht verständlichen Format aus, einschließlich des ARGB-Werts und des Namens.
```csharp
// Lesen Sie die Farbe
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
Der `ToArgb()` Methode gibt uns die Farbe im ARGB-Format (Alpha, Rot, Grün, Blau), während die `Name` Die Eigenschaft gibt den Farbnamen in einem besser lesbaren Format an. Sie können diese Farbdetails verwenden, um sie in anderen Anwendungen abzugleichen oder Ihre Excel-Dateien programmgesteuert zu ändern.

## Abschluss
Und da haben Sie es! Mit diesen Schritten haben Sie gelernt, wie Sie die von MS Excel gewählte Farbe mit Aspose.Cells für .NET programmgesteuert berechnen. Dieser Ansatz ist äußerst nützlich für die Automatisierung von Excel-basierten Aufgaben, insbesondere bei komplexer bedingter Formatierung. Wenn Sie das nächste Mal in Excel auf eine mysteriöse Farbe stoßen, wissen Sie genau, wie Sie ihre Geheimnisse lüften können.
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells programmgesteuert eine bedingte Formatierung anwenden?
Ja, mit Aspose.Cells können Sie bedingte Formatierungen in Excel-Dateien programmgesteuert anwenden, ändern und sogar entfernen.
### Unterstützt Aspose.Cells alle Excel-Versionen?
Absolut! Aspose.Cells unterstützt Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) und weitere Formate, darunter PDF, HTML und CSV.
### Ist Aspose.Cells für andere Plattformen als .NET verfügbar?
Ja, Aspose.Cells ist für verschiedene Plattformen verfügbar, darunter Java, C++ und Android über Java.
### Wie kann ich eine kostenlose Testversion von Aspose.Cells erhalten?
Sie können eine kostenlose Testversion von Aspose.Cells für .NET herunterladen von [Hier](https://releases.aspose.com/).
### Wie verarbeite ich große Excel-Dateien mit Aspose.Cells?
Aspose.Cells ist auf Leistung optimiert, auch bei großen Dateien. Nutzen Sie Streaming-APIs, um große Datenmengen effizient zu verarbeiten.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}