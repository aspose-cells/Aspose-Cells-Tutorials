---
title: Extrahieren Sie die eingebettete Mol-Datei aus der Arbeitsmappe
linktitle: Extrahieren Sie die eingebettete Mol-Datei aus der Arbeitsmappe
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem ausführlichen Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET eingebettete MOL-Dateien aus Excel-Arbeitsmappen extrahieren.
weight: 18
url: /de/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahieren Sie die eingebettete Mol-Datei aus der Arbeitsmappe

## Einführung
Beim Verwalten von Daten in Excel-Arbeitsmappen stoßen Sie manchmal auf verschiedene eingebettete Objekte, die nicht in einem Standardformat vorliegen. Ein solches Format ist MOL (Molecular Structure File), das in der Chemie häufig zur Darstellung molekularer Informationen verwendet wird. Wenn Sie diese MOL-Dateien mit Aspose.Cells für .NET aus einer Excel-Arbeitsmappe extrahieren möchten, sind Sie bei der richtigen Anleitung gelandet. In diesem Artikel führen wir Sie Schritt für Schritt durch den Prozess und entmystifizieren dabei jeden Teil.
## Voraussetzungen
Bevor Sie sich in den Code vertiefen, müssen Sie sicherstellen, dass Sie über die erforderlichen Fähigkeiten und Werkzeuge verfügen. Folgendes benötigen Sie:
1. Grundlegende Kenntnisse der .NET-Programmierung: Sie sollten mit C# und dem .NET-Framework vertraut sein.
2.  Aspose.Cells für .NET: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek haben. Sie können[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
3. Eine IDE: Sie können Visual Studio oder jede andere .NET-kompatible IDE verwenden.
4. Excel-Arbeitsmappe mit eingebetteten MOL-Dateien: Für dieses Tutorial benötigen Sie eine Excel-Datei mit MOL-Objekten. Sie können Ihre eigene Datei erstellen oder eine beliebige Beispieldatei verwenden.
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. Dies ist für den Zugriff auf die Aspose.Cells-Funktionen von entscheidender Bedeutung. So können Sie es tun:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Diese Namespaces ermöglichen Ihnen die Bearbeitung von Arbeitsmappen, den Zugriff auf Arbeitsblätter und die allgemeine Arbeit mit Dateien.
Nachdem wir nun unsere Voraussetzungen geklärt haben, tauchen wir in den Code ein und verstehen jeden Schritt, der zum Extrahieren eingebetteter MOL-Dateien aus einer Excel-Arbeitsmappe erforderlich ist. 
## Schritt 1: Einrichten Ihrer Verzeichnisse
Der erste Schritt besteht darin, zu definieren, wo sich Ihr Quelldokument befindet und wo Sie die extrahierten MOL-Dateien speichern möchten. Lassen Sie uns diese Verzeichnisse einrichten.
```csharp
string SourceDir = "Your Document Directory"; // Ersetzen Sie es durch Ihren Verzeichnispfad.
string outputDir = "Your Document Directory"; // Ersetzen Sie durch Ihren Ausgabepfad
```
 Hier ersetzen Sie`"Your Document Directory"`durch den Pfad zu Ihren tatsächlichen Verzeichnissen. Es ist wichtig, dass sowohl das Quell- als auch das Ausgabeverzeichnis für Ihre Anwendung zugänglich sind.
## Schritt 2: Laden der Arbeitsmappe
Nachdem Sie Ihre Verzeichnisse eingerichtet haben, besteht die nächste Aufgabe darin, die Excel-Arbeitsmappe zu laden. Lassen Sie uns das jetzt tun.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

 Wir erstellen eine Instanz des`Workbook` Klasse und übergeben Sie den Pfad zu unserer Excel-Datei mit dem Namen`EmbeddedMolSample.xlsx`Dieser Schritt initialisiert die Arbeitsmappe und ermöglicht Ihnen den Zugriff auf deren Inhalt.
## Schritt 3: Über Arbeitsblätter iterieren
Nachdem Ihre Arbeitsmappe nun geladen ist, müssen Sie jedes Arbeitsblatt in der Arbeitsmappe durchlaufen. Auf diese Weise können Sie jedes Blatt auf eingebettete Objekte untersuchen.

```csharp
var index = 1; // Wird zum Benennen extrahierter MOL-Dateien verwendet
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Die weitere Extraktionslogik finden Sie hier
}
```

 Hier verwenden Sie ein`foreach` Schleife, um durch die Arbeitsblätter zu navigieren. Für jedes Arbeitsblatt greifen Sie auf die`OleObjects` Sammlung, die alle eingebetteten Objekte enthält.
## Schritt 4: Extrahieren von MOL-Dateien
Jetzt kommt der kritische Teil – das Extrahieren der MOL-Dateien aus den OLE-Objekten. Dies erfordert eine weitere Schleife innerhalb der Arbeitsblattschleife.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

 Für jedes gefundene OLE-Objekt wird eine neue Datei im Ausgabeverzeichnis erstellt.`ObjectData` Eigentum der`OleObject` enthält die Daten des eingebetteten Objekts, die Sie mit einem`FileStream`Die Datei wird fortlaufend benannt (`OleObject1.mol`, `OleObject2.mol` , usw.), basierend auf der`index` Variable.
## Schritt 5: Bestätigung des Prozessabschlusses
Wenn schließlich alle MOL-Dateien extrahiert wurden, empfiehlt es sich, den Benutzer darüber zu informieren, dass der Vorgang erfolgreich abgeschlossen wurde.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Diese Zeile gibt einfach eine Meldung auf der Konsole aus, die Sie darüber informiert, dass die Extraktion erfolgreich war. Das ist eine nette Geste für Benutzerfeedback.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich eingebettete MOL-Dateien aus einer Excel-Arbeitsmappe mit Aspose.Cells für .NET extrahiert. Dieser Prozess integriert einige Kernschritte und gewährleistet einen strukturierten Ansatz für den Umgang mit eingebetteten Objekten. Egal, ob Sie in der wissenschaftlichen Forschung, der chemischen Analyse oder einfach im Umgang mit komplexen Datensätzen tätig sind, die Fähigkeit, diese Dateitypen zu extrahieren und zu bearbeiten, kann einen erheblichen Unterschied bei der Verwaltung Ihrer Informationen ausmachen. 
## Häufig gestellte Fragen
### Kann ich außer MOL auch andere Dateitypen aus Excel extrahieren?
Ja, Sie können verschiedene andere eingebettete Dateitypen mit ähnlichen Techniken extrahieren.
### Ist die Nutzung von Aspose.Cells kostenlos?
 Aspose.Cells ist eine kommerzielle Bibliothek, aber Sie können[für einen begrenzten Zeitraum kostenlos testen](https://releases.aspose.com/).
### Funktioniert diese Methode mit allen Excel-Versionen?
Ja, solange das Dateiformat von Aspose.Cells unterstützt wird.
### Kann ich diesen Extraktionsprozess automatisieren?
Auf jeden Fall! Sie können diesen Vorgang automatisieren, indem Sie den Code in eine geplante Aufgabe oder ein Skript einfügen.
### Wo finde ich weitere Dokumentation zu Aspose.Cells?
 Sie können sich die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für weitere Einzelheiten und Beispiele.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
