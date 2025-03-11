---
title: Kombinationsfeld zum Arbeitsblatt in Excel hinzufügen
linktitle: Kombinationsfeld zum Arbeitsblatt in Excel hinzufügen
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET programmgesteuert ein Kombinationsfeld zu einem Excel-Arbeitsblatt hinzufügen. Diese Schritt-für-Schritt-Anleitung führt Sie durch jedes Detail.
weight: 21
url: /de/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kombinationsfeld zum Arbeitsblatt in Excel hinzufügen

## Einführung
Das Erstellen interaktiver Excel-Tabellen kann das Benutzererlebnis erheblich verbessern, insbesondere wenn Sie Formularelemente wie Kombinationsfelder hinzufügen. Kombinationsfelder ermöglichen Benutzern die Auswahl von Optionen aus einer vordefinierten Liste, was die Dateneingabe einfacher und effizienter macht. Mit Aspose.Cells für .NET können Sie Kombinationsfelder in Excel-Tabellen programmgesteuert erstellen, ohne Excel direkt zu verwenden. Diese leistungsstarke Bibliothek ermöglicht Entwicklern die Bearbeitung von Excel-Dateien auf verschiedene Weise, einschließlich der Möglichkeit, Formularsteuerelemente zu automatisieren.
In diesem Tutorial führen wir Sie durch den Vorgang zum Hinzufügen eines Kombinationsfelds zu einem Arbeitsblatt in Excel mithilfe von Aspose.Cells für .NET. Wenn Sie dynamische, benutzerfreundliche Tabellen erstellen möchten, hilft Ihnen diese Anleitung beim Einstieg.
## Voraussetzungen
Bevor wir uns in den Code vertiefen, stellen wir sicher, dass Sie alles haben, was Sie brauchen:
- Aspose.Cells für .NET: Laden Sie die Aspose.Cells für .NET-Bibliothek herunter und installieren Sie sie von der[Download-Seite](https://releases.aspose.com/cells/net/).
- .NET Framework: Stellen Sie sicher, dass .NET Framework auf Ihrem Computer installiert ist. Jede von Aspose.Cells unterstützte Version funktioniert.
- Entwicklungsumgebung: Verwenden Sie eine IDE wie Visual Studio, um Ihr Projekt zu verwalten und Code zu schreiben.
-  Aspose-Lizenz: Sie können im Testmodus ohne Lizenz arbeiten, für die Vollversion müssen Sie jedoch eine Lizenz beantragen. Besorgen Sie sich eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/) falls erforderlich.
## Pakete importieren
Um zu beginnen, müssen Sie die erforderlichen Namespaces in Ihr Projekt importieren. Folgendes benötigen Sie:
```csharp
using System.IO;
using Aspose.Cells;
```
Diese sind für die Interaktion mit Excel-Dateien und die Bearbeitung von Formularelementen wie Kombinationsfeldern in der Arbeitsmappe von entscheidender Bedeutung.
Lassen Sie uns den Vorgang des Hinzufügens eines Kombinationsfelds zum leichteren Verständnis in mehrere einfache Schritte aufteilen.
## Schritt 1: Einrichten des Dokumentverzeichnisses
Der erste Schritt besteht darin, ein Verzeichnis zu erstellen, in dem Ihre Excel-Dateien gespeichert werden. Sie können einen neuen Ordner erstellen, falls dieser noch nicht vorhanden ist.
```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Gibt den Speicherort an, an dem die Ausgabedatei gespeichert wird.
- System.IO.Directory.Exists: Überprüft, ob das Verzeichnis bereits existiert.
- System.IO.Directory.CreateDirectory: Erstellt das Verzeichnis, falls es fehlt.
## Schritt 2: Erstellen Sie eine neue Arbeitsmappe
Erstellen Sie jetzt eine neue Excel-Arbeitsmappe, in die Sie das Kombinationsfeld hinzufügen.

```csharp
// Erstellen Sie eine neue Arbeitsmappe.
Workbook workbook = new Workbook();
```

- Arbeitsmappe Arbeitsmappe: Initialisiert eine neue Instanz der Arbeitsmappenklasse, die eine Excel-Datei darstellt.
## Schritt 3: Holen Sie sich das Arbeitsblatt und die Zellen
Greifen Sie als Nächstes auf das erste Arbeitsblatt der Arbeitsmappe zu und rufen Sie die Zellensammlung ab, in die Sie die Daten eingeben werden.

```csharp
// Holen Sie sich das erste Arbeitsblatt.
Worksheet sheet = workbook.Worksheets[0];
// Holen Sie sich die Arbeitsblattzellensammlung.
Cells cells = sheet.Cells;
```

- Arbeitsblatt: Holt das erste Arbeitsblatt aus der Arbeitsmappe.
- Zellen: Ruft die Sammlung von Zellen aus dem Arbeitsblatt ab.
## Schritt 4: Werte für Kombinationsfeld eingeben
Jetzt müssen wir einige Werte in die Zellen eingeben. Diese Werte dienen als Optionen für das Kombinationsfeld.

```csharp
// Geben Sie einen Wert ein.
cells["B3"].PutValue("Employee:");
// Markieren Sie es fett.
cells["B3"].GetStyle().Font.IsBold = true;
// Geben Sie einige Werte ein, die den Eingabebereich für das Kombinationsfeld bezeichnen.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- Zellen["B3"].PutValue: Platziert die Bezeichnung "Mitarbeiter" in Zelle B3.
- Font.IsBold = true: Stellt den Text fett dar, damit er hervorsticht.
- Eingabebereich: Gibt mehrere Mitarbeiter-IDs in die Zellen A2 bis A7 ein. Diese werden in der Dropdown-Liste der Combobox angezeigt.
## Schritt 5: Hinzufügen des Kombinationsfelds zum Arbeitsblatt
Der nächste Schritt besteht darin, Ihrem Arbeitsblatt das Kombinationsfeld-Steuerelement hinzuzufügen. Mit diesem Kombinationsfeld können Benutzer eine der zuvor eingegebenen Mitarbeiter-IDs auswählen.

```csharp
// Fügen Sie ein neues Kombinationsfeld hinzu.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Fügt dem Arbeitsblatt ein neues Kombinationsfeld hinzu. Die Zahlen (2, 0, 2, 0, 22, 100) stellen die Position und Abmessungen des Kombinationsfelds dar.
## Schritt 6: Verknüpfen Sie das Kombinationsfeld mit einer Zelle und legen Sie den Eingabebereich fest
Damit das Kombinationsfeld funktionsfähig ist, müssen wir es mit einer bestimmten Zelle verknüpfen und den Zellbereich definieren, aus dem es seine Optionen bezieht.

```csharp
// Legen Sie die verknüpfte Zelle fest.
comboBox.LinkedCell = "A1";
// Stellen Sie den Eingabebereich ein.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Verknüpft die Auswahl der Combobox mit Zelle A1. Der ausgewählte Wert aus der Combobox wird in dieser Zelle angezeigt.
- InputRange: Definiert den Zellbereich (A2:A7), der die Werte enthält, die die Kombinationsfeldoptionen füllen.
## Schritt 7: Anpassen des Erscheinungsbilds des Kombinationsfelds
Sie können das Kombinationsfeld weiter anpassen, indem Sie die Anzahl der Dropdown-Zeilen angeben und die 3D-Schattierung für eine bessere Ästhetik aktivieren.

```csharp
// Legen Sie die Anzahl der Listenzeilen fest, die im Listenabschnitt der Kombinationsbox angezeigt werden.
comboBox.DropDownLines = 5;
// Stellen Sie die Kombinationsbox mit 3D-Schattierung ein.
comboBox.Shadow = true;
```

- DropDownLines: Steuert, wie viele Optionen gleichzeitig im Dropdown-Kombinationsfeld angezeigt werden.
- Schatten: Fügt dem Kombinationsfeld einen 3D-Schattierungseffekt hinzu.
## Schritt 8: Spalten automatisch anpassen und Arbeitsmappe speichern
Zum Schluss passen wir die Spalten automatisch an, um ein übersichtliches Layout zu erhalten, und speichern die Arbeitsmappe.

```csharp
// Spalten automatisch anpassen
sheet.AutoFitColumns();
// Speichert die Datei.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Passt die Spaltenbreiten automatisch an den Inhalt an.
- Speichern: Speichert die Arbeitsmappe als Excel-Datei im angegebenen Verzeichnis.

## Abschluss
Das Hinzufügen eines Kombinationsfelds zu Ihren Excel-Arbeitsblättern mit Aspose.Cells für .NET ist ein unkomplizierter Vorgang, der die Flexibilität bei der Dateneingabe erheblich verbessert. Durch die programmgesteuerte Erstellung von Formularsteuerelementen können Sie ganz einfach interaktive Tabellen erstellen. In diesem Tutorial wurde Ihnen gezeigt, wie Sie ein Kombinationsfeld hinzufügen, es mit einer Zelle verknüpfen und seinen Eingabebereich konfigurieren – alles mit Aspose.Cells.
 Aspose.Cells bietet eine große Auswahl an Funktionen für die Bearbeitung von Excel-Dateien und ist damit die ideale Wahl für Entwickler, die Tabellenkalkulationsaufgaben automatisieren möchten. Probieren Sie es aus mit einem[Kostenlose Testversion](https://releases.aspose.com/).
## Häufig gestellte Fragen
### Kann ich Aspose.Cells verwenden, ohne dass Excel installiert ist?
Ja, Aspose.Cells funktioniert unabhängig von Excel und erfordert keine Installation von Excel.
### Wie wende ich eine Lizenz in Aspose.Cells an?
 Sie können eine Lizenz beantragen, indem Sie sie von[Hier](https://purchase.aspose.com/buy) und ruft`License.SetLicense()` in Ihrem Code.
### Welche Formate unterstützt Aspose.Cells zum Speichern von Dateien?
Aspose.Cells unterstützt das Speichern von Dateien in mehreren Formaten wie XLSX, XLS, CSV, PDF und mehr.
### Gibt es eine Begrenzung für die Anzahl der Kombinationsfelder, die ich hinzufügen kann?
Nein, es gibt keine strikte Begrenzung. Sie können so viele Kombinationsfelder hinzufügen, wie Ihr Projekt erfordert.
### Wie erhalte ich Unterstützung für Aspose.Cells?
 Unterstützung erhalten Sie vom[Aspose-Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
