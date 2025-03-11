---
title: Festlegen der Formatoptionen für Pivot-Tabellen in .NET
linktitle: Festlegen der Formatoptionen für Pivot-Tabellen in .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET mühelos Pivot-Tabellen formatieren. Entdecken Sie schrittweise Techniken zur Verbesserung Ihrer Datenpräsentation.
weight: 20
url: /de/net/creating-and-configuring-pivot-tables/setting-format-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Festlegen der Formatoptionen für Pivot-Tabellen in .NET

## Einführung
Haben Sie sich schon einmal von der schieren Datenmenge überwältigt gefühlt, die Ihnen zur Verfügung steht? Oder haben Sie Schwierigkeiten gehabt, diese Daten klar und aufschlussreich darzustellen? Wenn ja, dann herzlich willkommen an Bord! Heute tauchen wir in die erstaunliche Welt der Pivot-Tabellen in Excel ein und verwenden dabei die Aspose.Cells-Bibliothek für .NET. Pivot-Tabellen können die Superhelden der Datenpräsentation sein und Unmengen von Zahlen in strukturierte, aufschlussreiche Berichte umwandeln, die die Entscheidungsfindung zum Kinderspiel machen. Ist das nicht ein echter Game-Changer?
## Voraussetzungen
Bevor wir mit dem Tutorial beginnen, stellen wir sicher, dass Sie über alles verfügen, was Sie zum Erfolg benötigen. Hier sind die Voraussetzungen:
1. Grundkenntnisse in C#: Sie sollten über grundlegende Kenntnisse der Programmiersprache C# verfügen. Wenn Sie mit den Grundlagen vertraut sind, sind Sie bereit, dies in Angriff zu nehmen!
2. Visual Studio oder eine beliebige C#-IDE: Sie benötigen eine integrierte Entwicklungsumgebung (IDE) wie Visual Studio. Hier geschieht die Magie. 
3. Aspose.Cells-Bibliothek: Um die Leistung von Aspose.Cells zu nutzen, müssen Sie dieses Paket herunterladen. Sie finden es ganz einfach unter[Aspose.Cells Download-Seite](https://releases.aspose.com/cells/net/).
4. Excel-Datei: Zum Ausführen des Tutorials ist eine Excel-Beispieldatei erforderlich. Sie können für diese Übung gerne einen einfachen Datensatz in einem Excel-Tabellenblatt (z. B. „Book1.xls“) erstellen.
5. .NET Framework: Stellen Sie sicher, dass das .NET Framework auf Ihrem Computer installiert ist.
Alles klar? Fantastisch! Jetzt machen wir uns an den ersten Schritt.
## Pakete importieren
Um die Aspose.Cells-Bibliothek verwenden zu können, müssen wir zunächst die erforderlichen Pakete importieren. So geht's:
### Öffnen Sie Ihr Projekt
Öffnen Sie Visual Studio (oder eine beliebige C#-IDE, die Sie verwenden) und erstellen Sie ein neues Projekt. Wählen Sie eine Konsolenanwendung, da Sie damit das Skript problemlos ausführen können.
### Aspose.Cells-Referenz hinzufügen
1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
2. Wählen Sie „NuGet-Pakete verwalten“ aus.
3.  Geben Sie in das Suchfeld ein`Aspose.Cells` und installieren Sie es.
Jetzt können Sie die Bibliothek einbinden. Sie müssen am Anfang Ihrer Codedatei die folgende using-Direktive hinzufügen:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
Über diese Zeile können Sie auf alle in der Aspose.Cells-Bibliothek verfügbaren Klassen und Methoden zugreifen.
Nachdem wir nun die Grundlagen gelegt haben, gehen wir nun Schritt für Schritt jeden Teil des Prozesses durch. Wir werden uns damit befassen, wie Sie verschiedene Formatierungsoptionen für eine Pivot-Tabelle effektiv festlegen.
## Schritt 1: Definieren Sie Ihr Dokumentverzeichnis
Zuerst müssen Sie den Pfad Ihres Dokumentverzeichnisses festlegen, in dem sich Ihre Excel-Eingabedatei befindet. Diese Codezeile gibt an, wo sich Ihre Dateien befinden.
```csharp
string dataDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad, in dem Ihre Datei „Book1.xls“ gespeichert ist. So weiß das Programm, wo es nach der Eingabedatei suchen muss.
## Schritt 2: Laden Sie die Vorlagendatei
 Als nächstes laden wir die Excel-Datei, die wir bearbeiten möchten. Dies geschieht mit dem`Workbook` Klasse.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
Im Wesentlichen weist dieser Befehl Ihr Programm an, die Datei „Book1.xls“ zu öffnen, damit wir mit ihren Daten arbeiten können.
## Schritt 3: Holen Sie sich das erste Arbeitsblatt
Nachdem wir nun unsere Arbeitsmappe geöffnet haben, tauchen wir in das Arbeitsblatt ein, das unsere Daten enthält. 
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Hier greifen wir auf das erste Arbeitsblatt der Arbeitsmappe zu (da die Indizierung bei Null beginnt). Wenn Ihre Daten auf einem anderen Blatt liegen, passen Sie einfach den Index an.
## Schritt 4: Zugriff auf die Pivot-Tabelle
Pivot-Tabellen sind leistungsstark, aber zuerst müssen wir uns die Tabelle aussuchen, mit der wir arbeiten möchten. Vorausgesetzt, Sie kennen den Index Ihrer Pivot-Tabelle, erfahren Sie hier, wie Sie darauf zugreifen.
```csharp
int pivotindex = 0;
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
In diesem Fall greifen wir auf die erste Pivot-Tabelle (Index 0) im Arbeitsblatt zu. 
## Schritt 5: Festlegen der Gesamtsummen für die Zeilen der Pivot-Tabelle
Beginnen wir mit der Formatierung! Wir können konfigurieren, ob Gesamtsummen für Zeilen in unserer Pivot-Tabelle angezeigt werden sollen.
```csharp
pivotTable.RowGrand = true;
```
 Wenn Sie diese Eigenschaft auf`true` zeigt die Gesamtsummen am Ende jeder Zeile in Ihrer Pivot-Tabelle an. Dies ist eine einfache, aber effektive Möglichkeit, Zusammenfassungen bereitzustellen.
## Schritt 6: Festlegen der Gesamtsummen für die Spalten der Pivot-Tabelle
Genauso wie wir Gesamtsummen für Zeilen festlegen, können wir dies auch für Spalten tun.
```csharp
pivotTable.ColumnGrand = true;
```
Wenn Sie diese Option aktivieren, werden auf der rechten Seite jeder Spalte Summen angezeigt. Jetzt ist Ihre Pivot-Tabelle ein Meister darin, Daten in beide Richtungen zusammenzufassen!
## Schritt 7: Benutzerdefinierte Zeichenfolge für Nullwerte anzeigen
Ein oft übersehenes Detail ist der Umgang mit Nullwerten. Möglicherweise möchten Sie, dass in Zellen mit Nullwerten eine bestimmte Zeichenfolge angezeigt wird. 
```csharp
pivotTable.DisplayNullString = true;
pivotTable.NullString = "null";
```
Dadurch wird die Pivot-Tabelle so eingerichtet, dass bei jeder leeren Zelle „Null“ angezeigt wird. Dies sorgt für mehr Übersichtlichkeit und Konsistenz in Ihren Berichten.
## Schritt 8: Festlegen des PivotTable-Layouts
Pivot-Tabellen können verschiedene Layouts haben und wir können sie je nach Bedarf anpassen. Lassen Sie uns das Layout auf „DownThenOver“ festlegen.
```csharp
pivotTable.PageFieldOrder = PrintOrderType.DownThenOver;
```
Dieser Befehl passt die Reihenfolge an, in der die Felder in Ihrem Bericht angezeigt werden, und sorgt so für eine leichtere Lesbarkeit. 
## Schritt 9: Speichern der Excel-Datei
Wenn Sie alle diese schönen Anpassungen vorgenommen haben, müssen Sie Ihre Änderungen schließlich wieder in einer Excel-Datei speichern. 
```csharp
workbook.Save(dataDir + "output.xls");
```
Diese Zeile speichert die geänderte Arbeitsmappe als „output.xls“ in Ihrem angegebenen Verzeichnis. 
Und schon haben Sie Ihre Pivot-Tabelle mit all diesen fantastischen Formatierungsoptionen erweitert!
## Abschluss
Wow, wir haben eine ziemliche Reise zusammen hinter uns, nicht wahr? Indem Sie die Funktionen der Aspose.Cells-Bibliothek für .NET nutzen, können Sie das Aussehen und Verhalten Ihrer Daten in Excel mühelos verändern. Wir haben erläutert, wie man eine Arbeitsmappe lädt, auf eine Pivot-Tabelle zugreift und sie formatiert, und zum Abschluss haben wir unsere Änderungen gespeichert. Daten müssen nicht eintönig und öde sein; mit ein paar Optimierungen können sie brillant glänzen.
## Häufig gestellte Fragen
### Was ist eine Pivot-Tabelle?
Pivot-Tabellen sind eine Excel-Funktion zum dynamischen Zusammenfassen und Analysieren von Daten.
### Muss Excel installiert sein, um Aspose.Cells zu verwenden?
Nein, Aspose.Cells ist eine eigenständige Bibliothek, für die keine Installation von Excel erforderlich ist.
### Kann ich mit Aspose.Cells Pivot-Tabellen erstellen?
Ja, mit Aspose.Cells können Sie Pivot-Tabellen erstellen, ändern und bearbeiten.
### Ist Aspose.Cells kostenlos?
Aspose.Cells ist eine kostenpflichtige Bibliothek, aber eine kostenlose Testversion ist verfügbar.
### Wo finde ich weitere Aspose.Cells-Dokumentation?
 Schauen Sie sich die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für ausführliche Anleitungen und Beispiele.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
