---
title: Zusammengeführte Zellen in Excel aufheben
linktitle: Zusammengeführte Zellen in Excel aufheben
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Mit Aspose.Cells für .NET können Sie verbundene Zellen in Excel ganz einfach trennen. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um bessere Tabellen zu erstellen.
weight: 10
url: /de/net/excel-merging-unmerging-cells/unmerge-merged-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zusammengeführte Zellen in Excel aufheben

## Einführung

Sind Sie es leid, sich in Ihren Excel-Tabellen mit verbundenen Zellen herumzuschlagen? Damit sind Sie nicht allein! Verbundene Zellen können eine praktische Funktion für die Formatierung sein, aber sie können bei der Datenbearbeitung und -analyse oft zu Kopfschmerzen führen. Aber wissen Sie was? Das Aufheben dieser lästigen Zellen ist einfacher, als Sie vielleicht denken – insbesondere, wenn Sie Aspose.Cells für .NET verwenden. In diesem Artikel zeige ich Ihnen Schritt für Schritt, wie Sie verbundene Zellen aufheben, um sicherzustellen, dass Ihre Daten ordentlich, aufgeräumt und einsatzbereit sind! Also schnappen Sie sich Ihren Programmierhut und tauchen Sie ein in die Welt von Aspose.Cells.

## Voraussetzungen

Bevor wir loslegen, müssen Sie ein paar grundlegende Dinge bereitlegen:

### Grundkenntnisse in C# und .NET Framework
Wenn Sie mit der C#-Programmierung vertraut sind und ein grundlegendes Verständnis des .NET-Frameworks haben, haben Sie bereits einen guten Start. Wenn nicht, machen Sie sich keine Sorgen! Dieses Tutorial ist unkompliziert gestaltet, sodass Sie die erforderlichen Konzepte im Laufe der Zeit erlernen.

### Aspose.Cells-Bibliothek
Stellen Sie sicher, dass die Aspose.Cells-Bibliothek in Ihrer .NET-Umgebung installiert ist. Sie können diese ganz einfach herunterladen, indem Sie die[Aspose.Cells Download-Seite](https://releases.aspose.com/cells/net/).

### IDE-Einrichtung
Sie sollten eine Entwicklungsumgebung wie Visual Studio eingerichtet haben, in der Sie Ihren C#-Code schreiben und ausführen können.

### Beispiel-Excel-Datei
Holen Sie sich eine Excel-Beispieldatei, die einige verbundene Zellen enthält. Mit dieser Datei üben Sie das Aufheben der Zellzusammenführung.

Nachdem alle diese Voraussetzungen erfüllt sind, können wir nun mit dem spannenden Teil beginnen: der Codierung unserer Lösung!

## Pakete importieren

Als Erstes importieren wir die erforderlichen Pakete. Mit Aspose.Cells interagieren Sie mit verschiedenen Klassen, um Ihre Excel-Dateien effektiv zu verwalten. Folgendes müssen Sie oben in Ihre C#-Datei einfügen:

```csharp
using System;
using System.IO;

using Aspose.Cells;
```

Durch die Einbindung dieses Pakets haben Sie Zugriff auf alle von Aspose.Cells angebotenen Funktionen.

Lassen Sie uns den Aufhebungsprozess in überschaubare Schritte unterteilen. Jeder Schritt wird klar definiert, sodass Sie ihn problemlos nachvollziehen können.

## Schritt 1: Verzeichnisse definieren

Der erste Schritt besteht darin, die Verzeichnisse zu definieren, in denen sich Ihre Excel-Eingabedatei (die mit den zusammengeführten Zellen) und Ihre Ausgabedatei (die, in der die nicht zusammengeführten Daten gespeichert werden) befinden. So richten Sie das ein:

```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory"; 

// Ausgabeverzeichnis
string outputDir = "Your Document Directory"; 
```

 Ersetzen Sie unbedingt`"Your Document Directory"` durch den tatsächlichen Pfad zu Ihren Dateien.

## Schritt 2: Erstellen Sie eine Arbeitsmappe

Nachdem Sie nun die Verzeichnisse festgelegt haben, ist es an der Zeit, ein Workbook-Objekt zu erstellen. Mit diesem Objekt können Sie die Excel-Datei bearbeiten. Sie können dies mit dem folgenden Code tun:

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

Dieser Code erfasst das erste Arbeitsblatt. Wenn sich Ihre zusammengeführten Zellen auf einem anderen Blatt befinden, aktualisieren Sie den Index entsprechend.

## Schritt 4: Auf Zellen im Arbeitsblatt zugreifen

Als Nächstes müssen Sie einen Verweis auf die Zellen in Ihrem Arbeitsblatt erstellen. Dies erreichen Sie mit:

```csharp
//Erstellen Sie ein Cells-Objekt, um alle Zellen abzurufen
Cells cells = worksheet.Cells;
```

Mit dieser Zeile haben Sie nun Zugriff auf alle Zellen des Arbeitsblattes und können diese nach Bedarf bearbeiten.

## Schritt 5: Die Zellen trennen

Jetzt kommt der entscheidende Schritt: das Aufheben der Zellenverschmelzung! Sie müssen den Bereich der verbundenen Zellen angeben, den Sie aufheben möchten. Verwenden Sie den folgenden Code:

```csharp
// Die Zellen trennen
cells.UnMerge(5, 2, 2, 3);
```

 In diesem Beispiel`UnMerge` Die Methode verwendet vier Parameter: den Startzeilenindex (5), den Startspaltenindex (2), die Anzahl der aufzuhebenden Zeilen (2) und die Anzahl der aufzuhebenden Spalten (3). Passen Sie diese Parameter an die jeweiligen zusammengeführten Zellen in Ihrer Excel-Datei an.

## Schritt 6: Speichern der Arbeitsmappe

Nach dem Aufheben der Zusammenführung möchten Sie Ihre Änderungen in einer neuen Excel-Datei speichern. So geht's:

```csharp
// Speichern Sie die Datei
wbk.Save(outputDir + "outputUnMergingtheMergedCells.xlsx");
```

Diese Zeile speichert Ihre nicht zusammengeführten Daten im angegebenen Ausgabeverzeichnis. So einfach ist das!

## Schritt 7: Bestätigen Sie den Vorgang

Abschließend sollten Sie noch bestätigen, dass alles reibungslos gelaufen ist. Sie können eine Meldung auf der Konsole ausgeben, die Sie darüber informiert, dass der Vorgang erfolgreich ausgeführt wurde:

```csharp
Console.WriteLine("UnMerging the Cells executed successfully.");
```

Und da haben Sie es! Sie haben erfolgreich Zellen in einer Excel-Datei mit Aspose.Cells für .NET getrennt.

## Abschluss

Das Aufheben von Zellen kann mühsam erscheinen, insbesondere wenn Sie mit großen Tabellenkalkulationen arbeiten, aber mit Aspose.Cells für .NET ist es ein Kinderspiel! Dieses Tutorial hat Sie durch alles geführt, vom Einrichten Ihrer Umgebung bis zum Ausführen des Codes, der zum effektiven Aufheben von Zellen erforderlich ist. Die Flexibilität der Aspose.Cells-Bibliothek ermöglicht Ihnen die effiziente Verarbeitung von Tabellenkalkulationen und ist daher die ideale Wahl für Entwickler, die mit Excel-Dateien arbeiten. Tauchen Sie also ein und freuen Sie sich über übersichtlichere, besser verwaltbare Tabellenkalkulationen.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?  
Aspose.Cells ist eine leistungsstarke Bibliothek zum Erstellen, Bearbeiten und Konvertieren von Excel-Dokumenten in .NET-Anwendungen.

### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?  
 Obwohl Aspose.Cells eine kostenlose Testversion anbietet, ist für die vollständige Nutzung eine Lizenz erforderlich. Sie können eine[vorläufige Lizenz hier](https://purchase.aspose.com/temporary-license/).

### Kann ich Zellen in mehreren Blättern gleichzeitig trennen?  
Ja, Sie können mehrere Arbeitsblätter innerhalb einer Arbeitsmappe durchlaufen und Zellen nach Bedarf trennen.

### Ist Aspose.Cells mit .NET Core kompatibel?  
Ja, Aspose.Cells ist mit .NET Core kompatibel und daher vielseitig für verschiedene .NET-Anwendungen einsetzbar.

### Wo finde ich weitere Dokumentation zu Aspose.Cells?  
 Die vollständige Dokumentation finden Sie auf der[Aspose.Cells Referenzseite](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
