---
title: Exportieren benutzerdefinierter Eigenschaften aus Excel in PDF
linktitle: Exportieren benutzerdefinierter Eigenschaften aus Excel in PDF
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET benutzerdefinierte Eigenschaften von Excel in PDF exportieren. Optimieren Sie Ihren Datenaustausch.
weight: 10
url: /de/net/excel-file-handling/export-custom-properties-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportieren benutzerdefinierter Eigenschaften aus Excel in PDF

## Einführung
Beim Arbeiten mit Excel-Dateien besteht häufig die Notwendigkeit, Daten in einem allgemein akzeptierten Format wie PDF freizugeben. Das Exportieren benutzerdefinierter Eigenschaften aus Excel-Dateien in PDFs kann ohne die richtigen Tools eine gewaltige Aufgabe sein. Hier kommt Aspose.Cells für .NET ins Spiel und bietet eine robuste Lösung, um diesen Prozess nahtlos und effizient zu gestalten. In diesem Artikel führen wir Sie durch die erforderlichen Schritte zum Exportieren benutzerdefinierter Eigenschaften aus einer Excel-Datei in das PDF-Format mit Aspose.Cells für .NET. Am Ende dieses Handbuchs verfügen Sie über das gesamte Wissen, das Sie benötigen, um diese Aufgabe direkt anzugehen!
## Voraussetzungen
Bevor wir ins Detail gehen, gehen wir einige Voraussetzungen durch, die Sie benötigen:
1. .NET-Umgebung: Stellen Sie sicher, dass Sie eine .NET-Entwicklungsumgebung wie Visual Studio eingerichtet haben.
2.  Aspose.Cells für .NET: Laden Sie die neueste Version von Aspose.Cells für .NET herunter und installieren Sie sie. Sie finden sie[Hier](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie den Codebeispielen leichter folgen.
## Pakete importieren
Um zu beginnen, müssen Sie zunächst die erforderlichen Pakete in Ihr Projekt importieren. So können Sie das tun:
### Neues Projekt erstellen
1. Öffnen Sie Visual Studio.
2. Klicken Sie auf „Neues Projekt erstellen“.
3. Wählen Sie je nach Wunsch „Konsolen-App (.NET Framework)“ oder „Konsolen-App (.NET Core)“ und klicken Sie auf „Weiter“.
4. Geben Sie Ihrem Projekt einen Namen und klicken Sie auf „Erstellen“.
### Fügen Sie Aspose.Cells zu Ihrem Projekt hinzu
Um Aspose.Cells zu verwenden, müssen Sie es als Referenz hinzufügen:
1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt.
2. Wählen Sie „NuGet-Pakete verwalten“ aus.
3. Suchen Sie nach „Aspose.Cells“ und installieren Sie die neueste Version.
Nachdem Ihre Pakete nun importiert sind, können Sie mit der Codierung beginnen.

```csharp
using System.IO;
using System.Web;
using Aspose.Cells;
using System;
```

Kommen wir nun zum entscheidenden Teil: der Schritt-für-Schritt-Anleitung zum Exportieren benutzerdefinierter Eigenschaften aus einer Excel-Datei in ein PDF-Dokument. Schnall dich an!
## Schritt 1: Richten Sie Ihre Verzeichnisse ein
Bevor Sie mit dem Codieren beginnen, müssen Sie Ihre Eingabe- und Ausgabeverzeichnisse definieren. Hier lesen Sie die Excel-Datei und hier wird das generierte PDF gespeichert.
```csharp
// Eingabeverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
 Ersetzen Sie in diesem Codeausschnitt`"Your Document Directory"` durch den tatsächlichen Pfad, in dem sich Ihre Dateien befinden oder in dem Sie sie speichern möchten.
## Schritt 2: Laden Sie die Excel-Datei
 Als nächstes müssen Sie die Excel-Datei laden, die die benutzerdefinierten Eigenschaften enthält. Dies geschieht mit dem`Workbook` Klasse in Aspose.Cells.
```csharp
// Laden Sie eine Excel-Datei mit benutzerdefinierten Eigenschaften
Workbook workbook = new Workbook(sourceDir + "sampleWithCustProps.xlsx");
```
 Stellen Sie hier sicher, dass`sampleWithCustProps.xlsx` ist der Name Ihres Excel-Dokuments und es sollte sich im angegebenen Verzeichnis befinden.
## Schritt 3: PdfSaveOptions erstellen
 Sobald Ihre Arbeitsmappe geladen ist, ist es an der Zeit, die Optionen zum Speichern der PDF einzurichten. Sie erstellen eine Instanz von`PdfSaveOptions` und legen Sie die entsprechenden Eigenschaften fest.
```csharp
// Erstellen Sie eine Instanz von PdfSaveOptions und übergeben Sie SaveFormat an den Konstruktor
Aspose.Cells.PdfSaveOptions pdfSaveOpt = new Aspose.Cells.PdfSaveOptions();
```
Diese Zeile initiiert die PDF-Speicheroptionen, die Sie in Kürze anpassen werden.
## Schritt 4: Konfigurieren des Exports benutzerdefinierter Eigenschaften
Sie müssen angeben, wie die benutzerdefinierten Eigenschaften exportiert werden sollen. In diesem Fall verwenden wir die`Standard` Option zum Exportieren.
```csharp
// Legen Sie die Eigenschaft CustomPropertiesExport auf PdfCustomPropertiesExport.Standard fest.
pdfSaveOpt.CustomPropertiesExport = Aspose.Cells.Rendering.PdfCustomPropertiesExport.Standard;
```
Durch Festlegen dieser Eigenschaft werden die benutzerdefinierten Eigenschaften aus Ihrem Excel-Dokument in das PDF aufgenommen.
## Schritt 5: Speichern Sie die Arbeitsmappe als PDF
Nachdem nun alles eingestellt ist, ist es an der Zeit, Ihre Arbeitsmappe mit den definierten Optionen als PDF-Datei zu speichern.
```csharp
// Speichern Sie die Arbeitsmappe im PDF-Format, während Sie das Objekt von PdfSaveOptions übergeben
workbook.Save(outputDir + "outSampleWithCustProps.pdf", pdfSaveOpt);
```
 In dieser Zeile`outSampleWithCustProps.pdf` ist der Name Ihrer neuen PDF-Datei. Stellen Sie daher sicher, dass er eindeutig ist, um ein Überschreiben zu vermeiden.
## Schritt 6: Erfolg bestätigen
Bestätigen wir abschließend, dass der Vorgang erfolgreich war, indem wir eine Meldung auf der Konsole ausgeben:
```csharp
Console.WriteLine("ExportCustomPropertiesToPDF executed successfully.");
```
Diese Meldung wird in Ihrer Konsole angezeigt, um Sie darüber zu informieren, dass alles reibungslos verlaufen ist.
## Abschluss
Und da haben Sie es! Sie haben gelernt, wie Sie benutzerdefinierte Eigenschaften aus einer Excel-Datei mit Aspose.Cells für .NET in ein PDF-Dokument exportieren. Dieser Ansatz erleichtert nicht nur die Datenfreigabe, sondern stellt auch sicher, dass die benutzerdefinierten Metadaten, die Sie in Ihre Excel-Dateien eingegeben haben, im PDF-Format intakt und zugänglich bleiben. Egal, ob Sie mit Projektdokumentation, Berichten oder Datenzusammenfassungen arbeiten, diese Methode ist eine wertvolle Ergänzung Ihres Toolkits. Zögern Sie nicht, die Aspose.Cells-Dokumentation zu erkunden[Hier](https://reference.aspose.com/cells/net/) für noch leistungsfähigere Funktionalitäten.
## Häufig gestellte Fragen
### Was sind benutzerdefinierte Eigenschaften in Excel?
Benutzerdefinierte Eigenschaften sind Metadatenfelder, die Sie einer Excel-Arbeitsmappe zuordnen können, z. B. den Namen des Autors, den Titel oder benutzerdefinierte Daten, die Ihren Anforderungen entsprechen.
### Kann ich benutzerdefinierte Eigenschaften in verschiedene Formate exportieren?
Ja, neben PDF ermöglichen auch andere von Aspose.Cells unterstützte Formate den Export benutzerdefinierter Eigenschaften, je nach Bedarf.
### Ist für Aspose.Cells eine Lizenz erforderlich?
Für die kommerzielle Nutzung ist eine Lizenz erforderlich, Sie können das Produkt aber auch zunächst kostenlos testen. Schauen Sie sich die[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) Optionen.
### Wo finde ich Unterstützung für Aspose.Cells?
 Sie können Community-Support finden und Fragen im Aspose-Forum stellen[Hier](https://forum.aspose.com/c/cells/9).
### Kann ich die gespeicherte PDF-Ausgabe anpassen?
 Absolut! Die`PdfSaveOptions` Die Klasse bietet verschiedene Eigenschaften, die eine detaillierte Anpassung der PDF-Ausgabe ermöglichen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
