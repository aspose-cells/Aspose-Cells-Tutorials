---
title: Erstellen von Zwischensummen in Excel
linktitle: Erstellen von Zwischensummen in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem einfachen Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET Zwischensummen in Excel erstellen.
weight: 10
url: /de/net/excel-subtotal-calculation/create-subtotals-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Erstellen von Zwischensummen in Excel

## Einführung
Sind Sie bereit, Ihre Excel-Kenntnisse zu verbessern und Ihre Tabellen dynamischer zu gestalten? Das Erstellen von Zwischensummen in Excel kann Ihnen dabei helfen, Daten effektiv zu kategorisieren und zusammenzufassen, was eine bessere Dateninterpretation und -berichterstattung ermöglicht. Wenn Sie jemand sind, der oft mit Unmengen von Zahlen zu kämpfen hat, ist das Erstellen strukturierter Zusammenfassungen unerlässlich. Heute werden wir uns damit befassen, wie Sie mühelos Zwischensummen mit Aspose.Cells für .NET erstellen können, einer leistungsstarken Bibliothek, die für die Handhabung aller Ihrer Excel-Dateimanipulationen entwickelt wurde.
## Voraussetzungen
Bevor wir uns mit den Einzelheiten der Erstellung von Zwischensummen in Excel befassen, sollten einige Voraussetzungen erfüllt sein:
1.  Aspose.Cells für .NET installiert: Stellen Sie sicher, dass Sie die Aspose.Cells-Bibliothek in Ihrer Entwicklungsumgebung eingerichtet haben. Wenn Sie dies noch nicht getan haben, können Sie dies ganz einfach tun.[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
2. .NET-Umgebung: Sie sollten über eine funktionierende .NET-Umgebung verfügen, in der wir mit der Bibliothek arbeiten können. Unabhängig davon, ob es sich um Visual Studio oder eine andere IDE handelt, stellen Sie sicher, dass Sie mit der Codierung in C# vertraut sind.
3. Grundkenntnisse in C#: Kenntnisse in C# sind von Vorteil. Die Beispiele, die wir bereitstellen, sind in C#-Syntax geschrieben. Wenn Sie sich also damit auskennen, wird Ihnen das dabei helfen, den Prozess zu verstehen.
4.  Excel-Arbeitsblatt: Eine Beispiel-Excel-Datei zum Üben. Wir verwenden eine Datei namens`book1.xls` in unserem Tutorial.
5.  Zugriff auf Online-Dokumentation und Support: Machen Sie sich mit der[Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) kann unglaublich hilfreich sein, wenn Sie mit der Nutzung der Bibliothek fortschreiten.
Nachdem wir nun die Grundlagen gelegt haben, stürzen wir uns auf den technischen Teil!
## Pakete importieren
Bevor wir mit dem eigentlichen Code beginnen, müssen wir sicherstellen, dass wir alle erforderlichen Pakete haben. Im Folgenden erfahren Sie, wie Sie den erforderlichen Namespace in Ihr Projekt importieren können:
```csharp
using System.IO;
using Aspose.Cells;
```
Dadurch wird alles importiert, was wir aus der Aspose-Bibliothek benötigen, um Excel-Dateien zu bearbeiten. Lassen Sie uns nun den Code Schritt für Schritt aufschlüsseln, um Zwischensummen in einem Excel-Arbeitsblatt zu erstellen.
## Schritt 1: Einrichten des Dateipfads
Zu Beginn müssen wir definieren, wo sich unsere Excel-Datei befindet. Hier teilen wir dem Programm unser Dokumentverzeichnis mit.
```csharp
string dataDir = "Your Document Directory";
```
 Ersetzen`"Your Document Directory"` mit dem tatsächlichen Pfad, auf dem Ihr`book1.xls` gespeichert ist. Dadurch wird dem Programm mitgeteilt, wo die zu bearbeitende Excel-Datei zu finden ist.
## Schritt 2: Instanziieren einer neuen Arbeitsmappe
Als Nächstes erstellen wir eine neue Instanz des Workbook-Objekts. Dadurch können wir unsere Excel-Datei öffnen und bearbeiten.
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 Hier erstellen wir ein Objekt von`Workbook` und laden Sie es mit unseren angegebenen`book1.xls` Datei. Dieses Arbeitsmappenobjekt enthält nun alle Informationen aus der Excel-Datei und ermöglicht es uns, diese zu ändern.
## Schritt 3: Zugriff auf die Zellensammlung
Um mit dem Inhalt des Excel-Arbeitsblatts zu arbeiten, müssen wir auf die Sammlung „Zellen“ zugreifen.
```csharp
Cells cells = workbook.Worksheets[0].Cells;
```
 Dadurch werden die Zellen aus dem ersten Arbeitsblatt (Index 0) unserer Arbeitsmappe abgerufen.`cells` -Objekt ermöglicht uns die Interaktion mit den einzelnen Zellen in der Tabelle.
## Schritt 4: Definieren Sie den Zellbereich für Zwischensummen
Jetzt ist es an der Zeit, den Zellbereich anzugeben, auf den wir die Zwischensumme anwenden möchten. 
```csharp
CellArea ca = new CellArea();
ca.StartRow = 2; // B3
ca.StartColumn = 1; 
ca.EndRow = 18; // 19. Jahrhundert
ca.EndColumn = 2;
```
 Hier definieren wir eine`CellArea` das gibt den Bereich an, der uns interessiert. In diesem Fall haben wir den Bereich von B3 (Zeile 2, Spalte 1) bis C19 (Zeile 18, Spalte 2) gewählt. Hier berechnen wir unsere Zwischensummen.
## Schritt 5: Zwischensummen anwenden
Dies ist der Kern unserer Operation – das Anwenden des Zwischenergebnisses auf den definierten Zellbereich.
```csharp
cells.Subtotal(ca, 0, ConsolidationFunction.Sum, new int[] { 1 });
```
 In dieser Zeile nennen wir die`Subtotal` Methode. Die definierten Parameter sind:
- `ca`: Der Zellbereich, den wir zuvor definiert haben.
- `0`: Dieser Index verweist auf die Spalte, die die zu subtrahierenden Werte enthält. 
- `ConsolidationFunction.Sum`Dies gibt an, dass wir die Werte summieren möchten.
- `new int[] { 1 }`: Dies zeigt an, dass wir die Werte aus der zweiten Spalte (Spalte C) summieren.
## Schritt 6: Speichern Sie die geänderte Excel-Datei
Schließlich müssen wir unsere Änderungen in einer neuen Excel-Datei speichern. 
```csharp
workbook.Save(dataDir + "output.out.xls");
```
 Der`Save` Methode schreibt die Änderungen in eine neue Datei namens`output.out.xls`. Sie können der Ausgabedatei je nach Bedarf einen beliebigen Namen geben.
## Abschluss
Mit diesen einfachen Schritten haben Sie mit Aspose.Cells für .NET erfolgreich Zwischensummen in Ihrem Excel-Arbeitsblatt erstellt! Vom Instanziieren einer Arbeitsmappe über das Anwenden von Zwischensummen bis hin zum Speichern der Ergebnisse haben wir alle Grundlagen abgedeckt. Diese Bibliothek vereinfacht nicht nur Ihre Excel-Manipulationen, sondern ermöglicht Ihnen auch eine effektivere Datenverarbeitung.
Probieren Sie es doch einfach mal aus! Sie werden staunen, wie viel einfacher die Datenverwaltung in Tabellenkalkulationen wird, wenn Sie die richtigen Tools verwenden. 
## Häufig gestellte Fragen
### Was ist Aspose.Cells für .NET?
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, die es Entwicklern ermöglicht, Excel-Dateien in .NET-Anwendungen programmgesteuert zu bearbeiten.
### Muss ich etwas Besonderes installieren, um Aspose.Cells zu verwenden?
 Ja, Sie müssen die Aspose.Cells-Bibliothek herunterladen und zu Ihrem .NET-Projekt hinzufügen.[Hier herunterladen](https://releases.aspose.com/cells/net/).
### Ist es möglich, mit Aspose.Cells andere Arten von Excel-Funktionen zu erstellen?
Auf jeden Fall! Aspose.Cells ermöglicht Ihnen die Durchführung verschiedener Excel-Operationen, wie z. B. das Erstellen von Diagrammen, das Verwalten von Arbeitsblättern und das Ändern von Zellformaten.
### Kann ich Aspose.Cells kostenlos nutzen?
 Du kannst[Kostenlose Testversion ausprobieren](https://releases.aspose.com/) von Aspose.Cells, um die Funktionen zu erkunden, bevor Sie sich für einen Kauf entscheiden.
### Welche Support-Optionen gibt es?
 Bei Problemen können Sie die[Aspose-Supportforum](https://forum.aspose.com/c/cells/9) um Hilfe zu erhalten und Erkenntnisse mit einer Community aus Benutzern und Entwicklern auszutauschen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
