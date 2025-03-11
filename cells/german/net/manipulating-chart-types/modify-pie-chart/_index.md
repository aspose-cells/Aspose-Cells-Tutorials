---
title: Kreisdiagramm ändern
linktitle: Kreisdiagramm ändern
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Nutzen Sie die Leistungsfähigkeit von Aspose.Cells für .NET, um Ihre Excel-Kreisdiagramme mühelos zu ändern. Folgen Sie diesem Tutorial für eine Schritt-für-Schritt-Anleitung.
weight: 16
url: /de/net/manipulating-chart-types/modify-pie-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kreisdiagramm ändern

## Einführung

Haben Sie sich schon einmal gefragt, wie Sie die Kreisdiagramme in Ihren Excel-Tabellen aufpeppen könnten? Kreisdiagramme können eine fantastische Möglichkeit sein, Daten zu visualisieren und Ihr Publikum zu fesseln und zu informieren. Manchmal erzählen diese Diagramme jedoch nicht sofort die Geschichte, die Sie erzählen möchten. Hier kommt Aspose.Cells für .NET ins Spiel. Mit dieser leistungsstarken Bibliothek können Sie Excel-Dateien programmgesteuert bearbeiten und erhalten die Tools, die Sie benötigen, um Ihre Kreisdiagramme bis ins kleinste Detail anzupassen. In diesem Tutorial werden wir uns eingehend mit der Änderung eines Kreisdiagramms mit Aspose.Cells befassen. Egal, ob es darum geht, Datenbeschriftungen zu ändern oder die Ästhetik des Diagramms zu optimieren.

## Voraussetzungen

Bevor wir uns in die Einzelheiten der Änderung von Kreisdiagrammen stürzen, sollten Sie einige Voraussetzungen erfüllen:

- Grundkenntnisse in C#: Grundlegende Kenntnisse der C#-Programmierung erleichtern Ihnen das Zurechtfinden.
- Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek installiert haben. Egal, ob Sie sich für die Vollversion oder eine kostenlose Testversion entscheiden, stellen Sie sicher, dass sie einsatzbereit ist.
- Visual Studio oder eine beliebige C#-IDE: Sie benötigen eine Umgebung zum Schreiben und Ausführen Ihres C#-Codes.
-  Excel-Beispieldatei: Für dieses Tutorial wird eine Excel-Beispieldatei mit dem Namen`sampleModifyPieChart.xlsx` verwendet wird.

 Sie können die Aspose.Cells-Bibliothek herunterladen[Hier](https://releases.aspose.com/cells/net/).

## Pakete importieren

Der erste Schritt auf unserem Weg besteht darin, die erforderlichen Pakete in unser C#-Projekt zu importieren. So können Sie das tun:

## Richten Sie Ihr Projekt ein

Öffnen Sie zunächst Ihre C# IDE (Visual Studio wird dringend empfohlen) und erstellen Sie ein neues Projekt:

1. Öffnen Sie Visual Studio.
2. Wählen Sie „Neues Projekt erstellen“.
3. Wählen Sie eine C#-Konsolenanwendung.
4.  Geben Sie Ihrem Projekt einen Namen (z. B.`ModifyPieChartDemo`).
5. Klicken Sie auf „Erstellen“.

## Installieren Sie Aspose.Cells

Sobald Ihr Projekt fertig ist, ist es an der Zeit, die Aspose.Cells-Bibliothek hinzuzufügen. Sie können sie mit NuGet installieren:

1. Klicken Sie im „Solution Explorer“ mit der rechten Maustaste auf Ihr Projekt.
2. Wählen Sie „NuGet-Pakete verwalten“ aus.
3. Navigieren Sie zur Registerkarte „Durchsuchen“.
4. Suchen Sie nach Aspose.Cells.
5. Klicken Sie auf „Installieren“ und akzeptieren Sie alle Lizenzvereinbarungen.

Nachdem Sie die Bibliothek installiert haben, importieren wir die erforderlichen Namespaces in Ihren Code.

## Namespaces importieren

 Ganz oben auf Ihrer`Program.cs` Importieren Sie die folgenden Namespaces:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Nachdem dies erledigt ist, können wir nun mit dem eigentlichen Code fortfahren!

## Schritt 1: Eingabe- und Ausgabeverzeichnisse definieren

Beginnen wir mit der Definition der Verzeichnisse für Ihre Eingabe- und Ausgabedateien. Hier geben Sie an, wo sich Ihre Excel-Datei befindet und wo Sie die geänderte Datei speichern möchten.

 In Ihrem`Main` Geben Sie den folgenden Code ein:

```csharp
// Ausgabeverzeichnis
string outputDir = "Your Output Directory Path";

// Quellverzeichnis
string sourceDir = "Your Document Directory Path";
```

 Ersetzen Sie unbedingt`Your Output Directory Path` Und`Your Document Directory Path` mit den tatsächlichen Pfaden auf Ihrem System.

## Schritt 2: Öffnen Sie die vorhandene Arbeitsmappe

 Als nächstes müssen wir die Excel-Datei öffnen, die das Kreisdiagramm enthält, das Sie ändern möchten. Verwenden Sie dazu das`Workbook` Klasse:

```csharp
// Öffnen Sie die vorhandene Datei.
Workbook workbook = new Workbook(sourceDir + "sampleModifyPieChart.xlsx");
```

 In diesem Snippet erstellen wir ein neues`Workbook` Objekt und laden unsere Excel-Datei hinein.

## Schritt 3: Zugriff auf das Arbeitsblatt

Schauen wir uns nun das Blatt an, das das Kreisdiagramm enthält. Wir gehen davon aus, dass sich das Kreisdiagramm auf dem zweiten Arbeitsblatt befindet (Index 1):

```csharp
// Holen Sie sich das Designerdiagramm auf dem zweiten Blatt.
Worksheet sheet = workbook.Worksheets[1];
```

 Durch den Zugriff auf die`Worksheets` Sammlung können wir zu dem spezifischen Blatt gelangen, das wir benötigen.

## Schritt 4: Holen Sie sich das Diagramm

Jetzt können wir auf das Diagramm selbst zugreifen. Vorausgesetzt, es gibt nur ein Diagramm auf diesem Arbeitsblatt, können wir es direkt abrufen:

```csharp
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Hier greifen wir auf das erste Diagramm aus dem angegebenen Arbeitsblatt zurück.

## Schritt 5: Auf Datenbeschriftungen zugreifen

Jetzt kommt der spannende Teil – das Ändern der Datenbeschriftungen im Kreisdiagramm. Greifen wir auf die Datenbeschriftungen der Datenreihe zu:

```csharp
// Holen Sie sich die Datenbeschriftungen in der Datenreihe des dritten Datenpunkts.
Aspose.Cells.Charts.DataLabels datalabels = chart.NSeries[0].Points[2].DataLabels;
```

Mit dieser Zeile zielen wir gezielt auf die Datenbeschriftungen für den dritten Punkt unserer Datenreihe ab. 

## Schritt 6: Ändern des Beschriftungstexts

Als Nächstes müssen wir den Inhalt des Etiketts ändern. Für unser Beispiel aktualisieren wir es auf „Vereinigtes Königreich, 400 K“:

```csharp
// Ändern Sie den Text des Etiketts.
datalabels.Text = "United Kingdom, 400K";
```

Und schon haben wir das Etikett aktualisiert! 

## Schritt 7: Speichern Sie die Arbeitsmappe

Nachdem wir nun unsere Änderungen vorgenommen haben, speichern wir die geänderte Arbeitsmappe. 

```csharp
// Speichern Sie die Excel-Datei.
workbook.Save(outputDir + "outputModifyPieChart.xlsx");
```

Diese Zeile speichert die Arbeitsmappe im angegebenen Ausgabeverzeichnis. 

## Schritt 8: Ausführung bestätigen

Lassen Sie uns abschließend eine Bestätigungsmeldung ausgeben, um sicherzustellen, dass alles reibungslos gelaufen ist:

```csharp
Console.WriteLine("ModifyPieChart executed successfully.");
```

Dies gibt Ihnen eine gewisse Sicherheit, dass Ihre Änderungen wie erwartet vorgenommen wurden.

# Abschluss

Da haben Sie es! Mit nur wenigen einfachen Schritten haben Sie erfolgreich ein Kreisdiagramm mit Aspose.Cells für .NET geändert. Diese leistungsstarke Bibliothek erleichtert nicht nur die Bearbeitung von Excel-Dateien, sondern ermöglicht Ihnen auch die Personalisierung Ihrer Datenvisualisierungen für maximale Wirkung. Wenn Sie in Ihrer Arbeit mit Datenpräsentationen arbeiten, lohnt es sich auf jeden Fall, Zeit in das Erlernen der Verwendung von Aspose.Cells zu investieren. Probieren Sie also diese Diagramme aus und sehen Sie, wie Sie Ihre Daten zum Leben erwecken können!

# Häufig gestellte Fragen

### Was ist Aspose.Cells für .NET?  
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek zum programmgesteuerten Erstellen, Bearbeiten und Konvertieren von Excel-Dateien ohne Microsoft Excel.

### Kann ich andere Diagramme als Kreisdiagramme ändern?  
Auf jeden Fall! Aspose.Cells unterstützt verschiedene Diagrammtypen, darunter Balken-, Linien- und Flächendiagramme, und ermöglicht so eine flexible Datenvisualisierung.

### Gibt es eine kostenlose Version von Aspose.Cells?  
Ja! Aspose bietet eine kostenlose Testversion an, mit der Sie die Bibliothek vor dem Kauf testen können.

### Wo finde ich Unterstützung für Aspose.Cells?  
Sie finden Unterstützung in den Aspose-Foren, wo Ihnen Community-Mitglieder und Aspose-Mitarbeiter weiterhelfen können.

### Muss Microsoft Excel installiert sein, um Aspose.Cells zu verwenden?  
Nein, Aspose.Cells funktioniert unabhängig von Microsoft Excel. Sie müssen es nicht auf Ihrem System installieren.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
