---
"description": "Erfahren Sie in diesem Schritt-für-Schritt-Tutorial, wie Sie mit Aspose.Cells für .NET Zellen in einem benannten Bereich zusammenführen. Erfahren Sie, wie Sie Excel-Berichte formatieren, gestalten und automatisieren."
"linktitle": "Zellen in benannten Bereichen in Excel zusammenführen"
"second_title": "Aspose.Cells .NET Excel-Verarbeitungs-API"
"title": "Zellen in benannten Bereichen in Excel zusammenführen"
"url": "/de/net/excel-advanced-named-ranges/merge-cells-in-named-range/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Zellen in benannten Bereichen in Excel zusammenführen

## Einführung

Beim programmgesteuerten Arbeiten mit Excel-Dateien ist das Zusammenführen von Zellen innerhalb eines benannten Bereichs eine der häufigsten Aufgaben. Ob Sie die Berichterstellung automatisieren, Dashboards erstellen oder einfach große Datensätze verwalten – das Zusammenführen von Zellen ist eine wichtige Technik. In diesem Tutorial erfahren Sie, wie Sie Zellen in einem benannten Bereich mit Aspose.Cells für .NET zusammenführen – einer leistungsstarken Bibliothek, die es Entwicklern ermöglicht, Excel-Dateien zu bearbeiten, ohne Microsoft Excel installieren zu müssen.

## Voraussetzungen

Bevor wir beginnen, stellen Sie sicher, dass Sie Folgendes bereit haben:

- Aspose.Cells für .NET: Sie können es herunterladen von der [Aspose.Cells-Releaseseite](https://releases.aspose.com/cells/net/).
- .NET Framework auf Ihrem Computer installiert.
- Grundlegende Kenntnisse in C#: Vertrautheit mit Konzepten wie Klassen, Methoden und Objekten ist hilfreich.

## Pakete importieren

Bevor wir mit dem Programmieren beginnen, müssen Sie die erforderlichen Namespaces importieren. Diese Namespaces ermöglichen Ihnen den Zugriff auf die Funktionalität der Aspose.Cells-Bibliothek.

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

Nachdem wir die Voraussetzungen und Pakete geklärt haben, kommen wir zum spaßigen Teil: dem Programmieren!

Hier finden Sie eine Aufschlüsselung, wie Sie mit Aspose.Cells für .NET Zellen in einem benannten Bereich in einem Excel-Blatt zusammenführen können.

## Schritt 1: Erstellen Sie eine neue Arbeitsmappe

Als Erstes benötigen wir eine Arbeitsmappe. Eine Arbeitsmappe entspricht in Excel einer Excel-Datei. Erstellen wir eine.

```csharp
// Instanziieren Sie eine neue Arbeitsmappe.
Workbook wb1 = new Workbook();
```

Durch die Initialisierung einer neuen Arbeitsmappe verfügen wir nun über eine leere Excel-Datei, die bearbeitet werden kann. Es ist, als würden Sie mit einer leeren Leinwand beginnen!

## Schritt 2: Zugriff auf das erste Arbeitsblatt

Jede Arbeitsmappe enthält Arbeitsblätter. In diesem Fall möchten wir mit dem ersten arbeiten. Schnappen wir es uns!

```csharp
// Holen Sie sich das erste Arbeitsblatt in der Arbeitsmappe.
Worksheet worksheet1 = wb1.Worksheets[0];
```

Stellen Sie sich das Arbeitsblatt als die einzelnen Registerkarten in einer Excel-Datei vor, in denen die eigentlichen Daten gespeichert sind. Standardmäßig greifen wir auf die allererste Registerkarte zu.

## Schritt 3: Erstellen Sie einen Zellbereich

Nachdem wir nun unser Arbeitsblatt erstellt haben, ist es an der Zeit, einen Bereich zu erstellen. Ein Bereich bezeichnet einen Zellblock, der sich über mehrere Zeilen und Spalten erstrecken kann.

```csharp
// Erstellen Sie einen Bereich.
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

Hier wählen wir die Zellen von D6 bis I12 aus – einen Block, der mehrere Zeilen und Spalten umfasst. Wir werden diesen Bereich bald zusammenführen!

## Schritt 4: Benennen Sie den Bereich

Durch die Benennung eines Bereichs können Sie später leichter darauf verweisen, insbesondere bei großen Datensätzen.

```csharp
// Benennen Sie den Bereich.
mrange.Name = "TestRange";
```

Indem wir diesen Bereich „TestRange“ nennen, können wir ihn später im Code schnell abrufen, ohne die Zellkoordinaten erneut angeben zu müssen.

## Schritt 5: Den Zellbereich zusammenführen

Und jetzt kommt die Magie: das Zusammenführen der Zellen innerhalb des Bereichs, den wir gerade erstellt haben!

```csharp
// Fügt die Zellen des Bereichs zusammen.
mrange.Merge();
```

Dieser Schritt führt alle Zellen von D6 bis I12 zu einer einzigen Zelle zusammen. Perfekt für Dinge wie Titel oder Zusammenfassungen!

## Schritt 6: Abrufen des benannten Bereichs

Sobald die Zellen zusammengeführt sind, können wir sie formatieren. Rufen wir zunächst unseren benannten Bereich ab.

```csharp
// Holen Sie sich die Reichweite.
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

Durch das Abrufen des Bereichs nach Namen können wir weitere Vorgänge ausführen, z. B. Stile hinzufügen oder Daten eingeben.

## Schritt 7: Definieren Sie einen Stil für die verbundenen Zellen

Was nützt eine verbundene Zelle, wenn sie nicht ansprechend aussieht? Erstellen wir ein Stilobjekt, um den Text auszurichten und eine Hintergrundfarbe anzuwenden.

```csharp
// Definieren Sie ein Stilobjekt.
Style style = wb1.CreateStyle();

// Legen Sie die Ausrichtung fest.
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

Hier richten wir den Text horizontal und vertikal zentriert aus und legen eine hellblaue (Aqua) Hintergrundfarbe fest. Stilvoll, oder?

## Schritt 8: Den Stil auf den Bereich anwenden

Nachdem Sie den Stil definiert haben, ist es an der Zeit, ihn auf den zusammengeführte Bereich anzuwenden.

```csharp
// Erstellen Sie ein StyleFlag-Objekt.
StyleFlag flag = new StyleFlag();

// Aktivieren Sie das relative Stilattribut.
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

// Wenden Sie den Stil auf den Bereich an.
range1.ApplyStyle(style, flag);
```

Der `StyleFlag` teilt Aspose.Cells mit, welche Stileigenschaften angewendet werden sollen – Ausrichtung, Schattierung usw. Dadurch haben Sie eine detaillierte Kontrolle darüber, wie der Stil angewendet wird.

## Schritt 9: Daten in den zusammengeführten Bereich eingeben

Was ist ein formatierter Bereich ohne Inhalt? Fügen wir etwas Text hinzu.

```csharp
// Geben Sie Daten in den Bereich ein.
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

Dadurch wird der Text „Willkommen bei Aspose APIs“ in die erste Zelle unseres zusammengeführten Bereichs eingefügt. Durch die Zusammenführung der Zelle erstreckt sich dieser Text über alle Zellen von D6 bis I12.

## Schritt 10: Speichern Sie die Excel-Datei

Abschließend speichern wir die Arbeitsmappe als Excel-Datei.

```csharp
// Speichern Sie die Excel-Datei.
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

Dabei wird die Arbeitsmappe unter dem Namen „outputMergeCellsInNamedRange.xlsx“ in Ihrem angegebenen Verzeichnis gespeichert.

## Abschluss

Und da haben Sie es! Sie haben erfolgreich Zellen in einem benannten Bereich zusammengeführt, ansprechend formatiert und sogar Daten eingegeben – alles mit Aspose.Cells für .NET. Egal, ob Sie Berichte automatisieren, Excel-Dateien bearbeiten oder einfach neue Techniken erlernen möchten – diese Schritt-für-Schritt-Anleitung bietet Ihnen die nötigen Grundlagen.

## Häufig gestellte Fragen

### Kann ich mehrere nicht zusammenhängende Bereiche in Aspose.Cells zusammenführen?  
Nein, Sie können in Aspose.Cells nur zusammenhängende Zellen zusammenführen.

### Kann ich einen Zusammenführungsvorgang programmgesteuert rückgängig machen?  
Sobald Zellen zusammengeführt sind, können Sie die Zusammenführung mit dem `UnMerge()` Methode in Aspose.Cells.

### Werden durch das Zusammenführen von Zellen die darin enthaltenen Daten entfernt?  
Wenn sich vor dem Zusammenführen Daten in den Zellen befinden, bleiben die Daten aus der ersten Zelle des Bereichs erhalten.

### Kann ich auf einzelne Zellen innerhalb eines zusammengeführten Bereichs unterschiedliche Stile anwenden?  
Nein, ein zusammengeführter Bereich verhält sich wie eine einzelne Zelle. Sie können den einzelnen Zellen darin also keine unterschiedlichen Stile zuweisen.

### Wie greife ich nach dem Zusammenführen auf eine zusammengeführte Zelle zu?  
Nach dem Zusammenführen können Sie weiterhin über die Koordinaten der oberen linken Ecke auf die zusammengeführte Zelle zugreifen.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}