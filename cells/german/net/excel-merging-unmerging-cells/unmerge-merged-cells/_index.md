---
"description": "Mit Aspose.Cells für .NET können Sie zusammengeführte Zellen in Excel ganz einfach trennen. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um bessere Tabellen zu erstellen."
"linktitle": "Zusammengeführte Zellen in Excel aufheben"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Zusammengeführte Zellen in Excel aufheben"
"url": "/de/net/excel-merging-unmerging-cells/unmerge-merged-cells/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zusammengeführte Zellen in Excel aufheben

## Einführung

Haben Sie es satt, sich mit verbundenen Zellen in Ihren Excel-Tabellen herumzuschlagen? Damit sind Sie nicht allein! Verbundene Zellen können zwar eine praktische Funktion für die Formatierung sein, verursachen aber oft Kopfschmerzen bei der Datenbearbeitung und -analyse. Aber wissen Sie was? Das Auflösen dieser lästigen Zellen ist einfacher als Sie denken – insbesondere mit Aspose.Cells für .NET. In diesem Artikel erkläre ich Ihnen Schritt für Schritt, wie Sie verbundene Zellen auflösen, damit Ihre Daten sauber, aufgeräumt und einsatzbereit sind! Also, schnappen Sie sich Ihren Programmierhut und tauchen Sie ein in die Welt von Aspose.Cells.

## Voraussetzungen

Bevor wir uns die Hände schmutzig machen, müssen Sie einige grundlegende Dinge bereithalten:

### Grundkenntnisse in C# und .NET Framework
Wenn Sie mit der C#-Programmierung vertraut sind und über Grundkenntnisse des .NET-Frameworks verfügen, haben Sie bereits einen guten Start. Falls nicht, kein Problem! Dieses Tutorial ist unkompliziert gestaltet, sodass Sie die notwendigen Konzepte im Laufe der Zeit erlernen.

### Aspose.Cells-Bibliothek
Stellen Sie sicher, dass die Aspose.Cells-Bibliothek in Ihrer .NET-Umgebung installiert ist. Sie können diese ganz einfach über die [Aspose.Cells Download-Seite](https://releases.aspose.com/cells/net/).

### IDE-Einrichtung
Sie sollten eine Entwicklungsumgebung wie Visual Studio eingerichtet haben, in der Sie Ihren C#-Code schreiben und ausführen können.

### Beispiel-Excel-Datei
Nehmen Sie eine Excel-Beispieldatei mit einigen verbundenen Zellen. Mit dieser Datei üben Sie das Aufheben der Zellzusammenführung.

Nachdem alle diese Voraussetzungen erfüllt sind, können wir uns nun dem spannenden Teil widmen – der Codierung unserer Lösung!

## Pakete importieren

Zunächst importieren wir die notwendigen Pakete. Mit Aspose.Cells interagieren Sie mit verschiedenen Klassen, um Ihre Excel-Dateien effektiv zu verwalten. Folgendes müssen Sie am Anfang Ihrer C#-Datei einfügen:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Durch die Einbindung dieses Pakets haben Sie Zugriff auf alle von Aspose.Cells angebotenen Funktionen.

Wir unterteilen den Aufhebungsprozess in überschaubare Schritte. Jeder Schritt ist klar definiert, sodass Sie ihn problemlos nachvollziehen können.

## Schritt 1: Verzeichnisse definieren

Der erste Schritt besteht darin, die Verzeichnisse zu definieren, in denen sich Ihre Excel-Eingabedatei (die mit den zusammengeführten Zellen) und Ihre Ausgabedatei (die mit den nicht zusammengeführten Daten) befinden. So richten Sie das ein:

```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory"; 

// Ausgabeverzeichnis
string outputDir = "Your Document Directory"; 
```

Stellen Sie sicher, dass Sie `"Your Document Directory"` durch den tatsächlichen Pfad zu Ihren Dateien.

## Schritt 2: Erstellen einer Arbeitsmappe

Nachdem Sie die Verzeichnisse festgelegt haben, erstellen Sie ein Workbook-Objekt. Mit diesem Objekt können Sie die Excel-Datei bearbeiten. Verwenden Sie dazu den folgenden Code:

```csharp
// Erstellen einer Arbeitsmappe
Workbook wbk = new Aspose.Cells.Workbook(sourceDir + "sampleUnMergingtheMergedCells.xlsx");
```

Diese Codezeile liest Ihre Excel-Beispieldatei und bereitet sie für die Verarbeitung vor. 

## Schritt 3: Zugriff auf das Arbeitsblatt

Jede Arbeitsmappe besteht aus Blättern. Sie müssen auf das jeweilige Arbeitsblatt zugreifen, dessen Zellen Sie trennen möchten. So geht's:

```csharp
// Erstellen Sie ein Arbeitsblatt und holen Sie sich das erste Blatt
Worksheet worksheet = wbk.Worksheets[0];
```

Dieser Code greift auf das erste Arbeitsblatt zu. Befinden sich die zusammengeführten Zellen auf einem anderen Blatt, aktualisieren Sie den Index entsprechend.

## Schritt 4: Auf Zellen im Arbeitsblatt zugreifen

Als Nächstes benötigen Sie einen Verweis auf die Zellen in Ihrem Arbeitsblatt. Dies erreichen Sie mit:

```csharp
// Erstellen Sie ein Cells-Objekt, um alle Zellen abzurufen
Cells cells = worksheet.Cells;
```

Mit dieser Zeile haben Sie nun Zugriff auf alle Zellen des Arbeitsblatts und können diese nach Bedarf bearbeiten.

## Schritt 5: Zellen trennen

Jetzt kommt der entscheidende Schritt: das Aufheben der Zellenverbindung! Geben Sie den Bereich der verbundenen Zellen an, den Sie aufheben möchten. Verwenden Sie den folgenden Code:

```csharp
// Trennen Sie die Zellen
cells.UnMerge(5, 2, 2, 3);
```

In diesem Beispiel `UnMerge` Die Methode verwendet vier Parameter: den Startzeilenindex (5), den Startspaltenindex (2), die Anzahl der aufzuhebenden Zeilen (2) und die Anzahl der aufzuhebenden Spalten (3). Passen Sie diese Parameter an die jeweiligen zusammengeführten Zellen in Ihrer Excel-Datei an.

## Schritt 6: Speichern der Arbeitsmappe

Nach dem Aufheben der Zusammenführung sollten Sie Ihre Änderungen in einer neuen Excel-Datei speichern. So geht's:

```csharp
// Speichern Sie die Datei
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Diese Zeile speichert Ihre nicht zusammengeführten Daten im angegebenen Ausgabeverzeichnis. So einfach ist das!

## Schritt 7: Bestätigen Sie den Vorgang

Abschließend sollten Sie überprüfen, ob alles reibungslos gelaufen ist. Sie können eine Meldung auf der Konsole ausgeben, um zu bestätigen, dass der Vorgang erfolgreich ausgeführt wurde:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

Und da haben Sie es! Sie haben Zellen in einer Excel-Datei mit Aspose.Cells für .NET erfolgreich getrennt.

## Abschluss

Das Auflösen von Zellen mag mühsam erscheinen, insbesondere bei großen Tabellenkalkulationen. Mit Aspose.Cells für .NET ist es jedoch ein Kinderspiel! Dieses Tutorial führt Sie durch alles, von der Einrichtung Ihrer Umgebung bis zur Ausführung des Codes, der zum effektiven Auflösen von Zellen erforderlich ist. Die Flexibilität der Aspose.Cells-Bibliothek ermöglicht Ihnen die effiziente Verarbeitung von Tabellenkalkulationen und ist daher ideal für Entwickler, die mit Excel-Dateien arbeiten. Tauchen Sie ein und freuen Sie sich über übersichtlichere und übersichtlichere Tabellenkalkulationen.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?  
Aspose.Cells ist eine leistungsstarke Bibliothek zum Erstellen, Bearbeiten und Konvertieren von Excel-Dokumenten in .NET-Anwendungen.

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?  
Aspose.Cells bietet zwar eine kostenlose Testversion an, für die volle Nutzung ist jedoch eine Lizenz erforderlich. Sie erhalten eine [vorläufige Lizenz hier](https://purchase.aspose.com/temporary-license/).

### Kann ich Zellen in mehreren Blättern gleichzeitig trennen?  
Ja, Sie können mehrere Arbeitsblätter innerhalb einer Arbeitsmappe durchlaufen und Zellen nach Bedarf trennen.

### Ist Aspose.Cells mit .NET Core kompatibel?  
Ja, Aspose.Cells ist mit .NET Core kompatibel und daher vielseitig für verschiedene .NET-Anwendungen einsetzbar.

### Wo finde ich weitere Dokumentation zu Aspose.Cells?  
Die vollständige Dokumentation finden Sie auf der [Aspose.Cells Referenzseite](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}