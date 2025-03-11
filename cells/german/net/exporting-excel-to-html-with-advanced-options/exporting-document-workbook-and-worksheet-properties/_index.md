---
title: Exportieren von Dokument-, Arbeitsmappen- und Arbeitsblatteigenschaften in HTML
linktitle: Exportieren von Dokument-, Arbeitsmappen- und Arbeitsblatteigenschaften in HTML
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET Excel-Dokument-, Arbeitsmappen- und Arbeitsblatteigenschaften in HTML exportieren. Einfache Schritt-für-Schritt-Anleitung enthalten.
weight: 11
url: /de/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportieren von Dokument-, Arbeitsmappen- und Arbeitsblatteigenschaften in HTML

## Einführung

Beim Umgang mit Tabellenkalkulationen müssen wir Excel-Dateien häufig in verschiedene Formate konvertieren, um sie freizugeben, aufzubewahren oder zu präsentieren. Eine häufige Aufgabe ist das Exportieren von Arbeitsmappen- und Arbeitsblatteigenschaften in das HTML-Format. In diesem Artikel zeigen wir Ihnen Schritt für Schritt, wie Sie dies mit Aspose.Cells für .NET erreichen. Keine Sorge, wenn Sie neu im Programmieren oder in der Aspose-Bibliothek sind; wir erklären es Ihnen Schritt für Schritt, damit Sie es leicht nachvollziehen können!

## Voraussetzungen

Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie zum Einstieg benötigen:

1. .NET Framework: Stellen Sie sicher, dass Ihre Entwicklungsumgebung mit .NET Framework eingerichtet ist. Aspose.Cells ist mit .NET Framework-Versionen bis 4.8 kompatibel.
   
2.  Aspose.Cells für .NET: Sie müssen Aspose.Cells installiert haben. Sie können die Bibliothek von der herunterladen[Downloads Seite](https://releases.aspose.com/cells/net/). 

3. IDE: Eine geeignete integrierte Entwicklungsumgebung (IDE) wie Visual Studio vereinfacht Ihre Codierung.

4.  Beispiel-Excel-Datei: Stellen Sie zu Testzwecken sicher, dass Sie eine Excel-Datei mit dem Namen haben`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx` in Ihrem Arbeitsverzeichnis.

## Pakete importieren

Nachdem wir nun die Voraussetzungen erfüllt haben, importieren wir zunächst die erforderlichen Pakete in unser C#-Projekt. So können Sie das tun:

### Neues Projekt erstellen

- Öffnen Sie Ihre IDE und erstellen Sie ein neues C#-Projekt. Sie können eine Konsolenanwendung auswählen, die sich perfekt zum Ausführen dieser Art von Aufgaben eignet.

### Fügen Sie das Aspose.Cells NuGet-Paket hinzu

Um das Paket Aspose.Cells hinzuzufügen, führen Sie diese Schritte aus:

- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt und wählen Sie „NuGet-Pakete verwalten“ aus.
- Suchen Sie im NuGet-Paket-Manager nach „Aspose.Cells“ und installieren Sie es.
- Dieses Paket stellt die erforderlichen Klassen und Methoden zum Arbeiten mit Excel-Dateien bereit.

### Namespaces importieren

Stellen Sie sicher, dass Sie oben in Ihrer Hauptprogrammdatei die folgenden Namespaces einschließen:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

 Damit erhalten wir Zugriff auf die`Workbook` Und`HtmlSaveOptions` Klassen, die wir in unserem Beispiel verwenden werden.

Nachdem Sie nun alles eingerichtet haben, unterteilen wir den Vorgang in einfache Schritte.

## Schritt 1: Richten Sie Ihre Dateiverzeichnisse ein

Zuerst müssen wir angeben, wo unsere Eingabe- und Ausgabedateien gespeichert werden. Initialisieren Sie in Ihrem Code die Verzeichnisse wie folgt:

```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory/";  // Aktualisieren Sie mit Ihrem tatsächlichen Pfad

// Ausgabeverzeichnis
string outputDir = "Your Document Directory/";  // Aktualisieren Sie mit Ihrem tatsächlichen Pfad
```

- Quellverzeichnis: Hier befindet sich Ihre Excel-Eingabedatei (`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`) gespeichert ist.
- Ausgabeverzeichnis: Dies ist der Pfad, in dem die HTML-Ausgabedatei gespeichert werden soll.

## Schritt 2: Laden Sie Ihre Excel-Datei

 Nun müssen wir die Excel-Datei laden mit dem`Workbook` Klasse:

```csharp
// Laden Sie die Excel-Beispieldatei
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

-  Arbeitsmappeninstanz: Die`Workbook` Der Konstruktor übernimmt den Dateipfad zu Ihrer Excel-Datei und erstellt eine neue Instanz, die Sie bearbeiten können.

## Schritt 3: HTML-Speicheroptionen einrichten

Als nächstes geben wir an, wie wir unsere Excel-Daten in HTML speichern möchten:

```csharp
// HTML-Speicheroptionen festlegen
HtmlSaveOptions options = new HtmlSaveOptions();

// Exportieren von Dokument-, Arbeitsmappen- und Arbeitsblatteigenschaften verhindern
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions: Diese Klasse hilft bei der Verwaltung, wie die Excel-Datei in HTML konvertiert wird.
-  Wir haben mehrere Optionen festgelegt, um`false`weil wir keine Arbeitsmappen- und Arbeitsblatteigenschaften in unsere HTML-Ausgabe einschließen möchten.

## Schritt 4: Alles in HTML exportieren

Jetzt können wir unsere Arbeitsmappe im HTML-Format speichern:

```csharp
// Exportieren Sie die Excel-Datei mit den HTML-Speicheroptionen in HTML
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

-  Der`Save` Die Methode nimmt zwei Parameter an: den Dateipfad für die HTML-Ausgabedatei und die von uns eingerichteten Optionen. Wenn Sie dies ausführen, wird Ihre HTML-Datei im angegebenen Ausgabeverzeichnis erstellt.

## Schritt 5: Konsolen-Feedback

Lassen Sie uns abschließend in der Konsole ein Feedback geben, um sicherzustellen, dass der Vorgang erfolgreich abgeschlossen wurde:

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## Abschluss

Und so haben Sie Arbeitsmappen- und Arbeitsblatteigenschaften mithilfe von Aspose.Cells für .NET erfolgreich in HTML exportiert! Sie haben einen unkomplizierten Prozess durchlaufen, vom Einrichten Ihrer Umgebung bis zum Exportieren Ihrer Excel-Daten. Das Schöne an der Verwendung von Bibliotheken wie Aspose.Cells ist, dass sie komplexe Aufgaben rationalisieren und Entwicklern das Leben erleichtern. Jetzt können Sie Ihre Tabellenkalkulationen mit HTML breiter teilen, so als ob Sie der Welt einen Blick in Ihre Arbeitsmappen gewähren, ohne ihnen das gesamte Buch zu geben.

## Häufig gestellte Fragen

### Wie installiere ich Aspose.Cells für .NET?  
Sie können die Aspose.Cells-Bibliothek über NuGet in Ihrem Visual Studio-Projekt über den NuGet-Paket-Manager installieren.

### Kann ich die HTML-Ausgabe anpassen?  
 Ja, Aspose.Cells bietet verschiedene Optionen in`HtmlSaveOptions` um anzupassen, wie Ihre Excel-Datei in HTML konvertiert wird.

### Gibt es eine Möglichkeit, Dokumenteigenschaften in den HTML-Export einzubeziehen?  
 Sie können festlegen`ExportDocumentProperties`, `ExportWorkbookProperties` , Und`ExportWorksheetProperties` Zu`true` In`HtmlSaveOptions` wenn Sie sie einschließen möchten.

### In welche Formate außer HTML kann ich meine Excel-Datei exportieren?  
Aspose.Cells unterstützt verschiedene Formate, darunter PDF, CSV, XML und andere.

### Gibt es eine Testversion?  
 Ja, Sie können eine kostenlose Testversion von Aspose.Cells erhalten von der[Webseite](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
