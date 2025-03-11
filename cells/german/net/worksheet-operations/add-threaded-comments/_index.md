---
title: Thread-Kommentare im Arbeitsblatt hinzufügen
linktitle: Thread-Kommentare im Arbeitsblatt hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET Thread-Kommentare in Excel-Arbeitsblätter einfügen. Verbessern Sie mühelos die Zusammenarbeit.
weight: 10
url: /de/net/worksheet-operations/add-threaded-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thread-Kommentare im Arbeitsblatt hinzufügen

## Einführung
Möchten Sie Ihre Excel-Arbeitsblätter mit Thread-Kommentaren verbessern? Wenn Sie Entwickler sind und Aspose.Cells für .NET verwenden, haben Sie Glück! Thread-Kommentare ermöglichen eine besser organisierte Diskussion innerhalb Ihrer Excel-Tabellen und ermöglichen Benutzern eine effektive Zusammenarbeit. Egal, ob Sie an einem Projekt arbeiten, das Feedback erfordert, oder einfach nur Daten kommentieren möchten, dieses Tutorial führt Sie durch den Prozess des Hinzufügens von Thread-Kommentaren in Ihre Excel-Arbeitsblätter mit Aspose.Cells. 
## Voraussetzungen
Bevor wir beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist, da es die gängigste IDE für die .NET-Entwicklung ist.
2.  Aspose.Cells für .NET: Sie müssen die Bibliothek Aspose.Cells für .NET installiert haben. Wenn Sie sie noch nicht installiert haben, können Sie sie von der Site herunterladen[Hier](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Kenntnisse in der C#-Programmierung sind unbedingt erforderlich, da dieses Tutorial in C# geschrieben wird.
4. .NET Framework: Stellen Sie sicher, dass Ihr Projekt mit einer kompatiblen .NET Framework-Version eingerichtet ist.
## Pakete importieren
Um mit Aspose.Cells zu arbeiten, müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. So können Sie das tun:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Über diese Namespaces erhalten Sie Zugriff auf die Klassen und Methoden, die zum Bearbeiten von Excel-Dateien und Verwalten von Thread-Kommentaren erforderlich sind.
Nachdem wir nun unsere Voraussetzungen eingerichtet und die erforderlichen Pakete importiert haben, wollen wir den Vorgang des Hinzufügens von Thread-Kommentaren der Übersichtlichkeit halber in mehrere Schritte aufteilen.
## Schritt 1: Erstellen Sie eine neue Arbeitsmappe
Als Erstes müssen wir eine neue Arbeitsmappe erstellen, in die wir unsere Thread-Kommentare einfügen.
```csharp
string outDir = "Your Document Directory"; // Legen Sie Ihr Ausgabeverzeichnis fest
Workbook workbook = new Workbook(); // Erstellen einer neuen Arbeitsmappe
```
 In diesem Schritt legen Sie das Ausgabeverzeichnis fest, in dem Ihre Excel-Datei gespeichert wird.`Workbook` Klasse ist der Einstiegspunkt zum Erstellen und Bearbeiten von Excel-Dateien in Aspose.Cells.
## Schritt 2: Einen Autor für die Kommentare hinzufügen
Bevor wir Kommentare hinzufügen können, müssen wir einen Autor definieren. Dieser Autor wird mit den von Ihnen erstellten Kommentaren verknüpft. Lassen Sie uns jetzt einen Autor hinzufügen.
```csharp
int authorIndex = workbook.Worksheets.ThreadedCommentAuthors.Add("Aspose Test", "", ""); // Autor hinzufügen
ThreadedCommentAuthor author = workbook.Worksheets.ThreadedCommentAuthors[authorIndex]; // Holen Sie sich den Autor
```
 Hier verwenden wir die`Add` Methode zum Erstellen eines neuen Autors. Sie können den Namen des Autors und andere optionale Details (wie E-Mail) in den Parametern angeben. Auf diesen Autor wird später beim Hinzufügen von Kommentaren verwiesen.
## Schritt 3: Einen Thread-Kommentar hinzufügen
Nachdem wir unseren Autor eingerichtet haben, ist es an der Zeit, einer bestimmten Zelle im Arbeitsblatt einen Thread-Kommentar hinzuzufügen. 
```csharp
workbook.Worksheets[0].Comments.AddThreadedComment("A1", "Test Threaded Comment", author); // Thread-Kommentar hinzufügen
```
 In diesem Schritt fügen wir einen Kommentar zur Zelle A1 im ersten Arbeitsblatt hinzu. Sie können ersetzen`"A1"` mit einem beliebigen Zellbezug, in den Sie Ihren Kommentar einfügen möchten. Die Nachricht in Anführungszeichen ist der Inhalt des Kommentars.
## Schritt 4: Speichern der Arbeitsmappe
Nachdem Sie Ihren Threadkommentar hinzugefügt haben, sollten Sie Ihre Arbeitsmappe speichern, damit die Änderungen bestehen bleiben.
```csharp
workbook.Save(outDir + "AddThreadedComments_out.xlsx"); // Speichern der Arbeitsmappe
```
 Dabei wird die Arbeitsmappe im angegebenen Ausgabeverzeichnis mit dem Namen`AddThreadedComments_out.xlsx`Stellen Sie sicher, dass das Verzeichnis vorhanden ist. Andernfalls wird die Fehlermeldung „Datei nicht gefunden“ angezeigt.
## Schritt 5: Erfolg bestätigen
Lassen Sie uns abschließend eine Meldung an die Konsole ausgeben, die angibt, dass unser Vorgang erfolgreich war.
```csharp
Console.WriteLine("AddThreadedComments executed successfully."); // Bestätigungsnachricht
```
Dieser Schritt ist optional, aber für die Fehlerbehebung nützlich. Er zeigt Ihnen, dass der Code ohne Fehler ausgeführt wurde.
## Abschluss
Und da haben Sie es! Sie haben Ihrem Excel-Arbeitsblatt mit Aspose.Cells für .NET erfolgreich Thread-Kommentare hinzugefügt. Diese Funktion kann die Zusammenarbeit erheblich verbessern und für Klarheit in der Kommunikation sorgen, wenn mehrere Benutzer am selben Dokument arbeiten.
Threaded-Kommentare ermöglichen nicht nur eine ausführlichere Diskussion innerhalb des Dokuments, sondern sorgen auch für die Organisation Ihrer Anmerkungen. Experimentieren Sie ruhig mit verschiedenen Zellen, Autoren und Kommentaren, um zu sehen, wie sie in Ihrer Arbeitsmappe angezeigt werden.
## Häufig gestellte Fragen
### Was ist ein Thread-Kommentar in Excel?  
Ein Thread-Kommentar ist ein Kommentar, der Antworten und Diskussionen innerhalb des Kommentars selbst ermöglicht und so die Zusammenarbeit erleichtert.
### Kann ich einer einzelnen Zelle mehrere Kommentare hinzufügen?  
Ja, Sie können einer einzelnen Zelle mehrere Thread-Kommentare hinzufügen und so ausführliche Diskussionen ermöglichen.
### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?  
 Während Sie Aspose.Cells mit einer kostenlosen Testversion ausprobieren können, ist für den produktiven Einsatz eine Lizenz erforderlich. Sie erhalten es[Hier](https://purchase.aspose.com/buy).
### Wie kann ich die Kommentare in Excel anzeigen?  
Nachdem Sie Kommentare hinzugefügt haben, können Sie diese anzeigen, indem Sie mit der Maus über die Zelle fahren, in der der Kommentar platziert ist, oder über den Kommentarbereich.
### Wo finde ich weitere Informationen zu Aspose.Cells?  
 Weitere Informationen finden Sie im[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für weitere Informationen und ausführliche Beispiele.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
