---
title: Benutzern das Bearbeiten von Bereichen im Excel-Arbeitsblatt gestatten
linktitle: Benutzern das Bearbeiten von Bereichen im Excel-Arbeitsblatt gestatten
second_title: Aspose.Cells für .NET API-Referenz
description: Ermöglichen Sie Benutzern, bestimmte Bereiche in einer Excel-Tabelle mit Aspose.Cells für .NET zu bearbeiten. Schritt-für-Schritt-Anleitung mit Quellcode in C#.
weight: 10
url: /de/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Benutzern das Bearbeiten von Bereichen im Excel-Arbeitsblatt gestatten

## Einführung

Beim Arbeiten mit Excel-Arbeitsblättern ist Flexibilität oft entscheidend – insbesondere, wenn mehrere Benutzer Zugriff benötigen, um bestimmte Bereiche zu bearbeiten, ohne die Datenintegrität des gesamten Blatts zu beeinträchtigen. Hier glänzt Aspose.Cells für .NET! In diesem Tutorial werden wir uns damit befassen, wie Benutzer bestimmte Bereiche in einem Excel-Arbeitsblatt bearbeiten können, während der Rest des Dokuments geschützt bleibt. Am Ende dieses Artikels werden Sie nicht nur die Konzepte verstehen, sondern auch ein konkretes Beispiel haben, mit dem Sie arbeiten können. 

## Voraussetzungen

Bevor wir ins Detail gehen, stellen wir sicher, dass Sie alles haben, was Sie für den Einstieg brauchen:

1. .NET-Entwicklungsumgebung: Sie sollten eine funktionierende .NET-Entwicklungsumgebung eingerichtet haben (dies kann Visual Studio oder eine andere IDE Ihrer Wahl sein).
2.  Aspose.Cells für .NET-Bibliothek: Laden Sie die Aspose.Cells-Bibliothek herunter und installieren Sie sie. Sie finden sie[Hier](https://releases.aspose.com/cells/net/).
3. Grundkenntnisse in C#: Wenn Sie mit der C#-Programmierung vertraut sind, können Sie problemlos durch die Codebeispiele navigieren.
4. Die Grundlagen von Excel verstehen: Wenn Sie wissen, wie Excel funktioniert, bilden Sie die Grundlage für die Funktionen, die wir besprechen werden.

Sobald diese Voraussetzungen erfüllt sind, kann es losgehen!

## Pakete importieren

Bevor wir mit dem Programmieren beginnen, müssen wir sicherstellen, dass unser Projekt den Aspose.Cells-Namespace erkennt. So importieren Sie die erforderlichen Pakete:

```csharp
using System.IO;
using Aspose.Cells;
```

Nachdem wir nun alles importiert haben, was wir brauchen, können wir uns Schritt für Schritt in unser Tutorial stürzen.

## Schritt 1: Einrichten des Dokumentverzeichnisses

Für alle Dateivorgänge ist es wichtig, einen definierten Speicherort für unsere Dokumente zu haben. Richten wir unser Arbeitsverzeichnis zum Speichern der Excel-Dateien ein.

```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Ersetzen Sie zunächst`"YOUR DOCUMENT DIRECTORY"` mit dem Pfad, in dem Ihre Dateien gespeichert werden sollen. Dieser Code prüft, ob das Verzeichnis existiert. Wenn nicht, wird eines erstellt.

## Schritt 2: Instanziieren einer neuen Arbeitsmappe

Nachdem unser Arbeitsverzeichnis bereit ist, ist es Zeit, unsere Excel-Arbeitsmappe zu erstellen. 

```csharp
// Instanziieren einer neuen Arbeitsmappe
Workbook book = new Workbook();
```

 Hier erstellen wir eine neue Instanz des`Workbook` Von Aspose.Cells bereitgestellte Klasse, die es uns ermöglicht, die Excel-Datei zu bearbeiten.

## Schritt 3: Zugriff auf das Standardarbeitsblatt

Jede neu erstellte Arbeitsmappe enthält mindestens ein Arbeitsblatt. Greifen wir darauf zu.

```csharp
// Holen Sie sich das erste (Standard-)Arbeitsblatt
Worksheet sheet = book.Worksheets[0];
```

In diesem Codeausschnitt greifen wir auf das erste Arbeitsblatt unserer Arbeitsmappe zu, das wir in den folgenden Schritten bearbeiten werden.

## Schritt 4: Bereiche zum Bearbeiten zulassen abrufen

 Um bestimmte Bereiche des Arbeitsblatts für die Bearbeitung freizugeben, müssen wir auf die`AllowEditRanges` Eigentum.

```csharp
// Holen Sie sich die zulässigen Bearbeitungsbereiche
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

Mit dieser Sammlung können wir verwalten, welche Bereiche in unserem Arbeitsblatt bearbeitet werden können.

## Schritt 5: Definieren Sie den geschützten Bereich

Als Nächstes definieren wir, welchen Teil des Arbeitsblatts wir schützen möchten, während wir Änderungen an einem angegebenen Bereich zulassen möchten.

```csharp
// Definieren Sie ProtectedRange
ProtectedRange proteced_range;

// Erstellen Sie den Bereich
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// Geben Sie das Kennwort an
proteced_range.Password = "123";
```

In diesem Schritt fügen wir einen neuen bearbeitbaren Bereich namens „r2“ hinzu, der Änderungen in den Zellen von Zeile 1, Spalte 1 bis Zeile 3, Spalte 3 ermöglicht. Zusätzlich legen wir ein Kennwort fest, um diesen Bereich zu schützen und sicherzustellen, dass nur autorisierte Benutzer ihn ändern können.

## Schritt 6: Schützen Sie das Arbeitsblatt

Nachdem wir nun unseren bearbeitbaren Bereich eingerichtet haben, müssen wir das Arbeitsblatt schützen.

```csharp
// Schützen Sie das Blatt
sheet.Protect(ProtectionType.All);
```

Dieser Code schützt das gesamte Arbeitsblatt vor unerwünschten Änderungen, mit Ausnahme des gerade angegebenen Bereichs.

## Schritt 7: Speichern Sie die Excel-Datei

Speichern wir die Arbeitsmappe, damit wir unsere Änderungen in einer Excel-Datei sehen können.

```csharp
// Speichern Sie die Excel-Datei
book.Save(dataDir + "protectedrange.out.xls");
```

Denken Sie daran, den Dateinamen nach Bedarf anzupassen. Dadurch wird eine Excel-Datei mit den von uns konfigurierten Einstellungen in Ihrem angegebenen Verzeichnis erstellt.

## Abschluss

Da haben Sie es! Sie haben erfolgreich ein Excel-Arbeitsblatt erstellt, das Änderungen auf einen bestimmten Bereich beschränkt und gleichzeitig den Rest des Blattes schützt. Die Verwendung von Aspose.Cells für .NET macht die Verwaltung dieser Art von Aufgaben viel einfacher und effizienter. Egal, ob Sie eine komplexe Anwendung entwickeln oder nur Daten sicher verwalten müssen, diese Funktionen können Ihren Arbeitsablauf erheblich verbessern.

## Häufig gestellte Fragen

### Was ist Aspose.Cells?
Aspose.Cells ist eine leistungsstarke .NET-Bibliothek zur Verarbeitung von Excel-Dateien und bietet Funktionen wie das programmgesteuerte Erstellen, Bearbeiten und Konvertieren von Tabellen.

### Kann ich mehrere bearbeitbare Bereiche anwenden?
 Absolut! Sie können anrufen unter`Add` Methode auf der`allowRanges` Sammlung mehrmals, um mehrere bearbeitbare Bereiche anzugeben.

### Was passiert, wenn ich das Passwort vergesse?
Wenn Sie das Kennwort für einen bearbeitbaren Bereich vergessen, müssen Sie leider den Schutz entfernen oder auf eine vordefinierte Weise auf die Datei zugreifen, wofür möglicherweise Anmeldeinformationen erforderlich sind.

### Gibt es eine kostenlose Version von Aspose.Cells?
Ja, Aspose bietet eine kostenlose Testversion an, mit der Sie die Funktionen vor dem Kauf erkunden können.

### Wo finde ich weitere Informationen zu Aspose.Cells?
 Sie können die[Dokumentation](https://reference.aspose.com/cells/net/)für detaillierte Anleitungen und Referenzen.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
