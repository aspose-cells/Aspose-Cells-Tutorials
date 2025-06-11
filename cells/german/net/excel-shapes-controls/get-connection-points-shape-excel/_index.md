---
"description": "Erfahren Sie, wie Sie mit Aspose.Cells für .NET Formverbindungspunkte in Excel erhalten. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um Formpunkte einfach programmgesteuert zu extrahieren und anzuzeigen."
"linktitle": "Verbindungspunkte einer Form in Excel abrufen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Verbindungspunkte einer Form in Excel abrufen"
"url": "/de/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Verbindungspunkte einer Form in Excel abrufen

## Einführung
Bei der programmgesteuerten Arbeit mit Excel-Dateien müssen wir häufig mit in die Tabellen eingebetteten Formen interagieren. Eine der komplexeren Aufgaben ist das Extrahieren von Verbindungspunkten aus einer Form. Verbindungspunkte dienen dazu, Formen mit Konnektoren zu verbinden und ihr Layout präziser zu verwalten. Wenn Sie die Verbindungspunkte einer Form in Excel abrufen möchten, ist Aspose.Cells für .NET das richtige Tool für Sie. In diesem Tutorial führen wir Sie Schritt für Schritt durch den Prozess.
## Voraussetzungen
Bevor Sie sich in den Code vertiefen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
- Aspose.Cells für .NET: Sie müssen Aspose.Cells in Ihrer Entwicklungsumgebung installiert haben. Falls Sie es noch nicht haben, können Sie [Laden Sie hier die neueste Version herunter](https://releases.aspose.com/cells/net/).
- Entwicklungsumgebung: Stellen Sie sicher, dass Sie über eine funktionierende Installation von Visual Studio oder einer anderen .NET-kompatiblen IDE verfügen.
- Grundkenntnisse in C#: Dieses Tutorial setzt voraus, dass Sie über grundlegende Kenntnisse der C#-Programmierung und der objektorientierten Prinzipien verfügen.
Sie können sich auch für eine [kostenlose Testversion von Aspose.Cells](https://releases.aspose.com/) falls Sie dies noch nicht getan haben. Dadurch erhalten Sie Zugriff auf alle für dieses Handbuch erforderlichen Funktionen.

## Pakete importieren
Um mit Aspose.Cells in Ihrem Projekt arbeiten zu können, müssen Sie die erforderlichen Namespaces einbinden. Die folgenden Importanweisungen sollten am Anfang Ihres Codes platziert werden:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Diese Namespaces geben Ihnen Zugriff auf die Kernfunktionalität von Aspose.Cells und ermöglichen Ihnen die Bearbeitung von Arbeitsblättern und Formen.

## Schritt-für-Schritt-Anleitung zum Abrufen der Verbindungspunkte einer Form
In diesem Abschnitt erfahren Sie, wie Sie die Verbindungspunkte einer Form in einem Excel-Arbeitsblatt extrahieren. Befolgen Sie jeden Schritt sorgfältig, um ein klares Verständnis zu gewährleisten.
## Schritt 1: Instanziieren einer neuen Arbeitsmappe
Das Wichtigste zuerst: Wir müssen eine Instanz des `Workbook` Klasse. Dies stellt eine Excel-Datei in Aspose.Cells dar. Wenn Sie keine vorhandene Datei haben, ist das kein Problem – Sie können mit einer leeren Arbeitsmappe beginnen.
```csharp
// Instanziieren einer neuen Arbeitsmappe
Workbook workbook = new Workbook();
```
In diesem Schritt haben wir eine leere Excel-Arbeitsmappe erstellt. Sie können aber auch eine vorhandene laden, indem Sie den Dateipfad an die `Workbook` Konstruktor.
## Schritt 2: Zugriff auf das erste Arbeitsblatt
Als Nächstes müssen wir auf das Arbeitsblatt zugreifen, in dem wir mit Formen arbeiten möchten. In diesem Fall verwenden wir das erste Arbeitsblatt der Arbeitsmappe.
```csharp
// Holen Sie sich das erste Arbeitsblatt in der Arbeitsmappe
Worksheet worksheet = workbook.Worksheets[0];
```
Diese Zeile greift auf das erste Arbeitsblatt aus der Sammlung der Arbeitsblätter in der Arbeitsmappe zu. Wenn Sie mit einem bestimmten Arbeitsblatt arbeiten, können Sie den Index `0` mit dem gewünschten Index.
## Schritt 3: Fügen Sie ein neues Textfeld (Form) hinzu
Fügen wir nun dem Arbeitsblatt eine neue Form hinzu. Wir erstellen ein Textfeld, eine Art Form. Sie können auch andere Formen hinzufügen, der Einfachheit halber beschränken wir uns in diesem Tutorial jedoch auf ein Textfeld.
```csharp
// Fügen Sie der Sammlung ein neues Textfeld hinzu
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Folgendes haben wir getan:
- Ein Textfeld in der Zeile hinzugefügt `2`, Spalte `1`.
- Legen Sie die Abmessungen des Textfelds fest auf `160` Einheiten in Breite und `200` Einheiten in der Höhe.
## Schritt 4: Zugriff auf die Form aus der Formensammlung
Sobald wir das Textfeld hinzugefügt haben, wird es Teil der Formensammlung des Arbeitsblatts. Jetzt greifen wir auf diese Form zu über die `Shapes` Sammlung.
```csharp
// Zugriff auf die Form (Textfeld) aus der Formensammlung
Shape shape = workbook.Worksheets[0].Shapes[0];
```
In diesem Schritt rufen wir die erste Form (unser Textfeld) aus der Sammlung ab. Wenn Sie mehrere Formen haben, können Sie den Index angeben oder die Form sogar nach Namen suchen.
## Schritt 5: Verbindungspunkte abrufen
Nachdem wir nun unsere Form erstellt haben, extrahieren wir ihre Verbindungspunkte. Diese Punkte werden zum Anbringen von Konnektoren an der Form verwendet. Die `ConnectionPoints` Die Eigenschaft der Form gibt alle verfügbaren Verbindungspunkte zurück.
```csharp
// Holen Sie sich alle Verbindungspunkte in dieser Form
var connectionPoints = shape.ConnectionPoints;
```
Dadurch erhalten wir eine Sammlung aller für diese Form verfügbaren Verbindungspunkte.
## Schritt 6: Verbindungspunkte anzeigen
Abschließend möchten wir die Koordinaten jedes Verbindungspunkts anzeigen. Dazu durchlaufen wir die Verbindungspunkte und geben sie auf der Konsole aus.
```csharp
// Alle Formpunkte anzeigen
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
Diese Schleife iteriert über jeden Verbindungspunkt und druckt die `X` Und `Y` Koordinaten. Dies kann zum Debuggen oder zur visuellen Bestätigung der Verbindungspunkte einer Form nützlich sein.
## Schritt 7: Ausführen und Abschließen
Sobald Sie alle oben genannten Schritte ausgeführt haben, können Sie den Code ausführen. Hier ist die letzte Zeile, die den erfolgreichen Abschluss des Vorgangs sicherstellt:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Diese Zeile protokolliert lediglich eine Nachricht an die Konsole, die angibt, dass der Vorgang abgeschlossen wurde.

## Abschluss
In diesem Tutorial haben wir gezeigt, wie man mit Aspose.Cells für .NET die Verbindungspunkte einer Form in Excel abruft. Indem wir die Aufgabe in kleine, überschaubare Schritte unterteilten, untersuchten wir den Prozess des Erstellens einer Arbeitsmappe, des Hinzufügens einer Form und des Extrahierens der Verbindungspunkte.
Wenn Sie verstehen, wie Sie Formen programmgesteuert bearbeiten, eröffnen sich Ihnen unzählige Möglichkeiten für die Erstellung dynamischer und interaktiver Excel-Tabellen. Ob Sie Berichte erstellen, Dashboards gestalten oder Diagramme erstellen – dieses Wissen ist von Nutzen.
## Häufig gestellte Fragen
### Was ist ein Verbindungspunkt in einer Form?
Ein Verbindungspunkt ist ein bestimmter Punkt auf einer Form, an dem Sie Verbinder anbringen oder sie mit anderen Formen verknüpfen können.
### Kann ich Verbindungspunkte für alle Formen in einem Arbeitsblatt abrufen?
Ja, mit Aspose.Cells können Sie Verbindungspunkte für jede Form abrufen, die diese unterstützt. Durchlaufen Sie einfach die Formensammlung im Arbeitsblatt.
### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
Ja, Sie können es kostenlos testen, für den vollen Funktionsumfang ist jedoch eine Lizenz erforderlich. Sie können [Kaufen Sie hier eine Lizenz](https://purchase.aspose.com/buy) oder erhalten Sie eine [vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
### Wie kann ich in Aspose.Cells verschiedene Arten von Formen hinzufügen?
Sie können die `Add` Methode für Formen wie Rechtecke, Ellipsen und mehr. Jede Form verfügt über spezifische Parameter, die Sie anpassen können.
### Wie lade ich eine vorhandene Excel-Datei, anstatt eine neue zu erstellen?
Um eine vorhandene Datei zu laden, übergeben Sie den Dateipfad an die `Workbook` Konstruktor, etwa so:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}