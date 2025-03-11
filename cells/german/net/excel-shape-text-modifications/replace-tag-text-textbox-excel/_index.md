---
title: Ersetzen Sie das Tag durch Text im Textfeld in Excel
linktitle: Ersetzen Sie das Tag durch Text im Textfeld in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Ersetzen Sie mühelos Text in Textfeldern in Ihren Excel-Tabellen mit Aspose.Cells für .NET. Eine Schritt-für-Schritt-Anleitung zur Excel-Automatisierung.
weight: 11
url: /de/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ersetzen Sie das Tag durch Text im Textfeld in Excel

## Einführung
In diesem Artikel werden wir uns mit einer bestimmten Aufgabe befassen: dem Ersetzen von Tags durch Text in Textfeldern in einer Excel-Tabelle mithilfe von Aspose.Cells. Wir führen Sie Schritt für Schritt durch den gesamten Prozess und stellen sicher, dass Sie jedes Detail verstehen. Am Ende dieses Tutorials werden Sie nicht nur Ihr Verständnis von Aspose.Cells verbessern, sondern auch Ihre Excel-bezogenen Aufgaben rationalisieren!
## Voraussetzungen
Bevor Sie beginnen können, müssen Sie einige Dinge bereitlegen:
1. Visual Studio: Stellen Sie sicher, dass Sie Visual Studio installiert haben. Es ist eine flexible IDE, die das Codieren in C# zum Kinderspiel macht.
2.  Aspose.Cells-Bibliothek: Falls noch nicht geschehen, laden Sie die Aspose.Cells-Bibliothek für .NET herunter von[Seite](https://releases.aspose.com/cells/net/)Sie können auch eine kostenlose Testversion erhalten, um die Funktionen auszuprobieren.
3. Grundkenntnisse in C#: Grundlegende Kenntnisse der C#-Programmierung werden Ihnen dabei helfen, dieser Anleitung problemlos zu folgen.
Nun, da Sie fertig sind, kommen wir zum spaßigen Teil: dem Schreiben des Codes!
## Pakete importieren
Das Wichtigste zuerst: importieren wir die erforderlichen Pakete. Dies ist wichtig, da Ihr Code ohne die richtigen Importe die von uns verwendeten Klassen und Methoden nicht erkennt.
## Starten Sie Ihr C#-Projekt
Öffnen Sie Visual Studio und erstellen Sie ein neues C#-Projekt, vorzugsweise eine Konsolenanwendung, da Sie so die Ausgabe einfacher sehen können.
## Aspose.Cells-Referenz hinzufügen
- Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf Ihr Projekt.
- Wählen Sie „Hinzufügen“ > „Referenz“.
- Navigieren Sie zu dem Speicherort, an dem Sie die Aspose.Cells-Bibliothek heruntergeladen haben, und fügen Sie sie in Ihr Projekt ein.
## Importieren der erforderlichen Namespaces
 Nachdem Sie die Referenz hinzugefügt haben, fügen Sie Folgendes hinzu`using` Direktive oben in Ihrer Hauptdatei:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Dadurch erhalten Sie Zugriff auf Klassen innerhalb des Aspose.Cells-Namespace.
Nachdem wir nun unsere Umgebung eingerichtet haben, kommen wir zum spannenden Teil – dem Codieren! Unser Ziel ist es, bestimmte Tags in Textfeldern in einer Excel-Datei zu finden und sie durch bereitgestellten Text zu ersetzen.
## Schritt 1: Definieren Sie das Quell- und Ausgabeverzeichnis
Zuerst müssen wir angeben, wo sich unsere Excel-Quelldatei befindet und wo wir die geänderte Version speichern möchten.
```csharp
// Quell- und Ausgabeverzeichnis
string sourceDir = "Your Document Directory"; // Wechseln Sie zu Ihrem Verzeichnis
string outputDir = "Your Document Directory"; // Wechseln Sie zu Ihrem Verzeichnis
```
## Schritt 2: Laden Sie die Arbeitsmappe
Hier laden wir unsere Excel-Arbeitsmappe. Wenn die Datei nicht existiert, wird ein Fehler ausgegeben. Stellen Sie also sicher, dass Ihr Dateipfad korrekt ist!
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
 Hier laden wir eine vorhandene Excel-Datei namens`sampleReplaceTagWithText.xlsx`.
## Schritt 3: Tags und Ersatztext definieren
Als Nächstes müssen wir die gesuchten Tags definieren und festlegen, wodurch sie ersetzt werden sollen.
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
 In diesem Beispiel werden die Tags aufgeteilt mit`$`. Sie können dies durch jedes beliebige Trennzeichen ersetzen.
## Schritt 4: Über Tags schleifen und ersetzen
Wir erstellen eine Schleife, die alle Tags durchläuft, die wir ersetzen möchten. Hier geschieht die Magie!
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## Schritt 5: Speichern der Arbeitsmappe
Nachdem wir unsere Ersetzungen vorgenommen haben, ist es an der Zeit, die geänderte Arbeitsmappe im gewünschten Format zu speichern. So konvertieren wir sie in eine PDF-Datei.
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
Sie können es auch in verschiedenen anderen Formaten speichern, einschließlich XLSX.
## Schritt 6: Implementieren der Ersetzungslogik
 Hier liegt das Herzstück unserer Funktionalität. Die`sheetReplace` Die Methode übernimmt den eigentlichen Ersetzungsvorgang in den Excel-Arbeitsblättern.
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- Zuerst durchlaufen wir jedes Arbeitsblatt in der Arbeitsmappe.
- Wir ersetzen das Haupt-Tag nicht nur im Zellinhalt, sondern auch in Kopf- und Fußzeilen (sofern vorhanden).
- Abschließend überprüfen wir jedes Textfeld im Blatt und ersetzen den darin enthaltenen Text basierend auf dem gesuchten Tag.
## Abschluss
Und voilà! Sie haben jetzt gelernt, wie Sie mit Aspose.Cells für .NET Tags durch Text in Textfeldern in Ihren Excel-Dokumenten ersetzen. Dies kann eine echte Zeitersparnis sein, insbesondere bei sich wiederholenden Aufgaben in Tabellenkalkulationen.
## Häufig gestellte Fragen
### Kann ich Tags in mehreren Excel-Dateien gleichzeitig ersetzen?
Ja, indem Sie eine Liste von Dateien durchlaufen, können Sie die gleiche Logik auf mehrere Excel-Dateien anwenden.
### Benötige ich eine kostenpflichtige Lizenz, um Aspose.Cells zu verwenden?
 Sie können mit einer kostenlosen Testversion beginnen, für die volle Funktionalität müssen Sie jedoch eine Lizenz erwerben. Schauen Sie sich an[Asposes Kaufoptionen](https://purchase.aspose.com/buy).
### Kann ich mit Aspose.Cells Bilder in Textfeldern ersetzen?
Aspose.Cells befasst sich hauptsächlich mit Text. Sie können Bilder jedoch bei Bedarf separat bearbeiten.
### In welchen Formaten kann ich meine geänderte Excel-Datei speichern?
Sie können es in verschiedenen Formaten speichern, darunter XLSX, PDF, CSV usw.
### Wo finde ich Unterstützung für Aspose.Cells?
 Sie finden Unterstützung und können Fragen stellen auf der[Aspose-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
