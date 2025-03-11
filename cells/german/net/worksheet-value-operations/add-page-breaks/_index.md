---
title: Fügen Sie mit Aspose.Cells Seitenumbrüche in das Arbeitsblatt ein
linktitle: Fügen Sie mit Aspose.Cells Seitenumbrüche in das Arbeitsblatt ein
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET horizontale und vertikale Seitenumbrüche in Excel hinzufügen. Machen Sie Ihre Excel-Dateien druckerfreundlich.
weight: 10
url: /de/net/worksheet-value-operations/add-page-breaks/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Fügen Sie mit Aspose.Cells Seitenumbrüche in das Arbeitsblatt ein

## Einführung
In diesem Tutorial führen wir Sie durch den Prozess des Hinzufügens horizontaler und vertikaler Seitenumbrüche zu Ihrem Excel-Arbeitsblatt. Sie erhalten außerdem eine Schritt-für-Schritt-Anleitung zur Verwendung von Aspose.Cells für .NET zur einfachen Bearbeitung von Seitenumbrüchen. Am Ende dieser Anleitung können Sie diese Techniken problemlos in Ihren eigenen Projekten verwenden. Lassen Sie uns anfangen!
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie bereit sind, diesem Tutorial zu folgen. Hier sind einige Voraussetzungen:
- Visual Studio: Sie müssen Visual Studio auf Ihrem System installiert haben.
-  Aspose.Cells für .NET: Sie sollten die Aspose.Cells-Bibliothek installiert haben. Wenn Sie das noch nicht getan haben, machen Sie sich keine Sorgen! Sie können eine kostenlose Testversion herunterladen, um loszulegen. (Sie erhalten sie[Hier](https://releases.aspose.com/cells/net/)).
- .NET Framework: Dieses Tutorial setzt voraus, dass Sie mit .NET Framework oder .NET Core arbeiten. Wenn Sie eine andere Umgebung verwenden, kann der Vorgang leicht abweichen.
Darüber hinaus sollten Sie über Grundkenntnisse der C#-Programmierung und des Konzepts von Seitenumbrüchen in Excel verfügen.
## Pakete importieren
Um mit Aspose.Cells arbeiten zu können, müssen wir die entsprechenden Namespaces in unser Projekt importieren. Dadurch können wir auf die von Aspose.Cells bereitgestellte Funktionalität zugreifen, um Excel-Dateien zu bearbeiten.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nachdem Sie diese Namespaces importiert haben, können Sie mit der Interaktion mit Excel-Dateien beginnen und verschiedene Änderungen vornehmen, darunter das Hinzufügen von Seitenumbrüchen.
Nachdem Sie nun alles eingerichtet haben, gehen wir die Schritte durch, um Ihrem Arbeitsblatt Seitenumbrüche hinzuzufügen. Wir werden jeden Teil des Prozesses aufschlüsseln und jede Codezeile im Detail erklären.
## Schritt 1: Richten Sie Ihre Arbeitsmappe ein
 Zuerst müssen Sie eine neue Arbeitsmappe erstellen. Die`Workbook` Die Klasse in Aspose.Cells stellt eine Excel-Arbeitsmappe dar und ist der Ausgangspunkt für die Bearbeitung von Excel-Dateien.
```csharp
// Geben Sie den Pfad zum Verzeichnis an, in dem Ihre Datei gespeichert wird
string dataDir = "Your Document Directory";
// Erstellen eines neuen Workbook-Objekts
Workbook workbook = new Workbook();
```
In diesem Code:
- `dataDir` gibt an, wo Ihre Datei gespeichert wird.
-  Der`Workbook` -Objekt erstellt, das zum Speichern und Bearbeiten Ihrer Excel-Datei verwendet wird.
## Schritt 2: Horizontalen Seitenumbruch hinzufügen
Als Nächstes fügen wir dem Arbeitsblatt einen horizontalen Seitenumbruch hinzu. Ein horizontaler Seitenumbruch teilt das Arbeitsblatt horizontal in zwei Teile, d. h. er bestimmt, wo der Inhalt beim Drucken vertikal auf eine neue Seite umgebrochen wird.
```csharp
//Fügen Sie in Zeile 30 einen horizontalen Seitenumbruch hinzu
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
In diesem Beispiel:
- `Worksheets[0]` bezieht sich auf das erste Blatt in der Arbeitsmappe (denken Sie daran, dass Arbeitsblätter nullindiziert sind).
- `HorizontalPageBreaks.Add("Y30")` fügt einen Seitenumbruch in Zeile 30 hinzu. Dies bedeutet, dass der Inhalt vor Zeile 30 auf einer Seite angezeigt wird und alles darunter auf einer neuen Seite beginnt.
## Schritt 3: Vertikalen Seitenumbruch hinzufügen
Ebenso können Sie einen vertikalen Seitenumbruch hinzufügen. Dadurch wird das Arbeitsblatt an einer bestimmten Spalte umgebrochen, sodass der Inhalt links vom Umbruch auf einer Seite und der Inhalt rechts vom Umbruch auf der nächsten Seite angezeigt wird.
```csharp
// Fügen Sie in Spalte Y einen vertikalen Seitenumbruch hinzu
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
Hier:
-  Der`VerticalPageBreaks.Add("Y30")` Methode fügt einen vertikalen Seitenumbruch in Spalte Y ein (also nach der 25. Spalte). Dadurch wird ein Seitenumbruch zwischen den Spalten X und Y erstellt.
## Schritt 4: Speichern der Arbeitsmappe
Nachdem Sie Ihre Seitenumbrüche hinzugefügt haben, besteht der letzte Schritt darin, die Arbeitsmappe in einer Datei zu speichern. Sie können den Pfad angeben, in dem Sie die Excel-Datei speichern möchten.
```csharp
// Speichern Sie die Excel-Datei
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
Dadurch wird die Arbeitsmappe mit den hinzugefügten Seitenumbrüchen im angegebenen Dateipfad gespeichert (`AddingPageBreaks_out.xls`).
## Abschluss
Das Hinzufügen von Seitenumbrüchen in Excel ist eine wichtige Funktion, wenn Sie mit großen Datensätzen arbeiten oder Dokumente für den Druck vorbereiten. Mit Aspose.Cells für .NET können Sie das Einfügen von horizontalen und vertikalen Seitenumbrüchen in Ihre Excel-Arbeitsblätter problemlos automatisieren und so sicherstellen, dass Ihre Dokumente gut organisiert und leicht zu lesen sind.
## Häufig gestellte Fragen
### Wie füge ich in Aspose.Cells für .NET mehrere Seitenumbrüche hinzu?
 Sie können mehrere Seitenumbrüche hinzufügen, indem Sie einfach den`HorizontalPageBreaks.Add()` oder`VerticalPageBreaks.Add()` Methoden mehrmals mit unterschiedlichen Zellbezügen.
### Kann ich in einem bestimmten Arbeitsblatt einer Arbeitsmappe Seitenumbrüche hinzufügen?
 Ja, Sie können das Arbeitsblatt angeben, indem Sie`Worksheets[index]` Eigentum, wo`index` ist der nullbasierte Index des Arbeitsblatts.
### Wie entferne ich einen Seitenumbruch in Aspose.Cells für .NET?
 Einen Seitenumbruch können Sie mit dem`HorizontalPageBreaks.RemoveAt()` oder`VerticalPageBreaks.RemoveAt()` Methoden, indem Sie den Index des Seitenumbruchs angeben, den Sie entfernen möchten.
### Was ist, wenn ich Seitenumbrüche automatisch basierend auf der Inhaltsgröße hinzufügen möchte?
Aspose.Cells bietet keine automatische Funktion zum Hinzufügen von Seitenumbrüchen basierend auf der Inhaltsgröße, aber Sie können basierend auf der Zeilen-/Spaltenanzahl programmgesteuert berechnen, wo Umbrüche erfolgen sollen.
### Kann ich Seitenumbrüche basierend auf einem bestimmten Zellbereich festlegen?
Ja, Sie können Seitenumbrüche für jede Zelle oder jeden Bereich festlegen, indem Sie den entsprechenden Zellbezug angeben, beispielsweise „A1“ oder „B15“.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
