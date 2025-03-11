---
title: Benannten Bereich in Excel entfernen
linktitle: Benannten Bereich in Excel entfernen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie mit detaillierten Schritt-für-Schritt-Anleitungen, wie Sie mit Aspose.Cells für .NET benannte Bereiche in Excel entfernen.
weight: 11
url: /de/net/excel-managing-named-ranges/remove-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benannten Bereich in Excel entfernen

## Einführung
Excel ist für viele Einzelpersonen und Organisationen zu einem festen Bestandteil der Datenverwaltung und -analyse geworden. Egal, ob Sie ein erfahrener Datenanalyst sind oder einfach nur gerne Ihre Daten organisieren, die Beherrschung von Excel ist unerlässlich. Heute tauchen wir in eine spezielle, aber leistungsstarke Funktion ein: das Entfernen benannter Bereiche mit Aspose.Cells für .NET. Diese Anleitung führt Sie durch die Schritte, um dies effektiv zu erreichen. Also krempeln Sie die Ärmel hoch und legen Sie los!

## Voraussetzungen

Bevor wir mit der eigentlichen Codierung beginnen, müssen Sie einige Dinge vorbereitet haben:

### Einrichten der .NET-Umgebung

Um nahtlos mit Aspose.Cells für .NET zu arbeiten, stellen Sie sicher, dass Sie über Folgendes verfügen:

1.  Visual Studio: Laden Sie Visual Studio herunter und installieren Sie es (Community Edition ist vollkommen ausreichend). Sie finden es auf der[Visual Studio-Website](https://visualstudio.microsoft.com/).
2. .NET Framework: Stellen Sie sicher, dass Sie eine geeignete Version des .NET Frameworks verwenden. Aspose.Cells unterstützt .NET Framework 4.0 und höher.
3. Aspose.Cells-Bibliothek: Sie müssen die Aspose.Cells-Bibliothek für .NET herunterladen und in Ihrer Anwendung referenzieren. Sie finden das herunterladbare Paket[Hier](https://releases.aspose.com/cells/net/).

### Grundlegende Kenntnisse in C#

Sie benötigen grundlegende Kenntnisse der C#-Programmierung. Dies wird Ihnen helfen, die Codeausschnitte zu verstehen, die wir besprechen werden.

### Zugriff auf Excel-Dateien

Stellen Sie sicher, dass Sie eine Excel-Datei zum Experimentieren zur Hand haben. Wenn nicht, können Sie schnell eine mit Microsoft Excel erstellen.

## Pakete importieren

Nachdem wir nun unsere Voraussetzungen erfüllt haben, importieren wir die Pakete, die wir in unserem Projekt benötigen. Öffnen Sie Visual Studio und erstellen Sie eine neue Konsolenanwendung. Fügen Sie dann den folgenden Namespace in Ihr Programm ein:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Mit diesem Setup können Sie die von Aspose.Cells bereitgestellten Funktionen nutzen, um Excel-Tabellen problemlos zu bearbeiten.

## Schritt 1: Einrichten des Ausgabeverzeichnisses

Zunächst müssen wir festlegen, wo unsere Ausgabedatei gespeichert wird. Dies ist wichtig, da es spätere Verwirrung darüber vermeidet, wo sich Ihre Dateien befinden.

```csharp
// Ausgabeverzeichnis
string outputDir = "Your Document Directory Here\\";
```

 Ersetzen`"Your Document Directory Here\\"`durch den Pfad auf Ihrem Computer, in dem Sie Ihre Datei speichern möchten.

## Schritt 2: Instanziieren einer neuen Arbeitsmappe

Wie beginnt man mit einem leeren Blatt? Natürlich indem man eine neue Arbeitsmappe erstellt! Diese Arbeitsmappe dient uns als leere Leinwand.

```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook workbook = new Workbook();
```

Diese Codezeile erstellt eine neue Arbeitsmappe, die wir bearbeiten können.

## Schritt 3: Zugriff auf die Arbeitsblattsammlung

Jede Arbeitsmappe besteht aus einem oder mehreren Arbeitsblättern. Um in einem bestimmten Arbeitsblatt arbeiten zu können, benötigen wir Zugriff auf diese Sammlung.

```csharp
// Holen Sie sich alle Arbeitsblätter im Buch.
WorksheetCollection worksheets = workbook.Worksheets;
```

Hier haben wir alle in unserer neuen Arbeitsmappe verfügbaren Arbeitsblätter abgerufen.

## Schritt 4: Auswählen des ersten Arbeitsblatts

Als Nächstes möchten wir im ersten Arbeitsblatt arbeiten, das in vielen Fällen der Standardausgangspunkt ist.

```csharp
// Holen Sie sich das erste Arbeitsblatt in der Arbeitsblattsammlung.
Worksheet worksheet = workbook.Worksheets[0];
```

Mit diesem Codeausschnitt können wir ganz einfach das erste Arbeitsblatt auswählen.

## Schritt 5: Benannte Bereiche erstellen

Lassen Sie uns nun einen benannten Bereich erstellen. Dies ist ein wesentlicher Bestandteil dieses Tutorials. So können wir später veranschaulichen, wie ein benannter Bereich entfernt wird.

```csharp
// Erstellen Sie einen Zellbereich.
Range range1 = worksheet.Cells.CreateRange("E12", "I12");

// Benennen Sie den Bereich.
range1.Name = "FirstRange";
```

Hier definieren wir einen Bereich von den Zellen E12 bis I12 und nennen ihn „FirstRange“.

## Schritt 6: Formatieren des benannten Bereichs

Um zu demonstrieren, wie vielseitig Aspose.Cells sein kann, fügen wir unserem benannten Bereich einige Formatierungen hinzu.

```csharp
// Legen Sie die Umrisslinie für den Bereich fest.
range1.SetOutlineBorder(BorderType.TopBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.BottomBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.LeftBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
range1.SetOutlineBorder(BorderType.RightBorder, CellBorderType.Medium, Color.FromArgb(0, 0, 128));
```

Wir fügen unserem Sortiment einen mittelgroßen marineblauen Rand hinzu, um es optisch ansprechend zu gestalten.

## Schritt 7: Einfügen von Daten in den Bereich

Als Nächstes können wir unsere Zellen mit einigen Daten füllen, um sie funktionsfähig zu machen.

```csharp
// Geben Sie einige Daten mit einigen Formatierungen in einige Zellen im Bereich ein.
range1[0, 0].PutValue("Test");            
range1[0, 4].PutValue(123);
```

In diesem Schritt haben wir das Wort „Test“ in Zelle E12 und die Zahl 123 in Zelle I12 eingetragen.

## Schritt 8: Einen weiteren benannten Bereich erstellen

Um unseren Standpunkt weiter zu verdeutlichen, erstellen wir einen weiteren benannten Bereich, der dem ersten ähnelt.

```csharp
//Erstellen Sie einen weiteren Zellbereich.
Range range2 = worksheet.Cells.CreateRange("B3", "F3");

// Benennen Sie den Bereich.
range2.Name = "SecondRange";
```

Jetzt steht uns ein weiterer benannter Bereich namens „SecondRange“ zur Verfügung.

## Schritt 9: Den ersten Bereich in den zweiten Bereich kopieren

Lassen Sie uns demonstrieren, wie wir unseren zweiten Bereich verwenden, indem wir Daten aus dem ersten Bereich kopieren.

```csharp
// Kopieren Sie den ersten Bereich in den zweiten Bereich.
range2.Copy(range1);
```

Mit diesem Schritt haben wir die Daten effektiv von „FirstRange“ in „SecondRange“ dupliziert.

## Schritt 10: Entfernen des benannten Bereichs

Nun zum Highlight unseres Tutorials: dem Entfernen des benannten Bereichs. Hier kommt alles zusammen.

```csharp
// Entfernen Sie den zuvor benannten Bereich (Bereich1) mit seinem Inhalt.
worksheet.Cells.ClearRange(range1.FirstRow, range1.FirstColumn, range1.FirstRow + range1.RowCount - 1, range1.FirstColumn + range1.ColumnCount - 1);
```

Diese Zeile löscht den Inhalt des Bereichs, den wir entfernen möchten, und stellt sicher, dass wir keine Spuren hinterlassen!

## Schritt 11: Löschen des benannten Bereichs aus dem Arbeitsblatt

Ein wichtiger letzter Schritt besteht darin, den benannten Bereich aus der Namenssammlung des Arbeitsblatts zu entfernen.

```csharp
worksheets.Names.RemoveAt(0);
```

Dadurch wird der benannte Bereich „FirstRange“ effektiv aus der Arbeitsmappe entfernt.

## Schritt 12: Speichern der Arbeitsmappe

Zu guter Letzt speichern wir unsere Arbeit. 

```csharp
// Speichern Sie die Excel-Datei.
workbook.Save(outputDir + "outputRemoveNamedRange.xlsx");
```

Dieser Befehl speichert Ihre Arbeitsmappe mit den von uns vorgenommenen Änderungen. Ihre gesamte harte Arbeit bleibt hier erhalten!

## Schritt 13: Erfolgreiche Ausführung bestätigen

Um die Sache ordentlich abzuschließen, möchten Sie vielleicht eine Erfolgsmeldung an die Konsole ausgeben.

```csharp
Console.WriteLine("RemoveNamedRange executed successfully.");
```

Dadurch werden Sie darüber informiert, dass der gesamte Vorgang reibungslos abgeschlossen wurde!

## Abschluss

In dieser Anleitung haben Sie gelernt, wie Sie benannte Bereiche in Excel mit Aspose.Cells für .NET bearbeiten. Sie haben Bereiche erstellt, sie mit Daten gefüllt, ihren Inhalt kopiert und sie schließlich entfernt und dabei sichergestellt, dass Ihre Excel-Datei organisiert und sauber bleibt. Excel lebt, ähnlich wie ein geschäftiges Café, von der Organisation. Egal, ob Sie Daten für einen Bericht verwalten oder Ihr persönliches Budgetblatt aufpolieren, die Beherrschung benannter Bereiche kann Ihnen dabei helfen, einige effiziente Lösungen zu entwickeln. 

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek für die programmgesteuerte Bearbeitung von Excel-Dateien.

### Kann ich mehrere benannte Bereiche gleichzeitig entfernen?
Ja, Sie können die Sammlung benannter Bereiche durchlaufen und sie nach Bedarf entfernen.

### Gibt es eine Testversion?
 Ja, Sie können eine kostenlose Testversion von Aspose.Cells herunterladen[Hier](https://releases.aspose.com/).

### Welche Programmiersprachen unterstützt Aspose.Cells?
Es unterstützt in erster Linie .NET-Sprachen wie unter anderem C# und VB.NET.

### Wo kann ich Unterstützung suchen, wenn ich auf Probleme stoße?
 Besuchen Sie die[Aspose-Supportforum](https://forum.aspose.com/c/cells/9) für Hilfe bei Fragen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
