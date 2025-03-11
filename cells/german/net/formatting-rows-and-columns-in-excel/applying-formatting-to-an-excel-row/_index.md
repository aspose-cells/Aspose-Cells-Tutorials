---
title: Programmgesteuertes Anwenden der Formatierung auf eine Excel-Zeile
linktitle: Programmgesteuertes Anwenden der Formatierung auf eine Excel-Zeile
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET programmgesteuert Formatierungen auf eine Excel-Zeile anwenden. Diese detaillierte Schritt-für-Schritt-Anleitung deckt alles von der Ausrichtung bis zu den Rändern ab.
weight: 11
url: /de/net/formatting-rows-and-columns-in-excel/applying-formatting-to-an-excel-row/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Programmgesteuertes Anwenden der Formatierung auf eine Excel-Zeile

## Einführung
In diesem Tutorial zeigen wir Ihnen, wie Sie mit Aspose.Cells für .NET programmgesteuert Formatierungen auf eine Excel-Zeile anwenden. Wir behandeln alles, vom Einrichten der Umgebung bis zum Anwenden verschiedener Formatierungsoptionen wie Schriftfarbe, Ausrichtung und Rahmen – und das alles auf einfache und ansprechende Weise. Lassen Sie uns eintauchen!
## Voraussetzungen
Bevor wir beginnen, stellen wir sicher, dass Sie alles haben, was Sie brauchen, um diesem Tutorial zu folgen. Folgendes benötigen Sie:
1.  Aspose.Cells für .NET-Bibliothek – Sie können es herunterladen von der[Aspose.Cells für .NET-Downloadseite](https://releases.aspose.com/cells/net/).
2. IDE – Jede .NET-Entwicklungsumgebung, beispielsweise Visual Studio.
3. Grundkenntnisse in C# – Sie sollten mit der Programmiersprache C# und der Arbeit mit .NET-Anwendungen vertraut sein.
Stellen Sie sicher, dass Sie auch die neueste Version von Aspose.Cells installieren, indem Sie sie entweder direkt herunterladen oder den NuGet Package Manager in Visual Studio verwenden.
## Pakete importieren
Stellen Sie zunächst sicher, dass Sie die erforderlichen Pakete importieren. Dies ist wichtig, um auf die Funktionen zuzugreifen, die für die Arbeit mit Excel-Dateien und die programmgesteuerte Anwendung von Stilen erforderlich sind.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
Nachdem die Einrichtung abgeschlossen ist, können wir mit dem spannenden Teil fortfahren: dem Formatieren der Zeilen!
In diesem Abschnitt werden wir jeden Schritt des Prozesses aufschlüsseln. Jeder Schritt wird von Codeausschnitten und einer ausführlichen Erklärung begleitet, sodass Sie auch als Neuling bei Aspose.Cells problemlos folgen können.
## Schritt 1: Einrichten der Arbeitsmappe und des Arbeitsblatts
Bevor Sie Formatierungen anwenden, müssen Sie eine Instanz der Arbeitsmappe erstellen und auf das erste Arbeitsblatt zugreifen. Das ist, als würden Sie eine leere Leinwand öffnen, bevor Sie mit dem Malen beginnen.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Instanziieren eines Workbook-Objekts
Workbook workbook = new Workbook();
// Abrufen der Referenz des ersten (Standard-)Arbeitsblatts durch Übergeben seines Blattindex
Worksheet worksheet = workbook.Worksheets[0];
```
Hier erstellen wir ein neues Arbeitsmappenobjekt und rufen das erste Arbeitsblatt ab. Dies ist das Blatt, auf das wir unsere Formatierung anwenden werden.
## Schritt 2: Einen Stil erstellen und anpassen
Nachdem Sie nun Ihr Arbeitsblatt vorbereitet haben, müssen Sie im nächsten Schritt die Stile definieren, die Sie auf die Zeile anwenden möchten. Wir beginnen mit der Erstellung eines neuen Stils und dem Festlegen von Eigenschaften wie Schriftfarbe, Ausrichtung und Rahmen.
```csharp
// Einen neuen Stil zu den Stilen hinzufügen
Style style = workbook.CreateStyle();
// Festlegen der vertikalen Ausrichtung des Textes in der Zelle "A1"
style.VerticalAlignment = TextAlignmentType.Center;
// Festlegen der horizontalen Ausrichtung des Textes in der Zelle "A1"
style.HorizontalAlignment = TextAlignmentType.Center;
// Festlegen der Schriftfarbe des Textes in der Zelle "A1"
style.Font.Color = Color.Green;
```
In diesem Teil legen wir die Ausrichtung des Textes in der Zeile fest (vertikal und horizontal) und geben die Schriftfarbe an. Hier beginnen Sie zu definieren, wie der Inhalt in Ihrem Excel-Blatt visuell angezeigt wird.
## Schritt 3: Anpassen durch Schrumpfen
Manchmal ist der Text in einer Zelle zu lang und läuft über. Ein guter Trick besteht darin, den Text so zu verkleinern, dass er in die Zelle passt und trotzdem lesbar bleibt.
```csharp
// Verkleinern des Textes, damit er in die Zelle passt
style.ShrinkToFit = true;
```
 Mit`ShrinkToFit`stellen Sie sicher, dass die Größe langer Texte so angepasst wird, dass sie in die Grenzen der Zelle passen. Dadurch sieht Ihr Excel-Blatt übersichtlicher aus.
## Schritt 4: Grenzen für die Zeile festlegen
Um Ihre Zeilen hervorzuheben, ist das Anwenden von Rahmen eine gute Option. In diesem Beispiel passen wir den unteren Rahmen an, indem wir seine Farbe auf Rot und seinen Stil auf Mittel setzen.
```csharp
// Festlegen der unteren Rahmenfarbe der Zelle auf Rot
style.Borders[BorderType.BottomBorder].Color = Color.Red;
// Den unteren Rahmentyp der Zelle auf mittel einstellen
style.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Medium;
```
Rahmen können dabei helfen, Inhalte optisch voneinander zu trennen, sodass Ihre Daten leichter lesbar und ästhetisch ansprechender werden.
## Schritt 5: Erstellen Sie ein StyleFlag-Objekt
 Der`StyleFlag`Objekt teilt Aspose.Cells mit, welche Aspekte des Stils angewendet werden sollen. Dadurch haben Sie genaue Kontrolle darüber, was angewendet wird, und stellen sicher, dass nur die beabsichtigte Formatierung festgelegt wird.
```csharp
// StyleFlag erstellen
StyleFlag styleFlag = new StyleFlag();
styleFlag.HorizontalAlignment = true;
styleFlag.VerticalAlignment = true;
styleFlag.ShrinkToFit = true;
styleFlag.Borders = true;
styleFlag.FontColor = true;
```
In diesem Fall geben wir an, dass horizontale und vertikale Ausrichtung, Schriftfarbe, Textverkleinerung und Rahmen angewendet werden sollen.
## Schritt 6: Zugriff auf die gewünschte Zeile
Sobald der Stil erstellt ist, besteht der nächste Schritt darin, auf die Zeile zuzugreifen, in der wir die Formatierung anwenden möchten. In diesem Beispiel formatieren wir die erste Zeile (Zeilenindex 0).
```csharp
// Auf eine Zeile aus der Rows-Sammlung zugreifen
Row row = worksheet.Cells.Rows[0];
```
Hier rufen wir die erste Zeile des Arbeitsblatts ab. Sie können den Index ändern, um jede andere Zeile zu formatieren.
## Schritt 7: Den Stil auf die Zeile anwenden
 Zum Schluss ist es Zeit, den Stil auf die Zeile anzuwenden! Wir verwenden die`ApplyStyle` Methode, um den definierten Stil auf die ausgewählte Zeile anzuwenden.
```csharp
// Zuweisen des Style-Objekts zur Style-Eigenschaft der Zeile
row.ApplyStyle(style, styleFlag);
```
Der Stil wird jetzt auf die gesamte Zeile angewendet, sodass Ihre Daten genau so aussehen, wie Sie es sich vorgestellt haben.
## Schritt 8: Speichern Sie die Arbeitsmappe
Wenn Sie mit der Formatierung fertig sind, müssen Sie die Arbeitsmappe in einer Excel-Datei speichern. Dies entspricht dem Klicken auf „Speichern“ in Excel, nachdem Sie Ihre Änderungen vorgenommen haben.
```csharp
// Speichern der Excel-Datei
workbook.Save(dataDir + "book1.out.xls");
```
Sie haben jetzt ein vollständig formatiertes Excel-Blatt, das in Ihrem angegebenen Verzeichnis gespeichert ist!
## Abschluss
Das ist es! In nur wenigen einfachen Schritten haben Sie gelernt, wie Sie mit Aspose.Cells für .NET programmgesteuert eine Formatierung auf eine Excel-Zeile anwenden. Von der Festlegung der Textausrichtung bis zur Anpassung von Rändern behandelte dieses Tutorial die Grundlagen, die Ihnen dabei helfen, programmgesteuert professionelle und optisch ansprechende Excel-Berichte zu erstellen. 
Aspose.Cells bietet eine breite Palette an Funktionen und die hier gezeigten Methoden können problemlos erweitert werden, um komplexere Stile und Formatierungen auf Ihre Excel-Dateien anzuwenden. Warum also nicht einfach mal ausprobieren und Ihre Daten zum Leben erwecken?
## Häufig gestellte Fragen
### Kann ich einzelnen Zellen in einer Zeile unterschiedliche Stile zuweisen?  
Ja, Sie können einzelne Zellen durch den direkten Zugriff über das`Cells` Sammlung, anstatt den Stil auf die gesamte Zeile anzuwenden.
### Ist es möglich, mit Aspose.Cells eine bedingte Formatierung anzuwenden?  
Auf jeden Fall! Aspose.Cells unterstützt bedingte Formatierung, sodass Sie Regeln basierend auf Zellwerten definieren können.
### Wie kann ich die Formatierung auf mehrere Zeilen anwenden?  
 Sie können mehrere Zeilen durchlaufen, indem Sie`for` Führen Sie eine Schleife aus und wenden Sie den gleichen Stil auf jede Zeile einzeln an.
### Unterstützt Aspose.Cells das Anwenden von Stilen auf ganze Spalten?  
 Ja, ähnlich wie bei Zeilen können Sie auf Spalten zugreifen, indem Sie`Columns` Sammlung und wenden Sie Stile darauf an.
### Kann ich Aspose.Cells mit .NET Core-Anwendungen verwenden?  
Ja, Aspose.Cells ist vollständig mit .NET Core kompatibel, sodass Sie es plattformübergreifend verwenden können.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
