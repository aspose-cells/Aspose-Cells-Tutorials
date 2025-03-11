---
title: Verbindungspunkte einer Form in Excel abrufen
linktitle: Verbindungspunkte einer Form in Excel abrufen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET Formverbindungspunkte in Excel erhalten. Folgen Sie unserer Schritt-für-Schritt-Anleitung, um Formpunkte einfach programmgesteuert zu extrahieren und anzuzeigen.
weight: 11
url: /de/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Verbindungspunkte einer Form in Excel abrufen

## Einführung
Wenn wir programmgesteuert mit Excel-Dateien arbeiten, müssen wir häufig mit in die Blätter eingebetteten Formen interagieren. Eine der fortgeschritteneren Aufgaben, die Sie ausführen können, ist das Extrahieren von Verbindungspunkten aus einer Form. Verbindungspunkte werden verwendet, um Formen mit Verbindern zu verbinden und ihr Layout präziser zu verwalten. Wenn Sie die Verbindungspunkte einer Form in Excel abrufen möchten, ist Aspose.Cells für .NET das richtige Tool für Sie. In diesem Tutorial führen wir Sie Schritt für Schritt durch den Prozess, um dies zu erreichen.
## Voraussetzungen
Bevor Sie in den Code eintauchen, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:
- Aspose.Cells für .NET: Sie müssen Aspose.Cells in Ihrer Entwicklungsumgebung installiert haben. Wenn Sie es noch nicht haben, können Sie[Laden Sie hier die neueste Version herunter](https://releases.aspose.com/cells/net/).
- Entwicklungsumgebung: Stellen Sie sicher, dass Sie über eine funktionierende Installation von Visual Studio oder einer anderen .NET-kompatiblen IDE verfügen.
- Grundlegende Kenntnisse in C#: Dieses Tutorial setzt voraus, dass Sie über grundlegende Kenntnisse der C#-Programmierung und der objektorientierten Prinzipien verfügen.
 Sie können sich auch anmelden für eine[kostenlose Testversion von Aspose.Cells](https://releases.aspose.com/) falls Sie dies noch nicht getan haben. Dadurch erhalten Sie Zugriff auf alle für dieses Handbuch erforderlichen Funktionen.

## Pakete importieren
Um in Ihrem Projekt mit Aspose.Cells arbeiten zu können, müssen Sie die erforderlichen Namespaces einbinden. Die folgenden Importanweisungen sollten am Anfang Ihres Codes platziert werden:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Diese Namespaces geben Ihnen Zugriff auf die Kernfunktionalität von Aspose.Cells und ermöglichen Ihnen die Bearbeitung von Arbeitsblättern und Formen.

## Schritt-für-Schritt-Anleitung zum Abrufen der Verbindungspunkte einer Form
In diesem Abschnitt zeigen wir Ihnen Schritt für Schritt, wie Sie die Verbindungspunkte einer Form in einem Excel-Arbeitsblatt extrahieren. Befolgen Sie jeden Schritt sorgfältig, damit Sie alles genau verstehen.
## Schritt 1: Instanziieren einer neuen Arbeitsmappe
 Als erstes müssen wir eine Instanz des`Workbook` Klasse. Dies stellt eine Excel-Datei in Aspose.Cells dar. Wenn Sie keine vorhandene Datei haben, ist das kein Problem – Sie können mit einer leeren Arbeitsmappe beginnen.
```csharp
// Instanziieren einer neuen Arbeitsmappe
Workbook workbook = new Workbook();
```
 In diesem Schritt haben wir eine leere Excel-Arbeitsmappe erstellt. Sie können jedoch auch eine vorhandene laden, indem Sie den Dateipfad an die`Workbook` Konstruktor.
## Schritt 2: Zugriff auf das erste Arbeitsblatt
Als Nächstes müssen wir auf das Arbeitsblatt zugreifen, in dem wir mit Formen arbeiten möchten. In diesem Fall verwenden wir das erste Arbeitsblatt der Arbeitsmappe.
```csharp
// Holen Sie sich das erste Arbeitsblatt in der Arbeitsmappe
Worksheet worksheet = workbook.Worksheets[0];
```
 Diese Zeile greift auf das erste Arbeitsblatt aus der Sammlung von Arbeitsblättern in der Arbeitsmappe zu. Wenn Sie mit einem bestimmten Blatt arbeiten, können Sie den Index ersetzen`0` mit dem gewünschten Index.
## Schritt 3: Neues Textfeld (Form) hinzufügen
Fügen wir nun dem Arbeitsblatt eine neue Form hinzu. Wir erstellen ein Textfeld, also eine Art Form. Sie können auch andere Formen hinzufügen, der Einfachheit halber beschränken wir uns in diesem Tutorial jedoch auf ein Textfeld.
```csharp
// Fügen Sie der Sammlung ein neues Textfeld hinzu
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
Folgendes haben wir getan:
-  Ein Textfeld wurde in der Zeile hinzugefügt`2` , Spalte`1`.
-  Stellen Sie die Abmessungen des Textfelds ein auf`160` Einheiten in Breite und`200` Einheiten in der Höhe.
## Schritt 4: Zugriff auf die Form aus der Formensammlung
 Sobald wir das Textfeld hinzugefügt haben, wird es Teil der Formensammlung des Arbeitsblatts. Jetzt greifen wir auf diese Form zu, indem wir`Shapes`Sammlung.
```csharp
// Zugriff auf die Form (Textfeld) aus der Formensammlung
Shape shape = workbook.Worksheets[0].Shapes[0];
```
In diesem Schritt rufen wir die erste Form (unser Textfeld) aus der Sammlung ab. Wenn Sie mehrere Formen haben, können Sie den Index angeben oder die Form sogar nach Namen suchen.
## Schritt 5: Verbindungspunkte abrufen
Nachdem wir nun unsere Form haben, extrahieren wir ihre Verbindungspunkte. Diese Punkte werden zum Anfügen von Verbindungsstücken an die Form verwendet. Die`ConnectionPoints` Die Eigenschaft der Form gibt alle verfügbaren Verbindungspunkte zurück.
```csharp
// Holen Sie sich alle Verbindungspunkte in dieser Form
var connectionPoints = shape.ConnectionPoints;
```
Dadurch erhalten wir eine Sammlung aller für diese Form verfügbaren Verbindungspunkte.
## Schritt 6: Verbindungspunkte anzeigen
Schließlich möchten wir die Koordinaten jedes Verbindungspunkts anzeigen. Dazu durchlaufen wir die Verbindungspunkte und geben sie auf der Konsole aus.
```csharp
// Alle Formpunkte anzeigen
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
 Diese Schleife durchläuft jeden Verbindungspunkt und gibt die`X` Und`Y` Koordinaten. Dies kann zum Debuggen oder zur visuellen Bestätigung der Verbindungspunkte einer Form nützlich sein.
## Schritt 7: Ausführen und Abschließen
Sobald Sie alle oben genannten Schritte eingerichtet haben, können Sie den Code ausführen. Hier ist die letzte Zeile, die sicherstellt, dass der Vorgang erfolgreich abgeschlossen wird:
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
Diese Zeile protokolliert lediglich eine Meldung an die Konsole, die angibt, dass der Vorgang abgeschlossen wurde.

## Abschluss
In diesem Tutorial haben wir erläutert, wie Sie mit Aspose.Cells für .NET Verbindungspunkte einer Form in Excel abrufen. Indem wir die Aufgabe in kleine, überschaubare Schritte unterteilten, haben wir den Prozess des Erstellens einer Arbeitsmappe, des Hinzufügens einer Form und des Extrahierens der Verbindungspunkte untersucht.
Wenn Sie verstehen, wie Sie Formen programmgesteuert bearbeiten, eröffnen sich Ihnen unzählige Möglichkeiten zum Erstellen dynamischer und interaktiver Excel-Tabellen. Egal, ob Sie Berichte erstellen, Dashboards entwerfen oder Diagramme erstellen, dieses Wissen wird Ihnen von Nutzen sein.
## Häufig gestellte Fragen
### Was ist ein Verbindungspunkt in einer Form?
Ein Verbindungspunkt ist ein bestimmter Punkt auf einer Form, an dem Sie Verbindungsstücke anbringen oder die Form mit anderen Formen verknüpfen können.
### Kann ich Verbindungspunkte für alle Formen in einem Arbeitsblatt abrufen?
Ja, mit Aspose.Cells können Sie Verbindungspunkte für jede Form abrufen, die diese unterstützt. Durchlaufen Sie einfach die Formensammlung im Arbeitsblatt.
### Benötige ich eine Lizenz, um Aspose.Cells zu verwenden?
Ja, Sie können es zwar kostenlos testen, für den vollen Funktionsumfang ist jedoch eine Lizenz erforderlich. Sie können[Kaufen Sie hier eine Lizenz](https://purchase.aspose.com/buy)oder erhalten Sie eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
### Wie kann ich in Aspose.Cells verschiedene Arten von Formen hinzufügen?
Sie können die`Add` Methode für Formen wie Rechtecke, Ellipsen usw. Jede Form hat spezifische Parameter, die Sie anpassen können.
### Wie lade ich eine vorhandene Excel-Datei, anstatt eine neue zu erstellen?
 Um eine vorhandene Datei zu laden, übergeben Sie den Dateipfad an die`Workbook` Konstruktor, wie folgt:  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
