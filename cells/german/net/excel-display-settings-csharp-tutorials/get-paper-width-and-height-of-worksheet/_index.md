---
title: Papierbreite und -höhe des Arbeitsblatts ermitteln
linktitle: Papierbreite und -höhe des Arbeitsblatts ermitteln
second_title: Aspose.Cells für .NET API-Referenz
description: Erfahren Sie mit einer einfachen Schritt-für-Schritt-Anleitung, wie Sie die Papierbreite und -höhe von Arbeitsblättern in Aspose.Cells für .NET ermitteln.
weight: 80
url: /de/net/excel-display-settings-csharp-tutorials/get-paper-width-and-height-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Papierbreite und -höhe des Arbeitsblatts ermitteln

## Einführung

Haben Sie schon einmal versucht, eine Excel-Tabelle zu drucken und sich mit den verwirrenden Abmessungen verschiedener Papierformate herumgeschlagen? Wenn Sie wie ich sind, wissen Sie, dass nichts Ihren Tag mehr verderben kann als ein Layout, das nicht richtig herauskommt! Egal, ob Sie Berichte, Rechnungen oder nur eine einfache Liste drucken, wenn Sie wissen, wie Sie die Papierabmessungen programmgesteuert anpassen, können Sie sich eine Menge Ärger ersparen. Heute tauchen wir in die Welt von Aspose.Cells für .NET ein, um zu untersuchen, wie Sie Papierformate direkt in Ihrer Anwendung abrufen und festlegen können. Krempeln wir die Ärmel hoch und gehen wir in die Details der Verwaltung dieser Papierabmessungen!

## Voraussetzungen 

Bevor wir uns in die Programmiermagie stürzen, wollen wir erst einmal zusammentragen, was Sie für den Anfang brauchen:

1. Grundlegende Kenntnisse in C#: Sie sollten über grundlegende Kenntnisse in C# verfügen. Wenn Sie neu in der Programmierung sind, machen Sie sich keine Sorgen! Wir halten es unkompliziert.
2.  Aspose.Cells-Bibliothek: Stellen Sie sicher, dass die Aspose.Cells-Bibliothek für .NET auf Ihrem Computer installiert ist. Sie können sie hier herunterladen:[dieser Link](https://releases.aspose.com/cells/net/).
3. .NET-Entwicklungsumgebung: Richten Sie Visual Studio oder eine beliebige IDE Ihrer Wahl ein, um Ihren C#-Code zu schreiben und auszuführen. Wenn Sie nicht sicher sind, wo Sie anfangen sollen, ist Visual Studio Community Edition eine gute Wahl.
4.  Referenzen und Dokumentation: Machen Sie sich mit der Aspose.Cells-Dokumentation vertraut, um tiefere Einblicke zu erhalten. Sie finden sie[Hier](https://reference.aspose.com/cells/net/).
5. Grundlegende Kenntnisse zu Excel-Dateien: Das Verständnis der Struktur von Excel-Dateien (Arbeitsblätter, Zeilen und Spalten) ist für Sie von großem Nutzen.

Großartig! Nachdem wir nun das Wesentliche abgehakt haben, können wir direkt mit dem Importieren der erforderlichen Pakete beginnen.

## Pakete importieren

 Um uns das Leben zu erleichtern und die volle Leistungsfähigkeit von Aspose.Cells zu nutzen, müssen wir einige Pakete importieren. Das geht ganz einfach, indem wir ein`using` Anweisung oben in Ihrer Codedatei. Folgendes müssen Sie importieren:

```csharp
using System;
using System.IO;
```

Mit dieser Zeile können wir auf alle Klassen und Methoden in der Aspose.Cells-Bibliothek zugreifen, was die Bearbeitung von Excel-Dateien erleichtert. Beginnen wir nun mit unserer Schritt-für-Schritt-Anleitung zum Abrufen der Papierbreite und -höhe für verschiedene Papiergrößen.

## Schritt 1: Erstellen Sie eine neue Arbeitsmappe

Der erste Schritt bei der Arbeit mit Aspose.Cells besteht darin, eine neue Arbeitsmappe zu erstellen. Stellen Sie sich eine Arbeitsmappe als leere Leinwand vor, auf der Sie Arbeitsblätter und Zellen hinzufügen und in unserem Fall Papiergrößen definieren können.

```csharp
//Arbeitsmappe erstellen
Workbook wb = new Workbook();
```

Diese Zeile instanziiert ein neues Arbeitsmappenobjekt, das wir bearbeiten können. Sie werden noch nichts sehen, aber unsere Leinwand ist fertig!

## Schritt 2: Zugriff auf das erste Arbeitsblatt

Da wir nun unsere Arbeitsmappe haben, müssen wir auf ein bestimmtes Arbeitsblatt darin zugreifen. Ein Arbeitsblatt ist wie eine einzelne Seite in Ihrer Arbeitsmappe und dort findet die ganze Aktion statt.

```csharp
//Greifen Sie auf das erste Arbeitsblatt zu
Worksheet ws = wb.Worksheets[0];
```

Hier nehmen wir das erste Arbeitsblatt (Index 0) aus unserer Arbeitsmappe. Sie können es sich so vorstellen, als würden Sie die erste Seite eines Buches aufschlagen. 

## Schritt 3: Papiergröße festlegen und Abmessungen ermitteln

Jetzt kommt der spannende Teil! Wir legen verschiedene Papiergrößen fest und rufen ihre Abmessungen nacheinander ab. Dieser Schritt ist entscheidend, da er uns zeigt, wie sich unterschiedliche Größen auf das Layout auswirken.

```csharp
//Stellen Sie das Papierformat auf A2 ein und drucken Sie Papierbreite und -höhe in Zoll
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

 In diesem Block stellen wir die Papiergröße auf A2 ein und ermitteln dann die Breite und Höhe.`PaperWidth` Und`PaperHeight` Eigenschaften geben die Abmessungen in Zoll an. Das ist, als ob man die Größe eines Rahmens prüft, bevor man ein Bild hineinsteckt.

## Schritt 4: Wiederholen Sie den Vorgang für andere Papierformate

Lassen Sie uns den Vorgang für andere gängige Papierformate wiederholen. Wir prüfen die Formate A3, A4 und Letter. Diese Wiederholung ist wichtig, um zu verstehen, wie jede Größe im Aspose.Cells-Framework definiert ist.

```csharp
//Stellen Sie das Papierformat auf A3 ein und drucken Sie Papierbreite und -höhe in Zoll
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//Stellen Sie das Papierformat auf A4 ein und drucken Sie Papierbreite und -höhe in Zoll
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//Stellen Sie das Papierformat auf „Letter“ ein und drucken Sie Papierbreite und -höhe in Zoll
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

 Jeder dieser Blöcke imitiert den vorherigen Schritt, passt aber die`PaperSize`Eigenschaft entsprechend. Durch einfaches Ändern des Größenindikators erhalten Sie mühelos unterschiedliche Papierabmessungen. Es ist, als würden Sie die Größe einer Schachtel ändern, je nachdem, was Sie aufbewahren müssen!

## Abschluss

Und da haben Sie es! Indem Sie diese Schritte befolgen, können Sie die Abmessungen verschiedener Papierformate in Aspose.Cells für .NET ganz einfach festlegen und abrufen. Diese Funktion spart Ihnen nicht nur Zeit, sondern verhindert auch Druckfehler, die aufgrund falsch konfigurierter Seiteneinstellungen auftreten können. Wenn Sie also das nächste Mal eine Excel-Tabelle drucken oder einen Bericht erstellen müssen, können Sie dies mit der Gewissheit tun, dass Sie die Abmessungen in Ihren Händen haben. 

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek zur Verarbeitung von Excel-Dateien, ohne dass Excel installiert sein muss.

### Kann ich Aspose.Cells kostenlos nutzen?
 Ja! Sie können mit einer kostenlosen Testversion beginnen, die verfügbar ist unter[dieser Link](https://releases.aspose.com/).

### Wie kann ich benutzerdefinierte Papiergrößen einstellen?
 Aspose.Cells bietet Optionen zum Festlegen benutzerdefinierter Papiergrößen mithilfe der`PageSetup` Klasse.

### Sind Programmierkenntnisse erforderlich, um Aspose.Cells zu verwenden?
Grundlegende Programmierkenntnisse sind hilfreich, Sie können aber zum leichteren Verständnis auch Tutorials durcharbeiten!

### Wo finde ich weitere Beispiele?
 Der[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) bietet eine Fülle von Beispielen und Tutorials.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
