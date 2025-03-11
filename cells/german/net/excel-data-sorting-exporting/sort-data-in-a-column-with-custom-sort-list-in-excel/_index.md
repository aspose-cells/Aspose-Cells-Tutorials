---
title: Sortieren Sie Daten in einer Spalte mit benutzerdefinierter Sortierliste in Excel
linktitle: Sortieren Sie Daten in einer Spalte mit benutzerdefinierter Sortierliste in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem umfassenden Tutorial, wie Sie mit Aspose.Cells für .NET Daten in Excel mithilfe einer benutzerdefinierten Sortierliste sortieren.
weight: 10
url: /de/net/excel-data-sorting-exporting/sort-data-in-a-column-with-custom-sort-list-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sortieren Sie Daten in einer Spalte mit benutzerdefinierter Sortierliste in Excel

## Einführung

Dieses Tutorial führt Sie durch den Prozess der Einrichtung Ihres Projekts, des Ladens einer Excel-Datei und des Sortierens von Daten innerhalb eines angegebenen Bereichs mithilfe einer benutzerdefinierten Sortierreihenfolge. Indem Sie dieser Anleitung folgen, sammeln Sie praktische Erfahrungen, die Ihre Datenverwaltungsfähigkeiten und die Benutzerfreundlichkeit der Aspose.Cells-Bibliothek verbessern können.

## Voraussetzungen

Bevor wir uns in das Lernprogramm stürzen, wollen wir einige Voraussetzungen erläutern, um ein reibungsloses Lernerlebnis zu gewährleisten.

### Grundkenntnisse in C#

Das Lernprogramm ist zwar so konzipiert, dass es Sie durch jeden Schritt führt, doch wenn Sie über grundlegende Kenntnisse von C# verfügen, wird Ihnen das Erfassen der vorgestellten Konzepte leichter fallen.

### .NET-Entwicklungsumgebung

Stellen Sie sicher, dass Sie eine funktionierende .NET-Entwicklungsumgebung eingerichtet haben. Sie können Visual Studio oder jede andere IDE verwenden, die die .NET-Entwicklung unterstützt.

### Aspose.Cells für .NET NuGet-Paket

Sie müssen die Aspose.Cells-Bibliothek für .NET in Ihrem Projekt installiert haben. Sie können sie einfach über den NuGet Package Manager hinzufügen. 

So geht's:

1. Öffnen Sie Ihr Projekt in Visual Studio.
2. Gehen Sie zu „Tools“ > „NuGet-Paket-Manager“ > „NuGet-Pakete für Lösung verwalten“.
3.  Suchen nach`Aspose.Cells` und installieren Sie die neueste Version.

### Einfache Excel-Datei zum Testen

Sie benötigen eine Excel-Beispieldatei zum Arbeiten. Sie können eine einfache Excel-Datei mit beliebigen Ländernamen und deren Codes erstellen.

## Pakete importieren

Lassen Sie uns zunächst die erforderlichen Pakete in Ihr Projekt importieren. Hier ist ein kurzer Ausschnitt, wie Sie Ihren Code einrichten:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Nachdem die Pakete importiert wurden, können wir fortfahren.

## Schritt 1: Definieren Sie die Quell- und Ausgabeverzeichnisse 

Der erste Schritt besteht darin, zu definieren, wo sich Ihre Eingabedatei befindet und wo die Ausgabe (sortierte Datei) gespeichert werden soll. Sie müssen zwei Pfade angeben: einen für die Excel-Quelldatei und einen anderen zum Speichern der Ausgabe nach dem Sortieren.

```csharp
string sourceDir = "Your Document Directory\\";
string outputDir = "Your Document Directory\\";
```

## Schritt 2: Laden Sie die Excel-Quelldatei

Als nächstes laden wir die Excel-Datei, die die zu sortierenden Daten enthält. Dies geschieht durch die Erstellung einer Instanz des`Workbook` Klasse und übergeben Sie den Pfad Ihrer Quelldatei.

```csharp
Workbook wb = new Workbook(sourceDir + "sampleSortData_CustomSortList.xlsx");
```

## Schritt 3: Zugriff auf das erste Arbeitsblatt 

Sobald die Datei geladen ist, müssen wir auf das spezifische Arbeitsblatt zugreifen, das die Daten enthält, die wir sortieren möchten. In diesem Fall zielen wir auf das erste Arbeitsblatt.

```csharp
Worksheet ws = wb.Worksheets[0];
```

## Schritt 4: Festlegen des zu sortierenden Zellbereichs

 Wir müssen den Zellbereich bestimmen, den wir sortieren werden. In diesem Beispiel sortieren wir die Zellen von A1 bis A40. Verwenden Sie die`CellArea.CreateCellArea` Methode zum Definieren des Zellbereichs.

```csharp
CellArea ca = CellArea.CreateCellArea("A1", "A40");
```

## Schritt 5: Erstellen Sie eine benutzerdefinierte Sortierliste

Vor dem Sortieren müssen wir die Kriterien festlegen, die wir für unsere benutzerdefinierte Sortierung verwenden. Sie können eine Sortierliste als Array von Zeichenfolgen definieren. Die benutzerdefinierte Sortierliste bestimmt die Sortierreihenfolge.

```csharp
string[] customSortList = new string[] { "USA,US", "Brazil,BR", "China,CN", "Russia,RU", "Canada,CA" };
```

## Schritt 6: Sortierschlüssel hinzufügen und die Sortierung durchführen

Jetzt ist es Zeit zu sortieren! Wir verwenden hierfür die Klasse DataSorter. Erstellen Sie einen Schlüssel zum Sortieren basierend auf unserer benutzerdefinierten Liste und führen Sie den Sortiervorgang aus.

```csharp
wb.DataSorter.AddKey(0, SortOrder.Ascending, customSortList);
wb.DataSorter.Sort(ws.Cells, ca);
```

## Schritt 7: Speichern Sie die Excel-Ausgabedatei

Nachdem die Sortierung abgeschlossen ist, besteht der letzte Schritt darin, die Änderungen in einer neuen Excel-Datei zu speichern. Geben Sie den Ausgabedateinamen an und speichern Sie die Arbeitsmappe.

```csharp
wb.Save(outputDir + "outputSortData_CustomSortList.xlsx");
```

## Schritt 8: Erfolgreiche Ausführung bestätigen

Um sicherzustellen, dass alles reibungslos funktioniert hat, können Sie eine Bestätigungsmeldung auf der Konsole ausgeben. Dies hilft bei der Fehlerbehebung und gibt Ihnen die Gewissheit, dass der Vorgang erfolgreich war.

```csharp
Console.WriteLine("SortDataInColumnWithCustomSortList executed successfully.\r\n");
```

## Abschluss

Und da haben Sie es! Sie haben erfolgreich Daten in einer Excel-Spalte mithilfe einer benutzerdefinierten Sortierliste mit Aspose.Cells für .NET sortiert. Durch das Sortieren erhalten Sie Struktur und Übersichtlichkeit in Ihren Daten, sodass sie leichter zu analysieren und zu interpretieren sind. Ich hoffe, dieser Leitfaden bringt Ihre Fähigkeiten auf die nächste Ebene und hilft Ihnen zu erkennen, wie leistungsstark Aspose.Cells für Ihre Excel-bezogenen Aufgaben sein kann.

## Häufig gestellte Fragen

### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine umfassende Bibliothek, mit der Sie Excel-Dateien in .NET-Anwendungen bearbeiten, erstellen, bearbeiten und konvertieren können.

### Kann ich mit einer benutzerdefinierten Sortierliste mehr als eine Spalte sortieren?
Ja! Sie können bei Bedarf zusätzliche Schlüssel hinzufügen, um nach mehreren Spalten zu sortieren. Führen Sie dazu einfach für jeden Schlüssel das gleiche Verfahren aus.

### Benötige ich Vorkenntnisse in C#, um Aspose.Cells zu verwenden?
Obwohl es hilfreich ist, können Sie diesem Tutorial folgen und dabei lernen! Grundlegende Kenntnisse in C# werden Ihren Lernerfolg verbessern.

### Ist es möglich, eine temporäre Lizenz für Aspose.Cells zu verwenden?
Auf jeden Fall! Sie können eine temporäre Lizenz erwerben, wenn Sie den vollen Funktionsumfang der Bibliothek ohne Einschränkungen testen möchten.

### Kann ich Beispiele oder Dokumentation für Aspose.Cells herunterladen?
 Ja! Aspose bietet umfangreiche Dokumentation und Beispielprojekte, die Ihnen sehr helfen können. Schauen Sie sich die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
