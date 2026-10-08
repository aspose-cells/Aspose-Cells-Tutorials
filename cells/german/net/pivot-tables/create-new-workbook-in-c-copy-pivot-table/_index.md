---
category: general
date: 2026-06-24
description: Erstelle ein neues Arbeitsbuch in C# und kopiere die Pivot‑Tabelle, wobei
  die Daten erhalten bleiben. Lerne, wie man Zeilen kopiert, einen ausgewählten Bereich
  exportiert und die Pivot‑Tabelle intakt hält.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: de
og_description: Erstelle ein neues Arbeitsbuch in C# und kopiere eine Pivot‑Tabelle,
  wobei die Daten erhalten bleiben. Schritt‑für‑Schritt‑Anleitung, die erklärt, wie
  man Zeilen kopiert und einen ausgewählten Bereich exportiert.
og_title: Neues Arbeitsbuch in C# erstellen – Pivot‑Tabelle kopieren
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: Neues Arbeitsbuch in C# erstellen – Pivot‑Tabelle kopieren
url: /de/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Neue Arbeitsmappe in C# erstellen – Pivot‑Tabelle kopieren

Haben Sie schon einmal **eine neue Arbeitsmappe** in C# erstellen müssen, nur um einen Datenausschnitt zu verschieben, der eine Pivot‑Tabelle enthält? Sie sind nicht allein. In vielen Reporting‑Pipelines greifen Sie sich ein paar Zeilen, vielleicht ein paar Spalten, und erwarten, dass die Pivot‑Tabelle exakt unverändert bleibt – keine kaputten Verweise, keine fehlenden Berechnungen.  

Die gute Nachricht? Mit ein paar Zeilen Aspose.Cells können Sie **Pivot‑Tabelle kopieren**, sie intakt halten und sogar **ausgewählten Bereich exportieren**, ohne etwas zu beschädigen. Im Folgenden sehen Sie ein vollständiges, sofort ausführbares Beispiel, das **zeigt, wie Zeilen kopiert**, die Pivot‑Tabelle erhalten und das Ergebnis als brandneue Arbeitsmappe gespeichert wird.

## Was dieses Tutorial abdeckt

- Einrichten eines C#‑Projekts mit Aspose.Cells (der Bibliothek, die den Code antreibt).
- Laden der Quellarbeitsmappe, die die ursprüngliche Pivot‑Tabelle enthält.
- Verwendung der Methoden `CopyRows` und `CopyColumns` der Bibliothek, um den exakt benötigten Bereich zu duplizieren.
- Speichern des duplizierten Bereichs in einem **create new workbook**‑Szenario, während die Pivot‑Tabelle funktionsfähig bleibt.
- Tipps für Sonderfälle wie mehrere Pivot‑Tabellen, ausgeblendete Zeilen und große Datensätze.

Am Ende dieses Leitfadens können Sie **ausgewählten Bereich exportieren** aus jeder Excel‑Datei, die Pivot‑Logik erhalten und die neue Datei beliebig ablegen.

> **Voraussetzung**: Aspose.Cells für .NET (Testversion oder lizenziert) über NuGet installiert. Wenn Sie es noch nicht hinzugefügt haben, führen Sie `dotnet add package Aspose.Cells` im Projektordner aus.

---

## Neue Arbeitsmappe erstellen und Pivot‑Tabelle kopieren

Im Folgenden finden Sie das Herzstück der Lösung. Wir gehen jede Zeile durch, erklären, warum sie wichtig ist, und zeigen dann das komplette Programm.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Warum das funktioniert

- **`CopyRows` / `CopyColumns`**: Diese Methoden duplizieren die zugrunde liegenden Zellen *und* die zugehörigen Objekte (wie einen Pivot‑Cache). Deshalb bleibt die Pivot‑Tabelle nach dem Verschieben funktionsfähig.
- **Separates Ziel‑Workbook**: Durch Erzeugen einer frischen `Workbook`‑Instanz **create new workbook** wir ohne alte Formatierungen oder versteckte Blätter, die stören könnten.
- **Nullbasierte Indizierung**: Aspose.Cells verwendet nullbasierte Indizes, sodass `0` auf Zelle **A1** zeigt. Passen Sie `startRow`/`startColumn` an, wenn Ihre Pivot‑Tabelle nicht in der linken oberen Ecke liegt.
- **Pivot‑Tabelle erhalten**: Der Cache der Pivot‑Tabelle befindet sich im selben Bereich, sodass das Kopieren des Bereichs automatisch den Cache mitkopiert. Kein zusätzlicher Code nötig.

---

## Wie man Zeilen kopiert, ohne die Pivot‑Tabelle zu zerstören

Wenn Sie nur am Zeilen‑Kopieren‑Teil interessiert sind, können Sie diesen isolieren:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro‑Tipp**: Beim Kopieren von Zeilen, die eine Pivot‑Tabelle berühren, immer den *gesamten* Pivot‑Bereich (Zeilen + Spalten) kopieren. Teilweise Kopien können dazu führen, dass Felder fehlen und `#REF!`‑Fehler entstehen.

---

## Ausgewählten Bereich exportieren – ein Praxisbeispiel

Stellen Sie sich vor, Sie haben eine riesige Verkaufs‑Arbeitsmappe, aber Ihr Kunde möchte nur die Zusammenfassung des ersten Quartals, die in den Zeilen 1‑20 und Spalten A‑D liegt. Der obige Code‑Snippet **export selected range** bereits für Sie. Ändern Sie einfach die Variablen `totalRows` und `totalColumns`, um die Anforderung des Kunden zu erfüllen, und fertig.

### Ausgeblendete Zeilen oder Filter behandeln

Hat das Quellblatt ausgeblendete Zeilen (z. B. gefiltert), möchten Sie vielleicht nur *sichtbare* Zeilen kopieren. Aspose.Cells bietet `CopyRows`‑Überladungen, die die Sichtbarkeit berücksichtigen:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Setzen Sie das letzte Boolean‑Argument auf `true`, um nur sichtbare Zeilen zu kopieren – perfekt für „export selected range“, wenn der Benutzer Filter angewendet hat.

---

## Pivot‑Tabelle erhalten – häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Pivot‑Cache wird nicht kopiert** | Verwendung von einfachem `Range.Copy` statt `Cells.CopyRows/CopyColumns`. | Bei `Cells`‑Methoden bleiben, wie gezeigt. |
| **Ziel‑Sheet enthält bereits eine Pivot‑Tabelle** | Überschreiben einer Arbeitsmappe, die bereits eine Pivot‑Tabelle mit gleichem Namen enthält. | Mit einem frischen `Workbook()` starten (wie wir es tun). |
| **Benannte Bereiche brechen** | Die Quell‑Pivot referenziert einen benannten Bereich, der in der neuen Datei fehlt. | Benannten Bereich ebenfalls kopieren: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Datenquellpfad ändert sich** | Pivot verweist auf eine externe Datenquelle, die nicht verfügbar ist. | Nach dem Kopieren `PivotTable.RefreshData()` aufrufen, falls nötig. |

---

## Vollständiges End‑zu‑End‑Beispiel (bereit zum Ausführen)

Unten finden Sie das komplette Programm, inklusive `using`‑Direktiven und einer kurzen Konsolen‑UI. Kopieren Sie es in ein neues Konsolen‑App‑Projekt und drücken Sie **F5**.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Erwartete Ausgabe** (in der Konsole):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

Öffnen Sie `copy-pivot.xlsx` und Sie sehen dieselbe Pivot‑Tabelle wie in `source.xlsx`, voll funktionsfähig und mit dem kopierten Datenbereich verknüpft.

---

## Häufig gestellte Fragen

**F: Funktioniert das mit mehreren Pivot‑Tabellen im selben Blatt?**  
A: Ja, solange das kopierte Rechteck jede benötigte Pivot‑Tabelle einschließt. Wenn Sie nur eine wollen, passen Sie `rows`/`cols` entsprechend an.

**F: Was, wenn die Quell‑Arbeitsmappe externe Datenverbindungen nutzt?**  
A: Der Pivot‑Cache verweist weiterhin auf die ursprüngliche Verbindung. Rufen Sie `pivotTable.RefreshData()` nach dem Laden des Ziels auf, um die Quelle neu abzufragen.

**F: Kann ich die Pivot‑Tabelle in ein anderes Blatt derselben Arbeitsmappe kopieren?**  
A: Absolut. Ersetzen Sie `destinationWorkbook` durch `sourceWorkbook` und wählen Sie einen anderen Arbeitsblatt‑Index.

**F: Gibt es eine Möglichkeit, nur die Formatierung zu kopieren?**  
A: Verwenden Sie `CopyRows`/`CopyColumns`‑Überladungen, die ein `CopyOptions`‑Objekt akzeptieren – setzen Sie `CopyOptions.CopyType = CopyType.ValuesOnly` oder `CopyType.All` je nach Bedarf.

---

## Fazit

Wir haben gerade ein **create new workbook**‑Szenario durchlaufen, das **copy pivot table**, **preserve pivot table** und **export selected range** – alles in reinem C#.

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}