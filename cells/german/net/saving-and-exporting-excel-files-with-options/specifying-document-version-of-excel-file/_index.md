---
"description": "Erfahren Sie anhand schrittweiser Anleitungen, wie Sie Dokumenteigenschaften wie Version, Autor und Titel in einer Excel-Datei programmgesteuert mit Aspose.Cells für .NET angeben."
"linktitle": "Programmgesteuertes Festlegen der Dokumentversion einer Excel-Datei in .NET"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Programmgesteuertes Festlegen der Dokumentversion einer Excel-Datei in .NET"
"url": "/de/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Programmgesteuertes Festlegen der Dokumentversion einer Excel-Datei in .NET

## Einführung
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler Excel-Dateien mühelos programmgesteuert bearbeiten können. Egal, ob Sie Excel-Dateien von Grund auf neu erstellen oder vorhandene bearbeiten möchten – Aspose.Cells bietet eine umfassende API, mit der Sie Ihre Ziele erreichen. Eine dieser Funktionen ist die Angabe von Dokumenteigenschaften wie Version, Autor oder Titel. Dieses Tutorial zeigt Ihnen, wie Sie die Dokumentversion einer Excel-Datei programmgesteuert mit Aspose.Cells für .NET festlegen.
## Voraussetzungen
Bevor wir in die Details eintauchen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um diesem Tutorial zu folgen:
1. Aspose.Cells für .NET: Sie können die neueste Version herunterladen [Hier](https://releases.aspose.com/cells/net/). Wenn Sie noch keine Lizenz erworben haben, können Sie sich für eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) um die Funktionen zu erkunden.
2. .NET-Entwicklungsumgebung: Sie können Visual Studio oder jede .NET-kompatible IDE verwenden.
3. Grundkenntnisse in C#: Wenn Sie die C#-Programmierung verstehen, können Sie den Anweisungen leichter folgen.
## Pakete importieren
Bevor Sie mit dem Programmieren beginnen können, müssen Sie die erforderlichen Namespaces aus der Aspose.Cells-Bibliothek importieren. Dadurch erhalten Sie Zugriff auf die Klassen und Methoden, die für die Bearbeitung von Excel-Dateien erforderlich sind.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Diese beiden Namespaces sind für die Interaktion mit der Arbeitsmappe und ihren integrierten Dokumenteigenschaften von entscheidender Bedeutung.
Lassen Sie uns nun den Vorgang zum Angeben von Dokumenteigenschaften in einer Excel-Datei, einschließlich Version, Titel und Autor, aufschlüsseln.
## Schritt 1: Initialisieren des Arbeitsmappenobjekts
Der erste Schritt besteht darin, eine neue Instanz des `Workbook` Objekt. Dieses Objekt stellt die gesamte Excel-Datei dar, mit der Sie arbeiten.
```csharp
Workbook wb = new Workbook();
```
Der `Workbook` Die Klasse stellt eine Darstellung einer Excel-Datei dar. Durch die Instanziierung erstellen wir eine leere Excel-Arbeitsmappe, die wir bearbeiten können.
## Schritt 2: Zugriff auf integrierte Dokumenteigenschaften
Aspose.Cells bietet integrierte Dokumenteigenschaften, darunter Felder wie Titel, Autor und Dokumentversion. Sie können auf diese Eigenschaften zugreifen über `BuiltInDocumentProperties` Sammlung.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
Der `BuiltInDocumentPropertyCollection` Die Klasse bietet Zugriff auf eine Sammlung integrierter Dokumenteigenschaften, wie etwa Titel, Autor und andere Metadaten, die normalerweise mit dem Dokument verknüpft sind.
## Schritt 3: Legen Sie den Titel des Excel-Dokuments fest
Als Nächstes legen wir den Titel des Excel-Dokuments fest. Diese Metadaten helfen später bei der Identifizierung und Verwaltung der Datei.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Das Festlegen des Titels ist wichtig für die Dokumentorganisation. Diese Metadaten sind in den Dateieigenschaften sichtbar und können von externen Systemen zur effektiveren Katalogisierung oder Identifizierung des Dokuments verwendet werden.
## Schritt 4: Autor angeben
Außerdem kann der Autor des Dokuments angegeben werden, um anzugeben, wer die Datei erstellt oder geändert hat.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Dieser Schritt hilft dabei, das Dokument seinem Ersteller zuzuordnen und stellt zusätzliche Metadaten für die Dokumentenverwaltung oder Zusammenarbeitsszenarien bereit.
## Schritt 5: Dokumentversion angeben
Eine der wichtigsten Eigenschaften, die wir in diesem Tutorial behandeln, ist die Dokumentversion. In diesem Schritt können Sie die Version des Dokuments angeben, was in Umgebungen mit Versionskontrolle hilfreich ist.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Durch Festlegen der Dokumentversion können Sie nachvollziehen, welche Version des Dokuments oder der Bibliothek zum Erstellen der Datei verwendet wurde. Dies ist besonders wichtig in Umgebungen, in denen Dateirevisionen oder die Kompatibilität mit verschiedenen Bibliotheksversionen nachverfolgt werden müssen.
## Schritt 6: Speichern Sie die Excel-Datei
Abschließend können Sie die Excel-Datei mit allen zuvor festgelegten Eigenschaften speichern. Aspose.Cells ermöglicht Ihnen das Speichern der Datei in verschiedenen Formaten. Für dieses Beispiel verwenden wir jedoch das `.xlsx` Format.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
Der `Save` Die Methode wird verwendet, um die Datei in Ihrem angegebenen Verzeichnis zu speichern. Hier speichern wir sie als Excel-Datei im `.xlsx` Format. Bei Bedarf unterstützt Aspose.Cells auch Formate wie `.xls`, `.csv`, Und `.pdf`, und bietet Flexibilität basierend auf den Anforderungen Ihres Projekts.
## Abschluss
In diesem Tutorial haben wir gezeigt, wie Sie Dokumenteigenschaften, insbesondere die Dokumentversion, in einer Excel-Datei mit Aspose.Cells für .NET festlegen. Aspose.Cells ist ein äußerst flexibles und leistungsstarkes Tool, mit dem Sie Excel-Dateien programmgesteuert bearbeiten können. Es ist daher eine große Hilfe für jeden .NET-Entwickler, der mit Tabellenkalkulationen arbeitet.
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells andere integrierte Eigenschaften ändern?  
Ja, Sie können andere integrierte Eigenschaften wie beispielsweise Betreff, Schlüsselwörter und Kommentare ändern.
### Welche Dateiformate werden von Aspose.Cells unterstützt?  
Aspose.Cells unterstützt eine Vielzahl von Formaten, darunter `.xls`, `.xlsx`, `.csv`, `.pdf`und mehr.
### Benötige ich eine Lizenz, um Aspose.Cells für .NET zu verwenden?  
Sie können Aspose.Cells erkunden mit einem [kostenlose Testversion](https://releases.aspose.com/) oder bewerben Sie sich für eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) für erweiterte Tests.
### Kann ich Aspose.Cells in einer Webanwendung verwenden?  
Ja, Aspose.Cells kann sowohl in Desktop- als auch in Webanwendungen verwendet werden. Es ist äußerst vielseitig und lässt sich gut in .NET-Web-Frameworks integrieren.
### Wo erhalte ich Support für Aspose.Cells?  
Sie können auf die Community und den Support zugreifen über die [Aspose.Cells Support-Forum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}