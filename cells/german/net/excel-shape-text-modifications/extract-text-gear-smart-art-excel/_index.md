---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET Text aus zahnradartigem SmartArt in Excel extrahieren. Schritt-für-Schritt-Anleitung und Codebeispiel inklusive."
"linktitle": "Extrahieren Sie Text aus Smart Art vom Typ „Zahnrad“ in Excel"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Extrahieren Sie Text aus Smart Art vom Typ „Zahnrad“ in Excel"
"url": "/de/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahieren Sie Text aus Smart Art vom Typ „Zahnrad“ in Excel

## Einführung
Bei der Arbeit mit Excel stoßen Sie möglicherweise auf SmartArt-Grafiken, die Ihre Botschaften optisch ansprechend vermitteln. Zahnrad-SmartArts sind aufgrund ihrer hierarchischen und gerichteten Abläufe besonders beliebt und werden häufig im Projektmanagement oder in der Systemmodellierung eingesetzt. Doch was, wenn Sie Text aus diesen Formen programmgesteuert extrahieren müssen? Hier kommt Aspose.Cells für .NET ins Spiel! In diesem Blogbeitrag zeigen wir Ihnen Schritt für Schritt, wie Sie mit Aspose.Cells für .NET Text aus zahnradartigen SmartArt-Formen in Excel extrahieren.
## Voraussetzungen
Bevor wir loslegen, müssen Sie einige grundlegende Voraussetzungen erfüllen. Keine Sorge, es ist ganz einfach, und ich führe Sie durch den Prozess.
### .NET-Umgebung
Stellen Sie sicher, dass auf Ihrem Computer eine .NET-Entwicklungsumgebung eingerichtet ist. Dies kann Visual Studio oder eine beliebige IDE Ihrer Wahl sein, die die .NET-Entwicklung unterstützt.
### Aspose.Cells für .NET
Als Nächstes müssen Sie die Aspose.Cells-Bibliothek installieren. Mit dieser Bibliothek können Sie Excel-Dateien nahtlos bearbeiten. Sie können sie von der [Aspose-Releases-Seite](https://releases.aspose.com/cells/net/)Wenn Sie es zuerst erkunden möchten, nutzen Sie die [kostenlose Testversion](https://releases.aspose.com/).
### Grundkenntnisse in C#
Grundlegende Kenntnisse der C#-Programmierung sind genau das, was Sie brauchen, um diesem Tutorial zu folgen. Falls Sie neu darin sind, keine Sorge – ich werde die Schritte so anfängerfreundlich wie möglich gestalten.
### Beispiel-Excel-Datei
Für dieses Tutorial benötigen Sie außerdem eine Excel-Beispieldatei mit SmartArt-Formen im Zahnrad-Stil. Sie können ganz einfach eine erstellen oder online eine Vorlage finden. Stellen Sie einfach sicher, dass die SmartArt mindestens eine Zahnradform enthält.
## Pakete importieren
Um mit dem Programmieren zu beginnen, müssen Sie die erforderlichen Pakete importieren. So geht's:
### Neues Projekt erstellen
1. Öffnen Sie Ihre .NET IDE.
2. Erstellen Sie ein neues Projekt. Wählen Sie beispielsweise unter den .NET-Optionen „Konsolenanwendung“ aus.
3. Geben Sie Ihrem Projekt einen Namen und legen Sie den gewünschten Rahmen fest. 
### Referenzen hinzufügen
Um Aspose.Cells zu verwenden, müssen Sie Ihrem Projekt die Bibliotheksverweise hinzufügen:
1. Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihren Projektnamen.
2. Wählen Sie „NuGet-Pakete verwalten“.
3. Suchen Sie nach „Aspose.Cells“ und installieren Sie es.
Nach der Installation sind Sie bereit zum Codieren!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Lassen Sie uns nun den Code analysieren, den Sie zum Extrahieren des Textes verwenden. Wir werden dabei Schritt für Schritt vorgehen.
## Schritt 1: Richten Sie das Quellverzeichnis ein
Definieren Sie zunächst das Verzeichnis, in dem sich Ihre Excel-Datei befindet:
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
```
Stellen Sie sicher, dass Sie `"Your Document Directory"` durch den tatsächlichen Pfad zu Ihrer Excel-Datei.
## Schritt 2: Laden Sie die Excel-Arbeitsmappe
Als Nächstes laden wir die Excel-Arbeitsmappe. So können wir auf ihren Inhalt zugreifen:
```csharp
// Laden Sie eine Excel-Beispieldatei mit einer Smart-Art-Form vom Typ „Zahnrad“.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Dieser Teil lädt Ihre Beispiel-Excel-Arbeitsmappe.
## Schritt 3: Zugriff auf das erste Arbeitsblatt
Nachdem wir die Arbeitsmappe geladen haben, greifen wir auf das erste Arbeitsblatt zu, in dem unser SmartArt vorhanden ist:
```csharp
// Greifen Sie auf das erste Arbeitsblatt zu.
Worksheet ws = wb.Worksheets[0];
```
Dadurch wird das erste Arbeitsblatt zur weiteren Bearbeitung abgerufen.
## Schritt 4: Zugriff auf die erste Form
Als Nächstes müssen wir auf die erste Form in unserem Arbeitsblatt zugreifen. Auf diese Weise können wir durch unsere SmartArt-Grafiken navigieren:
```csharp
// Greifen Sie auf die erste Form zu.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Hier konzentrieren wir uns auf die erste Form, von der wir annehmen, dass es sich dabei um das SmartArt handelt, das wir benötigen.
## Schritt 5: Holen Sie sich die Gruppenform
Sobald wir unsere Form haben, ist es Zeit, das Ergebnis unserer SmartArt-Darstellung abzurufen:
```csharp
// Erhalten Sie das Ergebnis der Smart-Art-Form vom Zahnradtyp in Form einer Gruppenform.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Dadurch wird unser SmartArt-Objekt vom Zahnradtyp als gruppierte Form abgerufen.
## Schritt 6: Einzelne Formen extrahieren
Extrahieren wir nun die einzelnen Formen, aus denen unser SmartArt besteht:
```csharp
// Holen Sie sich die Liste der einzelnen Formen, die aus Gruppenformen bestehen.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Dieses Array enthält alle einzelnen Formen, die wir durchlaufen müssen.
## Schritt 7: Text extrahieren und drucken
Schließlich können wir unser Formen-Array durchlaufen und den Text aus jeder zahnradartigen Form extrahieren:
```csharp
// Extrahieren Sie den Text von Zahnradformen und drucken Sie ihn auf der Konsole.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
In dieser Schleife überprüfen wir den Formtyp und drucken den Text, wenn es sich um eine Zahnradform handelt.
## Schritt 8: Ausführungsbestätigung
Abschließend möchten Sie möglicherweise eine Bestätigungsnachricht hinzufügen, sobald der Vorgang erfolgreich abgeschlossen wurde:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Damit ist Ihre Extraktion abgeschlossen und Sie sollten Ihre Textausgabe in der Konsole sehen!
## Abschluss
Herzlichen Glückwunsch! Sie haben gerade gelernt, wie Sie mit Aspose.Cells für .NET Text aus zahnradartigen SmartArt-Formen in Excel extrahieren. Diese praktische Technik eröffnet Ihnen die Möglichkeit, Berichte oder Dokumentationen zu automatisieren, die auf visueller Datendarstellung basieren. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen: Die Kontrolle und Extraktion von Informationen aus SmartArt kann Ihren Workflow optimieren und Ihre Effizienz steigern. Vergessen Sie nicht, die detaillierten [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für weitere Fähigkeiten.
## Häufig gestellte Fragen
### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek, mit der Entwickler Excel-Dateien einfach erstellen und bearbeiten können.
### Kann ich Aspose.Cells mit anderen Sprachen verwenden?
Ja! Aspose.Cells ist in mehreren Programmiersprachen verfügbar, darunter Java und Python.
### Muss ich Aspose.Cells für .NET kaufen?
Aspose.Cells bietet eine kostenlose Testversion an, für die erweiterte Nutzung ist jedoch ein Kauf erforderlich. Hier finden Sie Kaufoptionen [Hier](https://purchase.aspose.com/buy).
### Gibt es Support für Aspose.Cells-Benutzer?
Absolut! Community-Support finden Sie unter [Aspose.Cells-Forum](https://forum.aspose.com/c/cells/9).
### Kann ich mit dieser Methode andere SmartArt-Typen extrahieren?
Ja, mit geringfügigen Änderungen können Sie Text aus verschiedenen SmartArt-Formen extrahieren, indem Sie die Bedingungen in Ihrem Code ändern.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}