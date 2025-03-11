---
title: Bestimmte Zeile im Excel-Arbeitsblatt schützen
linktitle: Bestimmte Zeile im Excel-Arbeitsblatt schützen
second_title: Aspose.Cells für .NET API-Referenz
description: Erfahren Sie, wie Sie mit Aspose.Cells für .NET bestimmte Zeilen in Excel-Arbeitsblättern schützen. Eine Schritt-für-Schritt-Anleitung für Entwickler.
weight: 90
url: /de/net/protect-excel-file/protect-specific-row-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bestimmte Zeile im Excel-Arbeitsblatt schützen

## Einführung

In der heutigen schnelllebigen Welt ist die effektive Verwaltung von Tabellenkalkulationen wichtiger denn je. Microsoft Excel ist in vielen Branchen und Berufen ein unverzichtbares Werkzeug. Da wir diese Dokumente jedoch gemeinsam nutzen, insbesondere in kollaborativen Umgebungen, ist der Schutz bestimmter Informationen in Tabellenkalkulationen von entscheidender Bedeutung. Wie können Sie also eine Zeile in Excel versiegeln, um unerwünschte Änderungen zu verhindern? Wenn Sie mit .NET arbeiten, haben Sie Glück! Aspose.Cells ist eine hervorragende Bibliothek für den programmgesteuerten Umgang mit Excel-Dateien, mit der wir bestimmte Zeilen effizient schützen können.

## Voraussetzungen

Bevor wir beginnen, benötigen Sie einige Dinge:

1. Visual Studio: Stellen Sie sicher, dass Visual Studio auf Ihrem Computer installiert ist. Sie können jede Version verwenden, die .NET-Entwicklung unterstützt.
2.  Aspose.Cells für .NET: Sie müssen die Aspose.Cells-Bibliothek installiert haben. Besuchen Sie[dieser Link zum Download](https://releases.aspose.com/cells/net/) die neueste Version.
3. Grundlegende .NET-Kenntnisse: Vertrautheit mit C# und grundlegenden Programmierkonzepten ist hilfreich, da wir mit Codeausschnitten arbeiten werden.

Sobald Sie alles vorbereitet haben, können wir zur Sache kommen!

## Pakete importieren

Bevor wir unseren Code schreiben, müssen wir die erforderlichen Aspose.Cells-Namespaces importieren. Dadurch wird unsere Anwendung darauf vorbereitet, die von der Aspose.Cells-Bibliothek bereitgestellten Klassen und Methoden zu verwenden. Folgendes müssen Sie tun:

### Richten Sie Ihr Projekt ein

1. Neues Projekt erstellen:
   - Öffnen Sie Visual Studio und erstellen Sie ein neues Konsolenanwendungsprojekt. Dieses Projekt wird unseren Excel-Manipulationscode hosten.

2. Aspose.Cells-Referenz hinzufügen:
   - Klicken Sie im Solution Explorer mit der rechten Maustaste auf das Projekt, gehen Sie zu „NuGet-Pakete verwalten“ und suchen Sie nach „Aspose.Cells“. Klicken Sie, um es zu installieren.

3. Fügen Sie die erforderlichen Namespaces in Ihren Code ein:
```csharp
using System.IO;
using Aspose.Cells;
```

Nachdem wir nun alles eingerichtet haben, schützen wir Schritt für Schritt eine bestimmte Zeile in unserem Excel-Arbeitsblatt. In unserem Beispiel wird die erste Zeile gesperrt, Sie können dies jedoch für jede gewünschte Zeile anpassen.

## Schritt 1: Definieren Sie das Dokumentverzeichnis

Zuerst müssen wir ein Verzeichnis definieren, in dem wir unsere Excel-Datei speichern. So geht's:

```csharp
// Der Pfad zum Dokumentverzeichnis.
string dataDir = "YOUR DOCUMENT DIRECTORY"; // Wechseln Sie zu Ihrem gewünschten Pfad.

// Erstellen Sie ein Verzeichnis, falls es noch nicht vorhanden ist.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

 Ersetzen`"YOUR DOCUMENT DIRECTORY"` durch den tatsächlichen Pfad, in dem Sie Ihre neue Excel-Datei speichern möchten.

## Schritt 2: Erstellen Sie eine neue Arbeitsmappe

Als Nächstes erstellen wir mit Aspose.Cells eine neue Arbeitsmappe. Dies ist Ihre leere Leinwand zum Erstellen einer Tabelle.

```csharp
// Erstellen Sie eine neue Arbeitsmappe.
Workbook wb = new Workbook();
```

## Schritt 3: Erstellen und Zugreifen auf ein Arbeitsblatt

Greifen wir nun auf das erste Arbeitsblatt in unserer Arbeitsmappe zu, um die erforderlichen Änderungen vorzunehmen.

```csharp
// Erstellen Sie ein Arbeitsblattobjekt und rufen Sie das erste Blatt ab.
Worksheet sheet = wb.Worksheets[0];
```

## Schritt 4: Alle Spalten entsperren

Bevor wir eine Zeile sperren, müssen wir sicherstellen, dass alle Spalten entsperrt sind. Dies gibt uns die Flexibilität, nur die gewünschte Zeile zu schützen.

```csharp
// Definieren Sie das Stilobjekt.
Style style;
// Definieren Sie das Styleflag-Objekt.
StyleFlag flag;
// Durchlaufen Sie alle Spalten im Arbeitsblatt und entsperren Sie sie.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false; // Spalte „Entsperren“
    flag = new StyleFlag();
    flag.Locked = true; // Setzen Sie das Flag zum Sperren auf „True“.
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag); // Anwenden des Stils
}
```

## Schritt 5: Die gewünschte Zeile sperren

Jetzt ist es an der Zeit, die Zeile zu sperren, die Sie schützen möchten. In diesem Fall sperren wir die erste Zeile.

```csharp
//Holen Sie sich den Stil der ersten Zeile.
style = sheet.Cells.Rows[0].Style;
// Sperren Sie es.
style.IsLocked = true;
//Instanziieren Sie die Flagge.
flag = new StyleFlag();
// Legen Sie die Sperreinstellung fest.
flag.Locked = true;
// Wenden Sie den Stil auf die erste Zeile an.
sheet.Cells.ApplyRowStyle(0, style, flag);
```

## Schritt 6: Schützen Sie das Arbeitsblatt

Nachdem wir die gewünschte Zeile gesperrt haben, müssen wir den Schutz für das Arbeitsblatt aktivieren. Und hier geschieht die Magie!

```csharp
// Schützen Sie das Blatt.
sheet.Protect(ProtectionType.All);
```

## Schritt 7: Speichern Sie die Arbeitsmappe

Schließlich ist es an der Zeit, Ihre neue Excel-Datei zu speichern. Sie können das gewünschte Format für Ihre Excel-Datei auswählen.

```csharp
// Speichern Sie die Excel-Datei.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```

## Abschluss

Und da haben Sie es! Sie haben erfolgreich eine bestimmte Zeile in einem Excel-Arbeitsblatt mit Aspose.Cells für .NET geschützt. Diese Funktion ist unglaublich nützlich für Entwickler und Benutzer, die die Datenintegrität sicherstellen müssen, während sie ihre Excel-Dateien weiterhin freigeben. Jetzt können Sie Ihre Tabellenblätter vertrauensvoll freigeben und gleichzeitig wichtige Informationen darin schützen.

## Häufig gestellte Fragen

### Kann ich mehrere Zeilen mit derselben Methode schützen?  
Ja, Sie können den Sperrvorgang für alle weiteren Zeilen auf die gleiche Weise wiederholen wie für die erste Zeile.

### Was ist, wenn ich bestimmte Zellen statt Zeilen schützen und entsperren möchte?  
Sie können Zellen einzeln auswählen und Sperrstile anwenden, ähnlich wie Sie eine Zeile sperren.

### Ist die Nutzung von Aspose.Cells kostenlos?  
 Aspose.Cells ist ein kommerzielles Produkt, aber Sie können es mit einer kostenlosen Testversion ausprobieren[Hier](https://releases.aspose.com/).

### Benötige ich eine Internetverbindung, um Aspose.Cells zu verwenden?  
Nein, Aspose.Cells ist eine .NET-Bibliothek und kann nach der Installation offline verwendet werden.

### Wo erhalte ich Support für Aspose.Cells?  
 Für Anfragen oder Unterstützung besuchen Sie bitte die[Aspose-Supportforum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
