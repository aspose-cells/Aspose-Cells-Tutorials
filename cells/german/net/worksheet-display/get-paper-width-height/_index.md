---
title: Abrufen der Papierbreite und -höhe zum Drucken von Arbeitsblättern
linktitle: Abrufen der Papierbreite und -höhe zum Drucken von Arbeitsblättern
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie in Aspose.Cells für .NET die Papierbreite und -höhe zum Drucken von Arbeitsblättern ermitteln.
weight: 16
url: /de/net/worksheet-display/get-paper-width-height/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Abrufen der Papierbreite und -höhe zum Drucken von Arbeitsblättern

## Einführung
Um Dokumente genau drucken zu können, müssen Sie die Papiermaße kennen. Wenn Sie Entwickler sind oder an einer Anwendung arbeiten, die mit Excel-Dateien arbeitet, müssen Sie möglicherweise wissen, wie Sie beim Drucken von Arbeitsblättern die Papierbreite und -höhe ermitteln. Glücklicherweise bietet Aspose.Cells für .NET eine robuste Möglichkeit, Excel-Dokumente programmgesteuert zu verwalten. In diesem Artikel führen wir Sie durch den Prozess der Bestimmung der Papiergröße und verwenden einfache Beispiele, um grundlegende Konzepte zu veranschaulichen. 
## Voraussetzungen
Bevor wir uns in die technischen Details vertiefen, wollen wir ein paar Grundlagen schaffen. Um dieses Tutorial erfolgreich durchführen zu können, benötigen Sie:
### 1. Grundkenntnisse in C#
Sie sollten über gute Kenntnisse der C#-Programmierung verfügen, da wir in einer .NET-Umgebung arbeiten werden.
### 2. Aspose.Cells-Bibliothek
Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek in Ihrem Projekt installiert haben. Wenn Sie dies noch nicht getan haben, können Sie die neueste Version von der[Aspose.Cells-Downloadseite](https://releases.aspose.com/cells/net/).
### 3. Visual Studio IDE
Es ist von Vorteil, Visual Studio zum Ausführen und Verwalten Ihrer C#-Projekte zu haben. Jede Version, die .NET unterstützt, sollte problemlos funktionieren.
### 4. Eine gültige Aspose-Lizenz
 Obwohl Aspose.Cells getestet werden kann, sollten Sie den Kauf einer Lizenz in Betracht ziehen, wenn Sie es für langfristige Projekte verwenden. Sie können es kaufen über[dieser Link](https://purchase.aspose.com/buy) oder erkunden Sie eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) für kurze Testphasen.
Wenn Sie fertig sind, können wir mit dem Code beginnen!
## Pakete importieren
Der erste Schritt auf unserem Weg besteht darin, wichtige Namespaces zu importieren. Dies ist entscheidend, da wir dadurch auf die Klassen und Methoden zugreifen können, die wir zum Bearbeiten von Excel-Dateien verwenden werden. So geht's:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Stellen Sie sicher, dass Sie diese Zeile oben in Ihrer CS-Datei einfügen. Nachdem wir nun die Importe vorbereitet haben, können wir mit der Erstellung unserer Arbeitsmappe und dem Zugriff auf das Arbeitsblatt fortfahren.
## Schritt 1: Erstellen Sie Ihre Arbeitsmappe
Wir beginnen mit der Erstellung einer Instanz des`Workbook` Klasse. Dies bildet die Grundlage unserer Excel-Dateimanipulation.
```csharp
Workbook wb = new Workbook();
```
Diese Zeile weist das Programm an, eine neue Arbeitsmappe zu initialisieren, und bereitet uns darauf vor, in unsere Arbeitsblätter einzutauchen.
## Schritt 2: Zugriff auf das erste Arbeitsblatt
Als Nächstes greifen wir auf das erste Arbeitsblatt in unserer neu erstellten Arbeitsmappe zu. Das ist ziemlich unkompliziert:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Hier greifen wir auf das erste Blatt (mit Index 0) in unserer Arbeitsmappe zu. Hier legen wir die Papiergrößen fest.
## Papierformat festlegen und Abmessungen abrufen
Jetzt kommen wir zum Kern der Operation: dem Einstellen der Papiergröße und dem Abrufen der Abmessungen! Lassen Sie uns dies Schritt für Schritt durchgehen.
## Schritt 3: Stellen Sie das Papierformat auf A2 ein
Stellen wir zunächst unser Papierformat auf A2 ein und drucken die Abmessungen aus.
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
 Nach dieser Einrichtung verwenden wir`Console.WriteLine` um die Abmessungen anzuzeigen. Wenn Sie dies ausführen, sehen Sie die Breite und Höhe in Zoll für das Papierformat A2.
## Schritt 4: Papiergröße auf A3 einstellen
Jetzt ist es Zeit für A3! Wir wiederholen einfach den Vorgang:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Voila! Die Deklaration druckt die spezifische Höhe und Breite für A3-Papier.
## Schritt 5: Papiergröße auf A4 einstellen
Lassen Sie uns nach demselben Muster prüfen, wie A4 abschneidet:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Damit erhalten wir die Abmessungen für A4, eines der am häufigsten verwendeten Papierformate.
## Schritt 6: Papierformat auf Letter einstellen
Um unsere Untersuchung der Papiergröße abzurunden, stellen wir sie auf die Größe „Letter“ ein:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Auch hier sehen wir die spezifische Breite und Höhe für die Briefgröße.
## Abschluss
Und da haben Sie es! Sie haben gerade gelernt, wie Sie die Papierbreite und -höhe für verschiedene Größen ermitteln, wenn Sie Arbeitsblätter für den Druck mit Aspose.Cells für .NET vorbereiten. Dieses Dienstprogramm kann unglaublich hilfreich sein, insbesondere wenn Sie Ihre Drucklayouts planen oder Druckeinstellungen programmgesteuert verwalten. Wenn Sie die genauen Abmessungen in Zoll kennen, können Sie häufige Fehler vermeiden und sicherstellen, dass Ihre Dokumente wie vorgesehen ausgedruckt werden.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek, die eine Reihe von Funktionen für die programmgesteuerte Arbeit mit Excel-Dateien bietet.
### Wie beginne ich mit Aspose.Cells?
Beginnen Sie mit dem Herunterladen der Bibliothek von der[Aspose-Website](https://releases.aspose.com/cells/net/) und befolgen Sie die Dokumentation, um es in Ihrem Projekt einzurichten.
### Kann ich Aspose.Cells kostenlos nutzen?
Aspose.Cells bietet eine Testversion an, mit der Sie die Funktionen erkunden können. Für die langfristige Nutzung müssen Sie eine Lizenz erwerben.
### Welche Papierformate werden von Aspose.Cells unterstützt?
Aspose.Cells unterstützt verschiedene Papierformate, darunter A2, A3, A4, Letter und viele andere.
### Wo finde ich weitere Ressourcen oder Support für Aspose.Cells?
 Sie können die[Aspose-Forum](https://forum.aspose.com/c/cells/9) für die Hilfe der Gemeinschaft und die[Dokumentation](https://reference.aspose.com/cells/net/) für Tutorials und Referenzmaterialien.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
