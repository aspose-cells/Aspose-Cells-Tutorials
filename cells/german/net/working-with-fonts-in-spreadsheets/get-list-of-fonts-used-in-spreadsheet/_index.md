---
title: Liste der in der Tabelle verwendeten Schriftarten abrufen
linktitle: Liste der in der Tabelle verwendeten Schriftarten abrufen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem leicht verständlichen Tutorial, wie Sie mit Aspose.Cells für .NET Schriftarten aus Excel-Tabellen abrufen und auflisten.
weight: 10
url: /de/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Liste der in der Tabelle verwendeten Schriftarten abrufen

## Einführung
Haben Sie sich schon einmal dabei ertappt, wie Sie durch eine Excel-Tabelle gescrollt sind und sich gefragt haben, welche Schriftarten in den verschiedenen Zellen verwendet wurden? Vielleicht sind Sie auf ein altes Dokument gestoßen und möchten wissen, welche Typografie-Entscheidungen getroffen wurden? Nun, Sie haben Glück! Mit Aspose.Cells für .NET haben Sie eine Toolbox, mit der Sie die in Ihren Tabellen verborgenen Schriftartengeheimnisse durchforsten und aufdecken können. In dieser Anleitung zeigen wir Ihnen, wie Sie ganz einfach eine Liste aller in einer Excel-Datei verwendeten Schriftarten abrufen können. Schnall dich an und tauche ein in die Welt der Tabellen!
## Voraussetzungen
Bevor wir uns an den Code machen, müssen Sie zunächst ein paar Dinge erledigen. Keine Sorge, es ist ganz einfach. Hier ist eine Checkliste mit den Dingen, die Sie brauchen:
1. Visual Studio: Stellen Sie sicher, dass auf Ihrem Computer eine Version von Visual Studio installiert ist. Hier schreiben wir unseren Code.
2. Aspose.Cells für .NET: Sie müssen die Bibliothek Aspose.Cells zur Verfügung haben. Wenn Sie sie noch nicht heruntergeladen haben, können Sie sie von der[Website](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Ein wenig Verständnis der C#-Programmierung wird Ihnen sicherlich dabei helfen, problemlos durch den Code zu navigieren.
4. Eine Excel-Beispieldatei: Sie benötigen eine Excel-Beispieldatei, z. B. „sampleGetFonts.xlsx“, mit der Sie arbeiten können. Hier werden wir unsere Schriftarten-Erkundung anwenden.
Sobald Sie alles geregelt haben, können Sie mit dem Programmieren loslegen!
## Pakete importieren
Lassen Sie uns zunächst die erforderlichen Namespaces importieren. In .NET ist das Importieren von Paketen so, als würden Sie die richtigen Gäste zu Ihrer Party einladen – ohne sie läuft es einfach nicht reibungslos.
So importieren Sie Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Mit dieser einfachen Zeile laden wir die Kernfunktionalität von Aspose.Cells in unser Projekt ein. Fahren wir nun mit dem Laden der Arbeitsmappe fort.
## Schritt 1: Dokumentverzeichnis festlegen
Das Wichtigste zuerst – bevor wir uns in den Code vertiefen, müssen Sie den Pfad zu Ihrem Dokumentverzeichnis festlegen. Hier befindet sich Ihre Excel-Datei. 
```csharp
string dataDir = "Your Document Directory";
```
Sie ersetzen „Ihr Dokumentverzeichnis“ durch den tatsächlichen Pfad, in dem sich Ihre Excel-Datei befindet. Stellen Sie sich das so vor, als würden Sie dem Programm sagen: „Hey, hier habe ich meine Excel-Datei gespeichert. Schauen Sie mal nach!“
## Schritt 2: Laden der Quellarbeitsmappe
 Es ist Zeit, die Excel-Datei zu laden. Wir erstellen eine neue Instanz des`Workbook` Klasse und übergeben Sie den Pfad der Datei. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 Was passiert hier? Wir öffnen im Grunde die Tür zu unserer Tabelle. Die`Workbook` Klasse ermöglicht uns, mit dem Inhalt der Excel-Datei zu interagieren. 
## Schritt 3: Alle Schriftarten abrufen
 Jetzt kommt der magische Moment – holen wir uns die Schriften! Die`GetFonts()` Methode ist unser goldenes Ticket.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Hier bitten wir die Arbeitsmappe, alle darin verwendeten Schriftarten preiszugeben.`fnts` Dieses Array wird unsere Schätze bewahren.
## Schritt 4: Drucken Sie die Schriftarten
Nehmen wir zum Schluss die Schriftarten und drucken sie aus. So können wir unsere Ergebnisse überprüfen.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Diese Schleife durchläuft jede Schriftart in unserem`fnts` Array und gibt sie nacheinander an die Konsole aus. Es ist, als würden Sie alle coolen Typografieoptionen in Ihrer Excel-Datei angeben!
## Abschluss
Und da haben Sie es! Mit nur wenigen Codezeilen haben Sie die Liste der in Ihrer Excel-Tabelle verwendeten Schriftarten mithilfe von Aspose.Cells für .NET erfolgreich abgerufen und ausgedruckt. Dabei geht es nicht nur um Schriftarten; es geht darum, die Feinheiten Ihrer Dokumente zu verstehen, Ihre Präsentationen zu verbessern und die Kunst der Typografie in Ihren Tabellen zu beherrschen. Egal, ob Sie Entwickler sind oder einfach gerne mit Excel herumbasteln, dieser kleine Codeausschnitt könnte bahnbrechend sein. 
## Häufig gestellte Fragen
### Muss ich Aspose.Cells separat installieren?
Ja, Sie müssen die Bibliothek herunterladen und in Ihrem Projekt darauf verweisen. 
### Kann ich Aspose.Cells für andere Formate verwenden?
Absolut! Aspose.Cells funktioniert mit mehreren Excel-Formaten wie XLSX, XLS und CSV.
### Gibt es eine kostenlose Testversion?
 Ja, Sie können eine kostenlose Testversion erhalten von der[Downloadlink](https://releases.aspose.com/).
### Wie erhalte ich technischen Support?
 Wenn Sie Hilfe benötigen,[Aspose-Supportforum](https://forum.aspose.com/c/cells/9) ist eine großartige Ressource.
### Ist Aspose.Cells mit .NET Core kompatibel?
Ja, Aspose.Cells ist auch mit .NET Core-Projekten kompatibel.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
