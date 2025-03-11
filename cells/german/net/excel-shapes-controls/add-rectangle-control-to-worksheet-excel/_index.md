---
title: Rechteck-Steuerelement zum Arbeitsblatt in Excel hinzufügen
linktitle: Rechteck-Steuerelement zum Arbeitsblatt in Excel hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in einer ausführlichen Schritt-für-Schritt-Anleitung, wie Sie mit Aspose.Cells für .NET einem Excel-Arbeitsblatt ein Rechteck-Steuerelement hinzufügen.
weight: 25
url: /de/net/excel-shapes-controls/add-rectangle-control-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rechteck-Steuerelement zum Arbeitsblatt in Excel hinzufügen

## Einführung
Wenn es um die Automatisierung von Excel-Aufgaben geht, ist Aspose.Cells für .NET ein leistungsstarkes Tool, mit dem Sie eine Vielzahl von Zielen erreichen können, darunter das Hinzufügen von Formen wie Rechtecken zu Ihren Arbeitsblättern. In diesem Handbuch erfahren Sie, wie Sie mit Aspose.Cells für .NET einem Excel-Arbeitsblatt ein Rechteck-Steuerelement hinzufügen. Am Ende können Sie ein Arbeitsblatt mit einem darin eingebetteten Rechteck-Steuerelement erstellen, anpassen und speichern.
Aber bevor wir eintauchen, sprechen wir über die Voraussetzungen.
## Voraussetzungen
Um diesem Tutorial folgen zu können, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:
1.  Aspose.Cells für .NET-Bibliothek: Falls noch nicht geschehen,[Laden Sie die Bibliothek herunter](https://releases.aspose.com/cells/net/) oder installieren Sie es mit NuGet in Visual Studio.
2. .NET Framework: Sie müssen die .NET-Entwicklungsumgebung auf Ihrem Computer eingerichtet haben.
3. Grundkenntnisse in C#: Obwohl wir Sie Schritt für Schritt anleiten, sind Grundkenntnisse in C# und objektorientierter Programmierung von Vorteil.
4.  Lizenz: Die Verwendung von Aspose.Cells im Evaluierungsmodus funktioniert für grundlegende Aufgaben gut, aber für die volle Funktionalität sollten Sie eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/)oder den Kauf eines von[Hier](https://purchase.aspose.com/buy).
Tauchen wir jetzt in den Code ein!
## Pakete importieren
Um mit Aspose.Cells zu beginnen, stellen Sie sicher, dass Sie die erforderlichen Namespaces in Ihr Projekt importiert haben. Diese Importe ermöglichen den Zugriff auf verschiedene Klassen und Methoden, die Sie für die Interaktion mit Excel-Dateien benötigen.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Diese Zeilen stellen sicher, dass Ihr Projekt mit Dateiverzeichnissen interagieren kann (`System.IO`), Excel-Arbeitsmappen (`Aspose.Cells`) und Formzeichnen (`Aspose.Cells.Drawing`).
Lassen Sie uns den Vorgang nun in einfache Schritte aufteilen, damit Sie ihn problemlos nachvollziehen und in Ihren eigenen Projekten wiederholen können.
## Schritt 1: Einrichten des Verzeichnispfads
Als Erstes müssen Sie das Verzeichnis definieren, in dem Ihre Excel-Datei gespeichert wird. Dieser Schritt stellt sicher, dass Ihr Projekt weiß, wo die Ausgabedatei erstellt und gespeichert werden soll.
### Definieren des Datenverzeichnisses
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
```
 Hier geben Sie den Verzeichnispfad an, in dem die Excel-Datei gespeichert wird. Sie können ersetzen`"Your Document Directory"` durch den tatsächlichen Pfad auf Ihrem Computer oder erstellen Sie dynamisch einen Ordner, falls dieser nicht vorhanden ist.
### Überprüfen und Erstellen des Verzeichnisses
```csharp
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Dieser Block prüft, ob das Verzeichnis existiert. Wenn nicht, wird eines erstellt. Stellen Sie es sich so vor, als ob Sie Ihren Aktenschrank fertig haben, bevor Sie irgendwelche Dokumente speichern.
## Schritt 2: Instanziieren einer neuen Arbeitsmappe
 In diesem Schritt erstellen Sie eine neue Excel-Arbeitsmappe mit dem`Aspose.Cells.Workbook` Klasse. Dies dient als Container für Ihr Arbeitsblatt und Ihre Formen.
```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook excelbook = new Workbook();
```
 Durch einen Anruf bei`Workbook` Konstruktor haben Sie jetzt eine leere Excel-Arbeitsmappe, die zur Anpassung bereit ist.
## Schritt 3: Hinzufügen eines Rechteck-Steuerelements
Und jetzt geschieht die Magie. Sie fügen dem ersten Arbeitsblatt Ihrer Arbeitsmappe eine rechteckige Form hinzu.
```csharp
// Fügen Sie ein rechteckiges Steuerelement hinzu.
Aspose.Cells.Drawing.RectangleShape rectangle = excelbook.Worksheets[0].Shapes.AddRectangle(3, 0, 2, 0, 70, 130);
```
Lassen Sie uns das aufschlüsseln:
- `excelbook.Worksheets[0]`: Dadurch wird auf das erste Arbeitsblatt in Ihrer Arbeitsmappe zugegriffen.
- `.Shapes.AddRectangle(3, 0, 2, 0, 70, 130)`: Dadurch wird dem Arbeitsblatt eine rechteckige Form hinzugefügt. Die Parameter hier definieren die Position (Zeile und Spalte) sowie die Breite und Höhe des Rechtecks.
## Schritt 4: Anpassen des Rechtecks
Das bloße Hinzufügen eines Rechtecks reicht nicht aus – Sie möchten es auch anpassen. In diesem Schritt legen wir die Platzierung, Linienstärke und Strichart des Rechtecks fest.
### Festlegen der Platzierung
```csharp
// Legen Sie die Platzierung des Rechtecks fest.
rectangle.Placement = PlacementType.FreeFloating;
```
Dadurch wird festgelegt, dass das Rechteck frei schwebt, also nicht an die Zellenabmessungen gebunden ist.
### Festlegen der Linienstärke
```csharp
// Stellen Sie die Linienstärke ein.
rectangle.Line.Weight = 4;
```
Hier stellen wir die Linienstärke des Rechtecks auf 4 Punkt ein. Je höher die Zahl, desto dicker die Linie.
### Festlegen des Strichstils
```csharp
// Legen Sie den Strichstil des Rechtecks fest.
rectangle.Line.DashStyle = MsoLineDashStyle.Solid;
```
 Diese Zeile setzt den Strichstil des Rechteckrandes auf durchgezogen. Sie können mit verschiedenen Stilen experimentieren, wie`Dash` oder`Dot` abhängig von Ihren Anforderungen.
## Schritt 5: Speichern der Arbeitsmappe
Nachdem das Rechteck hinzugefügt und angepasst wurde, besteht der letzte Schritt darin, die Arbeitsmappe im angegebenen Verzeichnis zu speichern.
```csharp
// Speichern Sie die Excel-Datei.
excelbook.Save(dataDir + "book1.out.xls");
```
 Dadurch wird die Arbeitsmappe als`.xls` Datei in dem Ordner, den Sie zuvor definiert haben. Sie können das Dateiformat ändern, indem Sie die Erweiterung ändern, z. B.`.xlsx` wenn Sie das neuere Excel-Format bevorzugen.
## Abschluss
Und da haben Sie es! Das Hinzufügen eines Rechteck-Steuerelements zu einem Excel-Arbeitsblatt mit Aspose.Cells für .NET ist ein unkomplizierter Vorgang, wenn Sie ihn Schritt für Schritt aufschlüsseln. Ob Sie nun Formen für die optische Attraktivität hinzufügen, Abschnitte Ihrer Daten hervorheben oder Ihre Berichte anpassen möchten, Aspose.Cells bietet Ihnen die Flexibilität, dies programmgesteuert zu tun.
Dieser Leitfaden sollte Ihnen alles Wissen vermittelt haben, das Sie benötigen, um mit Aspose.Cells Formen wie Rechtecke zu Ihren Excel-Tabellen hinzuzufügen. Jetzt ist es an der Zeit zu experimentieren und zu sehen, was Sie sonst noch mit dieser leistungsstarken Bibliothek erreichen können!
## Häufig gestellte Fragen
### Kann ich mit Aspose.Cells für .NET andere Formen wie Kreise oder Linien hinzufügen?  
Ja, mit Aspose.Cells können Sie verschiedene Formen hinzufügen, darunter Kreise, Linien, Pfeile und mehr.
### Welche anderen Eigenschaften kann ich für das Rechteck-Steuerelement festlegen?  
Sie können die Füllfarbe, Linienfarbe und Transparenz anpassen und sogar Text innerhalb des Rechtecks hinzufügen.
### Ist Aspose.Cells mit .NET Core kompatibel?  
Ja, Aspose.Cells unterstützt .NET Core sowie .NET Framework und andere .NET-basierte Plattformen.
### Kann ich das Rechteck relativ zu einer bestimmten Zelle positionieren?  
 Ja, Sie können das Rechteck in bestimmten Zeilen und Spalten platzieren oder die`PlacementType` um zu steuern, wie es verankert ist.
### Gibt es eine kostenlose Testversion für Aspose.Cells?  
 Ja, Sie können eine[Kostenlose Testversion](https://releases.aspose.com/) von der Website, um die Funktionen der Bibliothek vor dem Kauf zu testen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
