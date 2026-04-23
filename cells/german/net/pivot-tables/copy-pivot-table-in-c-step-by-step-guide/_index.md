---
category: general
date: 2026-03-18
description: Pivot‑Tabelle in C# mit Aspose.Cells kopieren. Erfahren Sie, wie Sie
  einen Excel‑Bereich kopieren, eine Excel‑Pivot‑Tabelle duplizieren, einen Bereich
  in ein neues Blatt kopieren und eine Pivot‑Tabelle in ein Blatt kopieren – in wenigen
  Minuten.
draft: false
keywords:
- copy pivot table
- copy excel range
- duplicate excel pivot
- copy range to new
- copy pivot to sheet
language: de
og_description: Pivot‑Tabelle in C# mit Aspose.Cells kopieren. Lernen Sie, ein Excel‑Pivot
  zu duplizieren, einen Excel‑Bereich an einen neuen Ort zu kopieren und das Pivot
  in ein Blatt zu übertragen, mit vollständigen Codebeispielen.
og_title: Pivot‑Tabelle in C# kopieren – Vollständiger Programmierleitfaden
tags:
- Aspose.Cells
- C#
- Excel automation
title: Pivot‑Tabelle in C# kopieren – Schritt‑für‑Schritt‑Anleitung
url: /de/net/pivot-tables/copy-pivot-table-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot-Tabelle in C# kopieren – Vollständiger Programmierleitfaden

Haben Sie jemals eine **Pivot-Tabelle** von einem Teil einer Arbeitsmappe in einen anderen kopieren müssen, waren sich aber nicht sicher, wie das ohne Verlust der zugrunde liegenden Datenverbindungen funktioniert? Sie sind nicht allein. Viele Entwickler stoßen bei der Automatisierung von Excel‑Berichten auf dieses Problem, besonders wenn die Pivot‑Tabelle in einem größeren Datenblock eingebettet ist. Die gute Nachricht? Mit Aspose.Cells können Sie die Pivot‑Tabelle **genau so kopieren, wie sie aussieht**, und Sie lernen außerdem, wie man **Excel‑Bereich kopiert**, **Excel‑Pivot dupliziert** und sogar **Pivot zu Blatt kopiert** mit nur wenigen Zeilen C#.

In diesem Tutorial gehen wir ein reales Szenario durch: Wir verschieben eine Pivot‑Tabelle, die den Bereich *A1:J20* belegt, in einen neuen Bereich *M1:V20* im selben Arbeitsblatt. Am Ende haben Sie ein ausführbares Programm, verstehen, warum jeder Schritt wichtig ist, und wissen, wie Sie den Code für andere Bereiche oder sogar separate Arbeitsblätter anpassen können. Keine externen Dokumente nötig – alles ist hier enthalten.

---

## Voraussetzungen

- **Aspose.Cells for .NET** (Version 23.9 oder höher). Sie können es über NuGet beziehen: `Install-Package Aspose.Cells`.
- Eine grundlegende C#‑Entwicklungsumgebung (Visual Studio 2022, Rider oder VS Code mit der C#‑Erweiterung).
- Eine Excel‑Datei (`source.xlsx`), die eine Pivot‑Tabelle im Bereich *A1:J20* enthält.

Das ist alles. Wenn Sie sich mit der Erstellung einer Konsolenanwendung auskennen, können Sie loslegen.

---

## Wie man Pivot‑Tabellen in Aspose.Cells kopiert

Der Kern der Lösung ist ein einzelner Aufruf von `Worksheet.Cells.CopyRange`. Diese Methode kopiert nicht nur rohe Zellwerte, sondern bewahrt automatisch Pivot‑Tabellen, Diagramme und andere Rich‑Objekte. Lassen Sie uns das aufschlüsseln.

### Schritt 1: Quellarbeitsmappe laden

Zuerst müssen wir die Arbeitsmappe in den Speicher laden.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source workbook from disk
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Warum das wichtig ist:** Das Laden der Arbeitsmappe erzeugt eine In‑Memory‑Repräsentation, die Aspose.Cells manipulieren kann, ohne Excel zu starten. Es ist schnell, thread‑sicher und funktioniert auf Servern.

### Schritt 2: Erstes Arbeitsblatt holen

Die meisten Beispiele verwenden das erste Blatt, aber Sie können jeden Index oder Namen anvisieren.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = sourceWorkbook.Worksheets[0];
```

> **Tipp:** Wenn Sie **Pivot zu Blatt kopieren** statt im selben Blatt, ändern Sie einfach die `worksheet`‑Referenz zu einem anderen `Worksheet`‑Objekt.

### Schritt 3: Quell‑ und Zielbereiche definieren

Wir verwenden `CellArea`‑Strukturen, um die zu verschiebenden Bereiche zu beschreiben.

```csharp
        // Define the source range (A1:J20) that contains the pivot table
        CellArea sourceRange = new CellArea(0, 0, 19, 9);   // rows 0‑19, columns 0‑9

        // Define the target range (M1:V20) where the data will be copied
        CellArea targetRange = new CellArea(0, 12, 19, 21); // rows 0‑19, columns 12‑21
```

> **Erklärung:** Zeilen‑ und Spaltenindizes beginnen bei Null. Spalte 0 = **A**, Spalte 12 = **M** usw. Passen Sie diese Zahlen an, falls Ihre Pivot‑Tabelle an anderer Stelle liegt.

### Schritt 4: Kopiervorgang ausführen

Jetzt geschieht die Magie. Das Setzen des letzten booleschen Parameters auf `true` weist Aspose.Cells an, alle Objekte zu kopieren – einschließlich der Pivot‑Tabelle.

```csharp
        // Copy the source range to the target range; pivot tables are copied automatically
        worksheet.Cells.CopyRange(
            sourceRange.StartRow, sourceRange.StartColumn,
            sourceRange.EndRow, sourceRange.EndColumn,
            targetRange.StartRow, targetRange.StartColumn,
            true);
```

> **Warum `true`?** Das Flag bedeutet „alle Objekte kopieren“. Wenn Sie es auf `false` setzen, werden nur reine Zellwerte verschoben und die Pivot‑Tabelle geht verloren.

### Schritt 5: Arbeitsmappe speichern

Zum Schluss schreiben wir die modifizierte Arbeitsmappe zurück auf die Festplatte.

```csharp
        // Save the workbook with the copied range
        sourceWorkbook.Save(@"YOUR_DIRECTORY\copy-pivot.xlsx");
    }
}
```

> **Ergebnis:** `copy-pivot.xlsx` enthält jetzt die ursprüngliche Pivot‑Tabelle bei *A1:J20* **und** eine identische Kopie bei *M1:V20*. Öffnen Sie die Datei in Excel, um zu überprüfen, dass beide Pivot‑Tabellen funktionsfähig sind und ihre Datenverbindungen behalten.

---

## Excel‑Bereich an einen neuen Ort kopieren – eine schnelle Variante

Manchmal müssen Sie nur **Excel‑Bereich kopieren**, ohne sich um Pivot‑Tabellen zu kümmern. Die gleiche `CopyRange`‑Methode erledigt das; setzen Sie einfach das letzte Argument auf `false`.

```csharp
worksheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    false); // plain values only
```

> **Wann zu verwenden:** Wenn Sie Rohdaten für ein temporäres Berechnungsblatt verschieben, spart das Deaktivieren des Objekt‑Kopierens Speicher und beschleunigt den Vorgang.

---

## Excel‑Pivot über mehrere Blätter duplizieren

Was, wenn Sie **Excel‑Pivot duplizieren** möchten, aber auf einem anderen Arbeitsblatt? Das Muster bleibt gleich; Sie referenzieren einfach ein anderes `Worksheet` für das Ziel.

```csharp
// Assume we have a second sheet already created
Worksheet destSheet = sourceWorkbook.Worksheets.Add("PivotCopy");

// Copy the pivot (and its data source) to the new sheet starting at A1
destSheet.Cells.CopyRange(
    sourceRange.StartRow, sourceRange.StartColumn,
    sourceRange.EndRow, sourceRange.EndColumn,
    0, 0, // destination at A1
    true);
```

> **Randfall:** Wenn die Quell‑Pivot‑Tabelle eine Tabelle verwendet, die auf dem Originalblatt liegt, kopiert Aspose.Cells auch die zugrunde liegende Tabellendefinition, sodass die neue Pivot‑Tabelle sofort funktioniert.

---

## Häufige Fallstricke und wie man sie vermeidet

| Pitfall | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Pivot verliert ihren Cache** | Verwendung von `CopyRange` mit `false` oder einer benutzerdefinierten Kopierroutine, die Objekte ignoriert. | Immer `true` übergeben, wenn Sie die Pivot‑Tabelle selbst benötigen. |
| **Zielzellen enthalten bereits Daten** | Überschreibt stillschweigend und kann vorhandene Formeln beschädigen. | Löschen Sie zuerst den Zielbereich: `worksheet.Cells.ClearRange(targetRange.StartRow, targetRange.StartColumn, targetRange.EndRow, targetRange.EndColumn, true);` |
| **Quellbereich umfasst nicht die gesamte Pivot** | Pivot‑Tabellen erstrecken sich über mehr Zeilen/Spalten als erwartet (z. B. versteckte Zeilen). | Verwenden Sie `worksheet.PivotTables[0].DataRange`, um programmgesteuert die genauen Grenzen zu ermitteln. |
| **Kopieren zwischen Arbeitsmappen** | `CopyRange` funktioniert nur innerhalb derselben Arbeitsmappe. | Verwenden Sie `sourceWorksheet.Cells.CopyRange` zu einem temporären Bereich und anschließend `destWorkbook.Worksheets.AddCopy(sourceWorksheet);` |

---

## Erwartete Ausgabe & Verifizierung

Nach dem Ausführen des Programms:

1. Öffnen Sie `copy-pivot.xlsx`.
2. Sie sehen zwei identische Pivot‑Tabellen – eine bei **A1:J20**, eine andere bei **M1:V20**.
3. Aktualisieren Sie eine beliebige Pivot‑Tabelle; beide sollten dieselben zugrunde liegenden Daten anzeigen.
4. Wenn Sie auf ein anderes Blatt dupliziert haben, enthält das neue Blatt ebenfalls eine funktionierende Kopie.

Eine schnelle Möglichkeit, dies per Code zu überprüfen:

```csharp
int pivotCount = worksheet.PivotTables.Count; // should be 2 after copy
Console.WriteLine($"Pivot tables on the sheet: {pivotCount}");
```

---

## Profi‑Tipp: Bereichserkennung automatisieren

Das Hard‑Coden von `CellArea` funktioniert für statische Berichte, aber Produktionscode muss die Pivot‑Tabelle häufig dynamisch finden.

```csharp
// Find the first pivot table on the sheet
PivotTable pt = worksheet.PivotTables[0];
CellArea ptRange = pt.DataRange;

// Use the detected range for copying
worksheet.Cells.CopyRange(
    ptRange.StartRow, ptRange.StartColumn,
    ptRange.EndRow, ptRange.EndColumn,
    targetRange.StartRow, targetRange.StartColumn,
    true);
```

> **Warum sich die Mühe machen?** Dadurch wird Ihre Lösung robust gegenüber Layout‑Änderungen – keine „Ups, die Pivot ist nach B2 verschoben“‑Fehler mehr.

![Beispiel für das Kopieren einer Pivot‑Tabelle](copy-pivot.png){alt="Beispiel für das Kopieren einer Pivot‑Tabelle"}

*Der Screenshot (Platzhalter) zeigt die ursprüngliche Pivot‑Tabelle links und die duplizierte rechts.*

---

## Zusammenfassung

Wir haben gerade behandelt, wie man **Pivot‑Tabellen** in C# mit Aspose.Cells **kopiert**, Wege erkundet, **Excel‑Bereich zu kopieren**, **Excel‑Pivot zu duplizieren** und sogar **Pivot zu Blatt zu kopieren** über Arbeitsblätter hinweg. Die wichtigsten Erkenntnisse sind:

- Verwenden Sie `Worksheet.Cells.CopyRange` mit dem `true`‑Flag, um Rich‑Objekte zu erhalten.
- Definieren Sie Quell‑ und Ziel‑`CellArea`‑Objekte mit nullbasierten Indizes.
- Passen Sie das Ziel‑Arbeitsblatt an, wenn Sie **Pivot zu Blatt kopieren** müssen.
- Beachten Sie Randfälle wie vorhandene Daten, versteckte Zeilen und Szenarien über mehrere Arbeitsmappen hinweg.

## Was kommt als Nächstes?

- **Dynamische Pivot‑Entdeckung**: Erstellen Sie einen Helfer, der eine Arbeitsmappe nach allen Pivot‑Tabellen scannt und sie automatisch repliziert.
- **Export nach PDF/HTML**: Nach dem Kopieren möchten Sie das Blatt vielleicht in ein Berichtformat rendern – Aspose.Cells unterstützt das ebenfalls.
- **Performance‑Optimierung**: Bei sehr großen Arbeitsmappen sollten Sie die Berechnung vor dem Kopieren deaktivieren und danach wieder aktivieren.

Experimentieren Sie gern: Ändern Sie die Zielkoordinaten, kopieren Sie in eine brandneue Arbeitsmappe oder iterieren Sie über mehrere Arbeitsblätter, um einen konsolidierten Bericht zu erstellen. Die Möglichkeiten sind endlos, und mit dem jetzigen Fundament können Sie den Code an praktisch jede Excel‑Automatisierungsaufgabe anpassen.

Viel Spaß beim Programmieren, und mögen Ihre Pivot‑Tabellen stets perfekt synchron bleiben!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}