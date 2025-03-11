---
title: Dokumentversion einer Excel-Datei programmgesteuert in .NET angeben
linktitle: Dokumentversion einer Excel-Datei programmgesteuert in .NET angeben
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie anhand schrittweiser Anleitungen, wie Sie Dokumenteigenschaften wie Version, Autor und Titel in einer Excel-Datei programmgesteuert mit Aspose.Cells für .NET angeben.
weight: 12
url: /de/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dokumentversion einer Excel-Datei programmgesteuert in .NET angeben

## Einführung
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler Excel-Dateien mühelos programmgesteuert bearbeiten können. Egal, ob Sie Excel-Dateien von Grund auf neu erstellen oder vorhandene ändern möchten, Aspose.Cells bietet eine umfassende API, um Ihre Ziele zu erreichen. Eine solche Funktion ist das Angeben von Dokumenteigenschaften wie Version, Autor oder Titel. In diesem Tutorial erfahren Sie, wie Sie die Dokumentversion einer Excel-Datei programmgesteuert mit Aspose.Cells für .NET angeben.
## Voraussetzungen
Bevor wir in die Details eintauchen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um diesem Tutorial folgen zu können:
1. Aspose.Cells für .NET: Sie können die neueste Version herunterladen[Hier](https://releases.aspose.com/cells/net/) Wenn Sie noch keine Lizenz erworben haben, können Sie sich für eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) um die Funktionen zu erkunden.
2. .NET-Entwicklungsumgebung: Sie können Visual Studio oder jede .NET-kompatible IDE verwenden.
3. Grundkenntnisse in C#: Wenn Sie die C#-Programmierung verstehen, können Sie den Schritten leichter folgen.
## Pakete importieren
Bevor Sie mit dem Codieren beginnen können, müssen Sie die erforderlichen Namespaces aus der Aspose.Cells-Bibliothek importieren. Dadurch erhalten Sie Zugriff auf die Klassen und Methoden, die für die Excel-Dateibearbeitung erforderlich sind.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Diese beiden Namespaces sind für die Interaktion mit der Arbeitsmappe und ihren integrierten Dokumenteigenschaften von entscheidender Bedeutung.
Lassen Sie uns nun den Vorgang zum Angeben von Dokumenteigenschaften in einer Excel-Datei, einschließlich Version, Titel und Autor, aufschlüsseln.
## Schritt 1: Initialisieren Sie das Arbeitsmappenobjekt
 Der erste Schritt besteht in der Erstellung einer neuen Instanz des`Workbook` Objekt. Dieses Objekt stellt die gesamte Excel-Datei dar, mit der Sie arbeiten.
```csharp
Workbook wb = new Workbook();
```
 Der`Workbook`Klasse stellt eine Darstellung einer Excel-Datei bereit. Indem wir sie instanziieren, erstellen wir eine leere Excel-Arbeitsmappe, die wir bearbeiten können.
## Schritt 2: Zugriff auf integrierte Dokumenteigenschaften
 Aspose.Cells bietet integrierte Dokumenteigenschaften, darunter Felder wie Titel, Autor und Dokumentversion. Sie können auf diese Eigenschaften über das`BuiltInDocumentProperties`Sammlung.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
 Der`BuiltInDocumentPropertyCollection` Die Klasse bietet Zugriff auf eine Sammlung integrierter Dokumenteigenschaften wie Titel, Autor und andere Metadaten, die normalerweise mit dem Dokument verknüpft sind.
## Schritt 3: Legen Sie den Titel des Excel-Dokuments fest
Als nächstes legen wir den Titel des Excel-Dokuments fest. Diese Metadaten helfen später bei der Identifizierung und Verwaltung der Datei.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Das Festlegen des Titels ist für die Dokumentorganisation wichtig. Diese Metadaten sind in den Dateieigenschaften sichtbar und können von externen Systemen verwendet werden, um das Dokument effektiver zu katalogisieren oder zu identifizieren.
## Schritt 4: Autor angeben
Außerdem kann der Autor des Dokuments angegeben werden, um anzuzeigen, wer die Datei erstellt oder geändert hat.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Dieser Schritt hilft dabei, das Dokument seinem Ersteller zuzuordnen und stellt zusätzliche Metadaten für die Dokumentenverwaltung oder Zusammenarbeitsszenarien bereit.
## Schritt 5: Dokumentversion angeben
Eine der wichtigsten Eigenschaften, die wir in diesem Tutorial behandeln, ist die Dokumentversion. In diesem Schritt können Sie die Version des Dokuments angeben, was hilfreich ist, wenn Sie in Umgebungen arbeiten, die eine Versionskontrolle erfordern.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Durch das Festlegen der Dokumentversion wird klar, welche Version des Dokuments oder der Bibliothek zum Erstellen der Datei verwendet wurde. Dies ist insbesondere in Umgebungen wichtig, in denen Dateirevisionen oder die Kompatibilität mit verschiedenen Bibliotheksversionen nachverfolgt werden müssen.
## Schritt 6: Speichern Sie die Excel-Datei
 Abschließend können Sie die Excel-Datei mit allen Eigenschaften speichern, die Sie gerade festgelegt haben. Aspose.Cells ermöglicht Ihnen, die Datei in verschiedenen Formaten zu speichern, aber für dieses Beispiel bleiben wir beim`.xlsx` Format.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
 Der`Save` Methode wird verwendet, um die Datei in dem angegebenen Verzeichnis zu speichern. Hier speichern wir sie als Excel-Datei im`.xlsx`Format. Bei Bedarf unterstützt Aspose.Cells auch Formate wie`.xls`, `.csv` , Und`.pdf`, und bietet Flexibilität basierend auf den Anforderungen Ihres Projekts.
## Abschluss
In diesem Tutorial haben wir gezeigt, wie man Dokumenteigenschaften, insbesondere die Dokumentversion, in einer Excel-Datei mit Aspose.Cells für .NET angibt. Aspose.Cells ist ein äußerst flexibles und leistungsstarkes Tool, mit dem Sie Excel-Dateien programmgesteuert bearbeiten können. Es ist daher eine große Hilfe für jeden .NET-Entwickler, der mit Tabellenkalkulationen arbeitet.
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells andere integrierte Eigenschaften ändern?  
Ja, Sie können andere integrierte Eigenschaften wie beispielsweise den Betreff, Schlüsselwörter und Kommentare ändern.
### Welche Dateiformate werden von Aspose.Cells unterstützt?  
 Aspose.Cells unterstützt eine Vielzahl von Formaten, darunter`.xls`, `.xlsx`, `.csv`, `.pdf`, und mehr.
### Benötige ich eine Lizenz, um Aspose.Cells für .NET zu verwenden?  
 Sie können Aspose.Cells erkunden mit einem[Kostenlose Testversion](https://releases.aspose.com/) oder bewerben Sie sich für eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) für erweiterte Tests.
### Kann ich Aspose.Cells in einer Webanwendung verwenden?  
Ja, Aspose.Cells kann sowohl in Desktop- als auch in Webanwendungen verwendet werden. Es ist äußerst vielseitig und lässt sich gut in .NET-Webframeworks integrieren.
### Wo erhalte ich Support für Aspose.Cells?  
 Sie erhalten Zugang zur Community und zum Support über die[Aspose.Cells Support-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
