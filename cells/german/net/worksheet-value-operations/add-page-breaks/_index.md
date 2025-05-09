---
"description": "Erfahren Sie in dieser Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET horizontale und vertikale Seitenumbrüche in Excel hinzufügen. Gestalten Sie Ihre Excel-Dateien druckerfreundlich."
"linktitle": "Fügen Sie mit Aspose.Cells Seitenumbrüche im Arbeitsblatt hinzu"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Fügen Sie mit Aspose.Cells Seitenumbrüche im Arbeitsblatt hinzu"
"url": "/de/net/worksheet-value-operations/add-page-breaks/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Fügen Sie mit Aspose.Cells Seitenumbrüche im Arbeitsblatt hinzu

## Einführung
In diesem Tutorial führen wir Sie durch das Hinzufügen horizontaler und vertikaler Seitenumbrüche zu Ihrem Excel-Arbeitsblatt. Sie erhalten außerdem eine Schritt-für-Schritt-Anleitung zur einfachen Bearbeitung von Seitenumbrüchen mit Aspose.Cells für .NET. Am Ende dieser Anleitung werden Sie diese Techniken sicher in Ihren eigenen Projekten anwenden können. Los geht‘s!
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie bereit sind, diesem Tutorial zu folgen. Hier sind einige Voraussetzungen:
- Visual Studio: Sie müssen Visual Studio auf Ihrem System installiert haben.
- Aspose.Cells für .NET: Sie sollten die Aspose.Cells-Bibliothek installiert haben. Falls noch nicht geschehen, keine Sorge! Sie können eine kostenlose Testversion herunterladen, um loszulegen. (Sie erhalten sie [Hier](https://releases.aspose.com/cells/net/)).
- .NET Framework: Dieses Tutorial setzt voraus, dass Sie mit .NET Framework oder .NET Core arbeiten. Wenn Sie eine andere Umgebung verwenden, kann der Prozess leicht abweichen.
Darüber hinaus sollten Sie über Grundkenntnisse in der C#-Programmierung und dem Konzept von Seitenumbrüchen in Excel verfügen.
## Pakete importieren
Um mit Aspose.Cells arbeiten zu können, müssen wir die entsprechenden Namespaces in unser Projekt importieren. Dadurch können wir auf die von Aspose.Cells bereitgestellten Funktionen zur Bearbeitung von Excel-Dateien zugreifen.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nachdem Sie diese Namespaces importiert haben, können Sie mit der Interaktion mit Excel-Dateien beginnen und verschiedene Änderungen vornehmen, einschließlich dem Hinzufügen von Seitenumbrüchen.
Nachdem Sie alles eingerichtet haben, gehen wir nun die Schritte zum Hinzufügen von Seitenumbrüchen zu Ihrem Arbeitsblatt durch. Wir werden jeden Teil des Prozesses detailliert aufschlüsseln und jede Codezeile erklären.
## Schritt 1: Richten Sie Ihre Arbeitsmappe ein
Zuerst müssen Sie eine neue Arbeitsmappe erstellen. Die `Workbook` Die Klasse in Aspose.Cells stellt eine Excel-Arbeitsmappe dar und ist der Ausgangspunkt für die Bearbeitung von Excel-Dateien.
```csharp
// Definieren Sie den Pfad zum Verzeichnis, in dem Ihre Datei gespeichert wird
string dataDir = "Your Document Directory";
// Erstellen eines neuen Arbeitsmappenobjekts
Workbook workbook = new Workbook();
```
In diesem Code:
- `dataDir` gibt an, wo Ihre Datei gespeichert wird.
- Der `Workbook` Es wird ein Objekt erstellt, das zum Speichern und Bearbeiten Ihrer Excel-Datei verwendet wird.
## Schritt 2: Horizontalen Seitenumbruch hinzufügen
Als Nächstes fügen wir dem Arbeitsblatt einen horizontalen Seitenumbruch hinzu. Ein horizontaler Seitenumbruch teilt das Arbeitsblatt horizontal in zwei Teile und bestimmt so, wo der Inhalt beim Drucken vertikal auf eine neue Seite umgebrochen wird.
```csharp
// Fügen Sie in Zeile 30 einen horizontalen Seitenumbruch hinzu
workbook.Worksheets[0].HorizontalPageBreaks.Add("Y30");
```
In diesem Beispiel:
- `Worksheets[0]` bezieht sich auf das erste Blatt in der Arbeitsmappe (denken Sie daran, dass Arbeitsblätter nullindiziert sind).
- `HorizontalPageBreaks.Add("Y30")` fügt einen Seitenumbruch in Zeile 30 hinzu. Dies bedeutet, dass der Inhalt vor Zeile 30 auf einer Seite angezeigt wird und alles darunter auf einer neuen Seite beginnt.
## Schritt 3: Vertikalen Seitenumbruch hinzufügen
Ebenso können Sie einen vertikalen Seitenumbruch hinzufügen. Dadurch wird das Arbeitsblatt an einer bestimmten Spalte umgebrochen. Der Inhalt links vom Umbruch wird auf einer Seite und der Inhalt rechts vom Umbruch auf der nächsten Seite angezeigt.
```csharp
// Fügen Sie in Spalte Y einen vertikalen Seitenumbruch hinzu
workbook.Worksheets[0].VerticalPageBreaks.Add("Y30");
```
Hier:
- Der `VerticalPageBreaks.Add("Y30")` Die Methode fügt einen vertikalen Seitenumbruch in Spalte Y (also nach der 25. Spalte) ein. Dadurch entsteht ein Seitenumbruch zwischen den Spalten X und Y.
## Schritt 4: Speichern der Arbeitsmappe
Nachdem Sie Ihre Seitenumbrüche hinzugefügt haben, speichern Sie die Arbeitsmappe im letzten Schritt in einer Datei. Sie können den Pfad angeben, in dem Sie die Excel-Datei speichern möchten.
```csharp
// Speichern Sie die Excel-Datei
workbook.Save(dataDir + "AddingPageBreaks_out.xls");
```
Dadurch wird die Arbeitsmappe mit den hinzugefügten Seitenumbrüchen im angegebenen Dateipfad gespeichert (`AddingPageBreaks_out.xls`).
## Abschluss
Das Einfügen von Seitenumbrüchen in Excel ist eine wichtige Funktion, wenn Sie mit großen Datensätzen arbeiten oder Dokumente für den Druck vorbereiten. Mit Aspose.Cells für .NET können Sie das Einfügen horizontaler und vertikaler Seitenumbrüche in Ihre Excel-Arbeitsblätter einfach automatisieren und so sicherstellen, dass Ihre Dokumente übersichtlich und leicht lesbar sind.
## Häufig gestellte Fragen
### Wie füge ich in Aspose.Cells für .NET mehrere Seitenumbrüche hinzu?
Sie können mehrere Seitenumbrüche hinzufügen, indem Sie einfach die `HoderizontalPageBreaks.Add()` or `VerticalPageBreaks.Add()` Methoden mehrmals mit unterschiedlichen Zellbezügen.
### Kann ich in einem bestimmten Arbeitsblatt einer Arbeitsmappe Seitenumbrüche hinzufügen?
Ja, Sie können das Arbeitsblatt angeben, indem Sie das `Worksheets[index]` Eigentum, wo `index` ist der nullbasierte Index des Arbeitsblatts.
### Wie entferne ich einen Seitenumbruch in Aspose.Cells für .NET?
Einen Seitenumbruch können Sie mit dem `HoderizontalPageBreaks.RemoveAt()` or `VerticalPageBreaks.RemoveAt()` Methoden, indem Sie den Index des Seitenumbruchs angeben, den Sie entfernen möchten.
### Was ist, wenn ich Seitenumbrüche automatisch basierend auf der Inhaltsgröße hinzufügen möchte?
Aspose.Cells bietet keine automatische Funktion zum Hinzufügen von Seitenumbrüchen basierend auf der Inhaltsgröße, Sie können jedoch programmgesteuert berechnen, wo Umbrüche basierend auf der Zeilen-/Spaltenanzahl erfolgen sollen.
### Kann ich Seitenumbrüche basierend auf einem bestimmten Zellbereich festlegen?
Ja, Sie können Seitenumbrüche für jede Zelle oder jeden Bereich festlegen, indem Sie den entsprechenden Zellbezug angeben, beispielsweise „A1“ oder „B15“.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}