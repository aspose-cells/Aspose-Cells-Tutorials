---
"description": "Erfahren Sie in diesem umfassenden und leicht verständlichen Tutorial, wie Sie mit Aspose.Cells für .NET fernöstliche und lateinische Schriftarten in Excel angeben."
"linktitle": "Geben Sie die fernöstliche und lateinische Schriftart in Excel an"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Geben Sie die fernöstliche und lateinische Schriftart in Excel an"
"url": "/de/net/excel-shape-text-modifications/specify-far-east-latin-font-excel/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Geben Sie die fernöstliche und lateinische Schriftart in Excel an

## Einführung
Möchten Sie Ihre Excel-Berichte oder -Dokumente mit spezifischen Schriftarten optimieren? Egal, ob Sie mehrere Sprachen verwenden oder Ihren Tabellen eine einzigartige Ästhetik verleihen möchten – das Wissen, wie Sie fernöstliche und lateinische Schriftarten in Excel definieren, ist unerlässlich. Zum Glück haben wir die Lösung! In diesem Tutorial erfahren Sie, wie Sie diese Funktion mit Aspose.Cells für .NET nahtlos implementieren. Los geht‘s!
## Voraussetzungen
Bevor wir ins Detail gehen, müssen Sie einige Dinge einrichten, bevor Sie mit Aspose.Cells beginnen können:
### .NET Framework oder .NET Core
Stellen Sie sicher, dass .NET Framework oder .NET Core auf Ihrem Computer installiert ist. Diese Bibliothek funktioniert mit beiden problemlos.
### Installation von Aspose.Cells
Sie müssen die Aspose.Cells-Bibliothek herunterladen. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/cells/net/)Wenn Sie mit der Installation von NuGet-Paketen nicht vertraut sind, folgen Sie [dieses Handbuch](https://www.nuget.org/).
### Integrierte Entwicklungsumgebung (IDE)
Eine IDE wie Visual Studio oder JetBrains Rider kann das Codieren, Debuggen und Ausführen Ihres Projekts vereinfachen.
### Grundkenntnisse in C#
Um diesem Tutorial folgen zu können, sind Kenntnisse in der C#-Programmierung von großem Nutzen.
## Pakete importieren
Bevor wir mit Aspose.Cells arbeiten können, müssen wir die erforderlichen Pakete in unser Projekt importieren. So geht's:
### Neues Projekt erstellen
1. Öffnen Sie Ihre IDE und erstellen Sie ein neues Konsolenanwendungsprojekt.
2. Geben Sie Ihrem Projekt einen aussagekräftigen Namen, wie zum Beispiel `FontSpecifyingApp`.
### Aspose.Cells NuGet-Paket hinzufügen
1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
2. Wählen `Manage NuGet Packages...`.
3. Suchen nach `Aspose.Cells` und installieren Sie es.
Am Ende dieser Schritte sollte alles bereit sein, um mit dem Programmieren zu beginnen!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nach der Einrichtung können Sie mit dem Programmieren beginnen. Wir erstellen eine neue Excel-Arbeitsmappe und legen für Textfelder sowohl die fernöstliche als auch die lateinische Schriftart fest. So geht's Schritt für Schritt:
## Schritt 1: Einrichten des Ausgabeverzeichnisses
Wir legen zunächst fest, wo wir unsere Excel-Datei speichern möchten. Dies ist wichtig, da wir sicherstellen möchten, dass unsere Ausgabedatei an einem leicht zugänglichen Ort gespeichert wird.
```csharp
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
## Schritt 2: Erstellen Sie eine leere Arbeitsmappe
Nachdem wir unser Verzeichnis eingerichtet haben, erstellen wir eine neue Arbeitsmappe, in die wir unsere Inhalte einfügen. Das ist vergleichbar mit dem Beginn einer neuen Leinwand vor dem Malen.
```csharp
// Erstellen Sie eine leere Arbeitsmappe.
Workbook wb = new Workbook();
```
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Als Nächstes möchten wir mit einem Arbeitsblatt aus unserer Arbeitsmappe arbeiten. Stellen Sie sich ein Arbeitsblatt wie eine Seite in Ihrem Buch vor, auf der die ganze Magie passiert.
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu.
Worksheet ws = wb.Worksheets[0];
```
## Schritt 4: Fügen Sie ein Textfeld hinzu
Jetzt fügen wir unserem Arbeitsblatt ein Textfeld hinzu. Hier geben wir unseren Text ein. Stellen Sie sich das wie das Erstellen eines Textfelds innerhalb einer Präsentationsfolie vor.
```csharp
// Fügen Sie dem Arbeitsblatt ein Textfeld hinzu.
int idx = ws.TextBoxes.Add(5, 5, 50, 200);
Aspose.Cells.Drawing.TextBox tb = ws.TextBoxes[idx];
```
## Schritt 5: Legen Sie den Text des Textfelds fest
Geben wir Text ein. In diesem Beispiel verwenden wir japanische Schriftzeichen, um die Schriftart Far East zu demonstrieren. Es ist so einfach wie das Schreiben in ein Textfeld auf Ihrem Computer!
```csharp
// Legen Sie den Text des Textfelds fest.
tb.Text = "こんにちは世界"; // Auf Japanisch bedeutet dies „Hallo Welt“.
```
## Schritt 6: Schriftarten festlegen
Jetzt kommt der spannende Teil! Wir legen sowohl die lateinische als auch die fernöstliche Schriftart für den Text fest. Das ist vergleichbar mit der Auswahl der perfekten Schriftart für eine elegante Hochzeitseinladung!
```csharp
// Geben Sie den fernöstlichen und lateinischen Namen der Schriftart an.
tb.TextOptions.LatinName = "Comic Sans MS"; // Dies ist unsere gewählte lateinische Schriftart.
tb.TextOptions.FarEastName = "KaiTi"; // Dies ist unsere gewünschte fernöstliche Schriftart.
```
## Schritt 7: Speichern Sie die Excel-Ausgabedatei
Zum Schluss speichern wir unsere Arbeitsmappe! Dieser Schritt schließt unsere Aufgabe ab und stellt sicher, dass all unsere harte Arbeit ordnungsgemäß gespeichert wird. 
```csharp
// Speichern Sie die Excel-Ausgabedatei.
wb.Save(outputDir + "outputSpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape.xlsx", SaveFormat.Xlsx);
```
## Schritt 8: Bestätigungsnachricht
Um uns mitzuteilen, dass alles erfolgreich ausgeführt wurde, drucken wir eine Bestätigungsnachricht auf die Konsole:
```csharp
Console.WriteLine("SpecifyFarEastAndLatinNameOfFontInTextOptionsOfShape executed successfully.");
```
## Abschluss
Und da haben Sie es! Sie haben erfolgreich fernöstliche und lateinische Schriftarten in einer Excel-Arbeitsmappe mit Aspose.Cells für .NET festgelegt. Diese Fähigkeit verleiht Ihren Dokumenten nicht nur einen professionellen Touch, sondern verbessert auch das Leseerlebnis für Benutzer verschiedener Sprachen.
Experimentieren Sie ruhig mit verschiedenen Schriftarten und Stilen, um eine Kombination zu finden, die Ihren spezifischen Anforderungen entspricht. Viel Spaß beim Programmieren!
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek zum Erstellen und Verwalten von Excel-Tabellen, ohne dass Microsoft Excel auf Ihrem Computer installiert sein muss. 
### Kann ich Aspose.Cells für Webanwendungen verwenden?
Ja! Aspose.Cells kann sowohl für Desktop-Anwendungen als auch für mit .NET erstellte Webanwendungen verwendet werden.
### Gibt es eine kostenlose Version von Aspose.Cells?
Ja, Aspose bietet eine kostenlose Testversion an. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/).
### Wie erhalte ich Support für Aspose.Cells?
Sie können um Unterstützung bitten und wertvolle Ressourcen finden auf der [Aspose-Foren](https://forum.aspose.com/c/cells/9).
### Wo kann ich Aspose.Cells kaufen?
Sie können Aspose.Cells direkt von der [Aspose-Website](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}