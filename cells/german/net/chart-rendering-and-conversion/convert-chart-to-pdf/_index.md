---
"description": "Lernen Sie mit dieser einfachen Schritt-für-Schritt-Anleitung, Excel-Diagramme mit Aspose.Cells für .NET in PDF zu konvertieren. Entdecken Sie wichtige Tipps und Programmierbeispiele."
"linktitle": "Diagramm in PDF konvertieren"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Diagramm in PDF konvertieren"
"url": "/de/net/chart-rendering-and-conversion/convert-chart-to-pdf/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Diagramm in PDF konvertieren

## Einführung

Bei der Verarbeitung von Tabellenkalkulationen spielen Diagramme oft eine entscheidende Rolle für die effektive Visualisierung von Daten. Ob Sie einen Bericht erstellen, eine Präsentation halten oder einfach nur eine Datenanalyse durchführen – die Konvertierung dieser Diagramme ins PDF-Format verleiht ihnen einen professionellen Touch. Hier führen wir Sie durch die Schritte zur Konvertierung eines Excel-Diagramms ins PDF-Format mit Aspose.Cells für .NET, einer leistungsstarken Bibliothek zur Vereinfachung der Excel-Bearbeitung.

## Voraussetzungen

Bevor Sie mit dem Tutorial beginnen, müssen Sie sicherstellen, dass Sie die richtige Konfiguration haben. Folgendes benötigen Sie:

### .NET Framework
Stellen Sie sicher, dass das .NET Framework auf Ihrem Computer installiert ist. Aspose.Cells ist mit verschiedenen Versionen kompatibel, funktioniert aber in der Regel am besten mit der neuesten.

### Aspose.Cells-Bibliothek
Sie benötigen die Aspose.Cells für .NET-Bibliothek. Sie können sie herunterladen von [Hier](https://releases.aspose.com/cells/net/)Die Bibliothek verfügt über eine umfangreiche API, die alle Funktionen enthält, die Sie für Excel-Manipulationen benötigen.

### Visual Studio
Die Installation von Visual Studio ist unbedingt erforderlich, da es sich dabei um eine hervorragende IDE zum nahtlosen Schreiben Ihres .NET-Codes handelt.

### Grundkenntnisse in C#
Wenn Sie sich mit der Programmiersprache C# auskennen, können Sie die Codesegmente besser verstehen.

## Pakete importieren

Um Aspose.Cells erfolgreich in Ihrem Projekt zu verwenden, müssen Sie die erforderlichen Pakete importieren. So geht's:

### Neues Projekt erstellen

Beginnen Sie mit der Erstellung eines neuen C#-Projekts in Visual Studio:

1. Öffnen Sie Visual Studio.
2. Klicken Sie auf „Neues Projekt erstellen“.
3. Wählen Sie je nach Bedarf „Konsolen-App (.NET Core)“ oder „Konsolen-App (.NET Framework)“ aus.
4. Geben Sie Ihrem Projekt einen Namen und klicken Sie auf „Erstellen“.

### Aspose.Cells-Referenz hinzufügen

Nachdem Sie Ihr Projekt erstellt haben, müssen Sie einen Verweis auf die Aspose.Cells-Bibliothek hinzufügen:

1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
2. Wählen Sie „NuGet-Pakete verwalten“.
3. Suchen Sie nach „Aspose.Cells“ und installieren Sie es.

Sobald Sie die Bibliothek in Ihr Projekt eingebunden haben, können Sie mit dem Code fortfahren.

### Importieren der erforderlichen Namespaces

Oben auf Ihrer `Program.cs` Fügen Sie der Datei die folgenden Namespaces hinzu:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Charts;
using System.IO;
```

So konvertieren Sie ein Excel-Diagramm systematisch in PDF. Folgen Sie den Anweisungen Schritt für Schritt!

## Schritt 1: Ausgabe- und Quellverzeichnisse einrichten

Um mit Ihrem Code zu beginnen, müssen Sie zunächst angeben, wo Sie Ihre Ausgabe speichern und wo sich Ihr Quelldokument befindet.

```csharp
// Ausgabeverzeichnis
string outputDir = "Your Output Directory";

// Quellverzeichnis
string sourceDir = "Your Document Directory";
```

Stellen Sie sicher, dass Sie `"Your Output Directory"` Und `"Your Document Directory"` durch den tatsächlichen Pfad, in dem sich Ihre Dateien befinden.

## Schritt 2: Laden Sie die Excel-Arbeitsmappe

Laden wir nun die Excel-Datei mit den zu konvertierenden Diagrammen. Das ist ganz einfach:

```csharp
// Excel-Datei mit Diagrammen laden
Workbook workbook = new Workbook(sourceDir + "sampleChartToPdf.xlsx");
```

Dieser Code initialisiert ein neues Arbeitsmappenobjekt und lädt die angegebene Excel-Datei. Stellen Sie sicher, dass der Dateiname mit dem Namen in Ihrem Quellverzeichnis übereinstimmt.

## Schritt 3: Zugriff auf das Arbeitsblatt

Als Nächstes müssen Sie auf das Arbeitsblatt zugreifen, das das zu konvertierende Diagramm enthält. So geht's:

```csharp
// Greifen Sie auf das erste Arbeitsblatt zu
Worksheet worksheet = workbook.Worksheets[0];
```

Dieser Code greift auf das erste Arbeitsblatt in Ihrer Arbeitsmappe zu und ermöglicht Ihnen, damit zu arbeiten.

## Schritt 4: Zugriff auf das Diagramm 

Sobald Sie das Arbeitsblatt haben, können Sie auf das spezifische Diagramm zugreifen, das Sie konvertieren möchten:

```csharp
// Greifen Sie auf das erste Diagramm im Arbeitsblatt zu
Chart chart = worksheet.Charts[0];
```

Diese Zeile greift auf das erste Diagramm im Arbeitsblatt zu. Wenn Ihr Arbeitsblatt mehrere Diagramme enthält und Sie ein bestimmtes Diagramm ansprechen müssen, passen Sie den Index entsprechend an.

## Schritt 5: Konvertieren Sie das Diagramm in PDF

Jetzt kommt der spannende Teil: die Konvertierung des Diagramms in das PDF-Format. Sie können es entweder in einer Datei oder in einem Speicherstream speichern.

### Option 1: Diagramm in Datei speichern

Um das Diagramm direkt in einer PDF-Datei zu speichern, verwenden Sie den folgenden Code:

```csharp
// Speichern Sie das Diagramm im PDF-Format
chart.ToPdf(outputDir + "outputChartToPdf.pdf");
```

Stellen Sie einfach sicher, dass das Ausgabeverzeichnis tatsächlich vorhanden ist, um Fehler zu vermeiden.

### Option 2: Diagramm im Memory Stream speichern

Wenn Sie die PDF-Datei weiter bearbeiten oder sofort in Ihrer Anwendung verwenden möchten, ist das Speichern in einem Speicherstream möglicherweise die bessere Wahl:

```csharp
// Speichern Sie das Diagramm im PDF-Format im Stream
MemoryStream ms = new MemoryStream();
chart.ToPdf(ms);
```

Dabei speichern Sie das PDF in einem Speicherstream, der je nach Bedarf Ihrer Anwendung genutzt werden kann.

## Schritt 6: Erfolgsmeldung anzeigen

Abschließend ist es immer hilfreich, den Erfolg Ihrer Operation anzuzeigen. Sie können einfach eine Erfolgsmeldung auf der Konsole ausgeben:

```csharp
Console.WriteLine("ChartToPdf executed successfully.");
```

## Abschluss

Und da haben Sie es! Mit Aspose.Cells für .NET wird die Konvertierung von Excel-Diagrammen in PDF-Formate zum Kinderspiel. Egal, ob Sie in einer Datei oder einem Speicherstream speichern, die Bibliothek verspricht Flexibilität und Benutzerfreundlichkeit. Probieren Sie es doch einfach mal aus! Ihre Berichte werden mit professionell formatierten PDF-Diagrammen deutlich schärfer!

## Häufig gestellte Fragen

### Kann Aspose.Cells mehrere Diagramme gleichzeitig konvertieren?
Ja, Sie können die `worksheet.Charts` Sammlung, um jedes Diagramm einzeln zu konvertieren.

### Ist Aspose.Cells für große Excel-Dateien geeignet?
Absolut! Aspose.Cells ist auf Leistung optimiert und kann große Excel-Dateien effizient verarbeiten.

### Welche .NET-Versionen unterstützt Aspose.Cells?
Aspose.Cells unterstützt verschiedene Versionen von .NET, einschließlich .NET Framework und .NET Core.

### Wo finde ich eine ausführliche Dokumentation?
Besuchen Sie die [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für ausführliche Informationen und Beispiele.

### Gibt es eine kostenlose Testversion?
Ja! Sie können eine kostenlose Testversion herunterladen unter [Hier](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}