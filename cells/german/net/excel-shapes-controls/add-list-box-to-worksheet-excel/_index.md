---
title: Listenfeld zum Arbeitsblatt in Excel hinzufügen
linktitle: Listenfeld zum Arbeitsblatt in Excel hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET einem Excel-Arbeitsblatt ein Listenfeld hinzufügen. Folgen Sie unserer einfachen Schritt-für-Schritt-Anleitung und machen Sie Ihre Excel-Tabellen interaktiv.
weight: 20
url: /de/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Listenfeld zum Arbeitsblatt in Excel hinzufügen

## Einführung
Das Hinzufügen interaktiver Elemente zu Ihren Excel-Arbeitsblättern, wie z. B. ein Listenfeld, kann die Datenverwaltung und -präsentation erheblich verbessern. Egal, ob Sie ein interaktives Formular oder ein benutzerdefiniertes Dateneingabetool erstellen, die Möglichkeit, Benutzereingaben mit einem Listenfeld zu steuern, ist von unschätzbarem Wert. Aspose.Cells für .NET bietet eine effiziente Möglichkeit, diese Steuerelemente in Ihren Excel-Dateien hinzuzufügen und zu verwalten. In dieser Anleitung führen wir Sie durch den Prozess des Hinzufügens eines Listenfelds zu einem Arbeitsblatt mit Aspose.Cells für .NET.
## Voraussetzungen
Bevor Sie mit der Codierung beginnen, stellen Sie sicher, dass Sie über die folgenden Tools und Ressourcen verfügen:
-  Aspose.Cells für .NET-Bibliothek: Sie können es herunterladen von der[Aspose.Cells für .NET-Downloadseite](https://releases.aspose.com/cells/net/).
- Entwicklungsumgebung: Jede IDE, die .NET-Entwicklung unterstützt, z. B. Visual Studio.
- .NET Framework: Stellen Sie sicher, dass Ihr Projekt auf eine unterstützte Version des .NET Frameworks abzielt.
 Erwägen Sie auch die Anschaffung eines[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) wenn Sie alle Funktionen ohne Einschränkungen erkunden möchten.
## Pakete importieren
Stellen Sie vor dem Start sicher, dass Sie die erforderlichen Aspose.Cells-Namespaces importiert haben. So geht's:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
In diesem Tutorial unterteilen wir den Vorgang zum Hinzufügen eines Listenfelds in mehrere einfache Schritte. Befolgen Sie jeden Schritt genau, um sicherzustellen, dass alles wie erwartet funktioniert.
## Schritt 1: Einrichten Ihres Dokumentverzeichnisses
Bevor Sie eine Excel-Datei erstellen, benötigen Sie einen Speicherort dafür. So richten Sie das Verzeichnis ein:
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
In diesem Schritt legen Sie fest, wo Ihre Datei gespeichert wird. Der Code prüft, ob das Verzeichnis existiert, und erstellt es, wenn nicht. Dadurch wird sichergestellt, dass Sie später keine „Datei nicht gefunden“-Fehler erhalten.
## Schritt 2: Erstellen Sie eine neue Arbeitsmappe und greifen Sie auf das erste Arbeitsblatt zu
Als Nächstes erstellen wir eine neue Arbeitsmappe und greifen auf das erste Arbeitsblatt zu, wo wir unser Listenfeld hinzufügen.
```csharp
// Erstellen Sie eine neue Arbeitsmappe.
Workbook workbook = new Workbook();
// Holen Sie sich das erste Arbeitsblatt.
Worksheet sheet = workbook.Worksheets[0];
```
Eine Arbeitsmappe ist im Wesentlichen Ihre Excel-Datei. Hier erstellen wir eine neue Arbeitsmappe und greifen auf das erste Arbeitsblatt zu, in dem wir unser Listenfeld platzieren. Stellen Sie sich das so vor, als würden Sie eine leere Leinwand erstellen, auf der Sie die Steuerelemente ausmalen.
## Schritt 3: Daten für die Listbox eingeben
Bevor wir das Listenfeld hinzufügen, müssen wir einige Daten eingeben, auf die das Listenfeld verweist.
```csharp
// Holen Sie sich die Arbeitsblattzellensammlung.
Cells cells = sheet.Cells;
// Geben Sie einen Wert für das Etikett ein.
cells["B3"].PutValue("Choose Dept:");
// Stellen Sie die Beschriftung auf fett ein.
cells["B3"].GetStyle().Font.IsBold = true;
// Eingabewerte für das Listenfeld.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Hier fügen wir dem Arbeitsblatt etwas Text hinzu. Die Beschriftung „Abteilung auswählen:“ wird in Zelle B3 platziert und ihre Schriftart ist fett eingestellt. In Spalte A fügen wir Werte ein, die als Eingabebereich für unser Listenfeld dienen und verschiedene Abteilungen darstellen. Dieser Eingabebereich ist das, was Benutzer auswählen, wenn sie mit dem Listenfeld interagieren.
## Schritt 4: Das Listenfeld zum Arbeitsblatt hinzufügen
Nachdem wir nun die Daten eingerichtet haben, fügen wir das Listenfeld-Steuerelement selbst hinzu.
```csharp
// Fügen Sie ein neues Listenfeld hinzu.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Dieser Code fügt das Listenfeld zum Arbeitsblatt hinzu. Die Parameter definieren die Position und Größe des Listenfelds. Das Listenfeld wird in Zeile 2, Spalte 0 mit einer Breite von 122 und einer Höhe von 100 platziert. Diese Koordinaten und die Größe bestimmen, wo das Listenfeld im Arbeitsblatt angezeigt wird.
## Schritt 5: Eigenschaften des Listenfelds festlegen
Als Nächstes legen wir verschiedene Eigenschaften für das Listenfeld fest, um es voll funktionsfähig zu machen.
```csharp
// Legen Sie den Platzierungstyp fest.
listBox.Placement = PlacementType.FreeFloating;
// Legen Sie die verknüpfte Zelle fest.
listBox.LinkedCell = "A1";
// Stellen Sie den Eingabebereich ein.
listBox.InputRange = "A2:A7";
// Legen Sie den Auswahltyp fest.
listBox.SelectionType = SelectionType.Single;
// Stellen Sie das Listenfeld mit 3D-Schattierung ein.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Diese Eigenschaft stellt sicher, dass das Listenfeld an seiner Position bleibt, unabhängig davon, wie das Arbeitsblatt geändert wird.
- LinkedCell: Dadurch wird eine Zelle (in diesem Fall A1) festgelegt, in der der ausgewählte Wert aus dem Listenfeld angezeigt wird.
- InputRange: Dies teilt dem Listenfeld mit, wo nach der Optionsliste gesucht werden soll (A2 bis A7, die wir zuvor festgelegt haben).
- SelectionType.Single: Dadurch kann der Benutzer nur ein Element aus dem Listenfeld auswählen.
- Schatten: Der Schatteneffekt verleiht der Listenbox ein dreidimensionaleres Aussehen und macht sie optisch ansprechender.
## Schritt 6: Speichern Sie die Excel-Datei
Zum Schluss speichern wir unsere Arbeitsmappe mit dem enthaltenen Listenfeld.
```csharp
// Speichern Sie die Arbeitsmappe.
workbook.Save(dataDir + "book1.out.xls");
```
Diese Codezeile speichert die Arbeitsmappe in dem Verzeichnis, das wir zuvor eingerichtet haben. Die Datei heißt „book1.out.xls“, Sie können jedoch einen beliebigen Namen wählen, der zu Ihrem Projekt passt.
## Abschluss
Und da haben Sie es! Sie haben erfolgreich ein Listenfeld zu einem Excel-Arbeitsblatt hinzugefügt, indem Sie Aspose.Cells für .NET verwenden. Mit nur wenigen Codezeilen haben wir ein voll funktionsfähiges Listenfeld erstellt, das das Arbeitsblatt interaktiver und dynamischer macht. Dieses Tutorial sollte Ihnen eine solide Grundlage bieten, um andere Steuerelemente und Funktionen in Aspose.Cells für .NET zu erkunden. Experimentieren Sie weiter und schon bald werden Sie die umfangreiche Funktionalität der Bibliothek beherrschen!
## Häufig gestellte Fragen
### Kann ich im Listenfeld Mehrfachauswahl zulassen?  
 Ja, Sie können die`SelectionType` Zu`SelectionType.Multi` um Mehrfachauswahl zu ermöglichen.
### Kann ich das Erscheinungsbild des Listenfelds ändern?  
Auf jeden Fall! Mit Aspose.Cells können Sie das Aussehen des Listenfelds anpassen, einschließlich Größe, Schriftart und sogar Farbe.
### Was ist, wenn ich das Listenfeld später entfernen muss?  
 Sie können auf das Listenfeld zugreifen und es aus dem`Shapes` Sammlung mit`sheet.Shapes.RemoveAt(index)`.
### Kann ich das Listenfeld mit einer anderen Zelle verknüpfen?  
 Ja, ändern Sie einfach die`LinkedCell` -Eigenschaft in jede andere Zelle, in der Sie den ausgewählten Wert anzeigen möchten.
### Wie füge ich dem Listenfeld weitere Elemente hinzu?  
Aktualisieren Sie einfach den Eingabebereich, indem Sie weitere Werte in die angegebenen Zellen einfügen. Das Listenfeld wird dann automatisch aktualisiert.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
