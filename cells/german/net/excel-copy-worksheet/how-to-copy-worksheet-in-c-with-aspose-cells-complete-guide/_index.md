---
category: general
date: 2026-03-30
description: Wie man ein Arbeitsblatt in C# mit Aspose.Cells kopiert – Schritt‑für‑Schritt‑Anleitung,
  die das Kopieren von Zellbereichen, das Kopieren von Spalten zwischen Arbeitsblättern,
  das Kopieren von Pivot‑Tabellen eines Arbeitsblatts und das Hinzufügen von neuem
  Arbeitsblatt‑Code abdeckt.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: de
og_description: Erfahren Sie, wie Sie ein Arbeitsblatt in C# mit Aspose.Cells kopieren.
  Dieser Leitfaden zeigt das Kopieren von Zellbereichen, das Beibehalten von Pivot-Tabellen,
  das Kopieren von Spalten zwischen Arbeitsblättern und das Hinzufügen von Code für
  ein neues Arbeitsblatt.
og_title: Wie man ein Arbeitsblatt in C# kopiert – Vollständiges Aspose.Cells‑Tutorial
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Wie man ein Arbeitsblatt in C# mit Aspose.Cells kopiert – Komplettanleitung
url: /de/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man ein Arbeitsblatt in C# mit Aspose.Cells – Komplettanleitung

Haben Sie sich jemals gefragt, **wie man ein Arbeitsblatt** in C# kopiert, ohne dabei eine einzige Pivot-Tabelle oder Formel zu verlieren? Sie sind nicht allein – viele Entwickler stoßen an Grenzen, wenn sie ein Blatt duplizieren müssen und dabei alle Funktionen erhalten wollen. In diesem Tutorial führen wir Sie durch eine praktische, End‑to‑End‑Lösung, die nicht nur die Daten kopiert, sondern auch die **copy worksheet pivot table** beibehält, **copy cell range** verarbeitet und den **add new worksheet code** zeigt, den Sie benötigen.

Wir behandeln alles vom Laden der Quellarbeitsmappe bis zum Speichern der Zieldatei, sodass Sie Spalten zwischen Blättern kopieren, Objekte erhalten und Ihren Code sauber halten können. Keine vagen Verweise, nur ein vollständiges, ausführbares Beispiel, das Sie noch heute in Ihr Projekt einbinden können.

## Was dieses Tutorial abdeckt

- Laden einer bestehenden Excel-Datei mit Aspose.Cells  
- Verwendung von **add new worksheet code**, um ein Zielblatt zu erstellen  
- Definition eines **copy cell range**, das eine Pivot-Tabelle enthält  
- Einrichtung von **CopyOptions**, um Diagramme, Formeln und Pivot-Tabellen unverändert zu lassen  
- Ausführen von **copy columns between sheets** mit zeilenweiser Präzision  
- Speichern des Ergebnisses und Überprüfen, dass das Arbeitsblatt korrekt kopiert wurde  

Am Ende dieses Leitfadens können Sie die Frage „how to copy worksheet“ selbstbewusst beantworten, egal ob Sie Berichte automatisieren oder eine tabellenkalkulationsbasierte Benutzeroberfläche erstellen.

---

## Wie man ein Arbeitsblatt kopiert – Übersicht

Bevor wir in den Code eintauchen, skizzieren wir den groben Ablauf. Denken Sie daran wie an ein Rezept:

1. **Load** die Quellarbeitsmappe (`Source.xlsx`).  
2. **Add** ein neues Arbeitsblatt, um die Kopie zu halten (`add new worksheet code`).  
3. **Define** den Bereich, den Sie duplizieren möchten (`copy cell range`).  
4. **Configure** die Kopieroptionen, damit die Pivot-Tabelle erhalten bleibt (`copy worksheet pivot table`).  
5. **Copy** Zeilen und Spalten (`copy columns between sheets`).  
6. **Save** die neue Arbeitsmappe (`Destination.xlsx`).  

Das war's – sechs Schritte, kein Zauber. Jeder Schritt wird unten mit Code‑Snippets und der jeweiligen Begründung erklärt.

---

## Schritt 1 – Laden der Quellarbeitsmappe

Zuerst das Wichtigste: Sie benötigen eine `Workbook`‑Instanz, die auf die Datei zeigt, die Sie duplizieren möchten. Dieser Schritt ist entscheidend, weil Aspose.Cells direkt mit dem Dateisystem arbeitet, nicht mit der Office‑Benutzeroberfläche.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Warum das wichtig ist:* Das Laden der Datei erzeugt eine In‑Memory‑Darstellung jedes Blatts, jeder Zelle und jedes Objekts. Ohne das gibt es nichts zu kopieren, und jeder Versuch, später `add new worksheet code` auszuführen, würde fehlschlagen, weil die Quelldaten nicht vorhanden sind.

---

## Schritt 2 – Hinzufügen eines neuen Arbeitsblatts (add new worksheet code)

Jetzt benötigen wir einen Ort, um die kopierten Daten einzufügen. Hier kommt der **add new worksheet code** zum Einsatz. Sie können das Blatt beliebig benennen; hier nennen wir es `"Copy"`.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*Pro‑Tipp:* Wenn Sie mehrere Blätter kopieren möchten, rufen Sie `Worksheets.Add` innerhalb einer Schleife auf und geben jedem Blatt einen eindeutigen Namen. So vermeiden Sie Namenskollisionen und halten Ihre Arbeitsmappe übersichtlich.

---

## Schritt 3 – Definieren des Kopierbereichs (Copy Cell Range)

Ein **copy cell range** gibt Aspose.Cells genau an, welche Zeilen und Spalten dupliziert werden sollen. In vielen Praxis‑Szenarien beinhaltet der Bereich eine Pivot‑Tabelle, daher müssen wir präzise sein.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Warum wir das benötigen:* Durch die explizite Angabe des Bereichs vermeiden Sie das Kopieren des gesamten Blatts (was verschwenderisch sein kann) und stellen sicher, dass die Pivot‑Tabelle im kopierten Bereich bleibt. Das ist das Kernstück von **how to copy worksheet**, wenn Sie nur einen Teil des Blatts benötigen.

---

## Schritt 4 – Kopieroptionen festlegen (preserve copy worksheet pivot table)

Aspose.Cells bietet ein `CopyOptions`‑Objekt, das steuert, was eingefügt wird. Um die Pivot‑Tabelle, Diagramme und Formeln zu erhalten, setzen wir `PasteType.All` und aktivieren `PasteSpecial`.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Erklärung:* `PasteType.All` ist die umfassendste Option, während `PasteSpecial` der Engine mitteilt, komplexe Objekte – wie Pivot‑Tabellen – korrekt zu behandeln. Das Überspringen dieses Schrittes ist ein häufiger Stolperstein; das kopierte Blatt würde seine interaktiven Funktionen verlieren.

---

## Schritt 5 – Zeilen und Spalten kopieren (copy columns between sheets)

Jetzt kommt die eigentliche Arbeit: das Verschieben der Daten. Wir verwenden `CopyRows` und `CopyColumns`, um **copy columns between sheets** zu bewältigen. Das Ausführen beider Schritte stellt sicher, dass zusammengeführte Zellen und Spaltenbreiten erhalten bleiben.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Was passiert:* `CopyRows` verschiebt die Daten Zeile für Zeile, während `CopyColumns` dasselbe Spalte für Spalte tut. Das Ausführen beider Schritte garantiert, dass der gesamte rechteckige Block dupliziert wird, was entscheidend ist, wenn Sie **copy columns between sheets** benötigen, die unterschiedliche Spaltenbreiten oder ausgeblendete Spalten haben.

---

## Schritt 6 – Arbeitsmappe speichern

Zum Schluss schreiben Sie die Änderungen zurück auf die Festplatte. Dieser Schritt schließt den **how to copy worksheet**‑Prozess ab.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Verifizierungstipp:* Öffnen Sie `Destination.xlsx` und prüfen Sie, ob das Blatt `"Copy"` identisch zum Original aussieht, die Pivot‑Tabellen funktionieren und die Spaltenbreiten übereinstimmen. Wenn etwas nicht stimmt, überprüfen Sie die `CopyOptions`‑Einstellungen erneut.

---

## Sonderfälle & häufige Variationen

### Kopieren mehrerer Arbeitsblätter

Wenn Sie mehrere Blätter duplizieren müssen, verpacken Sie die obige Logik in eine `foreach`‑Schleife:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Formeln über verschiedene Arbeitsmappen hinweg erhalten

Wenn die Quell‑ und Zielarbeitsmappe unterschiedliche benannte Bereiche haben, setzen Sie `copyOptions` zusätzlich zu `All` auf `PasteType.Formulas`:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Große Bereiche und Leistung

Für massive Datensätze (Hunderttausende von Zeilen) sollten Sie erwägen, nur `CopyRows` zu verwenden und `CopyColumns` zu überspringen, wenn Spaltenbreiten nicht kritisch sind. Das kann ein paar Sekunden einsparen.

---

## Vollständiges funktionierendes Beispiel

Unten finden Sie das vollständige, sofort ausführbare Programm, das alles, was wir besprochen haben, zusammenfasst. Fügen Sie es in eine Konsolen‑App ein, passen Sie die Dateipfade an und drücken Sie **F5**.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Erwartetes Ergebnis:** Beim Öffnen von `Destination.xlsx` wird ein Blatt namens **Copy** angezeigt, das das erste Blatt von `Source.xlsx` widerspiegelt – einschließlich aller Pivot‑Tabellen, Formatierungen und Spaltenbreiten. Die Originaldatei bleibt unverändert.

---

## Häufig gestellte Fragen

**Q: Funktioniert das mit .xlsx‑Dateien, die mit Excel 2019 erstellt wurden?**  
A: Absolut. Aspose.Cells unterstützt alle modernen Excel‑Formate, sodass derselbe Code für `.xlsx`, `.xlsm` und sogar ältere `.xls`‑Dateien funktioniert

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}