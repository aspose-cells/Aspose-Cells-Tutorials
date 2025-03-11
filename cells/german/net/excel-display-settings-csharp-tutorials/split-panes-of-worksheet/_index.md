---
title: Geteilte Bereiche des Arbeitsblatts
linktitle: Geteilte Bereiche des Arbeitsblatts
second_title: Aspose.Cells für .NET API-Referenz
description: Erfahren Sie in unserer Schritt-für-Schritt-Anleitung, wie Sie Arbeitsblattbereiche in Aspose.Cells für .NET aufteilen. Verbessern Sie die Excel-Dateinavigation mit diesem einfachen Tutorial.
weight: 130
url: /de/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Geteilte Bereiche des Arbeitsblatts

## Einführung

Sind Sie bereit, die Bereiche eines Excel-Arbeitsblatts mit Aspose.Cells für .NET aufzuteilen? Stellen Sie sich Folgendes vor: Sie haben ein riesiges Excel-Arbeitsblatt und sind es leid, ständig zu den Überschriften zurückzuscrollen, nur um sich daran zu erinnern, mit welcher Spalte Sie arbeiten. Hier kommt „Bereiche aufteilen“ ins Spiel. Mit dieser praktischen Funktion können Sie einen Teil Ihres Arbeitsblatts fixieren, was die Navigation erheblich erleichtert. Ganz gleich, ob Sie mit Finanzdaten, Bestandsverwaltung oder riesigen Datensätzen arbeiten, das Aufteilen von Bereichen kann Ihre Produktivität um das Zehnfache steigern. 

## Voraussetzungen

Bevor wir beginnen, Bereiche wie ein Tabellenkalkulationsassistent aufzuteilen, müssen wir zunächst die Konfiguration richtig vornehmen. Folgendes benötigen Sie:

-  Aspose.Cells für .NET: Stellen Sie sicher, dass Sie es heruntergeladen und installiert haben. Wenn Sie es noch nicht getan haben, holen Sie es sich[Hier](https://releases.aspose.com/cells/net/).
- .NET Framework: Diese Anleitung setzt voraus, dass Sie in einer .NET-Umgebung arbeiten.
- Eine Excel-Arbeitsmappe: Wir verwenden eine Excel-Beispieldatei, um zu zeigen, wie diese Funktion funktioniert.
-  Eine temporäre oder Volllizenz: Aspose.Cells erfordert eine Lizenz. Wenn Sie es nur ausprobieren möchten, holen Sie sich eine[kostenlose temporäre Lizenz](https://purchase.aspose.com/temporary-license/) um Auswertungseinschränkungen zu vermeiden.

## Pakete importieren

Bevor wir uns in den Code vertiefen, importieren wir zunächst die erforderlichen Namespaces. Ohne diese können Sie in Aspose.Cells eigentlich nichts tun.

```csharp
using System.IO;
using Aspose.Cells;
```

Nachdem wir nun die wesentlichen Punkte abgedeckt haben, kommen wir zum spannenden Teil: dem Teilen von Fenstern!

## Schritt 1: Instanziieren einer Arbeitsmappe

 Der erste Schritt in diesem Prozess ist die Erstellung einer`Workbook` Objekt, das die Excel-Datei darstellt, die Sie ändern möchten. In diesem Fall laden wir eine Datei aus einem Verzeichnis. Dies ist Ihre Leinwand, das Excel-Blatt, auf dem Sie Ihre Magie wirken lassen.

Bevor wir Bereiche teilen können, benötigen wir eine Arbeitsmappe, mit der wir arbeiten können! Dieser Schritt ist so wichtig wie das Öffnen eines Buches, bevor Sie mit dem Lesen beginnen.

```csharp
// Der Pfad zum Dokumentenverzeichnis
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Instanziieren einer neuen Arbeitsmappe und Öffnen einer Vorlagendatei
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 Ersetzen Sie im obigen Code`"YOUR DOCUMENT DIRECTORY"` mit dem tatsächlichen Pfad, in dem sich Ihre Excel-Datei befindet. Die`Workbook`Klasse lädt die Excel-Datei in den Speicher.

## Schritt 2: Aktive Zelle festlegen

 Nach dem Laden der Arbeitsmappe ist es an der Zeit, die aktive Zelle festzulegen. In Excel ist die aktive Zelle diejenige, die aktuell ausgewählt oder im Fokus ist. In diesem Tutorial wählen wir die Zelle`A20` im ersten Arbeitsblatt.

Das Festlegen der aktiven Zelle ist entscheidend, da die Teilung der Bereiche von dieser aktiven Zelle aus beginnt. Es ist, als ob Sie entscheiden, wo Sie den ersten Schnitt in eine Pizza machen – suchen Sie sich Ihr Stück aus!

```csharp
// Aktive Zelle festlegen
book.Worksheets[0].ActiveCell = "A20";
```

 Dieser Code macht`A20` die aktive Zelle. Dies ist wichtig, da die Aufteilung an diesem Punkt erfolgt, genau wie Ihre Navigation in Excel oft auf eine bestimmte Zelle ausgerichtet ist.

## Schritt 3: Teilen Sie das Arbeitsblatt

Nachdem die aktive Zelle nun festgelegt ist, kommen wir zum spaßigen Teil – dem Aufteilen des Arbeitsblatts! In diesem Schritt geschieht die Magie. Sie können das Arbeitsblatt zur einfacheren Anzeige und Navigation in mehrere Bereiche aufteilen.

Dies ist der Kern des gesamten Tutorials. Indem Sie das Arbeitsblatt aufteilen, erstellen Sie separate Bereiche, die es Ihnen ermöglichen, durch verschiedene Abschnitte Ihres Excel-Blatts zu blättern, ohne Überschriften oder andere wichtige Bereiche aus den Augen zu verlieren.

```csharp
// Teilen des Arbeitsblattfensters
book.Worksheets[0].Split();
```

 Mit dem`Split()` Methode sagen Sie Aspose.Cells, dass das Arbeitsblatt an der aktiven Zelle geteilt werden soll (`A20` in diesem Fall). Ab diesem Punkt erstellt Excel eine Unterteilung im Blatt, die die Bereiche voneinander trennt, damit Sie unabhängig voneinander navigieren können.

## Schritt 4: Speichern der Arbeitsmappe

Nachdem Sie die Bereiche geteilt haben, müssen Sie Ihre Arbeit nur noch speichern. Dieser letzte Schritt stellt sicher, dass Ihre Änderungen in der angegebenen Ausgabedatei gespeichert werden.

Was nützt Ihnen all Ihre harte Arbeit, wenn Sie sie nicht aufbewahren? Durch das Aufbewahren bleiben Ihre schön gespaltenen Scheiben für die zukünftige Verwendung intakt.

```csharp
// Speichern Sie die Excel-Datei
book.Save(dataDir + "output.xls");
```

 Hier die`Save()` Die Methode speichert die Arbeitsmappe mit den neu aufgeteilten Bereichen in einer Excel-Ausgabedatei. Die vorgenommenen Änderungen können Sie – oder jeder andere – jetzt verwenden.

## Abschluss

Und da haben Sie es! Sie haben gerade gelernt, wie Sie mit Aspose.Cells für .NET Bereiche in einem Excel-Arbeitsblatt aufteilen. Kein endloses Scrollen oder den Überblick über Ihre Daten mehr. Diese Methode macht die Handhabung großer Excel-Dateien weitaus weniger überwältigend und viel effizienter. Mit der Möglichkeit, Bereiche aufzuteilen, können Sie jetzt beim Arbeiten mit komplexen Tabellenkalkulationen kritische Datenpunkte im Auge behalten.

## Häufig gestellte Fragen

### Kann ich mehr als zwei Scheiben teilen?  
 Ja, Sie können das Arbeitsblatt in mehrere Bereiche aufteilen, indem Sie verschiedene aktive Zellen angeben und den`Split()` Verfahren.

### Was ist der Unterschied zwischen dem Spalten von Scheiben und dem Einfrieren von Scheiben?  
Durch das Teilen von Fenstern können Sie in beiden Fenstern unabhängig voneinander scrollen. Durch das Fixieren von Fenstern werden die Überschriften oder bestimmte Zeilen/Spalten gesperrt, sodass sie beim Scrollen sichtbar bleiben.

### Kann ich den Split nach dem Auftragen wieder entfernen?  
Ja, Sie können die Teilung entfernen, indem Sie die Arbeitsmappe entweder schließen und erneut öffnen oder sie programmgesteuert zurücksetzen.

### Funktioniert das Aufteilen von Bereichen für verschiedene Excel-Dateiformate (XLS, XLSX) gleich?  
 Ja, die`Split()` Die Methode funktioniert sowohl für das XLS- als auch für das XLSX-Format.

### Kann ich Aspose.Cells ohne Lizenz verwenden?  
 Ja, aber es gibt Einschränkungen. Für ein umfassendes Erlebnis verwenden Sie am besten ein[vorübergehend](https://purchase.aspose.com/temporary-license/) oder[bezahlte Lizenz](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
