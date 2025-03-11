---
title: Daten aus Zellen in Excel abrufen
linktitle: Daten aus Zellen in Excel abrufen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET Daten aus Excel-Zellen abrufen. Das Tutorial ist sowohl für Anfänger als auch für erfahrene Entwickler geeignet.
weight: 10
url: /de/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Daten aus Zellen in Excel abrufen

## Einführung

Wenn es um die Verwaltung von Daten in Excel geht, ist die Fähigkeit, Informationen aus Zellen zu lesen und abzurufen, von entscheidender Bedeutung. Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, mit der Entwickler Excel-Dateien nahtlos bearbeiten können. In diesem Tutorial erfahren Sie, wie Sie mit Aspose.Cells Daten aus Zellen in einer Excel-Arbeitsmappe abrufen. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, diese Anleitung führt Sie Schritt für Schritt durch den Prozess.

## Voraussetzungen

Bevor wir uns in den Code stürzen, müssen einige Voraussetzungen erfüllt sein:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Dies ist die IDE, die wir zum Schreiben und Ausführen unseres Codes verwenden werden.
2.  Aspose.Cells für .NET: Sie benötigen die Aspose.Cells-Bibliothek. Sie können sie von der[Aspose-Website](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, verstehen Sie die Beispiele besser.
4. Excel-Datei: Halten Sie eine Excel-Datei bereit (zum Beispiel`book1.xls`), die Sie für dieses Tutorial verwenden werden.

Sobald diese Voraussetzungen erfüllt sind, können wir damit beginnen, zu erkunden, wie Daten aus Excel-Zellen abgerufen werden.

## Pakete importieren

Um zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr C#-Projekt importieren. Dadurch können Sie die von Aspose.Cells bereitgestellten Klassen und Methoden nutzen.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Wenn diese Namespaces importiert sind, können Sie mit dem Codieren beginnen. Lassen Sie uns den Prozess in überschaubare Schritte unterteilen.

## Schritt 1: Richten Sie Ihr Dokumentverzeichnis ein

Der erste Schritt besteht darin, den Pfad zu Ihrem Dokumentenverzeichnis anzugeben, in dem sich Ihre Excel-Datei befindet. Dies ist wichtig, da es der Anwendung mitteilt, wo sich die Datei befindet, mit der Sie arbeiten möchten.


```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
```

 Ersetzen`"Your Document Directory"` mit dem tatsächlichen Pfad, auf dem Ihr`book1.xls` Datei wird gespeichert. In diesem Pfad sucht Aspose.Cells nach der Datei, wenn Sie versuchen, sie zu öffnen.

## Schritt 2: Öffnen Sie die vorhandene Arbeitsmappe

Nachdem Sie das Dokumentverzeichnis eingerichtet haben, besteht der nächste Schritt darin, die Arbeitsmappe (Excel-Datei) zu öffnen, mit der Sie arbeiten möchten.


```csharp
//Öffnen einer vorhandenen Arbeitsmappe
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

 Hier erstellen wir eine`Workbook` Objekt, indem Sie den vollständigen Pfad der Excel-Datei übergeben. Dieser Schritt initialisiert die Arbeitsmappe und bereitet sie für den Datenabruf vor.

## Schritt 3: Zugriff auf das erste Arbeitsblatt

Nachdem Sie die Arbeitsmappe geöffnet haben, möchten Sie auf das spezifische Arbeitsblatt zugreifen, aus dem Sie Daten abrufen möchten. In diesem Fall greifen wir auf das erste Arbeitsblatt zu.


```csharp
// Auf das erste Arbeitsblatt zugreifen
Worksheet worksheet = workbook.Worksheets[0];
```

 Der`Worksheets` Sammlung ermöglicht Ihnen den Zugriff auf verschiedene Blätter in der Arbeitsmappe. Der Index`[0]` verweist auf das erste Arbeitsblatt. Wenn Sie auf nachfolgende Blätter zugreifen möchten, können Sie den Index entsprechend ändern.

## Schritt 4: Durch die Zellen schleifen

Jetzt, da Sie das Arbeitsblatt haben, ist es an der Zeit, jede Zelle zu durchlaufen, um die Daten abzurufen. Hier geschieht die Magie!


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    // Variablen zum Speichern von Werten unterschiedlicher Datentypen
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    // Übergabe des Typs der in der Zelle enthaltenen Daten zur Auswertung
    switch (cell1.Type)
    {
        // Auswerten des Datentyps der Zellendaten für Zeichenfolgenwerte
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        // Auswerten des Datentyps der Zelldaten für doppelte Werte
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        //Auswerten des Datentyps der Zelldaten für boolesche Werte
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        // Auswerten des Datentyps der Zellendaten für Datums-/Zeitwerte
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        // Auswertung des unbekannten Datentyps der Zelldaten
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        // Beenden der Typprüfung des Typs der Zellendaten ist null
        case CellValueType.IsNull:
            break;
    }
}
```

 In diesem Schritt durchlaufen wir jede Zelle im Arbeitsblatt. Für jede Zelle überprüfen wir ihren Datentyp mithilfe eines`switch` Anweisung. Abhängig vom Typ rufen wir den Wert ab und drucken ihn auf der Konsole aus. Hier ist eine Aufschlüsselung der Fälle:

-  IsString: Wenn die Zelle einen String enthält, ermitteln wir diesen mit`StringValue`.
-  IsNumeric: Für numerische Werte verwenden wir`DoubleValue`.
-  IsBool: Wenn die Zelle einen booleschen Wert enthält, greifen wir darauf zu mit`BoolValue`.
-  IsDateTime: Für Datums- und Zeitwerte verwenden wir`DateTimeValue`.
- IsUnknown: Wenn der Datentyp unbekannt ist, rufen wir trotzdem die Zeichenfolgendarstellung ab.
- IsNull: Wenn die Zelle leer ist, überspringen wir sie einfach.

## Abschluss

Das Abrufen von Daten aus Excel-Zellen mit Aspose.Cells für .NET ist ein unkomplizierter Vorgang. Indem Sie diese Schritte befolgen, können Sie verschiedene Datentypen effizient aus Ihren Excel-Dateien extrahieren. Egal, ob Sie ein Berichterstellungstool erstellen, die Dateneingabe automatisieren oder einfach nur Daten analysieren müssen, Aspose.Cells bietet die Flexibilität und Leistung, die Sie für die Erledigung Ihrer Aufgabe benötigen.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?  
Aspose.Cells ist eine .NET-Bibliothek, mit der Entwickler Excel-Dateien erstellen, bearbeiten und konvertieren können, ohne dass Microsoft Excel installiert sein muss.

### Kann ich Aspose.Cells kostenlos nutzen?  
 Ja, Aspose.Cells bietet eine kostenlose Testversion an, mit der Sie die Funktionen testen können. Sie können sie herunterladen[Hier](https://releases.aspose.com/).

### Welche Arten von Daten kann ich aus Excel-Zellen abrufen?  
Sie können verschiedene Datentypen abrufen, darunter Zeichenfolgen, Zahlen, Boolesche Werte und Datums-/Uhrzeitwerte.

### Wie erhalte ich Unterstützung für Aspose.Cells?  
 Sie erhalten Unterstützung durch den Besuch der[Aspose-Forum](https://forum.aspose.com/c/cells/9) wo Sie Fragen stellen und Hilfe von der Community erhalten können.

### Ist eine temporäre Lizenz verfügbar?  
 Ja, Aspose bietet eine temporäre Lizenz zu Testzwecken an. Weitere Informationen finden Sie hier[Hier](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
