---
"description": "Erstellen Sie mit Aspose.Cells für .NET ein PDF mit Ihrem Excel-Diagramm. Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie es geht."
"linktitle": "Erstellen Sie ein Diagramm-PDF mit der gewünschten Seitengröße"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Erstellen Sie ein Diagramm-PDF mit der gewünschten Seitengröße"
"url": "/de/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen Sie ein Diagramm-PDF mit der gewünschten Seitengröße

## Einführung

Die Erstellung optisch ansprechender und informativer Diagramme ist für die Datendarstellung in verschiedenen Bereichen unerlässlich. Ob Verkaufsdaten, Leistungskennzahlen oder andere Informationen – die Erstellung hochwertiger Diagramme verleiht Ihren Erkenntnissen Tiefe und Klarheit. Für die Arbeit mit .NET-Anwendungen ist Aspose.Cells eine leistungsstarke Bibliothek, die die Bearbeitung von Excel-Dokumenten und die Erstellung von Diagrammen zum Kinderspiel macht. In diesem Tutorial führen wir Sie durch die Erstellung eines PDF-Diagramms aus einer Excel-Datei mit der gewünschten Seitengröße.

## Voraussetzungen

Bevor Sie sich in den Code vertiefen, müssen Sie einige Voraussetzungen erfüllen, um ein reibungsloses Erlebnis zu gewährleisten:

### Grundkenntnisse in C# und .NET

Sie benötigen grundlegende Kenntnisse der C#-Programmierung und des .NET-Frameworks. Dies hilft Ihnen, die Struktur des Codes zu verstehen, den Sie in diesem Handbuch kennenlernen werden.

### Aspose.Cells für .NET

Stellen Sie sicher, dass Sie Aspose.Cells für .NET installiert haben. Alle Details finden Sie auf der [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/). 

### Entwicklungsumgebung

Richten Sie Ihre Entwicklungsumgebung ein. Dies kann Visual Studio oder eine andere IDE sein, die C# unterstützt. Laden Sie die Aspose.Cells-Bibliothek herunter und installieren Sie sie von [Download-Seite](https://releases.aspose.com/cells/net/).

### Beispiel-Excel-Datei

Sie benötigen eine Excel-Beispieldatei mit mindestens einem Diagramm. Sie können eine Beispieldatei erstellen oder herunterladen, um sie in diesem Tutorial zu verwenden.

## Pakete importieren

Um mit Aspose.Cells arbeiten zu können, müssen Sie die erforderlichen Namespaces in Ihre C#-Anwendung importieren. So geht's:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Über diese Namespaces erhalten Sie Zugriff auf die Klassen und Methoden, die zum Bearbeiten von Excel-Arbeitsmappen und deren Inhalten erforderlich sind.

Nachdem wir nun alle Voraussetzungen geklärt haben, wollen wir den Prozess in detaillierte Schritte unterteilen.

## Schritt 1: Ausgabe- und Quellverzeichnisse einrichten

Zu Beginn müssen Sie definieren, wo das Ausgabe-PDF gespeichert wird und wo sich Ihr Excel-Quelldokument befindet.

```csharp
//Ausgabeverzeichnis
string outputDir = "Your Output Directory";

//Quellverzeichnis
string sourceDir = "Your Document Directory";
```

Ersetzen Sie „Ihr Ausgabeverzeichnis“ und „Ihr Dokumentverzeichnis“ durch die tatsächlichen Pfade auf Ihrem System. Dies bestimmt, wo Aspose das generierte PDF speichert und wo die Excel-Datei gefunden wird.

## Schritt 2: Laden Sie die Excel-Beispieldatei

Als Nächstes müssen Sie die Excel-Datei mit dem Diagramm laden. So geht's:

```csharp
//Laden Sie eine Excel-Beispieldatei mit dem Diagramm.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

Der `Workbook` Die Klasse ist für die Interaktion mit Ihrem Excel-Dokument von zentraler Bedeutung. Stellen Sie sicher, dass der Pfad korrekt auf Ihre Excel-Datei verweist. Ein Fehler hier verhindert die Ausführung des restlichen Codes.

## Schritt 3: Zugriff auf das erste Arbeitsblatt

Sobald die Arbeitsmappe geladen ist, besteht der nächste Schritt darin, auf das Arbeitsblatt zuzugreifen, das das gewünschte Diagramm enthält.

```csharp
//Greifen Sie auf das erste Arbeitsblatt zu.
Worksheet ws = wb.Worksheets[0];
```

In Aspose.Cells werden Arbeitsblätter beginnend bei Null indiziert, also `Worksheets[0]` bezieht sich auf das erste Blatt.

## Schritt 4: Zugriff auf das erste Diagramm

Greifen wir nun auf das Diagramm zu, das Sie als PDF exportieren möchten. Dieser Schritt setzt voraus, dass Ihr Arbeitsblatt mindestens ein Diagramm enthält.

```csharp
//Greifen Sie auf das erste Diagramm im Arbeitsblatt zu.
Chart ch = ws.Charts[0];
```

Auch hier wird auf das erste Diagramm im Arbeitsblatt zugegriffen. Stellen Sie sicher, dass die Struktur Ihres Arbeitsblatts zu diesem Ansatz passt.

## Schritt 5: PDF mit der gewünschten Seitengröße erstellen

Abschließend erstellen wir aus dem Diagramm eine PDF-Datei mit der angegebenen Seitengröße. Hier ist die magische Codezeile, die das erledigt:

```csharp
//Erstellen Sie ein Diagramm-PDF mit der gewünschten Seitengröße.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

In diesem Code:
- Das PDF wird in dem zuvor angegebenen Ausgabeverzeichnis gespeichert.
- Die Zahlen `7, 7` stellen jeweils die Breite und Höhe der gewünschten Seitengröße dar.
- PageLayoutAlignmentType.Center stellt sicher, dass das Diagramm auf der Seite zentriert ist.

## Schritt 6: Bestätigungsnachricht

Um sich selbst (und andere) darüber zu informieren, dass alles reibungslos gelaufen ist, fügen Sie am Ende Ihres Codes eine Bestätigungsnachricht ein:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Diese Meldung wird nach Abschluss des Vorgangs im Konsolenfenster angezeigt und signalisiert, dass Ihr PDF ohne Probleme erstellt wurde.

## Abschluss

Herzlichen Glückwunsch! Sie haben gelernt, wie Sie mit Aspose.Cells für .NET ein PDF aus einem Diagramm in einer Excel-Datei erstellen. Diese leistungsstarke Bibliothek vereinfacht die Bearbeitung von Excel-Dokumenten und die Erstellung visueller Datendarstellungen und erspart Ihnen so stundenlange manuelle Formatierung. Entdecken Sie auch die zahlreichen weiteren Funktionen von Aspose.Cells, die über die reine PDF-Erstellung hinausgehen – wer weiß, was Ihre Projekte noch weiter verbessern könnte!

## Häufig gestellte Fragen

### Wofür wird Aspose.Cells für .NET verwendet?  
Aspose.Cells für .NET wird zum programmgesteuerten Erstellen, Bearbeiten und Konvertieren von Excel-Dokumenten in .NET-Anwendungen verwendet.

### Kann ich Aspose.Cells kostenlos nutzen?  
Ja, Aspose.Cells bietet eine [kostenlose Testversion](https://releases.aspose.com/) zu Auswertungszwecken.

### Gibt es eine Möglichkeit, meine Testphase über den Anfangszeitraum hinaus zu verlängern?  
Sie können sich bewerben für [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) für erweiterte Tests.

### Was ist, wenn ich auf Probleme stoße oder Fragen habe?  
Sie können Hilfe von der Aspose-Community auf deren [Support-Forum](https://forum.aspose.com/c/cells/9).

### Wie kann ich Aspose.Cells kaufen?  
Sie können Aspose.Cells kaufen von der [Kaufseite](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}