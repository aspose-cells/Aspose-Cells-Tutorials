---
title: Programmgesteuertes Konvertieren von JSON in CSV in .NET
linktitle: Programmgesteuertes Konvertieren von JSON in CSV in .NET
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells JSON programmgesteuert in .NET in CSV konvertieren. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um eine nahtlose Datentransformation zu gewährleisten.
weight: 15
url: /de/net/converting-excel-files-to-other-formats/converting-json-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programmgesteuertes Konvertieren von JSON in CSV in .NET

## Einführung
In der heutigen digitalen Welt ist die Handhabung von Daten in mehreren Formaten alltäglich geworden, und JSON (JavaScript Object Notation) ist eines der am häufigsten verwendeten Formate für den Datenaustausch. Aber was passiert, wenn Sie dieses JSON in ein für die Analyse leichter zugängliches Format wie CSV (Comma Separated Values) umwandeln müssen? Dieses Tutorial führt Sie durch den Prozess der programmgesteuerten Konvertierung von JSON in CSV mithilfe von Aspose.Cells für .NET – einer benutzerfreundlichen und dennoch leistungsstarken API zur Tabellenkalkulationsbearbeitung. 
## Voraussetzungen
Bevor wir uns in den Code vertiefen, müssen Sie sicherstellen, dass Sie über alle erforderlichen Komponenten und ein grundlegendes Verständnis der von uns verwendeten Tools verfügen. Lassen Sie uns skizzieren, was Sie benötigen:
-  Aspose.Cells für .NET: Dies ist die primäre Bibliothek, die wir für die Konvertierung von JSON in CSV verwenden werden. Sie können[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
- Visual Studio: Sie benötigen eine integrierte Entwicklungsumgebung (IDE) wie Visual Studio, um den .NET-Code zu schreiben und auszuführen.
- .NET Framework: Stellen Sie sicher, dass Sie das .NET Framework installiert haben. Aspose.Cells ist sowohl mit .NET Core als auch mit .NET Framework kompatibel.
- Grundkenntnisse in C#: Obwohl in diesem Handbuch jeder Teil des Codes aufgeschlüsselt wird, ist es hilfreich, wenn Sie einigermaßen mit C# vertraut sind.
## Pakete importieren
Um Aspose.Cells in Ihrem .NET-Projekt zu verwenden, müssen Sie zuerst die Bibliothek installieren. Sie können dies über den NuGet-Paket-Manager tun:
1. Öffnen Sie Visual Studio.
2. Gehen Sie zu Tools > NuGet-Paket-Manager > NuGet-Pakete für Lösung verwalten.
3. Suchen Sie nach Aspose.Cells und installieren Sie die neueste Version.
Stellen Sie nach der Installation sicher, dass Sie die folgenden Namespaces in Ihren Code einschließen:
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
Nachdem nun alles eingerichtet ist, analysieren wir den Code Schritt für Schritt, damit Sie sehen, wie einfach es ist, mit Aspose.Cells eine JSON-Datei in eine CSV-Datei zu konvertieren.
## Schritt 1: Lesen Sie die JSON-Datei
 Als erstes müssen wir die JSON-Daten aus einer Datei lesen. Wir gehen davon aus, dass Sie bereits eine JSON-Datei haben (nennen wir sie`SampleJson.json`) in einem Verzeichnis auf Ihrem System gespeichert.
Sie können die`File.ReadAllText()` Methode in C#, um den Inhalt der JSON-Datei in eine Zeichenfolge zu lesen.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// JSON-Datei lesen
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

Dieser Schritt ist entscheidend, da Sie die JSON-Rohdaten benötigen, um den Konvertierungsprozess zu starten. Indem Sie sie als Zeichenfolge lesen, bereiten Sie sie für die Verarbeitung durch Aspose.Cells vor.
## Schritt 2: Erstellen Sie eine leere Arbeitsmappe
Aspose.Cells arbeitet hauptsächlich mit Arbeitsmappen (Excel-Dateien). Um mit dem Importieren von JSON-Daten zu beginnen, müssen Sie zunächst eine leere Arbeitsmappe erstellen, in die diese Daten eingefügt werden.
```csharp
// Leere Arbeitsmappe erstellen
Workbook workbook = new Workbook();
```
Hier initialisieren Sie eine leere Arbeitsmappe, die schließlich die CSV-formatierten Daten enthalten wird. Stellen Sie es sich so vor, als würden Sie eine leere Tabelle in Excel erstellen, die bald mit Ihren JSON-Daten gefüllt wird.
## Schritt 3: Auf die Zellen in der Arbeitsmappe zugreifen
 Da wir nun eine leere Arbeitsmappe haben, müssen wir auf deren Zellen zugreifen.`Cells` Die Sammlung in Aspose.Cells stellt alle Zellen in einem Arbeitsblatt dar, in die Sie Ihre JSON-Daten einfügen.
```csharp
// Zellen abrufen
Cells cells = workbook.Worksheets[0].Cells;
```
Dieser Codeausschnitt wählt das erste Arbeitsblatt (Arbeitsblatt bei Index 0) aus und erhält dessen`Cells` Sammlung. Diese Zellen sind wie das Raster einer Tabelle, in das Daten eingefügt werden.
## Schritt 4: JsonLayoutOptions festlegen
 Aspose.Cells bietet verschiedene Anpassungsoptionen für den Import Ihrer JSON-Daten. Hier definieren wir`JsonLayoutOptions` um anzugeben, wie Aspose mit Arrays, numerischen Daten und Objekttiteln umgehen soll.
```csharp
// JsonLayoutOptions festlegen
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: Konvertiert automatisch Zeichenfolgenwerte, die numerische oder Datumswerte sind.
- ArrayAsTable: Behandeln Sie Arrays in JSON als Tabellen in der Arbeitsmappe.
- IgnoreArrayTitle und IgnoreObjectTitle: Diese Optionen ignorieren Titel für Arrays und Objekte und stellen sicher, dass nur die Rohdaten importiert werden.
## Schritt 5: Importieren der JSON-Daten
 Sobald die Layout-Optionen festgelegt sind, ist es an der Zeit, die JSON-Daten einzufügen. Die`JsonUtility.ImportData()` Die Methode übernimmt hier die Schwerstarbeit, indem sie die JSON-Daten in die Zellen der Arbeitsmappe einfügt.
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
Diese Methode verwendet mehrere Parameter:
- `str`Die JSON-Zeichenfolge, die wir in Schritt 1 gelesen haben.
- `cells`: Die Zellensammlung, in der die Daten platziert werden.
- `0, 0`: Dies sind die Zeilen- und Spaltenindizes, die angeben, wo die Daten beginnen sollen (d. h. in der oberen linken Ecke).
- `importOptions`: Die Layoutoptionen, die wir in Schritt 4 festgelegt haben.
## Schritt 6: Speichern Sie die Arbeitsmappe als CSV
Da sich die JSON-Daten nun in der Arbeitsmappe befinden, können wir diese problemlos als CSV-Datei speichern. CSV ist ein einfaches, leichtes Format zum Speichern tabellarischer Daten und eignet sich daher perfekt für die Datenanalyse.
```csharp
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
// Arbeitsmappe speichern
workbook.Save(outputDir + @"SampleJson_out.csv");
```
In diesem Schritt speichern wir die Arbeitsmappe als CSV-Datei. Sie geben den Pfad und den Dateinamen an (`SampleJson_out.csv`), wo die CSV gespeichert wird.
## Schritt 7: Bestätigen Sie den Vorgang
Um sicherzustellen, dass alles wie erwartet funktioniert hat, können wir eine Bestätigungsnachricht in der Konsole ausdrucken.
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
Eine einfache Erfolgsmeldung bestätigt, dass der Vorgang reibungslos verlief.
## Abschluss
Die Konvertierung von JSON in CSV mit Aspose.Cells für .NET ist ein unkomplizierter und dennoch leistungsstarker Prozess. Mit nur wenigen Codezeilen können Sie komplexe JSON-Daten in ein zugänglicheres CSV-Format umwandeln. Egal, ob Sie mit Arrays, Objekten oder numerischen Daten arbeiten, Aspose.Cells macht es einfach, den Konvertierungsprozess an Ihre Bedürfnisse anzupassen.
## Häufig gestellte Fragen
### Kann Aspose.Cells große JSON-Dateien verarbeiten?
Ja, Aspose.Cells ist für die effiziente Handhabung großer Datensätze konzipiert und eignet sich daher für die Verarbeitung großer JSON-Dateien ohne Leistungsprobleme.
### Wie kann ich die CSV-Ausgabe anpassen?
 Sie können die CSV-Ausgabe anpassen, indem Sie die`JsonLayoutOptions` oder die Formatierung der Arbeitsmappe bearbeiten, bevor Sie sie als CSV speichern.
### Gibt es eine Möglichkeit, bei der Konvertierung bestimmte Daten aus dem JSON auszuschließen?
Ja, indem Sie das JSON optimieren oder vor dem Importieren eine benutzerdefinierte Codelogik verwenden, können Sie bestimmte Datenfelder ausschließen oder herausfiltern.
### Unterstützt Aspose.Cells andere Dateiformate außer CSV?
Auf jeden Fall! Aspose.Cells unterstützt eine Vielzahl von Formaten, darunter Excel (XLS, XLSX), PDF, HTML und viele mehr.
### Wie kann ich Aspose.Cells kostenlos testen?
 Du kannst[Laden Sie hier eine kostenlose Testversion herunter](https://releases.aspose.com/) um alle Funktionen vor dem Kauf zu testen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
