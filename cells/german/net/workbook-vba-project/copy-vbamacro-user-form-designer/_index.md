---
title: Kopieren Sie den VBAMAcro User Form Designer-Speicher mit Aspose.Cells in die Arbeitsmappe
linktitle: Kopieren Sie den VBAMAcro User Form Designer-Speicher mit Aspose.Cells in die Arbeitsmappe
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie mit unserem umfassenden Schritt-für-Schritt-Tutorial, wie Sie den VBA-Makro-Benutzerformular-Designer in Aspose.Cells für .NET effizient kopieren! Schöpfen Sie das Potenzial von Excel aus.
weight: 11
url: /de/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieren Sie den VBAMAcro User Form Designer-Speicher mit Aspose.Cells in die Arbeitsmappe

## Einführung
Willkommen! Wenn Sie Ihre Excel-Erfahrung mit VBA-Makros und Benutzerformularen verbessern möchten, sind Sie hier richtig! In diesem Handbuch erfahren Sie, wie Sie mithilfe von Aspose.Cells für .NET einen VBA-Makro-Benutzerformular-Designer nahtlos von einer Arbeitsmappe in eine andere kopieren können. Egal, ob Sie ein erfahrener Entwickler sind oder gerade erst anfangen, wir führen Sie durch jeden entscheidenden Schritt. Betrachten Sie dies als Ihr Spielbuch, um die Kunst der programmgesteuerten Handhabung von Excel-Dateien zu meistern. Bereit, einzutauchen? Los geht‘s!
## Voraussetzungen
Bevor wir uns in die Einzelheiten der Codierung stürzen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:
1. C#-Entwicklungsumgebung: Sie sollten über eine Arbeitsumgebung für die C#-Entwicklung verfügen. Visual Studio wird dringend empfohlen.
2.  Aspose.Cells für .NET-Bibliothek: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek in Ihr Projekt integriert haben. Sie können ganz einfach[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse zu VBA und Excel-Makros: Gute Kenntnisse zu VBA und der Funktionsweise von Excel-Makros helfen Ihnen dabei, problemlos durch dieses Tutorial zu navigieren.
4. Eine Excel-Datei mit einem Benutzerformular: Um zu experimentieren, erstellen oder erhalten Sie eine Excel-Arbeitsmappe, die ein Benutzerformular enthält, vorzugsweise mit aktivierten Makros (wie`.xlsm` Dateien).
## Pakete importieren
In Ihrem C#-Projekt müssen Sie bestimmte Namespaces oben in Ihrer Datei importieren, um die Funktionen von Aspose.Cells nutzen zu können. So gehen Sie dabei vor:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Durch die Einbindung dieser Namespaces erhalten Sie Zugriff auf alle leistungsstarken Tools, die in der Aspose.Cells-Bibliothek eingebettet sind. 
Nachdem wir nun unsere Voraussetzungen und Pakete abgedeckt haben, ist es Zeit, zum spaßigen Teil überzugehen: dem Programmieren! Lassen Sie uns das Schritt für Schritt durchgehen.
## Schritt 1: Definieren Sie Ihre Quell- und Ausgabeverzeichnisse
Zunächst müssen Sie feststellen, wo sich Ihre Dateien befinden:
```csharp
// Quellverzeichnis
string sourceDir = "Your Document Directory";
// Ausgabeverzeichnis
string outputDir = "Your Document Directory";
```
 Ersetzen Sie hier`"Your Document Directory"` mit dem tatsächlichen Pfad, in dem Ihre Dateien gespeichert sind. Von hier wird unsere Quellarbeitsmappe (mit dem UserForm) abgerufen und die neue Arbeitsmappe wird dort gespeichert.
## Schritt 2: Erstellen Sie eine leere Zielarbeitsmappe
Als Nächstes erstellen wir unsere Zielarbeitsmappe, in die wir unser Benutzerformular und unsere Makros kopieren:
```csharp
// Leere Zielarbeitsmappe erstellen
Workbook target = new Workbook();
```
Diese Codezeile initialisiert eine neue, leere Arbeitsmappe, die wir mit Daten füllen können. Betrachten Sie sie als leere Leinwand für Ihr Meisterwerk!
## Schritt 3: Laden Sie Ihre Vorlagenarbeitsmappe
Wir müssen die Arbeitsmappe laden, die Ihr Benutzerformular und Ihre Makros enthält:
```csharp
// Laden Sie die Excel-Datei mit dem VBA-Macro Designer-Benutzerformular
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Achten Sie darauf, zu ändern`"sampleDesignerForm.xlsm"` zum Namen Ihrer eigentlichen Datei. Diese Arbeitsmappe ist wie Ihr Rezeptbuch – daraus entnehmen wir unsere Zutaten!
## Schritt 4: Arbeitsblätter in die Zielarbeitsmappe kopieren
Beginnen wir nun mit dem Kopieren der Arbeitsblätter aus unserer Vorlage in die Zielarbeitsmappe:
```csharp
// Alle Vorlagenarbeitsblätter in die Zielarbeitsmappe kopieren
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Nachricht in Zelle A2 des Zielarbeitsblatts einfügen
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
In diesem Schritt durchlaufen wir jedes Arbeitsblatt in der Vorlage und kopieren es in unsere Zielarbeitsmappe. Wenn Sie darüber nachdenken, ist es, als würden Sie Ihre besten Rezepte von einem Kochbuch in ein anderes übertragen!
## Schritt 5: VBA-Makros aus der Vorlage kopieren
Als Nächstes kopieren wir die VBA-Makros, einschließlich der UserForm Designer-Module, in unsere neue Arbeitsmappe:
```csharp
// Kopieren des VBA-Macro Designer UserForm von der Vorlage zum Ziel
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Kopieren Sie den Modulcode von ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Code und Daten anderer Module kopieren
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Holen Sie sich die Daten des Benutzerformulars, d. h. des Designerspeichers
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Fügen Sie dem Ziel-VBA-Projekt den Designerspeicher hinzu
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Dieser umfangreiche Codeblock überprüft jedes VBA-Modul in der Vorlagendatei. Wir kopieren das UserForm-Design und die zugehörigen Codes. Das ist, als ob Sie nicht nur Omas berühmtes Kuchenrezept, sondern auch ihre genauen Backtechniken erhalten würden!
## Schritt 6: Speichern der Zielarbeitsmappe
Nachdem wir alle unsere Kopien erstellt haben, ist es Zeit, unsere harte Arbeit zu speichern:
```csharp
// Speichern der Zielarbeitsmappe
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Denken Sie daran, den Namen der Ausgabedatei nach Bedarf zu ändern. Sobald Sie die Datei speichern, erstellen Sie praktisch Ihre eigene, maßgeschneiderte Version der Arbeitsmappe, die voller Makros und Benutzerformulare steckt. Ist das nicht aufregend?
## Schritt 7: Erfolg bestätigen
Lassen Sie uns abschließend eine Erfolgsmeldung auf der Konsole ausgeben:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Diese kleine Zeile versichert Ihnen, dass Ihr Vorgang reibungslos verlief. Sie ist die Kirsche auf Ihrem Codier-Eisbecher!
## Abschluss
Herzlichen Glückwunsch! Sie haben die Schritt-für-Schritt-Anleitung zum Kopieren eines VBA-Makro-Benutzerformular-Designers von einer Arbeitsmappe in eine andere mit Aspose.Cells für .NET abgeschlossen. Es mag zunächst etwas überwältigend erscheinen, aber mit etwas Übung werden Sie mit Arbeitsmappenmanipulationen wie ein Profi umgehen. Denken Sie daran, dass es beim Codieren vor allem auf Übung ankommt. Scheuen Sie sich also nicht, verschiedene Dinge in Ihren Excel-Dateien auszuprobieren. Wenn Sie Fragen haben oder auf Probleme stoßen, können Sie sich gerne an die Aspose-Foren oder die Dokumentation wenden, um Unterstützung zu erhalten!
## Häufig gestellte Fragen
### Welche Excel-Versionen unterstützt Aspose.Cells?
Aspose.Cells unterstützt eine breite Palette von Excel-Formaten, darunter XLSX, XLSM, CSV und mehr.
### Kann ich Aspose.Cells kostenlos nutzen?
 Ja! Sie können mit einer kostenlosen Testversion beginnen, mit der Sie die Bibliothek testen können:[Kostenlose Testversion](https://releases.aspose.com/).
### Benötige ich Visual Studio, um diesen Code auszuführen?
Obwohl es aufgrund seiner benutzerfreundlichen Funktionen dringend empfohlen wird, ist jede C#-IDE geeignet, solange sie die .NET-Entwicklung unterstützt.
### Wo finde ich weitere Beispiele und Dokumentation?
 Entdecken Sie die[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) für weitere Beispiele und ausführliche Erklärungen.
### Wie löse ich Probleme bei der Verwendung von Aspose.Cells?
 Besuchen Sie die[Aspose Support Forum](https://forum.aspose.com/c/cells/9) für Hilfe von der Community und dem Aspose-Supportpersonal.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
