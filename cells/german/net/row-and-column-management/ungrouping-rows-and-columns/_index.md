---
title: Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells
linktitle: Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem umfassenden Handbuch, wie Sie mit Aspose.Cells für .NET Zeilen und Spalten in Excel aufheben. Vereinfachen Sie Ihre Excel-Datenmanipulation.
weight: 15
url: /de/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gruppieren Sie Zeilen und Spalten in Excel mit Aspose.Cells

## Einführung
Beim Umgang mit Excel-Dateien kann es vorkommen, dass Sie Zeilen und Spalten aufheben müssen. Egal, ob Sie eine Tabelle bereinigen oder Daten für eine bessere Präsentation neu formatieren, Aspose.Cells für .NET ist ein fantastisches Tool, das den Vorgang vereinfacht. In diesem Tutorial führe ich Sie durch die Schritte zum Aufheben der Gruppierung von Zeilen und Spalten in Excel mit Aspose.Cells. Am Ende verfügen Sie über ein solides Verständnis für die programmgesteuerte Arbeit mit Excel-Dateien.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles eingerichtet haben. Folgendes benötigen Sie:
1.  Visual Studio: Sie sollten eine funktionierende Version von Visual Studio auf Ihrem Computer installiert haben. Wenn Sie es noch nicht haben, können Sie es hier herunterladen:[Website von Visual Studio](https://visualstudio.microsoft.com/).
2. Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek herunterladen. Sie finden sie im[Aspose-Releases-Seite](https://releases.aspose.com/cells/net/) . Stellen Sie sicher, dass Sie über die erforderlichen Lizenzen verfügen. Diese können Sie erwerben oder über einen[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
3. Grundkenntnisse in C#: Grundlegende Kenntnisse der C#-Programmierung helfen Ihnen dabei, den Anweisungen leichter zu folgen.
Sobald Sie alles bereit haben, können wir mit dem spaßigen Teil beginnen: dem Code!
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Pakete in Ihr C#-Projekt importieren. So geht's:
1. Öffnen Sie Ihr Projekt in Visual Studio.
2. Fügen Sie einen Verweis auf die Aspose.Cells-Bibliothek hinzu. Klicken Sie dazu mit der rechten Maustaste auf die Verweise in Ihrem Projekt und wählen Sie Verweis hinzufügen. Navigieren Sie zu dem Speicherort, an dem Sie die Aspose.Cells-DLL gespeichert haben.
3. Fügen Sie oben in Ihrer C#-Datei die folgenden Using-Direktiven hinzu:
```csharp
using System.IO;
using Aspose.Cells;
```
Nachdem nun alles eingerichtet ist, gehen wir die Schritte zum Aufheben der Gruppierung von Zeilen und Spalten in Ihrem Excel-Blatt durch. 
## Schritt 1: Definieren Sie das Dokumentverzeichnis
Zunächst müssen Sie das Verzeichnis angeben, in dem sich Ihre Excel-Datei befindet. Dies können Sie wie folgt einrichten:
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad auf Ihrem Computer, wo die Excel-Datei gespeichert ist. 
## Schritt 2: Erstellen eines Dateistreams
Als Nächstes müssen Sie einen Dateistream erstellen, um die Excel-Datei zu öffnen. So können Sie das tun:
```csharp
// Erstellen eines Dateistreams, der die zu öffnende Excel-Datei enthält
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Hier öffnen Sie die Datei mit dem Namen`book1.xls`. Stellen Sie sicher, dass diese Datei in dem von Ihnen angegebenen Verzeichnis vorhanden ist. Andernfalls wird die Fehlermeldung „Datei nicht gefunden“ angezeigt.
## Schritt 3: Instanziieren eines Arbeitsmappenobjekts
Laden wir nun die Excel-Datei in ein Workbook-Objekt. Dadurch können Sie das Arbeitsbuch programmgesteuert bearbeiten:
```csharp
// Instanziieren eines Workbook-Objekts
// Öffnen der Excel-Datei über den Dateistream
Workbook workbook = new Workbook(fstream);
```
Mit dieser Codezeile haben Sie die Excel-Datei erfolgreich in den Speicher geladen und können damit arbeiten.
## Schritt 4: Zugriff auf das Arbeitsblatt
Nachdem Sie die Arbeitsmappe haben, müssen Sie im nächsten Schritt auf das spezifische Arbeitsblatt zugreifen, in dem Sie die Gruppierung von Zeilen und Spalten aufheben möchten. So geht's:
```csharp
// Zugriff auf das erste Arbeitsblatt in der Excel-Datei
Worksheet worksheet = workbook.Worksheets[0];
```
In diesem Fall greifen wir auf das erste Arbeitsblatt zu. Wenn Ihre Daten auf einem anderen Blatt liegen, können Sie den Index entsprechend ändern.
## Schritt 5: Gruppierung der Zeilen aufheben
Jetzt kommt der spannende Teil! Lassen Sie uns die ersten sechs Zeilen (von Zeile 0 bis Zeile 5) auflösen. Verwenden Sie den folgenden Code:
```csharp
// Aufheben der Gruppierung der ersten sechs Zeilen (von 0 bis 5)
worksheet.Cells.UngroupRows(0, 5);
```
Mit dieser Methode wird jede Gruppierung entfernt, die auf die angegebenen Zeilen angewendet wurde. So einfach ist das!
## Schritt 6: Spaltengruppierung aufheben
Genau wie Zeilen können Sie auch Spalten aufheben. So heben Sie die Gruppierung der ersten drei Spalten auf (von Spalte 0 bis Spalte 2):
```csharp
// Aufheben der Gruppierung der ersten drei Spalten (von 0 bis 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Schritt 7: Speichern Sie die geänderte Excel-Datei
 Nachdem Sie die Gruppierung der Zeilen und Spalten aufgehoben haben, besteht der nächste Schritt darin, die Änderungen wieder in einer Excel-Datei zu speichern. Sie können dies tun, indem Sie das`Save` Verfahren:
```csharp
// Speichern der geänderten Excel-Datei
workbook.Save(dataDir + "output.xls");
```
 In diesem Beispiel speichern wir die geänderte Datei als`output.xls`. Sie können den Dateinamen nach Belieben ändern.
## Schritt 8: Schließen Sie den Dateistream
Um Ressourcen freizugeben, sollten Sie abschließend den Dateistream schließen:
```csharp
// Schließen des Dateistreams, um alle Ressourcen freizugeben
fstream.Close();
```
Dies ist eine bewährte Vorgehensweise, um sicherzustellen, dass Ihre Anwendung Dateihandles nicht länger als nötig festhält.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich gelernt, wie Sie mit Aspose.Cells für .NET Zeilen und Spalten in einer Excel-Datei aufheben. Mit nur wenigen Codezeilen können Sie programmgesteuert erhebliche Änderungen an Ihren Excel-Dateien vornehmen. Egal, ob Sie Berichte automatisieren oder Daten für die Analyse vorbereiten, die Beherrschung dieser Techniken kann Ihnen eine Menge Zeit sparen.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke Bibliothek für die Arbeit mit Excel-Dateien in .NET-Anwendungen, die eine einfache Bearbeitung, Konvertierung und Erstellung von Tabellen ermöglicht.
### Kann ich Zeilen und Spalten in Excel mithilfe anderer Bibliotheken aufheben?
Ja, es gibt andere Bibliotheken zur Excel-Bearbeitung in .NET, aber Aspose.Cells bietet umfangreiche Funktionen und Benutzerfreundlichkeit.
### Gibt es eine Möglichkeit, Änderungen nach dem Speichern rückgängig zu machen?
Sobald Sie eine Excel-Datei speichern, kann der vorherige Zustand nicht wiederhergestellt werden, es sei denn, Sie verfügen über eine Sicherungskopie der Originaldatei.
### Wie erhalte ich Unterstützung für Aspose.Cells?
 Unterstützung finden Sie unter[Aspose Support-Forum](https://forum.aspose.com/c/cells/9), wo Sie Fragen stellen und Lösungen finden können.
### Kann ich Aspose.Cells ohne Lizenz verwenden?
Ja, Sie können Aspose.Cells mit bestimmten Einschränkungen kostenlos nutzen und Sie können mit einem[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) für die volle Funktionalität.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
