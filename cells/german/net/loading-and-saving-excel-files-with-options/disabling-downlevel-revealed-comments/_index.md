---
"description": "Erfahren Sie in dieser ausführlichen Schritt-für-Schritt-Anleitung, wie Sie beim Speichern einer Excel-Arbeitsmappe im HTML-Format mit Aspose.Cells für .NET angezeigte Kommentare auf niedrigerer Ebene deaktivieren."
"linktitle": "Deaktivieren von Downlevel Revealed-Kommentaren beim Speichern im HTML-Format"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Deaktivieren von Downlevel Revealed-Kommentaren beim Speichern im HTML-Format"
"url": "/de/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Deaktivieren von Downlevel Revealed-Kommentaren beim Speichern im HTML-Format

## Einführung
Mussten Sie schon einmal eine Excel-Arbeitsmappe in HTML konvertieren und wollten dabei sicherstellen, dass unnötige Kommentare oder versteckte Inhalte nicht sichtbar werden? Hier ist das Deaktivieren von Downlevel-Kommentaren hilfreich. Mit Aspose.Cells für .NET haben Sie die volle Kontrolle darüber, wie Ihre Excel-Arbeitsmappen als HTML-Dateien dargestellt werden. In diesem Tutorial zeigen wir Ihnen Schritt für Schritt, wie Sie Downlevel-Kommentare beim Speichern einer Arbeitsmappe als HTML deaktivieren. 
Am Ende dieses Artikels wissen Sie genau, wie Sie diese Funktion verwenden und sicherstellen, dass Ihre HTML-Ausgabe sauber und kommentarfrei ist.
## Voraussetzungen
Bevor wir uns in die Schritt-für-Schritt-Anleitung stürzen, wollen wir ein paar Dinge besprechen, die Sie bereithalten müssen, um reibungslos vorgehen zu können:
1. Aspose.Cells für .NET: Sie benötigen die Aspose.Cells-Bibliothek. Falls Sie sie noch nicht installiert haben, können Sie sie herunterladen. [Hier](https://releases.aspose.com/cells/net/).
2. IDE: Eine Entwicklungsumgebung wie Visual Studio zum Schreiben und Ausführen Ihres C#-Codes.
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Syntax und der objektorientierten Programmierung vertraut sind, können Sie dem Code leichter folgen.
4. Temporäre oder lizenzierte Version: Sie können entweder die kostenlose Testversion nutzen oder eine temporäre Lizenz beantragen bei [Hier](https://purchase.aspose.com/temporary-license/)Dadurch wird sichergestellt, dass die Bibliothek ohne Einschränkungen funktioniert.
Jetzt, da Sie bereit sind, können wir direkt loslegen!
## Namespaces importieren
Bevor wir uns mit den Codebeispielen befassen, müssen die erforderlichen Namespaces für Aspose.Cells eingefügt werden. Ohne diese kann Ihr Code nicht auf die Methoden und Eigenschaften zugreifen, die für die Bearbeitung von Excel-Dateien erforderlich sind.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Stellen Sie sicher, dass Sie diese Zeile oben in Ihrer C#-Datei platzieren, um den Aspose.Cells-Namespace zu importieren.
## Schritt 1: Einrichten der Verzeichnispfade
Zunächst müssen wir das Quellverzeichnis (wo Ihre Excel-Datei gespeichert ist) und das Ausgabeverzeichnis (wo Ihre HTML-Datei gespeichert wird) einrichten. Dies ist wichtig, da Aspose.Cells die genauen Dateipfade zum Zugriff und Speichern von Dateien benötigt.
```csharp
// Quellverzeichnis, in dem sich Ihre Excel-Datei befindet
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis, in dem die resultierende HTML-Datei gespeichert wird
string outputDir = "Your Document Directory";
```
In diesem Schritt ersetzen `"Your Document Directory"` mit den tatsächlichen Dateipfaden auf Ihrem System. Sie können auch benutzerdefinierte Verzeichnisse erstellen, um Ihre Eingabe- und Ausgabedateien besser zu organisieren.
## Schritt 2: Laden Sie die Excel-Arbeitsmappe
In diesem Schritt laden wir die Excel-Arbeitsmappe in den Speicher, damit wir sie bearbeiten können. Zu Demonstrationszwecken verwenden wir eine Beispieldatei mit dem Namen `"sampleDisableDownlevelRevealedComments.xlsx"`. Sie können jede beliebige Arbeitsmappe verwenden.
```csharp
// Laden Sie die Beispielarbeitsmappe aus dem Quellverzeichnis
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
Dadurch wird ein Arbeitsmappenobjekt erstellt, das alle Daten und die Struktur Ihrer Excel-Datei enthält. Von hier aus können Sie es ändern, Einstellungen anwenden und schließlich in einem anderen Format speichern.
## Schritt 3: HTML-Speicheroptionen einrichten
Nun müssen wir das HtmlSaveOptions-Objekt so konfigurieren, dass die Anzeige von Kommentaren auf niedrigerer Ebene deaktiviert wird. Diese Option stellt sicher, dass Kommentare oder versteckte Inhalte in der resultierenden HTML-Datei nicht angezeigt werden.
```csharp
// Erstellen Sie ein neues HtmlSaveOptions-Objekt, um die Speicheroptionen zu konfigurieren
HtmlSaveOptions opts = new HtmlSaveOptions();
// Deaktivieren Sie auf niedrigerer Ebene angezeigte Kommentare
opts.DisableDownlevelRevealedComments = true;
```
Durch die Einstellung `DisableDownlevelRevealedComments` Zu `true`stellen Sie sicher, dass beim Speichern der Arbeitsmappe als HTML-Datei alle Downlevel-Kommentare deaktiviert werden.
## Schritt 4: Speichern Sie die Arbeitsmappe als HTML
Sobald das HtmlSaveOptions-Objekt konfiguriert ist, besteht der nächste Schritt darin, die Arbeitsmappe mit den angegebenen Optionen im HTML-Format zu speichern. Hier erfolgt die eigentliche Dateikonvertierung.
```csharp
// Speichern Sie die Arbeitsmappe als HTML-Datei mit den angegebenen Speicheroptionen
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
In dieser Codezeile speichern wir die Arbeitsmappe im zuvor angegebenen Ausgabeverzeichnis und wenden die Einstellung „DisableDownlevelRevealedComments“ an. Das Ergebnis ist eine saubere HTML-Datei ohne unerwünschte Kommentare.
## Schritt 5: Überprüfen und Ausführen
Um sicherzustellen, dass alles wie erwartet funktioniert hat, können Sie abschließend eine Erfolgsmeldung an die Konsole ausgeben.
```csharp
// Geben Sie eine Erfolgsmeldung an die Konsole aus
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
Dadurch wissen Sie, dass der Vorgang ohne Fehler abgeschlossen wurde.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich gelernt, wie Sie beim Speichern einer Excel-Arbeitsmappe als HTML mit Aspose.Cells für .NET die Anzeige von Downlevel-Kommentaren deaktivieren. Mit dieser Funktion können Sie nun steuern, wie Ihre Arbeitsmappen als HTML dargestellt werden, und unnötige Inhalte vermeiden. Egal, ob Sie eine Web-App entwickeln oder einfach nur saubere HTML-Ausgabe benötigen – diese Methode gewährleistet präzise und sichere Arbeitsmappenkonvertierungen.
Wenn Sie dieses Tutorial hilfreich fanden, sollten Sie auch andere Funktionen von Aspose.Cells erkunden, um Ihre Excel-Verarbeitungsfunktionen weiter zu verbessern.
## Häufig gestellte Fragen
### Was sind auf niedrigerer Ebene angezeigte Kommentare?
Downlevel-Kommentare werden typischerweise in der Webentwicklung verwendet, um zusätzliche Informationen für ältere Browser bereitzustellen, die bestimmte HTML-Funktionen nicht unterstützen. Bei Excel-zu-HTML-Konvertierungen können sie manchmal versteckte Inhalte oder Kommentare sichtbar machen, weshalb es sinnvoll sein kann, sie zu deaktivieren.
### Kann ich Downlevel-Kommentare aktivieren, wenn ich sie brauche?
Ja, stellen Sie einfach die `DisableDownlevelRevealedComments` Eigentum zu `false` wenn Sie beim Speichern Ihrer Arbeitsmappe als HTML Downlevel-Kommentare aktivieren möchten.
### Wie erhalte ich eine temporäre Lizenz für Aspose.Cells?
Sie können ganz einfach eine vorläufige Lizenz beantragen, indem Sie die [Aspose-Website](https://purchase.aspose.com/temporary-license/).
### Beeinflusst das Deaktivieren von Downlevel-Kommentaren das Erscheinungsbild des HTML?
Nein, das Deaktivieren von Kommentaren auf niedrigerer Ebene hat keinen Einfluss auf die visuelle Darstellung der HTML-Ausgabe. Es verhindert lediglich die Anzeige zusätzlicher Informationen, die für ältere Browser gedacht sind.
### Kann ich die Arbeitsmappe in anderen Formaten als HTML speichern?
Ja, Aspose.Cells unterstützt eine Vielzahl von Ausgabeformaten wie PDF, CSV und TXT. Weitere Optionen finden Sie im [Dokumentation](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}