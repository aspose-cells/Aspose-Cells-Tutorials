---
category: general
date: 2026-03-22
description: Wie man Excel mit Formatierung exportiert und das Zahlenformat beibehält.
  Erfahren Sie, wie Sie einen Excel‑Bereich konvertieren, das Formel­ergebnis erhalten
  und Excel mit Formatierung mithilfe von Aspose.Cells exportieren.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: de
og_description: Wie man Excel mit Formatierung exportiert und das Zahlenformat beibehält.
  Schritt‑für‑Schritt‑Anleitung zum Konvertieren eines Excel‑Bereichs, zum Abrufen
  des Formel­ergebnisses und zum Exportieren von Excel mit Formatierung in C#.
og_title: Wie man Excel mit Formatierung exportiert – Zahlenformat beibehalten
tags:
- C#
- Aspose.Cells
- Excel automation
title: Wie man Excel mit Formatierung exportiert – Zahlenformat beibehalten
url: /de/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel mit Formatierung exportieren – Zahlenformat beibehalten

Haben Sie sich jemals gefragt, **wie man Excel**‑Daten exportiert, während das Aussehen jeder Zelle exakt so bleibt, wie Sie es im Arbeitsblatt sehen? Vielleicht müssen Sie einen Bericht an einen Kunden senden, ein Grid‑Steuerelement füttern oder die Werte einfach in einer Datenbank speichern. Das Problem ist meist der Verlust von Zahlenformaten oder dass Formeln in rohe Zeichenketten umgewandelt werden.  

In diesem Tutorial gehen wir Schritt für Schritt durch ein vollständiges, sofort ausführbares C#‑Beispiel, das **Zahlenformat beibehält**, **einen Excel‑Bereich** in ein `DataTable` **konvertiert**, **das Formel‑Ergebnis liefert** und schließlich **Excel mit Formatierung exportiert** mithilfe von Aspose.Cells. Am Ende haben Sie eine einzelne Methode, die Sie in jedes Projekt einbinden und mit einem Arbeitsblatt‑Verweis aufrufen können.

> **Schnelle Vorschau:** Der Code erstellt eine Arbeitsmappe, schreibt einen Wert und eine Formel, weist Aspose.Cells an, die Zellen als formatierte Zeichenketten zu exportieren, und gibt `123.456 | 246.912` aus – genau das, was Sie in Excel erwarten würden.

---

## Was Sie benötigen

- **Aspose.Cells für .NET** (die kostenlose Testversion reicht für Lernzwecke)
- .NET 6.0 oder höher (die API ist identisch unter .NET Framework)
- Eine grundlegende C#‑Entwicklungsumgebung (Visual Studio, VS Code, Rider … Sie entscheiden)

Es werden keine zusätzlichen NuGet‑Pakete über Aspose.Cells hinaus benötigt. Wenn Sie es noch nicht installiert haben, führen Sie aus:

```bash
dotnet add package Aspose.Cells
```

---

## Schritt 1 – Arbeitsmappe erstellen und Werte schreiben (inkl. Formel)

Zuerst erzeugen wir eine neue Arbeitsmappe und schreiben einen numerischen Wert in **A1**. Anschließend fügen wir in **B1** eine einfache Formel ein, die die erste Zelle mit zwei multipliziert. Das legt die Grundlage, um später **Formelergebnis erhalten** zu demonstrieren.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Warum das wichtig ist:**  
- `PutValue` speichert die rohe Zahl, während `PutFormula` die Berechnung speichert.  
- Aspose.Cells hält die Formel **lebendig**, sodass wir später beim Abrufen des Zellwertes tatsächlich `246.912` erhalten und nicht den Text `"=A1*2"`.

---

## Schritt 2 – Aspose.Cells anweisen, Werte als formatierte Zeichenketten zu exportieren

Rufen Sie einfach `ExportDataTable` mit den Standardeinstellungen auf, werden numerische Zellen als ihre zugrunde liegenden `double`‑Werte zurückgegeben. Das entfernt Tausendertrennzeichen, Währungssymbole oder benutzerdefinierte Dezimalstellen, die Sie eventuell gesetzt haben. Die Klasse `ExportTableOptions` ermöglicht es uns, **Zahlenformat beizubehalten** und **als Zeichenkette zu exportieren**.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Wichtiger Hinweis:** `ExportNumberFormat = true` ist das Flag, das das **Beibehalten des Zahlenformats** aktiviert. Ohne diese Einstellung würden Sie `"123.456"` und `"246.912"` als rohe Zahlen sehen, was im Code zwar funktioniert, aber nicht, wenn Sie die Daten in eine UI einfügen, die das gleiche Format wie Excel erwartet.

---

## Schritt 3 – Exportierte Daten ausgeben (Verifizierung)

Jetzt, wo wir ein `DataTable` voller formatierter Zeichenketten haben, geben wir den Inhalt auf der Konsole aus. Das zeigt zudem, dass wir erfolgreich **Formelergebnis erhalten** haben, ohne die Formel selbst auszuwerten.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Das Programm gibt aus:

```
123.456 | 246.912
```

Beachten Sie, dass die zweite Spalte das **Formelergebnis** und nicht den Formelttext anzeigt. Genau das benötigen Sie, wenn Sie **Excel mit Formatierung exportieren** für nachgelagerte Verarbeitung.

---

## Schritt 4 – Größere Excel‑Bereiche konvertieren (optional)

Das obige Beispiel behandelt einen winzigen Ausschnitt `A1:B1`, aber in der Praxis müssen häufig ganze Tabellen exportiert werden. Die gleiche Methode funktioniert für jedes rechteckige Feld – passen Sie einfach die Argumente `firstRow`, `firstColumn`, `totalRows` und `totalColumns` an.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**Pro‑Tipp:** Wenn Ihr Blatt bereits eine Kopfzeile enthält, setzen Sie `includeColumnNames` auf `true`. Aspose.Cells verwendet dann die erste Zeile des Bereichs als Spaltennamen, was praktisch ist, wenn Sie das `DataTable` später an ein UI‑Grid binden.

---

## Schritt 5 – Häufige Stolperfallen & wie man sie vermeidet

| Problem | Warum es passiert | Lösung |
|---------|-------------------|--------|
| **Zahlen verlieren Kommas oder Währungssymbole** | `ExportAsString` ist `false` oder `ExportNumberFormat` fehlt | Setzen Sie sowohl `ExportAsString = true` **als auch** `ExportNumberFormat = true`. |
| **Formelzellen geben den Formelttext zurück** | Sie haben `CalculateFormula` nicht vor dem Export aufgerufen (nur nötig, wenn die Arbeitsmappe nicht automatisch berechnet) | Aktivieren Sie die Auto‑Berechnung (`workbook.CalculateFormula()`) oder nutzen Sie `ExportAsString`, das die Auswertung erzwingt. |
| **Kopfzeilen erscheinen als Datenzeilen** | `includeColumnNames` ist `false`, obwohl Ihr Bereich eine Kopfzeile enthält | Setzen Sie `includeColumnNames = true`, um die erste Zeile als Spaltennamen zu behandeln. |
| **Große Bereiche verursachen Speicherbelastung** | Das Exportieren des gesamten Blatts auf einmal lädt alles in den Speicher | Exportieren Sie in Teilen (z. B. 500 Zeilen gleichzeitig) und fügen Sie die `DataTable`s bei Bedarf zusammen. |

---

## Schritt 6 – Vollständiges Beispiel (Copy‑Paste‑bereit)

Unten finden Sie das gesamte Programm, von den `using`‑Anweisungen bis zur `Main`‑Methode. Kopieren Sie es in eine Konsolen‑App und drücken Sie **F5** – Sie sehen sofort die formatierte Ausgabe.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Erwartete Ausgabe**

```
123.456 | 246.912

Press any key to exit...
```

Damit ist der gesamte **Wie‑man‑Excel‑exportiert**‑Workflow abgedeckt: Formatierung bleibt erhalten, Formelergebnisse werden ausgewertet und ein sauberes `DataTable` steht jedem .NET‑Verbraucher bereit.

---

## Fazit

Wir haben alles behandelt, was Sie über **wie man Excel**‑Daten exportiert, **Zahlenformat beibehält**, **einen Excel‑Bereich** in ein `DataTable` **konvertiert** und **Formelergebnisse** ohne zusätzliche Analyse erhält, wissen müssen. Der Schlüssel liegt in der Konfiguration von `ExportTableOptions` – sobald Sie `ExportAsString` und `ExportNumberFormat` auf `true` setzen, übernimmt Aspose.Cells die schwere Arbeit für Sie.

Ab hier können Sie:

- Das `DataTable` in ein WPF‑`DataGrid` oder eine ASP.NET‑MVC‑View einbinden.  
- Die Tabelle in eine CSV‑Datei schreiben und dabei die exakte visuelle Darstellung beibehalten.  
- Den Ansatz auf mehrere Blätter oder dynamische Bereiche ausweiten.

Experimentieren Sie gern mit verschiedenen Formaten (Währung, Prozentsätze) und größeren Datenblöcken. Wenn Sie auf Eigenheiten stoßen, schauen Sie noch einmal in die **häufigen Stolperfallen**‑Tabelle – sie deckt die häufigsten Probleme beim **Exportieren von Excel mit Formatierung** ab.

Viel Spaß beim Coden und mögen Ihre exportierten Tabellen immer so poliert aussehen wie die Originale!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}