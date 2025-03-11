---
title: Konvertieren Sie Text in Spalten in Aspose.Cells .NET
linktitle: Konvertieren Sie Text in Spalten in Aspose.Cells .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem ausführlichen Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET Text mühelos in Spalten umwandeln.
weight: 15
url: /de/net/row-column-autofit-conversion/convert-text-to-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konvertieren Sie Text in Spalten in Aspose.Cells .NET

## Einführung
In der heutigen schnelllebigen Welt des Datenmanagements ist Effizienz der Schlüssel. Egal, ob Sie als Analyst Zahlen verarbeiten oder als Geschäftsprofi Berichte erstellen, Sie müssen Daten häufig schnell und präzise bearbeiten. Wenn Sie schon einmal mit Namen in einer einzelnen Zelle zu tun hatten, die Sie in separate Spalten aufteilen mussten, wissen Sie, wie mühsam das sein kann. Glücklicherweise bietet Aspose.Cells für .NET eine elegante Lösung zum Aufteilen von Text in Spalten. In dieser Anleitung werden wir den Prozess der Konvertierung von Text in Spalten mit Aspose.Cells durchgehen.
## Voraussetzungen
Bevor wir loslegen, stellen wir sicher, dass alles eingerichtet ist. Folgendes benötigen Sie:
1.  Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Wenn Sie es noch nicht haben, können Sie es hier herunterladen:[Microsoft-Website](https://visualstudio.microsoft.com/downloads/).
2. .NET Framework: Stellen Sie sicher, dass Sie an einem Projekt arbeiten, das auf eine kompatible Version des .NET Frameworks abzielt. Aspose.Cells ist mit .NET Core, .NET Framework und anderen Plattformen kompatibel.
3.  Aspose.Cells-Bibliothek: Sie müssen die Aspose.Cells-Bibliothek heruntergeladen und in Ihrem Projekt referenziert haben. Sie erhalten sie von[Aspose Downloads-Seite](https://releases.aspose.com/cells/net/).
4. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie dieses Tutorial leichter verstehen.
## Pakete importieren
Um loszulegen, müssen wir die erforderlichen Aspose.Cells-Pakete importieren. So können Sie das tun:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Dadurch können Sie auf alle erforderlichen Funktionen von Aspose.Cells zugreifen, um Ihre Daten zu bearbeiten.
Nachdem wir nun alles vorbereitet haben, beginnen wir mit der Aufteilung der Konvertierung von Text in Spalten in mehrere leicht verständliche Schritte.
## Schritt 1: Einrichten des Dokumentverzeichnisses
Zuerst müssen Sie das Verzeichnis konfigurieren, in dem Sie Ihre Ausgabedatei speichern. Es ist immer eine gute Idee, Ihre Dateien ordentlich zu strukturieren. Dadurch können Sie sie leichter verwalten.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
```
-  Ersetzen`"Your Document Directory"`mit dem tatsächlichen Pfad, in dem Sie Ihre Datei speichern möchten. Sie können beispielsweise verwenden`C:\\Documents\\AsposeOutput\\`.
## Schritt 2: Erstellen einer Arbeitsmappeninstanz
Als Nächstes erstellen wir unsere Arbeitsmappe. Dies ist im Wesentlichen die Datei, in der alle Ihre Daten verarbeitet werden.
```csharp
// Erstellen Sie eine Arbeitsmappeninstanz.
Workbook wb = new Workbook();
```
- Betrachten Sie das Arbeitsbuch als eine leere Leinwand. Sie können malen, wie Sie möchten!
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Da wir nun über eine Arbeitsmappe verfügen, müssen wir auf das erste Arbeitsblatt zugreifen, um mit dem Hinzufügen unserer Daten zu beginnen.
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu.
Worksheet ws = wb.Worksheets[0];
```
- Das Arbeitsblatt ist wie eine Seite in Ihrer Arbeitsmappe. Sie können mehrere Seiten haben, aber der Einfachheit halber konzentrieren wir uns auf die erste.
## Schritt 4: Daten zum Arbeitsblatt hinzufügen
Füllen wir unser Arbeitsblatt mit einigen Namen. Wir geben eine Liste von Namen ein, wobei Vor- und Nachnamen durch ein Leerzeichen getrennt sind.
```csharp
// Fügen Sie in Spalte A die Namen der Personen hinzu. Vorname und Nachname sind durch ein Leerzeichen getrennt.
ws.Cells["A1"].PutValue("John Teal");
ws.Cells["A2"].PutValue("Peter Graham");
ws.Cells["A3"].PutValue("Brady Cortez");
ws.Cells["A4"].PutValue("Mack Nick");
ws.Cells["A5"].PutValue("Hsu Lee");
```
- Sie möchten Ihre Namen nach Bedarf anpassen. Vielleicht möchten Sie mit Ihrer eigenen Namensliste testen oder einen vielfältigeren Satz erstellen.
## Schritt 5: Textladeoptionen erstellen
Bevor wir die Namen aufteilen, müssen wir definieren, wie wir den Text aufteilen möchten. In diesem Fall verwenden wir ein Leerzeichen als Trennzeichen.
```csharp
// Erstellen Sie Textladeoptionen mit Leerzeichen als Trennzeichen.
TxtLoadOptions opts = new TxtLoadOptions();
opts.Separator = ' ';
```
- Indem wir ein Leerzeichen als Trennzeichen definieren, teilen wir Aspose mit, dass die Namen hier getrennt werden sollen.
## Schritt 6: Die Spalte in mehrere Spalten aufteilen
 Und jetzt kommt der Zauber! Wir teilen nun den Inhalt der Spalte A in zwei separate Spalten auf (Vornamen in Spalte A und Nachnamen in Spalte B) und verwenden dazu`TextToColumns` Verfahren.
```csharp
// Teilen Sie Spalte A mit der Methode TextToColumns() in zwei Spalten auf.
// Jetzt enthält Spalte A den Vornamen und Spalte B den Nachnamen.
ws.Cells.TextToColumns(0, 0, 5, opts);
```
- Dieser Schritt nimmt Ihnen die ganze harte Arbeit ab. Es ist, als hätten Sie einen fleißigen kleinen Helfer, der genau weiß, was zu tun ist!
## Schritt 7: Speichern Sie die Arbeitsmappe
Speichern wir zum Schluss unsere Arbeitsmappe mit den vorgenommenen Änderungen. Es ist immer befriedigend, wenn man seine Arbeit sauber gespeichert sieht!
```csharp
// Speichern Sie die Arbeitsmappe im XLSX-Format.
wb.Save(dataDir + "outputTextToColumns.xlsx");
```
- Achten Sie darauf, der Datei einen aussagekräftigen Namen zu geben. In diesem Fall speichern wir sie als`outputTextToColumns.xlsx`, Sie können es aber gerne nach Belieben umbenennen.
## Abschluss
 Und da haben Sie es! Sie haben gerade gelernt, wie Sie mit Aspose.Cells für .NET Text in Spalten umwandeln. Es ist ein leistungsstarkes Tool, das die Datenverarbeitung vereinfacht und es Ihnen ermöglicht, Vorgänge, die früher Stunden dauerten, mit nur wenigen einfachen Codezeilen durchzuführen. Wenn Sie das nächste Mal Namen oder anderen Text aufteilen müssen, können Sie dies ganz einfach tun. Vergessen Sie nicht, Folgendes zu erkunden[Asposes Dokumentation](https://reference.aspose.com/cells/net/) für erweiterte Funktionen und Anpassungen, die Ihre Datenverarbeitungsfähigkeiten verbessern können!
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine robuste .NET-Bibliothek, die es Entwicklern ermöglicht, Excel-Tabellen effizient zu erstellen, zu bearbeiten und zu konvertieren, ohne dass Microsoft Excel installiert sein muss.
### Kann ich Aspose.Cells kostenlos nutzen?
 Ja! Sie können mit einer kostenlosen Testversion beginnen, die verfügbar ist unter[Aspose's Testseite](https://releases.aspose.com/).
### Wo finde ich Unterstützung für Aspose.Cells?
 Bei Fragen oder Problemen können Sie die[Aspose-Supportforum](https://forum.aspose.com/c/cells/9).
### Ist es einfach, Aspose.Cells zu erlernen?
Auf jeden Fall! Dank der einfachen Beispiele und der ausführlichen Dokumentation können sogar Anfänger es schnell verstehen.
### Welche weiteren Funktionen bietet Aspose.Cells?
Über die Textbearbeitung hinaus unterstützt Aspose.Cells die Diagrammerstellung, Datenvalidierung, Formelberechnungen und vieles mehr!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
