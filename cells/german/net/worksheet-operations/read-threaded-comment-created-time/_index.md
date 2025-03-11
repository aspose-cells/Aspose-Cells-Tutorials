---
title: Erstellungszeit von Thread-Kommentaren im Arbeitsblatt lesen
linktitle: Erstellungszeit von Thread-Kommentaren im Arbeitsblatt lesen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET die Erstellungszeit von Thread-Kommentaren in Excel lesen. Schritt-für-Schritt-Anleitung mit Codebeispielen.
weight: 21
url: /de/net/worksheet-operations/read-threaded-comment-created-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellungszeit von Thread-Kommentaren im Arbeitsblatt lesen

## Einführung
Beim Arbeiten mit Excel-Dateien kann die Verwaltung von Kommentaren ein entscheidender Aspekt der Datenzusammenarbeit und des Feedbacks sein. Wenn Sie Aspose.Cells für .NET verwenden, werden Sie feststellen, dass es unglaublich leistungsstark für die Handhabung verschiedener Excel-Funktionen ist, einschließlich Thread-Kommentaren. In diesem Tutorial konzentrieren wir uns darauf, wie man die Erstellungszeit von Thread-Kommentaren in einem Arbeitsblatt liest. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, diese Anleitung führt Sie Schritt für Schritt durch den Prozess.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie zum Einstieg benötigen:
1. Aspose.Cells für .NET: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek installiert haben. Sie können sie von der[Aspose-Website](https://releases.aspose.com/cells/net/).
2. Visual Studio: Eine funktionierende Installation von Visual Studio oder einer anderen .NET IDE, in der Sie Ihren C#-Code schreiben und ausführen können.
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, verstehen Sie die Codeausschnitte besser.
4.  Excel-Datei: Halten Sie eine Excel-Datei mit einigen Thread-Kommentaren bereit. Für dieses Beispiel verwenden wir eine Datei namens`ThreadedCommentsSample.xlsx`.
Nachdem wir nun unsere Voraussetzungen abgedeckt haben, importieren wir die erforderlichen Pakete.
## Pakete importieren
Um mit Aspose.Cells zu beginnen, müssen Sie die erforderlichen Namespaces importieren. So geht's:
### Importieren Sie den Aspose.Cells-Namespace
Öffnen Sie Ihr C#-Projekt in Visual Studio und fügen Sie oben in Ihrer Codedatei die folgende using-Direktive hinzu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Über diesen Namespace können Sie auf alle Klassen und Methoden zugreifen, die von der Aspose.Cells-Bibliothek bereitgestellt werden.
Nachdem wir nun die Bühne bereitet haben, wollen wir den Prozess des Lesens der Erstellungszeit von Thread-Kommentaren in überschaubare Schritte aufteilen.
## Schritt 1: Definieren Sie das Quellverzeichnis
Zuerst müssen Sie das Verzeichnis angeben, in dem sich Ihre Excel-Datei befindet. Dies ist wichtig, da das Programm wissen muss, wo es nach der Datei suchen muss.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"`mit dem tatsächlichen Pfad zu Ihrer Excel-Datei. Dies könnte etwa so aussehen:`"C:\\Documents\\"`.
## Schritt 2: Laden Sie die Arbeitsmappe
Als Nächstes laden Sie die Excel-Arbeitsmappe, die die Thread-Kommentare enthält. So gehen Sie dabei vor:
```csharp
Workbook workbook = new Workbook(sourceDir + "ThreadedCommentsSample.xlsx");
```
 Diese Codezeile erzeugt eine neue`Workbook` Objekt durch Laden der angegebenen Excel-Datei. Wenn die Datei nicht gefunden wird, wird eine Ausnahme ausgelöst. Stellen Sie daher sicher, dass der Pfad korrekt ist.
## Schritt 3: Zugriff auf das Arbeitsblatt
Sobald die Arbeitsmappe geladen ist, besteht der nächste Schritt darin, auf das spezifische Arbeitsblatt zuzugreifen, das die Kommentare enthält. In unserem Fall greifen wir auf das erste Arbeitsblatt zu:
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu
Worksheet worksheet = workbook.Worksheets[0];
```
Diese Zeile ruft das erste Arbeitsblatt (Index 0) aus der Arbeitsmappe ab. Wenn sich Ihre Kommentare auf einem anderen Arbeitsblatt befinden, passen Sie den Index entsprechend an.
## Schritt 4: Thread-Kommentare abrufen
Jetzt ist es an der Zeit, die Thread-Kommentare aus einer bestimmten Zelle abzurufen. In diesem Beispiel erhalten wir Kommentare aus Zelle A1:
```csharp
// Thread-Kommentare abrufen
ThreadedCommentCollection threadedComments = worksheet.Comments.GetThreadedComments("A1");
```
Diese Zeile ruft alle Thread-Kommentare ab, die mit Zelle A1 verknüpft sind. Wenn keine Kommentare vorhanden sind, ist die Sammlung leer.
## Schritt 5: Kommentare durchgehen
Nachdem wir die Thread-Kommentare abgerufen haben, können wir sie nun in einer Schleife durchlaufen und die Details anzeigen, einschließlich der Erstellungszeit:
```csharp
foreach (ThreadedComment comment in threadedComments)
{
    Console.WriteLine("Comment: " + comment.Notes);
    Console.WriteLine("Author: " + comment.Author.Name);
    Console.WriteLine("Created Time: " + comment.CreatedTime);
}
```
 Diese Schleife durchläuft jeden Kommentar im`threadedComments` Sammlung und druckt den Kommentartext, den Namen des Autors und den Zeitpunkt der Erstellung des Kommentars aus.
## Schritt 6: Bestätigungsnachricht
Abschließend ist es immer eine gute Idee, nach der Ausführung der Kommentarleselogik eine Bestätigungsmeldung bereitzustellen. Dies hilft beim Debuggen und stellt sicher, dass der Code erfolgreich ausgeführt wurde:
```csharp
Console.WriteLine("ReadThreadedCommentCreatedTime executed successfully.");
```
## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich gelernt, wie Sie mit Aspose.Cells für .NET die Erstellungszeit von Thread-Kommentaren in einem Excel-Arbeitsblatt lesen. Diese Funktion kann unglaublich nützlich sein, um Feedback und Zusammenarbeit in Ihren Excel-Dokumenten zu verfolgen. Mit nur wenigen Codezeilen können Sie wertvolle Informationen extrahieren, die Ihre Datenanalyse- und Berichtsprozesse verbessern können.
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler Excel-Dateien in .NET-Anwendungen erstellen, bearbeiten und konvertieren können.
### Wie kann ich Aspose.Cells für .NET herunterladen?
 Sie können es herunterladen von der[Aspose-Website](https://releases.aspose.com/cells/net/).
### Gibt es eine kostenlose Testversion?
 Ja, Sie können Aspose.Cells kostenlos testen, indem Sie die[Seite zur kostenlosen Testversion](https://releases.aspose.com/).
### Kann ich auf Kommentare aus anderen Zellen zugreifen?
Absolut! Sie können den Zellbezug im`GetThreadedComments` Methode, um auf Kommentare aus jeder Zelle zuzugreifen.
### Wo erhalte ich Support für Aspose.Cells?
 Für Unterstützung besuchen Sie bitte die[Aspose-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
