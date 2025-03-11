---
title: Geben Sie beim Importieren von Daten in eine Excel-Tabelle Formelfelder an
linktitle: Geben Sie beim Importieren von Daten in eine Excel-Tabelle Formelfelder an
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem ausführlichen Tutorial, wie Sie mit Aspose.Cells für .NET Daten mit angegebenen Formelfeldern in Excel-Tabellen importieren.
weight: 11
url: /de/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Geben Sie beim Importieren von Daten in eine Excel-Tabelle Formelfelder an

## Einführung

Wenn es um die programmgesteuerte Verarbeitung von Excel-Dateien geht, ist Aspose.Cells für .NET ein unschätzbar wertvolles Tool. Es bietet robuste Funktionen zum einfachen Erstellen, Ändern und Bearbeiten von Excel-Tabellen. Eine der interessanten Funktionen ist die Möglichkeit, beim Importieren von Daten in eine Excel-Tabelle Formelfelder anzugeben. Stellen Sie sich vor, Sie arbeiten an einem Finanzbericht und müssen basierend auf Benutzereingaben automatisch Summen berechnen. Dieses Tutorial führt Sie Schritt für Schritt durch die Erreichung genau dessen mit einem sauberen und unkomplizierten Ansatz.

## Voraussetzungen

Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie brauchen. 

1. Visual Studio oder eine beliebige integrierte Entwicklungsumgebung (IDE) von .NET: Stellen Sie sicher, dass Sie über eine geeignete IDE zum Schreiben und Ausführen Ihres C#-Codes verfügen.
2.  Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek herunterladen und in Ihrem Projekt referenzieren. Sie können sie von der[Aspose-Veröffentlichungen](https://releases.aspose.com/cells/net/).
3. Grundlegende C#-Kenntnisse: Wenn Sie mit C# und den Konzepten der objektorientierten Programmierung vertraut sind, können Sie die Beispiele besser verstehen.
4. .NET Framework: Dieses Tutorial setzt voraus, dass Sie .NET Framework 4.5 oder höher verwenden.

Sobald Sie die Voraussetzungen geklärt haben, können wir mit dem Importieren einiger Daten in ein Excel-Tabellenblatt mit angegebenen Formelfeldern fortfahren.

## Pakete importieren

Bevor Sie mit dem Schreiben Ihres Codes beginnen, müssen Sie den erforderlichen Aspose.Cells-Namespace importieren. Dies geschieht normalerweise am Anfang Ihrer C#-Datei:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Auf diese Weise können Sie die von der Aspose.Cells-Bibliothek bereitgestellten Klassen und Methoden verwenden, ohne ihnen jedes Mal den Namespace voranstellen zu müssen.

Lassen Sie uns den gesamten Prozess in überschaubare Schritte unterteilen:

## Schritt 1: Definieren Sie das Ausgabeverzeichnis

Zunächst müssen Sie festlegen, wo Sie Ihre Excel-Datei speichern möchten. So können Sie das tun:

```csharp
static string outputDir = "Your Document Directory"; // Geben Sie hier Ihr Dokumentverzeichnis an
```

 Ersetzen`"Your Document Directory"` durch Ihren tatsächlichen Dateipfad. Hier wird die generierte Excel-Datei gespeichert.

## Schritt 2: Erstellen einer benutzerdefinierten Klasse für Datenelemente

Als Nächstes definieren wir eine Klasse zur Strukturierung der Daten, die wir importieren möchten.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

 Das`DataItems` Die Klasse enthält die Rohzahlen und die Formeln, die wir in das Excel-Blatt schreiben. 

## Schritt 3: Initialisieren Sie eine Liste zum Speichern von Datenelementen

 Wir verwenden eine Liste, um mehrere Instanzen unserer`DataItems` Klasse.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Schritt 4: Datenelemente zur Liste hinzufügen

Fügen wir nun unserer Liste einige Einträge hinzu. Jeder Eintrag enthält zwei Zahlen und zwei Formeln.

```csharp
// Definieren und fügen Sie jedes Datenelement hinzu
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Aspose-Website\")";
dis.Add(di);

// Wiederholen Sie dies für weitere Datenelemente.
```

 Stellen Sie sicher, dass Sie jedes`DataItems` Instanz mit eindeutigen Werten und Formeln.

## Schritt 5: Arbeitsmappe und Access-Arbeitsblatt erstellen

Erstellen Sie als Nächstes die Arbeitsmappe und greifen Sie auf das erste Arbeitsblatt zu, in das wir schließlich die Daten importieren.

```csharp
Workbook wb = new Workbook(); // Erstellen einer neuen Arbeitsmappe
Worksheet ws = wb.Worksheets[0]; // Zugriff auf das erste Arbeitsblatt
```

## Schritt 6: Optionen für den Tabellenimport festlegen

Hier geschieht die Magie. Sie müssen angeben, welche Felder in Ihren Daten den Formeln entsprechen. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

 In diesem Beispiel enthalten die letzten beiden Felder Formeln, was durch`true` , während die ersten beiden Felder auf`false`.

## Schritt 7: Benutzerdefinierte Objekte importieren

Nachdem nun alles eingerichtet ist, importieren wir unsere Liste mit Datenelementen in das Arbeitsblatt.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Diese Zeile importiert effektiv die Daten ab Zelle A1.

## Schritt 8: Formeln berechnen

Da wir einige Formeln importiert haben, ist es wichtig, diese zu berechnen.

```csharp
wb.CalculateFormula();
```

Diese Methode stellt sicher, dass Ihre Formeln basierend auf ihren Abhängigkeiten ausgewertet werden.

## Schritt 9: Spalten automatisch anpassen

Um eine anzeigefreundliche Darstellung Ihrer Daten zu gewährleisten, können Sie die Spalten automatisch an den Inhalt anpassen.

```csharp
ws.AutoFitColumns();
```

Dieser Schritt optimiert das Layout der Excel-Datei. 

## Schritt 10: Speichern Sie Ihre Excel-Datei

Schließlich ist es an der Zeit, Ihre neu erstellte Excel-Datei zu speichern. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Stellen Sie sicher, dass Ihr Ausgabedateiname relevant und beschreibend ist!

## Schritt 11: Ausführung überprüfen

Um auf einfache Weise zu bestätigen, dass alles ordnungsgemäß ausgeführt wurde, können Sie eine Nachricht ausdrucken.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Dadurch erhalten Sie sofort die Rückmeldung, dass der Code problemlos funktioniert hat.

## Abschluss

Und da haben Sie es! Sie haben erfolgreich Daten in ein Excel-Blatt importiert, indem Sie Aspose.Cells für .NET verwendet und Formelfelder angegeben haben. Indem Sie diese Schritte befolgen, können Sie ähnliche Techniken anwenden, um Datenverarbeitungsaufgaben zu automatisieren, die auf Ihre Bedürfnisse zugeschnitten sind. Egal, ob Sie Zahlen für Berichte verarbeiten oder einfach nur Daten pflegen, die Kunst der Excel-Manipulation mit Aspose zu beherrschen, ist eine lohnende Fähigkeit.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek zum programmgesteuerten Erstellen, Bearbeiten und Konvertieren von Excel-Dateien.

### Wie installiere ich Aspose.Cells für .NET?
 Sie können es herunterladen von der[Aspose-Veröffentlichungen](https://releases.aspose.com/cells/net/) und verweisen Sie in Ihrem Projekt darauf.

### Kann ich Aspose.Cells kostenlos nutzen?
 Ja, Aspose bietet eine kostenlose Testversion an unter[dieser Link](https://releases.aspose.com/).

### Wo finde ich weitere Beispiele?
 Weitere Beispiele und Dokumentation finden Sie unter[Aspose-Dokumentationsseite](https://reference.aspose.com/cells/net/).

### Was ist, wenn bei der Verwendung von Aspose Probleme auftreten?
 Sie können im Aspose-Supportforum Hilfe suchen[Hier](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
