---
"description": "Automatisieren Sie die Zahlenformatierung in Excel mit Aspose.Cells für .NET. Erfahren Sie, wie Sie Datums-, Prozent- und Währungsformate programmgesteuert anwenden."
"linktitle": "Integrierte Zahlenformate in Excel programmgesteuert verwenden"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Integrierte Zahlenformate in Excel programmgesteuert verwenden"
"url": "/de/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Integrierte Zahlenformate in Excel programmgesteuert verwenden

## Einführung
In diesem Tutorial zeigen wir Ihnen, wie Sie integrierte Zahlenformate in Excel mit Aspose.Cells für .NET verwenden. Wir behandeln alles, von der Einrichtung Ihrer Umgebung bis hin zur Anwendung verschiedener Formate wie Datumsangaben, Prozentsätze und Währungen. Egal, ob Sie ein erfahrener Profi sind oder gerade erst in das .NET-Ökosystem einsteigen – mit dieser Anleitung wird Ihnen das Formatieren von Excel-Zellen zum Kinderspiel.
## Voraussetzungen
Bevor Sie loslegen, stellen Sie sicher, dass Sie Folgendes haben:
- Aspose.Cells für .NET Bibliothek installiert. Sie können [Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
- Gute Kenntnisse in C# und grundlegender .NET-Programmierung.
- Visual Studio oder eine beliebige .NET-IDE, die auf Ihrem Computer installiert ist.
- Eine gültige Aspose-Lizenz oder [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
- .NET Framework installiert (Version 4.0 oder höher).
  
Falls Sie etwas von den oben genannten Punkten vermissen, folgen Sie den bereitgestellten Links, um alles einzurichten. Bereit? Dann legen wir jetzt los!
## Pakete importieren
Bevor wir mit dem Tutorial beginnen, stellen Sie sicher, dass Sie die erforderlichen Namespaces für die Arbeit mit Aspose.Cells für .NET importieren:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Sobald Sie diese importiert haben, können Sie Excel-Dateien programmgesteuert bearbeiten. Tauchen Sie nun in die Schritt-für-Schritt-Anleitung ein!
## Schritt 1: Erstellen oder öffnen Sie Ihre Excel-Arbeitsmappe
In diesem Schritt erstellen Sie eine neue Arbeitsmappe. Stellen Sie sich das wie das Öffnen einer neuen Excel-Datei vor, nur dass Sie dies über Code tun!
```csharp
// Der Pfad zum Dokumentenverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
```
Hier instanziieren wir einfach eine neue `Workbook` Objekt. Dies dient als Ihre Excel-Datei, bereit zur Datenbearbeitung. Sie können auch eine vorhandene Datei laden, indem Sie deren Pfad angeben.
## Schritt 2: Zugriff auf das Arbeitsblatt
Excel-Arbeitsmappen können mehrere Arbeitsblätter enthalten. In diesem Schritt greifen wir auf das erste Arbeitsblatt Ihrer Arbeitsmappe zu:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Wir greifen nun auf das erste Arbeitsblatt der Arbeitsmappe zu. Wenn Sie weitere Blätter bearbeiten müssen, können Sie diese über ihren Index oder Namen referenzieren.
## Schritt 3: Daten zu Zellen hinzufügen
Beginnen wir mit dem Hinzufügen von Daten zu bestimmten Zellen. Zunächst fügen wir das aktuelle Systemdatum in Zelle "A1" ein:
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Diese Zeile fügt das aktuelle Datum in Zelle A1 ein. Ziemlich cool, oder? Stellen Sie sich vor, Sie müssten das manuell für Hunderte von Zellen tun – es wäre ein Albtraum. Nun geht es weiter mit der Formatierung!
## Schritt 4: Datum in Zelle „A1“ formatieren
Als Nächstes formatieren wir das Datum in ein besser lesbares Format, z. B. „15. Okt. 24“. Hier glänzt Aspose.Cells:
1. Rufen Sie den Stil der Zelle ab:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Hier übernehmen wir den Stil der Zelle A1. Stellen Sie sich das so vor, als würden wir die „Mode“ der Zelle übernehmen, bevor wir Änderungen vornehmen.
2. Legen Sie das Datumsformat fest:
```csharp
style.Number = 15;
```
Festlegen der `Number` Wenn Sie die Eigenschaft auf 15 setzen, wird das gewünschte Datumsformat angewendet. Dies ist ein integrierter Zahlenformatcode zur Anzeige von Datumsangaben im Format "t-mmm-jj".
3. Wenden Sie den Stil auf die Zelle an:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Diese Zeile wendet die Stiländerungen auf die Zelle an. Anstelle des Standarddatumsformats wird nun ein benutzerfreundlicheres Format wie „15. Okt. 24“ angezeigt.
## Schritt 5: Einen Prozentsatz in Zelle „A2“ hinzufügen und formatieren
Kommen wir nun zur Formatierung von Prozentwerten. Stellen Sie sich vor, Sie möchten einen Wert einfügen und ihn als Prozentsatz anzeigen. In diesem Schritt fügen wir der Zelle „A2“ einen numerischen Wert hinzu und formatieren ihn als Prozentsatz:
1. Numerischen Wert einfügen:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Dadurch wird die Zahl 20 in Zelle A2 eingefügt. Sie denken vielleicht: „Das ist doch nur eine einfache Zahl – wie kann ich daraus einen Prozentsatz machen?“ Nun, dazu kommen wir gleich.
2. Rufen Sie den Stil ab und legen Sie das Prozentformat fest:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Format als Prozentsatz
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Hier fügen wir 2546 in Zelle A3 ein. Anschließend formatieren wir diese Zahl so, dass sie als Währung angezeigt wird.
2. Rufen Sie den Stil ab und legen Sie das Währungsformat fest:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Als Währung formatieren
worksheet.Cells["A3"].SetStyle(style);
```
Festlegen der `Number` Wenn Sie die Eigenschaft auf 6 setzen, wird das Währungsformat angewendet. Der Wert in Zelle A3 wird nun als „2.546,00“ mit Kommas und zwei Dezimalstellen angezeigt.
## Schritt 7: Speichern Sie die Excel-Datei
Nachdem wir nun alle notwendigen Formatierungsmaßnahmen durchgeführt haben, ist es an der Zeit, die Datei zu speichern:
```csharp
// Speichern der Excel-Datei
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Diese Zeile speichert die Excel-Datei im Excel 97-2003-Format. Sie können die `SaveFormat` an Ihre Bedürfnisse angepasst. Und schon haben Sie programmgesteuert eine Excel-Datei erstellt und formatiert!
## Abschluss
Herzlichen Glückwunsch! Sie haben erfolgreich gelernt, wie Sie mit Aspose.Cells für .NET integrierte Zahlenformate auf Zellen in einer Excel-Datei anwenden. Von Datumsangaben über Prozentsätze bis hin zu Währungen haben wir einige der häufigsten Formatierungsanforderungen für die Excel-Datenverarbeitung abgedeckt. Anstatt Zellen manuell zu formatieren, können Sie nun den gesamten Prozess automatisieren – das spart Zeit und reduziert Fehler.
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells für .NET benutzerdefinierte Zahlenformate anwenden?
Ja! Zusätzlich zu den integrierten Formaten unterstützt Aspose.Cells auch benutzerdefinierte Zahlenformate. Sie können hochspezifische Formate erstellen mit dem `Custom` Eigentum in der `Style` Klasse.
### Wie kann ich eine Zelle als Währung mit einem bestimmten Symbol formatieren?
Um ein bestimmtes Währungssymbol anzuwenden, können Sie eine benutzerdefinierte Formatierung verwenden, indem Sie das `Style.Custom` Eigentum.
### Kann ich ganze Zeilen oder Spalten formatieren?
Absolut! Sie können Stile auf ganze Zeilen oder Spalten anwenden, indem Sie `Rows` oder `Columns` Sammlungen in der `Worksheet` Objekt.
### Wie kann ich mehrere Zellen gleichzeitig formatieren?
Sie können die `Range` Objekt, um mehrere Zellen auszuwählen und Stile auf alle gleichzeitig anzuwenden.
### Muss Microsoft Excel installiert sein, um Aspose.Cells zu verwenden?
Nein, Aspose.Cells funktioniert unabhängig von Microsoft Excel, Sie müssen Excel also nicht auf Ihrem Computer installiert haben.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}