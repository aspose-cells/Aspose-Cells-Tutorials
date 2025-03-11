---
title: Suchen Sie nach der maximalen Anzahl von Zeilen und Spalten, die von den Formaten XLS und XLSX unterstützt werden
linktitle: Suchen Sie nach der maximalen Anzahl von Zeilen und Spalten, die von den Formaten XLS und XLSX unterstützt werden
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Entdecken Sie die maximale Anzahl an Zeilen und Spalten, die von den Formaten XLS und XLSX mit Aspose.Cells für .NET unterstützt werden. Maximieren Sie Ihr Excel-Datenmanagement mit diesem umfassenden Tutorial.
weight: 11
url: /de/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Suchen Sie nach der maximalen Anzahl von Zeilen und Spalten, die von den Formaten XLS und XLSX unterstützt werden

## Einführung
In der Welt von Excel kann die Verwaltung großer Datensätze eine gewaltige Aufgabe sein, insbesondere wenn es darum geht, die maximale Anzahl von Zeilen und Spalten zu verarbeiten, die von verschiedenen Dateiformaten unterstützt werden. Dieses Tutorial führt Sie durch den Prozess zum Ermitteln der maximalen Zeilen und Spalten, die von den Formaten XLS und XLSX mithilfe der Aspose.Cells für .NET-Bibliothek unterstützt werden. Am Ende dieses Artikels verfügen Sie über ein umfassendes Verständnis dafür, wie Sie dieses leistungsstarke Tool nutzen können, um Ihre Excel-bezogenen Aufgaben effizient zu erledigen.
## Voraussetzungen
Bevor wir mit dem Tutorial beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) oder[.NET-Kern](https://dotnet.microsoft.com/en-us/download) auf Ihrem System installiert.
2. [Aspose.Cells für .NET](https://releases.aspose.com/cells/net/) Bibliothek heruntergeladen und in Ihrem Projekt referenziert.
 Wenn Sie dies noch nicht getan haben, können Sie die Aspose.Cells für .NET-Bibliothek von der[Webseite](https://releases.aspose.com/cells/net/) oder installieren Sie es über[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Pakete aus der Aspose.Cells-Bibliothek für .NET importieren. Fügen Sie oben in Ihrer C#-Datei die folgenden using-Anweisungen hinzu:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Schritt 1: Ermitteln Sie die maximale Anzahl an Zeilen und Spalten, die vom XLS-Format unterstützt werden
Beginnen wir mit der Untersuchung der maximalen Zeilen und Spalten, die vom XLS-Format (Excel 97-2003) unterstützt werden.
```csharp
// Meldung zum XLS-Format drucken.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Erstellen Sie eine Arbeitsmappe im XLS-Format.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Drucken Sie die maximale Anzahl an Zeilen und Spalten, die vom XLS-Format unterstützt wird.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
In diesem Schritt:
1. Drucken Sie eine Nachricht, um anzuzeigen, dass wir mit dem XLS-Format arbeiten.
2.  Erstellen Sie ein neues`Workbook` Instanz mit dem`FileFormatType.Excel97To2003` Enumeration, die das XLS-Format darstellt.
3.  Rufen Sie die maximale Anzahl an Zeilen und Spalten ab, die das XLS-Format unterstützt, mit dem`Workbook.Settings.MaxRow` Und`Workbook.Settings.MaxColumn`Eigenschaften. Wir addieren 1 zu diesen Werten, um die tatsächliche maximale Zeilen- und Spaltenanzahl zu erhalten (da sie nullbasiert sind).
4. Drucken Sie die maximale Anzahl an Zeilen und Spalten auf der Konsole.
## Schritt 2: Ermitteln Sie die maximale Anzahl an Zeilen und Spalten, die vom XLSX-Format unterstützt werden
Als Nächstes untersuchen wir die maximale Anzahl an Zeilen und Spalten, die vom XLSX-Format (Excel 2007 und höher) unterstützt werden.
```csharp
// Nachricht zum XLSX-Format drucken.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Erstellen Sie eine Arbeitsmappe im XLSX-Format.
wb = new Workbook(FileFormatType.Xlsx);
// Drucken Sie die maximale Anzahl an Zeilen und Spalten, die vom XLSX-Format unterstützt wird.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
In diesem Schritt:
1. Drucken Sie eine Nachricht, um anzuzeigen, dass wir mit dem XLSX-Format arbeiten.
2.  Erstellen Sie ein neues`Workbook` Instanz mit dem`FileFormatType.Xlsx` Enumeration, die das XLSX-Format darstellt.
3.  Rufen Sie die maximale Anzahl an Zeilen und Spalten ab, die vom XLSX-Format unterstützt werden, mit dem`Workbook.Settings.MaxRow` Und`Workbook.Settings.MaxColumn`Eigenschaften. Wir addieren 1 zu diesen Werten, um die tatsächliche maximale Zeilen- und Spaltenanzahl zu erhalten (da sie nullbasiert sind).
4. Drucken Sie die maximale Anzahl an Zeilen und Spalten auf der Konsole.
## Schritt 3: Eine Erfolgsmeldung anzeigen
Lassen Sie uns abschließend eine Erfolgsmeldung anzeigen, um anzuzeigen, dass das Beispiel „FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats“ erfolgreich ausgeführt wurde.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Dieser Schritt druckt einfach eine Erfolgsmeldung auf die Konsole.
## Abschluss
In diesem Tutorial haben Sie gelernt, wie Sie mit der Bibliothek Aspose.Cells für .NET die maximale Anzahl an Zeilen und Spalten ermitteln, die von den Dateiformaten XLS und XLSX unterstützt wird. Wenn Sie die Einschränkungen dieser Formate kennen, können Sie Ihre Excel-basierten Projekte besser planen und verwalten und sicherstellen, dass Ihre Daten in die unterstützten Bereiche passen.
## Häufig gestellte Fragen
### Was ist die maximale Zeilenanzahl, die vom XLS-Format unterstützt wird?
Die maximale Zeilenanzahl, die vom XLS-Format (Excel 97-2003) unterstützt wird, beträgt 65.536.
### Wie viele Spalten werden vom XLS-Format maximal unterstützt?
Die maximale Anzahl der vom XLS-Format (Excel 97-2003) unterstützten Spalten beträgt 256.
### Was ist die maximale Zeilenanzahl, die vom XLSX-Format unterstützt wird?
Die maximale Zeilenanzahl, die vom XLSX-Format (Excel 2007 und höher) unterstützt wird, beträgt 1.048.576.
### Was ist die maximale Anzahl an Spalten, die vom XLSX-Format unterstützt werden?
Die maximale Anzahl der vom XLSX-Format (Excel 2007 und höher) unterstützten Spalten beträgt 16.384.
### Kann ich die Aspose.Cells-Bibliothek für .NET verwenden, um mit anderen Excel-Dateiformaten zu arbeiten?
 Ja, die Aspose.Cells für .NET-Bibliothek unterstützt eine Vielzahl von Excel-Dateiformaten, darunter XLS, XLSX, ODS und mehr. Sie können die[Dokumentation](https://reference.aspose.com/cells/net/) um mehr über die verfügbaren Features und Funktionen zu erfahren.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
