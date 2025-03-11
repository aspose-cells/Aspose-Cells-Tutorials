---
title: Liniendiagramm erstellen
linktitle: Liniendiagramm erstellen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erstellen Sie beeindruckende Liniendiagramme mit Aspose.Cells für .NET. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um Ihre Daten effektiv zu visualisieren.
weight: 11
url: /de/net/manipulating-chart-types/create-line-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Liniendiagramm erstellen

## Einführung

Sind Sie bereit, Ihre Daten in atemberaubender Klarheit zu visualisieren? Liniendiagramme sind eine fantastische Möglichkeit, Trends im Zeitverlauf oder die Beziehung zwischen zwei Variablen anzuzeigen. Egal, ob Sie Daten für ein Geschäftsprojekt verwalten oder persönliche Kennzahlen analysieren, die Möglichkeit, Liniendiagramme programmgesteuert zu erstellen, kann Ihnen Zeit sparen und mehr Flexibilität bieten. In diesem Handbuch führen wir Sie Schritt für Schritt durch die Erstellung eines Liniendiagramms mit Aspose.Cells für .NET. Bereit, loszulegen? Dann legen wir los!

## Voraussetzungen

Bevor wir uns in die Einzelheiten der Erstellung eines Liniendiagramms stürzen, stellen wir sicher, dass Sie den Schritten folgen können:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist, da es eine der beliebtesten IDEs für die .NET-Entwicklung ist.
2.  Aspose.Cells für .NET-Bibliothek: Sie benötigen die Aspose.Cells-Bibliothek, die Sie hier herunterladen können.[Hier](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Die Vertrautheit mit der Programmiersprache C# hilft Ihnen, die Beispiele und Codeausschnitte besser zu verstehen.
4. .NET Framework oder .NET Core: Eine grundlegende Konfiguration eines der beiden Frameworks, da dies die Grundlage für unsere Anwendungen bildet.

Sobald Sie diese Voraussetzungen erfüllt haben, können Sie mit der Erstellung einiger Diagramme beginnen!

## Pakete importieren

Nachdem wir unsere Umgebung eingerichtet haben, müssen wir die erforderlichen Pakete in unseren C#-Code importieren. Genau wie Sie Ihre Tools zusammenstellen, bevor Sie ein Projekt starten, ist das Importieren von Paketen wichtig, um sicherzustellen, dass Sie alles haben, was Sie brauchen.

So geht's:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

 Diese Zeile importiert die`Aspose.Cells` Namespace, der alle Klassen und Methoden enthält, die wir zum Erstellen unseres Liniendiagramms verwenden.

Lassen Sie uns nun den gesamten Prozess in einfache, leicht verständliche Schritte unterteilen. Jeder Schritt führt Sie durch den logischen Ablauf der Erstellung eines Liniendiagramms mit Aspose.Cells für .NET.

## Schritt 1: Einrichten des Ausgabeverzeichnisses

Der erste Schritt besteht darin, festzulegen, wo Sie Ihre Ausgabedatei speichern möchten. Das ist, als würden Sie Ihren Arbeitsbereich einrichten, bevor Sie mit der Arbeit beginnen. 

```csharp
// Ausgabeverzeichnis
string outputDir = "Your Output Directory";
```
 Ersetzen`"Your Output Directory"`durch den tatsächlichen Pfad, in dem Sie die generierte Excel-Datei speichern möchten.

## Schritt 2: Instanziieren des Arbeitsmappenobjekts

Als Nächstes müssen wir eine neue Arbeitsmappeninstanz erstellen. Stellen Sie sich die Arbeitsmappe als Leinwand vor, auf der Sie Ihrer Kreativität freien Lauf lassen können. 

```csharp
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
```
Diese Zeile initialisiert eine neue Arbeitsmappe, die alle Ihre Daten und Grafiken enthält.

## Schritt 3: Zugriff auf das Arbeitsblatt

In unserer neu erstellten Arbeitsmappe müssen wir einen Verweis auf das Arbeitsblatt erhalten, in das wir unsere Daten eingeben. Wenn die Arbeitsmappe unsere Leinwand ist, dann ist das Arbeitsblatt unsere Palette.

```csharp
// Abrufen der Referenz des neu hinzugefügten Arbeitsblatts durch Übergeben seines Blattindex
Worksheet worksheet = workbook.Worksheets[0];
```
 Hier greifen wir auf das erste Arbeitsblatt zu (Index`0`).

## Schritt 4: Beispielwerte zu Zellen hinzufügen

Jetzt kommt der spaßige Teil! Wir werden einige Beispielwerte in unser Arbeitsblatt eingeben. Diese Daten dienen als Grundlage für unser Liniendiagramm. 

```csharp
// Hinzufügen von Beispielwerten zu Zellen
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
In diesem Snippet fügen wir den Zellen in den Spalten A und B Werte hinzu. Spalte A stellt die Werte der X-Achse dar, während Spalte B die Werte der Y-Achse darstellt.

## Schritt 5: Fügen Sie dem Arbeitsblatt ein Liniendiagramm hinzu

Als Nächstes fügen wir dem Arbeitsblatt unser Liniendiagramm hinzu. Hier werden Ihre Daten wirklich zum Leben erweckt!

```csharp
// Hinzufügen eines Diagramms zum Arbeitsblatt
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Line, 5, 0, 25, 10);
```
Hier fügen wir an der angegebenen Stelle ein Liniendiagramm ein. Die Parameter (5, 0, 25, 10) definieren die Position und Größe des Diagramms innerhalb des Arbeitsblatts.

## Schritt 6: Zugriff auf die neue Diagramminstanz

Nachdem wir unser Diagramm hinzugefügt haben, ist es an der Zeit, das neu erstellte Diagrammobjekt in die Hände zu bekommen. 

```csharp
// Zugriff auf die Instanz des neu hinzugefügten Diagramms
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```
Dieser Code verbindet uns mit dem Diagramm, damit wir es weiter bearbeiten können.

## Schritt 7: SeriesCollection zum Diagramm hinzufügen

Jetzt müssen wir unserem Diagramm mitteilen, welche Daten angezeigt werden sollen. Hier definieren wir die Datenquelle für unser Liniendiagramm, indem wir eine SeriesCollection hinzufügen.

```csharp
// Hinzufügen einer SeriesCollection (Diagrammdatenquelle) zum Diagramm im Bereich von Zelle „A1“ bis Zelle „B3“
chart.NSeries.Add("A1:B3", true);
```
In diesem Beispiel weisen wir das Diagramm an, die Werte in den Zellen A1 bis B3 zu verwenden.

## Schritt 8: Speichern Sie die Excel-Datei

Das große Finale! Nach all Ihrer harten Arbeit ist es Zeit, die Excel-Datei zu speichern und Ihr Liniendiagramm in Aktion zu sehen.

```csharp
// Speichern der Excel-Datei
workbook.Save(outputDir + "outputHowToCreateLineChart.xlsx");
```
 Diese Zeile speichert Ihre Arbeitsmappe im angegebenen Ausgabeverzeichnis unter dem Namen`outputHowToCreateLineChart.xlsx`.

## Schritt 9: Ausführen und Überprüfen

Schließlich können Sie jetzt Ihren Code ausführen und überprüfen, ob das Liniendiagramm erfolgreich in Ihrem Ausgabeverzeichnis erstellt wurde! 

```csharp
Console.WriteLine("HowToCreateLineChart executed successfully.");
```
Dadurch wird in Ihrer Konsole eine Meldung ausgegeben, die Sie darüber informiert, dass alles reibungslos gelaufen ist.

## Abschluss

Das Erstellen eines Liniendiagramms mit Aspose.Cells für .NET ist eine effiziente Möglichkeit, Ihre Daten zum Leben zu erwecken. Indem Sie dieser Schritt-für-Schritt-Anleitung folgen, können Sie Trends und Beziehungen in Ihren Datensätzen problemlos visualisieren. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, Aspose.Cells bietet Ihnen die Flexibilität und Leistung, Ihre Datenvisualisierungsaufgaben zu automatisieren. 

## Häufig gestellte Fragen

### Was ist Aspose.Cells für .NET?  
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek zum programmgesteuerten Verwalten und Bearbeiten von Excel-Dateien, die es Entwicklern ermöglicht, Tabellen zu erstellen, zu bearbeiten und zu konvertieren.

### Unterstützt Aspose.Cells Diagramme?  
Ja, Aspose.Cells bietet umfassende Unterstützung für verschiedene Diagrammtypen, darunter Liniendiagramme, Kreisdiagramme, Balkendiagramme und mehr.

### Kann ich Aspose.Cells kostenlos nutzen?  
Ja, Sie können eine kostenlose Testversion herunterladen, um die Funktionen kennenzulernen. Für eine langfristige Nutzung sollten Sie den Kauf einer Lizenz in Erwägung ziehen.

### Gibt es ein Forum für Support?  
 Auf jeden Fall! Antworten und Fragen finden Sie auf der[Aspose.Cells-Forum](https://forum.aspose.com/c/cells/9).

### Wie kaufe ich eine Lizenz?  
 Lizenzen können einfach erworben werden über die[Kaufseite](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
