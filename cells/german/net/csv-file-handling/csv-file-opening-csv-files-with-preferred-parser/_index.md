---
title: Öffnen von CSV-Dateien mit dem bevorzugten Parser
linktitle: Öffnen von CSV-Dateien mit dem bevorzugten Parser
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie CSV-Dateien mit benutzerdefinierten Parsern in Aspose.Cells für .NET öffnen und analysieren. Bearbeiten Sie Text und Daten mühelos. Perfekt für Entwickler.
weight: 11
url: /de/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Öffnen von CSV-Dateien mit dem bevorzugten Parser

## Einführung
Beim Umgang mit CSV-Dateien möchten Sie manchmal verschiedene Datentypen mit benutzerdefinierten Parsern verarbeiten. Dieses Tutorial zeigt Ihnen, wie Sie CSV-Dateien mit einem bevorzugten Parser unter Verwendung von Aspose.Cells für .NET öffnen. Egal, ob Sie Text, Daten oder andere benutzerdefinierte Formate verarbeiten möchten, diese Anleitung führt Sie mit einer klaren Erklärung durch jeden Schritt.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, wollen wir die wesentlichen Elemente abdecken, die Sie für den Einstieg benötigen.
1.  Aspose.Cells für .NET-Bibliothek: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek installiert haben. Sie können sie herunterladen[Hier](https://releases.aspose.com/cells/net/) Sie können auch die kostenlose Testversion nutzen[Hier](https://releases.aspose.com/).
2. .NET-Entwicklungsumgebung: Visual Studio wird empfohlen, aber jede .NET-kompatible IDE funktioniert.
3. Grundkenntnisse in C#: Dieses Tutorial setzt voraus, dass Sie mit C# und objektorientierter Programmierung vertraut sind.
## Pakete importieren
Um Aspose.Cells zu verwenden, müssen Sie die erforderlichen Namespaces oben in Ihrer C#-Datei importieren:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nachdem wir nun die Bühne bereitet haben, gehen wir durch, wie man eine CSV-Datei mit einem bevorzugten Parser öffnet und dabei unterschiedliche Datenformate wie Text und Datumsangaben verarbeitet.
## Schritt 1: Benutzerdefinierte Parser definieren
 Um verschiedene Datentypen wie Text oder bestimmte Datumsformate verarbeiten zu können, müssen Sie benutzerdefinierte Parser definieren. In Aspose.Cells implementieren benutzerdefinierte Parser die`ICustomParser` Schnittstelle.
### 1.1 Erstellen eines Textparsers
Dieser Parser verarbeitet normale Textwerte. Er ändert das Format nicht, sodass der Wert unverändert zurückgegeben wird.
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
 Der`ParseObject` Methode gibt einfach den Eingabewert zurück. Das ist, als würde man sagen: „Ändern Sie nichts, geben Sie mir einfach den Text!“
### 1.2 Erstellen eines Datumsparsers
 Bei Datumsangaben müssen Sie sicherstellen, dass die CSV-Daten korrekt analysiert werden in`DateTime` Objekte. So können Sie einen Datumsparser erstellen:
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
 In diesem Parser verwenden wir`ParseExact` um sicherzustellen, dass das Datum auf Grundlage eines vordefinierten Formats korrekt interpretiert wird (`"dd/MM/yyyy"`). Auf diese Weise wird jedes Datum in Ihrer CSV, das diesem Format folgt, problemlos verarbeitet.
## Schritt 2: Ladeoptionen konfigurieren
 Als nächstes müssen Sie konfigurieren, wie die CSV-Datei geladen wird. Dies geschieht über den`TxtLoadOptions` Klasse, mit der Sie Analyseoptionen, einschließlich Kodierung und benutzerdefinierter Parser, angeben können.
### 2.1 Ladeoptionen einrichten
 Wir beginnen mit der Initialisierung des`TxtLoadOptions` und Definieren wichtiger Parameter wie Trennzeichen und Kodierung:
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- Trennzeichen: Dies definiert das Zeichen, das zum Trennen von Werten in der CSV-Datei verwendet wird (in diesem Fall Kommas).
- Kodierung: Wir verwenden die UTF-8-Kodierung, um ein breites Spektrum an Zeichen zu verarbeiten.
-  ConvertDateTimeData: Wenn Sie diesen Wert auf true setzen, werden Datumswerte automatisch konvertiert in`DateTime` Objekte, wenn möglich.
### 2.2 Benutzerdefinierte Parser anwenden
Als Nächstes weisen wir die zuvor erstellten Parser zu, um die Werte in der CSV-Datei zu verarbeiten:
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
 Dies weist Aspose.Cells an, die`TextParser` für allgemeine Textwerte und die`DateParser`für alle Datumsfelder, die es in der CSV-Datei findet.
## Schritt 3: Laden und Lesen der CSV-Datei
 Nachdem die Ladeoptionen konfiguriert sind, können Sie die CSV-Datei in ein`Aspose.Cells.Workbook` Objekt.
### 3.1 Laden der CSV-Datei
 Wir laden die CSV-Datei durch Übergabe des Dateipfades und der konfigurierten`TxtLoadOptions` zur`Workbook` Konstruktor:
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
Dieser Schritt konvertiert Ihre CSV-Daten in eine voll funktionsfähige Excel-Arbeitsmappe, wobei jeder Wert entsprechend Ihren bevorzugten Regeln analysiert wird.
## Schritt 4: Auf Zellendaten zugreifen und diese anzeigen
Sobald die CSV-Datei in die Arbeitsmappe geladen ist, können Sie mit der Arbeit mit den Daten beginnen. Sie möchten beispielsweise den Typ und den Wert bestimmter Zellen ausdrucken.
### 4.1 Zelle A1 abrufen und anzeigen
Lassen Sie uns die erste Zelle (A1) abrufen und ihren Wert und Typ anzeigen:
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
 Hier die`Type` Eigenschaft zeigt den Datentyp an (z. B.`String` oder`DateTime` ), Und`DisplayStringValue` gibt Ihnen den formatierten Wert.
### 4.2 Zelle B1 abrufen und anzeigen
Auf ähnliche Weise können wir eine andere Zelle, beispielsweise B1, abrufen und anzeigen:
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
Dieser Vorgang kann für so viele Zellen wiederholt werden, wie Sie prüfen müssen.
## Schritt 5: Speichern der Arbeitsmappe
 Nachdem Sie mit den Daten gearbeitet haben, möchten Sie die Arbeitsmappe möglicherweise in einer neuen Datei speichern. Aspose.Cells macht dies einfach mit einem einfachen`Save` Verfahren:
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
Dadurch wird die Arbeitsmappe als Excel-Datei gespeichert, wobei die gesamte Formatierung und Datenanalyse, die Sie angewendet haben, erhalten bleibt.
## Abschluss
Das Öffnen von CSV-Dateien mit einem bevorzugten Parser in Aspose.Cells für .NET ist eine flexible und leistungsstarke Möglichkeit, verschiedene Datentypen zu verarbeiten. Indem Sie benutzerdefinierte Parser erstellen und Ladeoptionen konfigurieren, können Sie sicherstellen, dass Ihre CSV-Dateien genau so analysiert werden, wie Sie es benötigen, unabhängig davon, ob Sie mit Text, Daten oder anderen benutzerdefinierten Formaten arbeiten. Mit diesem Tutorial sind Sie nun in der Lage, komplexere Datenanalyseszenarien in Ihren Projekten zu verarbeiten.
## Häufig gestellte Fragen
### Was ist der Zweck benutzerdefinierter Parser in Aspose.Cells für .NET?
Mit benutzerdefinierten Parsern können Sie festlegen, wie bestimmte Datentypen, beispielsweise Text oder Daten, beim Laden einer CSV-Datei analysiert werden sollen.
### Kann ich in der CSV-Datei ein anderes Trennzeichen verwenden?
 Ja, Sie können jedes beliebige Zeichen als Trennzeichen im`TxtLoadOptions.Separator` Eigentum.
### Wie gehe ich mit der Kodierung in Aspose.Cells beim Laden einer CSV um?
 Sie können die`Encoding` Eigentum von`TxtLoadOptions` für jedes Kodierungsschema wie UTF-8, ASCII usw.
### Was passiert, wenn das Datumsformat in der CSV-Datei anders ist?
Sie können das spezifische Datumsformat mit einem benutzerdefinierten Parser definieren und so die korrekte Analyse der Datumswerte sicherstellen.
### Kann ich die Arbeitsmappe in anderen Formaten speichern?
Ja, Aspose.Cells ermöglicht Ihnen, die Arbeitsmappe in verschiedenen Formaten wie XLSX, CSV, PDF und mehr zu speichern.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
