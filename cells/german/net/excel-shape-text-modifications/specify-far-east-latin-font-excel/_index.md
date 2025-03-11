---
title: Geben Sie in Excel die fernöstliche und lateinische Schriftart an
linktitle: Geben Sie in Excel die fernöstliche und lateinische Schriftart an
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem umfassenden und leicht verständlichen Tutorial, wie Sie mit Aspose.Cells für .NET fernöstliche und lateinische Schriftarten in Excel angeben.
weight: 17
url: /de/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Geben Sie in Excel die fernöstliche und lateinische Schriftart an

## Einführung
Möchten Sie Ihre Excel-Berichte oder -Dokumente mit bestimmten Schriftartanforderungen verbessern? Egal, ob Sie mit mehreren Sprachen arbeiten oder einfach nur eine einzigartige Ästhetik in Ihren Tabellenkalkulationen anstreben, das Verständnis, wie fernöstliche und lateinische Schriftarten in Excel angegeben werden, ist eine wichtige Fähigkeit. Zum Glück haben wir eine Lösung für Sie! In diesem Tutorial untersuchen wir, wie Sie Aspose.Cells für .NET verwenden, um diese Funktion nahtlos zu implementieren. Tauchen wir ein!
## Voraussetzungen
Bevor wir ins Detail gehen, müssen Sie einige Dinge einrichten, bevor Sie mit Aspose.Cells beginnen können:
### .NET Framework oder .NET Core
Stellen Sie sicher, dass auf Ihrem Computer .NET Framework oder .NET Core installiert ist. Diese Bibliothek funktioniert mit beiden problemlos.
### Installation von Aspose.Cells
 Sie müssen die Aspose.Cells-Bibliothek herunterladen. Sie können[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/) Wenn Sie mit der Installation von NuGet-Paketen nicht vertraut sind, folgen Sie[dieser Leitfaden](https://www.nuget.org/).
### Integrierte Entwicklungsumgebung (IDE)
Eine IDE wie Visual Studio oder JetBrains Rider kann die Codierung, das Debuggen und die Ausführung Ihres Projekts vereinfachen.
### Grundkenntnisse in C#
Um diesem Tutorial folgen zu können, sind Kenntnisse in der C#-Programmierung von großem Nutzen.
## Pakete importieren
Bevor wir mit Aspose.Cells arbeiten können, müssen wir die erforderlichen Pakete in unser Projekt importieren. So können Sie das tun:
### Neues Projekt erstellen
1. Öffnen Sie Ihre IDE und erstellen Sie ein neues Konsolenanwendungsprojekt.
2.  Geben Sie Ihrem Projekt einen aussagekräftigen Namen, wie`FontSpecifyingApp`.
### Aspose.Cells NuGet-Paket hinzufügen
1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
2.  Wählen`Manage NuGet Packages...`.
3.  Suchen nach`Aspose.Cells` und installieren Sie es.
Am Ende dieser Schritte sollte alles bereit sein, um mit dem Codieren zu beginnen!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Wenn die Einrichtung abgeschlossen ist, ist es an der Zeit, die Ärmel hochzukrempeln und mit dem Codieren zu beginnen. Konkret erstellen wir eine neue Excel-Arbeitsmappe und geben sowohl die fernöstliche als auch die lateinische Schriftart für Textfelder an. So gehen Sie Schritt für Schritt vor:
## Schritt 1: Einrichten des Ausgabeverzeichnisses
Wir beginnen damit, anzugeben, wo wir unsere Excel-Datei speichern möchten. Dies ist wichtig, da wir sicherstellen möchten, dass unsere Ausgabedatei an einem leicht zugänglichen Ort gespeichert wird.
```csharp
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
## Schritt 2: Erstellen Sie eine leere Arbeitsmappe
Nachdem wir nun unser Verzeichnis eingerichtet haben, erstellen wir eine neue Arbeitsmappe, in die wir unseren Inhalt einfügen. Das ist vergleichbar damit, vor dem Malen mit einer leeren Leinwand zu beginnen.
```csharp
// Erstellen Sie eine leere Arbeitsmappe.
Workbook wb = new Workbook();
```
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Als nächstes wollen wir mit einem Arbeitsblatt aus unserer Arbeitsmappe arbeiten. Stellen Sie sich ein Arbeitsblatt als eine Seite in Ihrem Buch vor, auf der die ganze Magie passiert.
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu.
Worksheet ws = wb.Worksheets[0];
```
## Schritt 4: Fügen Sie ein Textfeld hinzu
Jetzt fügen wir unserem Arbeitsblatt ein Textfeld hinzu. Hier geben wir unseren Text ein. Stellen Sie sich das so vor, als würden Sie ein Textfeld innerhalb einer Folie einer Präsentation erstellen.
```csharp
// Fügen Sie dem Arbeitsblatt ein Textfeld hinzu.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Schritt 5: Legen Sie den Text des Textfelds fest
Lassen Sie uns einen Text eingeben. In diesem Beispiel werden wir japanische Zeichen eingeben, um die Schriftart Far East zu demonstrieren. Es ist so einfach wie das Schreiben in ein Textfeld auf Ihrem Computer!
```csharp
// Legen Sie den Text des Textfelds fest.
tb.Text = "こんにちは世界"; //Dies bedeutet auf Japanisch „Hallo Welt“.
```
## Schritt 6: Schriftarten festlegen
Jetzt kommt der spannende Teil! Wir legen sowohl die lateinische als auch die fernöstliche Schriftart für den Text fest. Das ist vergleichbar mit der Auswahl der perfekten Schriftart für eine schicke Hochzeitseinladung!
```csharp
// Geben Sie den fernöstlichen und lateinischen Namen der Schriftart an.
tb.TextOptions.LatinName = "Comic Sans MS"; // Dies ist unsere ausgewählte lateinische Schriftart.
tb.TextOptions.FarEastName = "KaiTi"; // Dies ist unsere gewünschte fernöstliche Schriftart.
```
## Schritt 7: Speichern Sie die Excel-Ausgabedatei
Zum Schluss speichern wir unsere Arbeitsmappe! Mit diesem Schritt schließen wir unsere Aufgabe ab und stellen sicher, dass die ganze harte Arbeit, die wir geleistet haben, ordnungsgemäß gespeichert wird. 
```csharp
// Speichern Sie die Excel-Ausgabedatei.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Schritt 8: Bestätigungsnachricht
Um uns mitzuteilen, dass alles erfolgreich ausgeführt wurde, drucken wir eine Bestätigungsmeldung auf die Konsole:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Abschluss
Und da haben Sie es! Sie haben erfolgreich fernöstliche und lateinische Schriftarten in einer Excel-Arbeitsmappe mit Aspose.Cells für .NET angegeben. Diese Fähigkeit verleiht Ihren Dokumenten nicht nur einen professionellen Touch, sondern bereichert auch das Leseerlebnis für Benutzer verschiedener Sprachen.
Experimentieren Sie ruhig mit verschiedenen Schriftarten und Stilen, um eine Kombination zu finden, die Ihren spezifischen Anforderungen entspricht. Viel Spaß beim Programmieren!
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek zum Erstellen und Verwalten von Excel-Tabellen, ohne dass Microsoft Excel auf Ihrem Computer installiert sein muss. 
### Kann ich Aspose.Cells für Webanwendungen verwenden?
Ja! Aspose.Cells kann sowohl für Desktop-Anwendungen als auch für mit .NET erstellte Webanwendungen verwendet werden.
### Gibt es eine kostenlose Version von Aspose.Cells?
 Ja, Aspose bietet eine kostenlose Testversion an. Sie können[Laden Sie es hier herunter](https://releases.aspose.com/).
### Wie erhalte ich Unterstützung für Aspose.Cells?
 Sie können um Unterstützung bitten und wertvolle Ressourcen finden auf der[Aspose-Foren](https://forum.aspose.com/c/cells/9).
### Wo kann ich Aspose.Cells kaufen?
 Sie können Aspose.Cells direkt kaufen bei der[Aspose-Website](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
