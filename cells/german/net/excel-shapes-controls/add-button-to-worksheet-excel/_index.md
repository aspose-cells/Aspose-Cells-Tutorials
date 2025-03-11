---
title: Hinzufügen einer Schaltfläche zum Arbeitsblatt in Excel
linktitle: Hinzufügen einer Schaltfläche zum Arbeitsblatt in Excel
second_title: Aspose.Cells .NET Excel-Verarbeitungs-API
description: Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET einem Excel-Arbeitsblatt eine Schaltfläche hinzufügen. Verbessern Sie Excel-Tabellen mit interaktiven Schaltflächen.
weight: 12
url: /de/net/excel-shapes-controls/add-button-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hinzufügen einer Schaltfläche zum Arbeitsblatt in Excel

## Einführung
Excel-Tabellen sind vielseitig und werden häufig zur Verwaltung von Daten verwendet, aber manchmal benötigen sie zusätzliche Interaktivität. Eine der besten Möglichkeiten, die Benutzererfahrung zu verbessern, besteht darin, einem Arbeitsblatt Schaltflächen hinzuzufügen. Diese Schaltflächen können Makros auslösen oder Benutzer zu hilfreichen Links führen. Wenn Sie ein .NET-Entwickler sind, der mit Excel-Dateien arbeitet, bietet Aspose.Cells für .NET eine einfache Möglichkeit, Excel-Arbeitsmappen programmgesteuert zu bearbeiten, einschließlich des Hinzufügens von Schaltflächen.
In diesem Tutorial führen wir Sie durch den Vorgang zum Hinzufügen einer Schaltfläche zu einem Arbeitsblatt in Excel mithilfe von Aspose.Cells für .NET. Wir behandeln jedes Detail, von der Einrichtung der Voraussetzungen bis hin zu schrittweisen Anweisungen. Tauchen wir ein!
## Voraussetzungen
Bevor Sie diesem Tutorial folgen können, stellen Sie sicher, dass Sie die folgenden Tools und Pakete installiert haben:
-  Aspose.Cells für .NET-Bibliothek: Sie können es herunterladen von[Hier](https://releases.aspose.com/cells/net/).
- .NET-Entwicklungsumgebung: Stellen Sie sicher, dass Sie eine funktionierende .NET-Umgebung wie Visual Studio installiert haben.
- Grundlegende Kenntnisse in C#: Sie sollten mit den Grundlagen der C#-Programmierung vertraut sein.
-  Lizenz: Sie benötigen eine gültige Lizenz. Wenn Sie keine haben, können Sie eine[Kostenlose Testversion](https://releases.aspose.com/) oder bewerben Sie sich für eine[vorläufige Lizenz](https://purchase.aspose.com/temporary-license/).
Fahren wir mit dem Importieren der erforderlichen Pakete fort.
## Pakete importieren
Bevor Sie mit dem Codieren beginnen, müssen Sie die erforderlichen Pakete in Ihr .NET-Projekt importieren. Hier ist ein einfacher Codeausschnitt, der Ihnen beim Importieren von Aspose.Cells in Ihr Projekt hilft:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
Nachdem wir nun die erforderlichen Pakete importiert haben, zerlegen wir das Beispiel in eine detaillierte Schritt-für-Schritt-Anleitung.
## Schritt 1: Einrichten der Arbeitsmappe und des Arbeitsblatts
In diesem ersten Schritt erstellen wir eine neue Excel-Arbeitsmappe und erhalten einen Verweis auf das erste Arbeitsblatt.
```csharp
// Definieren Sie den Pfad zu Ihrem Dokumentverzeichnis.
string dataDir = "Your Document Directory";
// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Erstellen Sie eine neue Arbeitsmappe.
Workbook workbook = new Workbook();
// Holen Sie sich das erste Arbeitsblatt aus der Arbeitsmappe.
Worksheet sheet = workbook.Worksheets[0];
```

-  Arbeitsmappenerstellung: Wir beginnen mit der Erstellung einer neuen`Workbook` Objekt, das eine Excel-Datei darstellt.
-  Arbeitsblattreferenz: Die`Worksheets[0]` Der Befehl ruft das erste Arbeitsblatt in der Arbeitsmappe ab, das wir ändern werden.
Dieser Schritt legt die Grundlage, indem eine leere Excel-Datei mit einem einzelnen Arbeitsblatt erstellt wird.
## Schritt 2: Dem Arbeitsblatt eine Schaltfläche hinzufügen
Als Nächstes fügen wir dem Arbeitsblatt eine Schaltfläche hinzu. Hier geschieht die Magie!
```csharp
// Fügen Sie dem Arbeitsblatt eine neue Schaltfläche hinzu.
Aspose.Cells.Drawing.Button button = sheet.Shapes.AddButton(2, 0, 2, 0, 28, 80);
```

- AddButton-Methode: Diese Methode fügt an einer bestimmten Stelle im Arbeitsblatt eine Schaltfläche hinzu. Die Parameter definieren die Position (Zeile, Spalte, X-Offset, Y-Offset) und Größe (Höhe, Breite) der Schaltfläche.
- Zeile und Spalte: Die Schaltfläche wird ohne zusätzlichen Versatz in Zeile 2 und Spalte 0 platziert.
- Größe: Die Höhe des Buttons wird auf 28 und die Breite auf 80 eingestellt.
Mit diesem Schritt wird dem Arbeitsblatt erfolgreich eine Schaltfläche hinzugefügt. Aber wir sind noch nicht fertig. Lassen Sie uns die Schaltfläche nun anpassen.
## Schritt 3: Schaltflächeneigenschaften festlegen
Jetzt ist es an der Zeit, das Erscheinungsbild der Schaltfläche anzupassen, indem Sie Text, Schriftart und Platzierung festlegen.
```csharp
// Legen Sie die Beschriftung der Schaltfläche fest.
button.Text = "Aspose";
// Legen Sie den Platzierungstyp fest, also die Art und Weise, wie die Schaltfläche an die Zellen angehängt wird.
button.Placement = PlacementType.FreeFloating;
```

- Text: Wir haben die Beschriftung der Schaltfläche auf „Aspose“ gesetzt.
-  Platzierung: Wir definieren, wie die Schaltfläche relativ zu den Arbeitsblattzellen positioniert wird.`FreeFloating` ermöglicht die Bewegung der Schaltfläche unabhängig von den Zellen.
Dieser Schritt personalisiert die Beschriftung und Platzierung der Schaltfläche.
## Schritt 4: Passen Sie die Schriftart der Schaltfläche an
Verleihen wir der Schaltfläche etwas Flair, indem wir die Schrifteigenschaften anpassen.
```csharp
// Legen Sie den Schriftnamen fest.
button.Font.Name = "Tahoma";
// Legen Sie fest, wie die Beschriftung fett dargestellt wird.
button.Font.IsBold = true;
// Stellen Sie die Farbe auf Blau ein.
button.Font.Color = Color.Blue;
```

- Schriftartname: Wir ändern die Schriftart in „Tahoma“, eine klare und moderne Schriftart.
- Fett: Wir machen den Buttontext zur Hervorhebung fett.
- Farbe: Die Schriftfarbe ist auf Blau eingestellt, wodurch der Buttontext hervorsticht.
Dieser Schritt verbessert das Erscheinungsbild des Buttons und stellt sicher, dass er sowohl funktional als auch optisch ansprechend ist.
## Schritt 5: Fügen Sie der Schaltfläche einen Hyperlink hinzu
Sie können die Schaltfläche noch nützlicher machen, indem Sie einen Hyperlink hinzufügen.
```csharp
// Legen Sie den Hyperlink für die Schaltfläche fest.
button.AddHyperlink("https://www.aspose.com/");
```

- AddHyperlink: Wir verwenden diese Methode, um der Schaltfläche einen anklickbaren Hyperlink hinzuzufügen. Wenn Sie darauf klicken, navigiert die Schaltfläche zur Aspose-Website.
Dieser Schritt macht die Schaltfläche interaktiv und verleiht ihr über die reine Ästhetik hinaus eine Funktionalität.
## Schritt 6: Speichern Sie die Excel-Datei
Vergessen Sie nicht, Ihre Änderungen zu speichern, wenn alles eingerichtet ist!
```csharp
// Speichert die Datei.
workbook.Save(dataDir + "book1.out.xls");
```

-  Speichermethode: Wir verwenden die`Save` Methode, um die geänderte Arbeitsmappe in eine neue Datei zu schreiben. Die Datei wird im angegebenen Verzeichnis gespeichert.
Herzlichen Glückwunsch! Sie haben jetzt einem Excel-Arbeitsblatt eine vollständig angepasste Schaltfläche hinzugefügt.
## Abschluss
Durch das Hinzufügen von Schaltflächen zu Excel-Arbeitsblättern können Sie die Funktionalität Ihrer Tabellen erheblich verbessern und sie interaktiver und benutzerfreundlicher gestalten. Mit Aspose.Cells für .NET können Sie dies mit nur wenigen Codezeilen erreichen, wie wir in diesem Tutorial gezeigt haben.
Aspose.Cells für .NET ist eine leistungsstarke Bibliothek, die endlose Möglichkeiten zur Excel-Manipulation bietet. Egal, ob Sie Aufgaben automatisieren oder Ihren Tabellenkalkulationen neue Funktionen hinzufügen, diese Bibliothek ist Ihre Lösung.
 Falls Sie es noch nicht getan haben,[Laden Sie die Aspose.Cells für .NET-Bibliothek herunter](https://releases.aspose.com/cells/net/) und beginnen Sie mit der Optimierung Ihrer Excel-Dateien.
## Häufig gestellte Fragen
### Kann ich in Aspose.Cells für .NET außer Schaltflächen auch andere Formen verwenden?
Ja, mit Aspose.Cells können Sie verschiedene Formen hinzufügen, darunter Kontrollkästchen, Optionsfelder und mehr.
### Kann ich ein Makro von einer Schaltfläche aus auslösen, die über Aspose.Cells hinzugefügt wurde?
Ja, Sie können die Schaltfläche mit einem Makro verknüpfen. Allerdings müssen Sie den Makrocode in Excel separat verarbeiten.
### Wie kann ich die Größe der Schaltfläche automatisch mit den Zellen anpassen?
 Verwenden Sie die`PlacementType.Move` -Eigenschaft, um die Größenanpassung der Schaltfläche an die Zellen zu ermöglichen.
### Ist es möglich, einem einzelnen Arbeitsblatt mehrere Schaltflächen hinzuzufügen?
 Auf jeden Fall! Sie können so viele Schaltflächen hinzufügen, wie Sie benötigen, indem Sie den`AddButton` Methode mehrmals.
### Kann ich das Erscheinungsbild der Schaltfläche weiter anpassen?
Ja, Sie können viele Eigenschaften ändern, einschließlich der Hintergrundfarbe, des Rahmenstils und mehr.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
