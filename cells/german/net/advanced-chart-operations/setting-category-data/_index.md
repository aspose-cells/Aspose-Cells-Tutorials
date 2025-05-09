---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET Kategoriedaten in Excel-Diagrammen festlegen. Folgen Sie unserer Schritt-für-Schritt-Anleitung für eine einfache Implementierung."
"linktitle": "Kategoriedaten festlegen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Kategoriedaten festlegen"
"url": "/de/net/advanced-chart-operations/setting-category-data/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kategoriedaten festlegen

## Einführung

Bei der programmgesteuerten Verwaltung und Bearbeitung von Excel-Dateien sind die richtigen Tools entscheidend. Aspose.Cells für .NET ist ein solches Tool, mit dem Entwickler Excel-Dateien mühelos erstellen, bearbeiten und konvertieren können. Egal, ob Sie eine komplexe Datenanalyseanwendung erstellen oder einfach die Berichterstellung automatisieren möchten – Aspose.Cells bietet Ihnen die passende Lösung. 

## Voraussetzungen 

Bevor wir in die Einzelheiten eintauchen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:

1. Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine .NET-Entwicklungsumgebung eingerichtet haben. Visual Studio wird empfohlen.
2. Aspose.Cells für .NET-Bibliothek: Laden Sie die neueste Version der Bibliothek von der [Aspose.Cells Download-Seite](https://releases.aspose.com/cells/net/).
3. Grundlegende Kenntnisse in C#: Wenn Sie mit den Konzepten von C# und Excel vertraut sind, können Sie die Inhalte leichter erfassen.
4. Zugriff auf die Dokumentation: Zugriff auf [Aspose.Cells-Dokumentation](https://reference.aspose.com/cells/net/) kann zusätzliche Erkenntnisse liefern, wenn Sie nicht weiterkommen. 

Nachdem nun alles vorbereitet ist, können wir Schritt für Schritt die Magie der Excel-Manipulation entschlüsseln.

## Pakete importieren 

Bevor wir mit dem Programmieren beginnen, ist es wichtig, die erforderlichen Pakete zu importieren. Dadurch können wir auf die von Aspose.Cells bereitgestellten Funktionen zugreifen.

## Schritt 1: Importieren des Namespace

Importieren wir zunächst den Aspose.Cells-Namespace in Ihre C#-Datei.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Indem Sie diese Zeile oben in Ihre Datei einfügen, können Sie auf alle relevanten Klassen und Methoden in der Aspose.Cells-Bibliothek zugreifen.

Nachdem wir nun mit den Voraussetzungen vertraut sind und die erforderliche Bibliothek importiert haben, wollen wir uns ansehen, wie Kategoriedaten in einem Excel-Diagramm festgelegt werden.

## Schritt 2: Definieren Sie Ihr Ausgabeverzeichnis

Geben Sie zunächst an, wo die Excel-Datei gespeichert werden soll. Erstellen Sie eine Variable für Ihr Ausgabeverzeichnis. 

```csharp
string outputDir = "Your Output Directory";
```

Ersetzen `"Your Output Directory"` mit dem tatsächlichen Pfad zum Speicherort Ihrer Excel-Ausgabedatei. So wissen Sie genau, wo Sie Ihr fertiges Produkt finden!

## Schritt 3: Instanziieren eines Arbeitsmappenobjekts

Als Nächstes erstellen Sie eine neue Instanz des Workbook-Objekts. Dieses Objekt dient als Container für Ihre Excel-Datei.

```csharp
Workbook workbook = new Workbook();
```

## Schritt 4: Zugriff auf das erste Arbeitsblatt

Sie müssen mit dem ersten Arbeitsblatt in der Arbeitsmappe arbeiten. Der Zugriff auf das Arbeitsblatt ist ganz einfach:

```csharp
Worksheet worksheet = workbook.Worksheets[0];
```

Der Index `0` verweist auf das erste Arbeitsblatt. In Excel bedeutet dies, dass die erste Registerkarte in Ihrer Arbeitsmappe geöffnet wird.

## Schritt 5: Hinzufügen von Beispielwerten zu Zellen

Geben wir einige Daten ein, mit denen wir arbeiten möchten. Sie können den ersten beiden Spalten numerische Werte hinzufügen. 

```csharp
worksheet.Cells["A1"].PutValue(10);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(170);
worksheet.Cells["A4"].PutValue(200);
worksheet.Cells["B1"].PutValue(120);
worksheet.Cells["B2"].PutValue(320);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(40);
```

In diesem Codeausschnitt füllen wir die Zeilen A1 bis A4 mit unterschiedlichen numerischen Werten und füllen auch die Spalten B1 bis B4 aus. Diese Daten dienen als Grundlage für unser Diagramm.

## Schritt 6: Kategoriedaten hinzufügen

Nun beschriften wir unsere Datenkategorien. Dies geschieht in der dritten Spalte (Spalte C):

```csharp
worksheet.Cells["C1"].PutValue("Q1");
worksheet.Cells["C2"].PutValue("Q2");
worksheet.Cells["C3"].PutValue("Y1");
worksheet.Cells["C4"].PutValue("Y2");
```

Hier kennzeichnen wir jeden Datensatz mit Kategorien wie „Q1“ und „Y1“, um die spätere Interpretation unseres Diagramms zu erleichtern.

## Erstellen des Diagramms

Nachdem wir unsere Daten vorliegen haben, können wir ein Diagramm hinzufügen, um diese Daten visuell darzustellen.

## Schritt 7: Hinzufügen eines Diagramms zum Arbeitsblatt

Fügen wir nun dem Arbeitsblatt ein Diagramm vom Typ „Spalte“ hinzu.

```csharp
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```

Diese Zeile erstellt ein neues Säulendiagramm, beginnend in Zeile 5 und Spalte 0 des Arbeitsblatts.

## Schritt 8: Zugriff auf die Diagramminstanz

Bevor wir das Diagramm mit Daten füllen können, müssen wir auf die Instanz des neu erstellten Diagramms zugreifen:

```csharp
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Mit diesem Schritt sind wir nun bereit, unsere Datenreihe zum Diagramm hinzuzufügen.

## Schritt 9: Datenreihen zum Diagramm hinzufügen

Als Nächstes fügen Sie die Seriensammlung hinzu, die die im Diagramm anzuzeigenden Daten definiert. 

```csharp
chart.NSeries.Add("A1:B4", true);
```

Diese Zeile gibt an, dass das Diagramm Daten aus den Bereichen A1 bis B4 übernehmen soll, damit diese Werte visuell angezeigt werden können.

## Schritt 10: Festlegen der Kategoriedaten

Hier kommt der entscheidende Teil: die Definition unserer Kategoriedaten. Dadurch werden unsere Datenpunkte auf der X-Achse beschriftet.

```csharp
chart.NSeries.CategoryData = "C1:C4";
```

Durch die Zuweisung dieses Bereichs teilen wir dem Diagramm mit, welche Zellen den Kategorien in unserer Datenreihe entsprechen. Ohne diesen Schritt wäre Ihr Diagramm lediglich eine Zahlenreihe!

## Schritt 11: Speichern der Excel-Datei

Nachdem alles eingerichtet ist, ist es Zeit, unsere harte Arbeit zu speichern. 

```csharp
workbook.Save(outputDir + "outputSettingCategoryData.xlsx");
```

Dieser Befehl speichert Ihre Arbeitsmappe im angegebenen Ausgabeverzeichnis unter dem Namen „outputSettingCategoryData.xlsx“. 

## Schritt 12: Bestätigungsnachricht

Abschließend können wir noch ein kleines Feedback hinzufügen, um zu bestätigen, dass alles reibungslos funktioniert hat:

```csharp
Console.WriteLine("SettingCategoryData executed successfully.");
```

Dadurch wird eine Meldung in der Konsole ausgegeben, die Sie darüber informiert, dass der Vorgang abgeschlossen ist. Einfach, oder?

## Abschluss

Und da haben Sie es! Sie haben erfolgreich Kategoriedaten für ein Diagramm in einer Excel-Arbeitsmappe mit Aspose.Cells für .NET festgelegt. Der Vorteil dieses Ansatzes liegt darin, dass Sie die Bearbeitung von Excel-Dateien automatisieren können, ohne Excel auf Ihrem Computer installieren zu müssen. 

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine .NET-Bibliothek zur Verwaltung von Excel-Dateien ohne Microsoft Excel. Sie ermöglicht das programmgesteuerte Erstellen, Bearbeiten und Konvertieren von Excel-Dokumenten.

### Kann ich Aspose.Cells kostenlos nutzen?
Ja, Sie können Aspose.Cells kostenlos testen. Es gibt eine kostenlose Testversion [Hier](https://releases.aspose.com/).

### Ist Aspose.Cells für große Datensätze geeignet?
Absolut! Aspose.Cells ist für die effiziente Verarbeitung großer Datensätze konzipiert und somit eine zuverlässige Wahl für datenintensive Anwendungen.

### Wie füge ich mit Aspose.Cells Diagramme hinzu?
Sie können Diagramme hinzufügen, indem Sie ein neues Diagrammobjekt erstellen und es mit Zellbereichen verknüpfen, die Ihre Daten enthalten, wie in diesem Lernprogramm gezeigt.

### Wo finde ich weitere Beispiele zur Verwendung von Aspose.Cells?
Weitere Beispiele und eine ausführliche Dokumentation finden Sie unter [Aspose.Cells-Dokumentationsseite](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}