---
title: Numbers-Tabelle programmgesteuert in .NET lesen
linktitle: Numbers-Tabelle programmgesteuert in .NET lesen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem ausführlichen Tutorial, wie Sie Numbers-Tabellen lesen und sie mit Aspose.Cells für .NET in PDF konvertieren.
weight: 18
url: /de/net/converting-excel-files-to-other-formats/reading-numbers-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Numbers-Tabelle programmgesteuert in .NET lesen

## Einführung
In der heutigen digitalen Welt ist Datenmanagement eine unverzichtbare Fähigkeit, und Tabellenkalkulationen stehen bei der Datenorganisation an vorderster Front. Aber was, wenn Sie mit einer Numbers-Tabelle arbeiten müssen – also mit den Dateien, die von Apples Numbers-App erstellt werden – und dabei .NET verwenden? Keine Sorge, Sie sind nicht allein! In diesem Tutorial führen wir Sie durch den Prozess des programmgesteuerten Lesens einer Numbers-Tabelle mit Aspose.Cells für .NET. Sie erfahren, wie Sie eine Numbers-Datei laden und in PDF konvertieren.
## Voraussetzungen
Bevor wir beginnen, müssen Sie einige Dinge vorbereitet haben:
1. Aspose.Cells für .NET: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek installiert haben. Sie können sie herunterladen[Hier](https://releases.aspose.com/cells/net/).
2. Visual Studio: Es wird empfohlen, Visual Studio (oder eine andere .NET-kompatible IDE) auf Ihrem Computer zu installieren.
3. Grundkenntnisse in C#: Ein wenig Vertrautheit mit der C#-Programmierung wird Ihnen helfen, problemlos zurechtzukommen.
4. Ihr Dokumentverzeichnis: Sie benötigen ein Verzeichnis, in dem Ihre Numbers-Datei gespeichert ist, sowie einen Speicherort für die konvertierte PDF-Datei.
Wenn Sie diese Voraussetzungen erfüllt haben, können Sie loslegen!
## Pakete importieren
Zunächst müssen wir die erforderlichen Pakete in unser C#-Projekt importieren. Dies ist ein entscheidender Schritt, da wir dadurch die von der Aspose.Cells-Bibliothek bereitgestellten Funktionen nutzen können.
1. Öffnen Sie Ihr C#-Projekt in Visual Studio.
2. Fügen Sie einen Verweis auf die Aspose.Cells-Bibliothek hinzu:
   - Wenn Sie NuGet verwenden, führen Sie einfach den folgenden Befehl in der Paket-Manager-Konsole aus:
```
 Install-Package Aspose.Cells
 ```
3. Importieren Sie die erforderlichen Namespaces in Ihren Code:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nachdem wir nun die erforderlichen Pakete importiert haben, fahren wir mit der Schritt-für-Schritt-Anleitung zum Lesen einer Numbers-Tabelle fort.
## Schritt 1: Quell- und Ausgabeverzeichnisse angeben
In diesem Schritt richten wir die Verzeichnisse ein, in denen sich Ihre Quell-Numbers-Datei befindet und in denen Sie das Ausgabe-PDF speichern möchten.
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory"; // Aktualisieren Sie dies auf Ihr aktuelles Verzeichnis
// Ausgabeverzeichnis
string outputDir = "Your Document Directory"; // Aktualisieren Sie dies auf Ihr aktuelles Verzeichnis
```
 Hier definieren wir zwei Stringvariablen,`sourceDir` Und`outputDir` , um die Speicherorte der Eingabe- und Ausgabedateien anzugeben. Stellen Sie sicher, dass Sie ersetzen`"Your Document Directory"` mit den tatsächlichen Pfaden auf Ihrem System.
## Schritt 2: Ladeoptionen für das Zahlenformat einrichten
Als Nächstes geben wir die Ladeoptionen zum Lesen einer Numbers-Tabelle an. Dieser Schritt ist wichtig, da er Aspose mitteilt, wie die Numbers-Datei zu interpretieren ist.
```csharp
// Geben Sie Ladeoptionen an. Wir möchten die Numbers-Tabelle laden.
LoadOptions opts = new LoadOptions(LoadFormat.Numbers);
```
 Wir schaffen eine`LoadOptions` Objekt und geben Sie das Format an als`LoadFormat.Numbers`. Dadurch wird der Aspose.Cells-Bibliothek mitgeteilt, dass wir mit einer Numbers-Datei arbeiten. 
## Schritt 3: Laden Sie die Numbers-Tabelle in eine Arbeitsmappe
Nun ist es an der Zeit, die eigentliche Numbers-Tabelle in ein`Workbook` Objekt.
```csharp
// Laden Sie die Numbers-Tabelle mit den oben genannten Ladeoptionen in die Arbeitsmappe
Workbook wb = new Workbook(sourceDir + "sampleNumbersByAppleInc.numbers", opts);
```
 Wir instantiieren ein`Workbook` Objekt und übergeben Sie den Dateipfad der Numbers-Datei zusammen mit unseren Ladeoptionen. Stellen Sie sicher, dass der Dateiname (`sampleNumbersByAppleInc.numbers`) entspricht dem tatsächlichen Namen Ihrer Numbers-Datei.
## Schritt 4: Speichern Sie die Arbeitsmappe als PDF
Nachdem die Numbers-Datei erfolgreich geladen wurde, besteht der nächste Schritt darin, sie in einem anderen Format zu speichern, insbesondere im PDF-Format.
```csharp
// Speichern Sie die Arbeitsmappe im PDF-Format
wb.Save(outputDir + "outputNumbersByAppleInc.pdf", SaveFormat.Pdf);
```
 Hier nennen wir die`Save` Methode auf der`Workbook` Objekt, das den Ausgabedateipfad und das Format angibt, in dem wir es speichern möchten. In diesem Fall speichern wir es als PDF. Stellen Sie sicher, dass der Ausgabedateiname (`outputNumbersByAppleInc.pdf`) ist eindeutig und überschreibt keine vorhandenen Dateien.
## Schritt 5: Erfolg bestätigen
Fügen wir abschließend eine Nachricht hinzu, um zu bestätigen, dass unser Vorgang erfolgreich war.
```csharp
Console.WriteLine("ReadNumbersSpreadsheet executed successfully.\r\n");
```
Diese Codezeile gibt eine Erfolgsmeldung auf der Konsole aus, sobald alles erledigt ist. Es ist immer schön, Feedback zu bekommen, oder?
## Abschluss
Und da haben Sie es! Sie haben erfolgreich eine Numbers-Tabelle gelesen und sie mit Aspose.Cells für .NET in PDF konvertiert. Mit dieser leistungsstarken Bibliothek können Sie Tabellen mühelos bearbeiten, sodass Ihre Datenverwaltungsaufgaben zum Kinderspiel werden. Egal, ob Sie Anwendungen entwickeln oder Tabellen einfach effizienter handhaben müssen, Aspose.Cells ist ein fantastisches Tool für Ihren Werkzeugkasten.
## Häufig gestellte Fragen
### Welche Dateitypen kann Aspose.Cells lesen?  
Aspose.Cells kann eine Vielzahl von Dateiformaten lesen, darunter XLS-, XLSX-, CSV- und Numbers-Dateien. 
### Kann ich Numbers-Dateien mit Aspose.Cells bearbeiten?  
Ja, Sie können Numbers-Dateien mit Aspose.Cells lesen, bearbeiten und speichern.
### Ist die Nutzung von Aspose.Cells kostenlos?  
 Aspose.Cells bietet eine kostenlose Testversion an, für die erweiterte Nutzung benötigen Sie jedoch eine Lizenz. Überprüfen Sie die Preise[Hier](https://purchase.aspose.com/buy).
### Was mache ich, wenn beim Laden einer Numbers-Datei ein Fehler auftritt?  
 Stellen Sie sicher, dass Sie die richtigen Ladeoptionen verwenden und dass der Dateipfad korrekt ist. Weitere Unterstützung finden Sie im[Aspose Support Forum](https://forum.aspose.com/c/cells/9).
### Wie kann ich eine temporäre Lizenz für Aspose.Cells erhalten?  
 Sie können eine vorläufige Lizenz beantragen[Hier](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
