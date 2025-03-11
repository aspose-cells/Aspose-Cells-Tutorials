---
title: Komprimierungsstufe anpassen
linktitle: Komprimierungsstufe anpassen
second_title: Aspose.Cells für .NET API-Referenz
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET die Komprimierungsstufen für Excel-Dateien anpassen. Optimieren Sie Ihre Dateigrößen effizient mit dieser Schritt-für-Schritt-Anleitung.
weight: 50
url: /de/net/excel-workbook/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Komprimierungsstufe anpassen

## Einführung

Beim Umgang mit großen Excel-Dateien ist eine effiziente Speicherung entscheidend. Egal, ob Sie Entwickler sind und die Dateigröße optimieren möchten, oder Datenanalyst, der Dateiübertragungen beschleunigen möchte: Wenn Sie wissen, wie Sie die Komprimierungsstufen in Aspose.Cells für .NET anpassen, kann das von entscheidender Bedeutung sein. In dieser Anleitung führen wir Sie durch die Schritte zum Anpassen der Komprimierungsstufen beim Speichern von Excel-Dateien und stellen so sicher, dass Sie die Leistung beibehalten, ohne die Qualität zu beeinträchtigen.

## Voraussetzungen

Bevor wir uns mit den Einzelheiten der Komprimierungsstufen befassen, stellen wir sicher, dass Sie alles haben, was Sie für den Einstieg benötigen:

1. Grundkenntnisse in C#: Grundlegende Kenntnisse der C#-Programmierung sind unerlässlich. Wenn Sie mit Variablen, Schleifen und grundlegenden Dateioperationen vertraut sind, können Sie loslegen!
2. Aspose.Cells für .NET-Bibliothek: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek installiert haben. Sie können sie von der[Webseite](https://releases.aspose.com/cells/net/) Wenn Sie gerade erst anfangen, sollten Sie eine kostenlose Testversion in Betracht ziehen[Hier](https://releases.aspose.com/).
3. Entwicklungsumgebung: Richten Sie Ihre Entwicklungsumgebung, idealerweise Visual Studio, ein, um Ihren C#-Code zu schreiben und auszuführen. 
4. Beispiel-Excel-Datei: Halten Sie eine große Excel-Datei zum Testen bereit. Sie können eine neue Datei erstellen oder eine vorhandene Datei verwenden. Stellen Sie jedoch sicher, dass sie groß genug ist, um die Auswirkungen der Komprimierung zu sehen.

Nachdem diese Voraussetzungen erfüllt sind, können wir loslegen!

## Pakete importieren

Bevor wir Excel-Dateien bearbeiten können, müssen wir die erforderlichen Namespaces importieren. Dies ist ein entscheidender Schritt, der uns den Zugriff auf die von Aspose.Cells bereitgestellten Klassen und Methoden ermöglicht.

### Importieren Sie den Aspose.Cells-Namespace

```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```

 Dieser Codeausschnitt importiert die`Aspose.Cells` Namespace, der alle Klassen enthält, die für die Arbeit mit Excel-Dateien erforderlich sind. Der`Aspose.Cells.Xlsb` Der Namespace ist speziell für die Handhabung von XLSB-Dateiformaten gedacht.

Nachdem wir nun alles eingerichtet haben, unterteilen wir den Vorgang zum Anpassen der Komprimierungsstufen in überschaubare Schritte. Wir speichern eine Arbeitsmappe mit verschiedenen Komprimierungsstufen und messen die für jeden Vorgang benötigte Zeit. 

## Schritt 1: Richten Sie Ihre Verzeichnisse ein

Als Erstes müssen wir definieren, wo unsere Dateien gespeichert werden. Dazu müssen wir das Quellverzeichnis für unsere Eingabedatei und das Ausgabeverzeichnis für unsere komprimierten Dateien angeben.

```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```

## Schritt 2: Laden Sie die Arbeitsmappe

Als Nächstes laden wir die Excel-Arbeitsmappe, die wir komprimieren möchten. Hier verweisen Sie auf Ihre große Excel-Datei.

```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```

 Diese Zeile initialisiert eine neue`Workbook` Objekt mit der angegebenen Datei. Stellen Sie sicher, dass der Dateipfad korrekt ist. Andernfalls treten Fehler auf.

## Schritt 3: Speicheroptionen für XLSB erstellen

 Jetzt erstellen wir eine Instanz von`XlsbSaveOptions`, wodurch wir angeben können, wie wir unsere Arbeitsmappe speichern möchten, einschließlich der Komprimierungsstufe.

```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```

Diese Zeile bereitet die Optionen vor, die wir zum Speichern unserer Arbeitsmappe im XLSB-Format verwenden.

## Schritt 4: Komprimierungsstufen festlegen und messen

Jetzt kommt der spaßige Teil! Wir speichern die Arbeitsmappe mit unterschiedlichen Komprimierungsstufen und messen die für jeden Vorgang benötigte Zeit. 

### Komprimierung der Stufe 1

Beginnen wir mit der niedrigsten Komprimierungsstufe:

```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```

In diesem Snippet setzen wir den Komprimierungstyp auf Stufe 1, speichern die Arbeitsmappe und protokollieren die benötigte Zeit. 

### Komprimierung der Stufe 6

Als Nächstes versuchen wir es mit einer Komprimierungsstufe im mittleren Bereich:

```csharp
options.CompressionType = OoxmlCompressionType.Level6;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```

Diesmal stellen wir den Komprimierungstyp auf Stufe 6 und wiederholen den Speichervorgang.

### Komprimierung der Stufe 9

Zum Schluss speichern wir mit der höchsten Komprimierungsstufe:

```csharp
options.CompressionType = OoxmlCompressionType.Level9;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```

In diesem Schritt stellen wir den Komprimierungstyp auf Stufe 9 ein. Dies sollte die kleinste Dateigröße ergeben, das Speichern kann jedoch länger dauern.

## Schritt 5: Endgültige Ausgabe

Nachdem Sie alle oben genannten Schritte ausgeführt haben, wird die verstrichene Zeit für jede Komprimierungsstufe auf der Konsole angezeigt. 

```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```

Diese Zeile bestätigt, dass der gesamte Vorgang ohne Probleme abgeschlossen wurde.

## Abschluss

Das Anpassen der Komprimierungsstufen beim Speichern von Excel-Dateien mit Aspose.Cells für .NET ist eine einfache, aber leistungsstarke Technik. Indem Sie die in diesem Handbuch beschriebenen Schritte befolgen, können Sie die Dateigröße problemlos ändern und sie so für die Speicherung und Übertragung besser handhabbar machen. Ganz gleich, ob Sie schnellen Zugriff auf Daten benötigen oder die Leistung Ihrer Anwendung optimieren möchten – die Beherrschung dieser Techniken wird Ihre Fähigkeiten als Entwickler zweifellos verbessern.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek, mit der Entwickler Excel-Dateien programmgesteuert erstellen, bearbeiten und konvertieren können.

### Wie lade ich Aspose.Cells herunter?
 Sie können die Aspose.Cells-Bibliothek herunterladen von der[Webseite](https://releases.aspose.com/cells/net/).

### Kann ich Aspose.Cells kostenlos nutzen?
 Ja, Aspose bietet eine kostenlose Testversion an, auf die Sie zugreifen können[Hier](https://releases.aspose.com/).

### Welche unterschiedlichen Komprimierungsstufen sind verfügbar?
Aspose.Cells unterstützt mehrere Komprimierungsstufen von Stufe 1 (geringste Komprimierung) bis Stufe 9 (maximale Komprimierung).

### Wo finde ich Unterstützung für Aspose.Cells?
 Sie erhalten Unterstützung und können Fragen stellen auf der[Aspose-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
