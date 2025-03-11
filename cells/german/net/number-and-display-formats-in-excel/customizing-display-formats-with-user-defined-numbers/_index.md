---
title: Anpassen von Anzeigeformaten mit benutzerdefinierten Zahlen
linktitle: Anpassen von Anzeigeformaten mit benutzerdefinierten Zahlen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie Anzeigeformate mit Aspose.Cells für .NET anpassen. Formatieren Sie Datumsangaben, Prozentsätze und Währungen mit dieser Schritt-für-Schritt-Anleitung.
weight: 11
url: /de/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassen von Anzeigeformaten mit benutzerdefinierten Zahlen

## Einführung
Beim Arbeiten mit Excel-Dateien ist häufig eine benutzerdefinierte Formatierung von Zellen erforderlich, um Daten aussagekräftiger und benutzerfreundlicher darzustellen. Stellen Sie sich vor, Sie erstellen eine Excel-Datei für einen Bericht. Sie möchten nicht nur Rohzahlen. Sie möchten, dass Daten, Prozentsätze und Währungen elegant und professionell aussehen, oder? Hier kommen benutzerdefinierte Anzeigeformate ins Spiel. In diesem Tutorial tauchen wir tief in Aspose.Cells für .NET ein, um Ihnen zu zeigen, wie Sie das Anzeigeformat von Zahlen mithilfe benutzerdefinierter Einstellungen anpassen.
## Voraussetzungen
Bevor Sie beginnen, stellen Sie sicher, dass Sie alles bereit haben, um diesem Tutorial folgen zu können. Folgendes benötigen Sie:
-  Aspose.Cells für .NET installiert.[Laden Sie es hier herunter](https://releases.aspose.com/cells/net/).
- Grundkenntnisse in C# und .NET Framework.
-  Eine gültige Lizenz für Aspose.Cells. Wenn Sie keine haben, holen Sie sich eine[Kostenlose Testversion](https://releases.aspose.com/) oder fordern Sie ein[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
- Eine IDE wie Visual Studio.
- .NET Framework 4.0 oder höher.
 Wenn Sie etwas vermissen, machen Sie sich keine Sorgen. Sie können diese Links jederzeit erneut aufrufen, um die erforderlichen Dateien herunterzuladen oder Hilfe von der[Aspose-Supportforum](https://forum.aspose.com/c/cells/9).
## Namespaces importieren
Bevor Sie mit dem Code beginnen, müssen Sie die erforderlichen Namespaces importieren, um auf alle erforderlichen Aspose.Cells-Funktionen zuzugreifen.
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Diese beiden Namespaces werden Ihre Kernwerkzeuge in diesem Tutorial sein. Kommen wir nun zum spaßigen Teil:
## Schritt 1: Einrichten des Projektverzeichnisses
Zuerst brauchen Sie einen Ort, an dem Sie Ihre Dateien speichern können, richtig? Lassen Sie uns ein Verzeichnis erstellen, in dem die Excel-Ausgabedatei gespeichert wird. In diesem Schritt stellen wir auch sicher, dass das Verzeichnis existiert, bevor wir etwas speichern.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
-  Wir definieren eine`dataDir` Variable zum Speichern des Pfads, in den die Excel-Ausgabedatei gespeichert wird.
-  Anschließend prüfen wir, ob das Verzeichnis existiert, indem wir`System.IO.Directory.Exists()`.
-  Wenn das Verzeichnis nicht existiert, wird es erstellt mit`System.IO.Directory.CreateDirectory()`.
## Schritt 2: Erstellen Sie eine neue Arbeitsmappe und fügen Sie ein Arbeitsblatt hinzu
Nachdem wir nun unser Verzeichnis haben, erstellen wir eine neue Excel-Arbeitsmappe und fügen ihr ein Arbeitsblatt hinzu.
```csharp
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
// Hinzufügen eines neuen Arbeitsblatts zum Excel-Objekt
int i = workbook.Worksheets.Add();
// Abrufen der Referenz des neu hinzugefügten Arbeitsblatts durch Übergeben seines Blattindex
Worksheet worksheet = workbook.Worksheets[i];
```
-  Zunächst erstellen wir ein neues`Workbook` Objekt. Stellen Sie sich das als Ihre Excel-Datei vor.
-  Wir fügen dieser Arbeitsmappe ein neues Arbeitsblatt hinzu, indem wir`Add()`Methode und speichern Sie den Index in der Variablen`i`.
-  Wir verweisen auf dieses Arbeitsblatt mit dem`workbook.Worksheets[i]`.
## Schritt 3: Einer Zelle ein Datum hinzufügen und ihr Format anpassen
 Fügen wir nun das aktuelle Datum in eine Zelle ein und formatieren es so, dass es auf benutzerdefinierte Weise angezeigt wird. Anstelle des Standarddatumsformats legen wir ein benutzerdefiniertes Format fest wie`d-mmm-yy`.
```csharp
// Hinzufügen des aktuellen Systemdatums zur Zelle „A1“
worksheet.Cells["A1"].PutValue(DateTime.Now);
// Den Stil der Zelle A1 abrufen
Style style = worksheet.Cells["A1"].GetStyle();
// Festlegen des benutzerdefinierten Anzeigeformats zur Anzeige des Datums als „d-mmm-yy“
style.Custom = "d-mmm-yy";
// Anwenden des Stils auf Zelle A1
worksheet.Cells["A1"].SetStyle(style);
```
-  Wir fügen das aktuelle Systemdatum zur Zelle hinzu`A1` mit`PutValue(DateTime.Now)`.
-  Wir rufen den aktuellen Stil der Zelle ab`A1` mit`GetStyle()`.
-  Wir ändern den Stil der Zelle durch die Einstellung`style.Custom = "d-mmm-yy"`, das das Datum so formatiert, dass Tag, Monat (abgekürzt) und Jahr angezeigt werden.
-  Zum Schluss wenden wir den neuen Stil auf die Zelle an mit`SetStyle()`.
## Schritt 4: Formatieren einer Zelle als Prozentsatz
 Als nächstes arbeiten wir mit Zahlen. Wir fügen einer anderen Zelle einen numerischen Wert hinzu, sagen wir`A2`, und formatieren Sie es als Prozentsatz.
```csharp
//Hinzufügen eines numerischen Wertes zur Zelle „A2“
worksheet.Cells["A2"].PutValue(20);
// Den Stil der Zelle A2 abrufen
style = worksheet.Cells["A2"].GetStyle();
// Festlegen des benutzerdefinierten Anzeigeformats zum Anzeigen des Werts als Prozentsatz
style.Custom = "0.0%";
// Anwenden des Stils auf Zelle A2
worksheet.Cells["A2"].SetStyle(style);
```
-  Wir schaffen Mehrwert`20` zur Zelle`A2`.
-  Wir rufen den Stil der Zelle ab`A2` und legen Sie das benutzerdefinierte Format fest auf`0.0%` um den Wert als Prozentsatz anzuzeigen (z. B. 20 %).
-  Zuletzt wenden wir den Stil auf die Zelle an mit`SetStyle()`.
## Schritt 5: Eine Zelle als Währung formatieren
 Fügen wir einen weiteren Wert hinzu, beispielsweise zur Zelle`A3`und formatieren Sie es so, dass es als Währung angezeigt wird. Um die Sache interessanter zu machen, verwenden wir ein Format, das positive Werte als Währung in Pfund und negative Werte in Dollar anzeigt.
```csharp
// Hinzufügen eines numerischen Wertes zur Zelle „A3“
worksheet.Cells["A3"].PutValue(2546);
// Den Stil der A3-Zelle abrufen
style = worksheet.Cells["A3"].GetStyle();
// Festlegen des benutzerdefinierten Anzeigeformats zum Anzeigen des Werts als Währung
style.Custom = "£#,##0;[Red]$-#,##0";
// Anwenden des Stils auf Zelle A3
worksheet.Cells["A3"].SetStyle(style);
```
-  Wir schaffen Mehrwert`2546` zur Zelle`A3`.
-  Wir legen ein benutzerdefiniertes Format fest`£#,##0;[Red]$-#,##0`, das positive Werte mit einem Nummernzeichen und negative Werte in Rot mit einem Dollarzeichen anzeigt.
- Wir wenden den Stil auf die Zelle an mit`SetStyle()`.
## Schritt 6: Speichern der Arbeitsmappe
Der letzte Schritt besteht darin, die Arbeitsmappe als Excel-Datei zu speichern. Für dieses Tutorial verwenden wir das Excel 97-2003-Format.
```csharp
// Speichern der Excel-Datei
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
-  Der`Save()` Die Methode speichert die Arbeitsmappe im angegebenen Verzeichnis.
-  Wir wählen`SaveFormat.Excel97To2003` um die Kompatibilität mit älteren Excel-Versionen sicherzustellen.
## Abschluss
Da haben Sie es! Wir haben gerade eine Excel-Datei erstellt, benutzerdefinierte Datums-, Prozent- und Währungsformate mit Aspose.Cells für .NET zu bestimmten Zellen hinzugefügt und die Datei gespeichert. Durch benutzerdefinierte Formatierung werden Ihre Excel-Dateien viel lesbarer und professioneller. Vergessen Sie nicht, andere Formatierungsoptionen in Aspose.Cells zu erkunden, wie z. B. bedingte Formatierung, um noch mehr Kontrolle über das Aussehen Ihrer Daten zu haben.
## Häufig gestellte Fragen
### Wie kann ich in Aspose.Cells komplexere Formatierungsoptionen anwenden?
Sie können verschiedene Formatierungsstile, beispielsweise Schriftfarbe, Rahmen und Hintergrundfarben, mit benutzerdefinierten Zahlenformaten kombinieren.
### Kann ich einem Zellbereich ein benutzerdefiniertes Zahlenformat zuweisen?
Ja, Aspose.Cells ermöglicht Ihnen die Anwendung eines Stils auf einen Zellbereich mithilfe der`Range.SetStyle()` Verfahren.
### In welchen anderen Dateiformaten kann ich die Arbeitsmappe speichern?
 Aspose.Cells unterstützt viele Formate, darunter XLSX, CSV und PDF. Ändern Sie einfach die`SaveFormat` im`Save()` Verfahren.
### Kann ich negative Zahlen anders formatieren?
Auf jeden Fall! Sie können benutzerdefinierte Zahlenformate verwenden, um negative Zahlen mit unterschiedlichen Farben oder Symbolen anzuzeigen.
### Ist Aspose.Cells für .NET kostenlos?
 Aspose.Cells bietet eine kostenlose Testversion an, für die volle Funktionalität benötigen Sie jedoch eine gültige Lizenz. Sie erhalten eine[vorläufige Lizenz hier](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
