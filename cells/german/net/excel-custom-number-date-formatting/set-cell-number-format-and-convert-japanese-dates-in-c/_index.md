---
category: general
date: 2026-11-19
description: Zellenzahlformat in C# festlegen und lernen, wie man das Excel‑Datumsformat
  für japanische Ära‑Daten anwendet, um eine zuverlässige C#‑Excel‑Datumskonvertierung
  zu ermöglichen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: de
lastmod: 2026-11-19
og_description: Zahlenformat einer Zelle in C# festlegen und das Excel-Datumsformat
  auf japanische Ära‑Daten anwenden. Folgen Sie diesem umfassenden Leitfaden für eine
  präzise C#‑Excel‑Datumskonvertierung.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Zell‑Nummernformat festlegen und japanische Datumsangaben in C# konvertieren
  – Schritt‑für‑Schritt‑Anleitung
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Zellenzahlformat festlegen und japanische Datumsangaben in C# konvertieren
url: /de/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Zellformat festlegen und japanische Daten in C# konvertieren

Wenn Sie in einem C# Excel‑Automatisierungsprojekt **Zellformat festlegen** müssen, zeigt Ihnen dieser Leitfaden, wie Sie **Excel‑Datumsformat anwenden** und **C# Excel‑Datumsumwandlung** für japanische Ära‑Daten durchführen. Sie erhalten ein vollständiges, ausführbares Beispiel, das einen Reiwa‑Ära‑String (z. B. `R3/04/01`) in das gregorianische Datum `2021‑04‑01` konvertiert.

## Was Sie lernen werden

* Wie man eine Arbeitsmappe erstellt und auf das erste Arbeitsblatt zugreift.  
* Wie man **Zellformat festlegt**, damit Excel den Wert als Datum behandelt.  
* Wie man **Excel‑Datumsformat anwendet**, das japanische Ära‑Zeichenketten erkennt.  
* Wie man **C# Excel‑Datumsumwandlung** auslöst, indem man Formeln neu berechnet.  
* Erwartete Ausgabe und Tipps zur Fehlersuche bei Randfällen.

**Prerequisites**

* .NET 6 oder höher (der Code funktioniert auch mit .NET Framework 4.6+).  
* Aspose.Cells für .NET 2024 oder neuer – Installation via NuGet: `dotnet add package Aspose.Cells`.  
* Grundlegende Kenntnisse in C# und dem Umgang mit Excel‑Datumswerten.

> **Profi‑Tipp:** Aspose.Cells funktioniert ohne installierten Microsoft Office und ist damit ideal für serverseitige Automatisierung.

## Zellformat mit Aspose.Cells in C# festlegen

Der erste Schritt besteht darin, Excel mitzuteilen, dass die Zelle ein Datum enthält. Excel speichert Daten als Seriennummern, daher müssen wir ein integriertes Datums‑Zahlenformat (ID 14) auf die Zielzelle anwenden.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Warum das funktioniert

* `Style.Number = 14` entspricht dem *Kurzdatum*-Format von Excel (`mm/dd/yyyy` standardmäßig).  
* Wenn die Zelle eine japanische Ära‑Zeichenkette wie `R3/04/01` enthält, erkennt Aspose.Cells interner Parser die Ära und konvertiert sie während `CalculateFormula()` in die entsprechende gregorianische Seriennummer.  
* Nach der Berechnung liefert `StringValue` das formatierte gregorianische Datum zurück.

## Excel‑Datumsformat für japanische Ära‑Daten anwenden

Wenn Sie möchten, dass die Zelle die japanische Ära anstelle des gregorianischen Datums anzeigt, können Sie ein benutzerdefiniertes Zahlenformat verwenden, das den Ära‑Code enthält. Dies demonstriert die Fähigkeit, **Excel‑Datumsformat anzuwenden**.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` erzwingt das japanische Gebietsschema.  
* `ggg` steht für den Ära‑Namen (z. B. `R` für Reiwa).  
* Durch Hinzufügen von Literalzeichen (`年`, `月`, `日`) entsteht ein vertrautes japanisches Datumslayout.

### Wann ein benutzerdefiniertes Format verwenden

* Berichte für ein japanisches Publikum.  
* Wenn die ursprünglichen Ära‑Informationen für Rechtsdokumente erhalten bleiben müssen.  
* In Dashboards, in denen sowohl gregorianische als auch Ära‑Daten nebeneinander angezeigt werden.

## C# Excel‑Datumsumwandlung – Umgang mit japanischen Ären

Der **c# excel date conversion**‑Prozess lässt sich in drei logische Teile gliedern:

1. **Parse the era string** – Aspose.Cells erkennt automatisch `R` (Reiwa), `H` (Heisei), `S` (Showa) usw.  
2. **Convert to a serial number** – Excel speichert Daten als Tage seit dem 30.12.1899.  
3. **Format the serial number** – entweder mit einem integrierten Format (ID 14) oder einem benutzerdefinierten japanischen Format.

### Vollständiges End‑zu‑Ende‑Beispiel

Unten steht ein eigenständiges Programm, das sowohl die gregorianische als auch die Ära‑Ausgabe in einem Durchlauf demonstriert.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Erwartete Konsolenausgabe**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Randfälle & häufige Stolperfallen

| Situation                              | Worauf zu achten ist                                   | Lösung / Empfehlung                                   |
|----------------------------------------|--------------------------------------------------------|--------------------------------------------------------|
| Leere oder fehlerhafte Ära‑Zeichenkette | `PutValue` speichert den wörtlichen Text; Umwandlung schlägt fehl | Validieren Sie die Eingabe mit einem regulären Ausdruck, bevor Sie sie in die Zelle schreiben. |
| Gebietsschema‑Fehlanpassung            | Benutzerdefiniertes Format zeigt westliche Ziffern statt japanischer Zeichen | Stellen Sie sicher, dass das `Custom`‑Format `[$-ja-JP]` enthält oder setzen Sie `Workbook.Settings.CultureInfo` auf `ja-JP`. |
| Arbeitsmappe enthält Formeln, die auf die Datumszelle verweisen | Neuberechnung kann Formelergebnisse überschreiben | Rufen Sie `CalculateFormula` **nach** allen Formatierungsschritten auf, oder verwenden Sie `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)`, wenn Sie Fehler überspringen müssen. |
| Verwendung älterer Aspose.Cells‑Versionen | Unterstützung für japanische Ären wurde in Q3 2022 hinzugefügt | Aktualisieren Sie auf das neueste NuGet‑Paket. |

## Die Lösung testen

1. **Programm ausführen** aus Visual Studio oder `dotnet run`.  
2. Verifizieren Sie, dass die Konsole das gregorianische Datum `2021‑04‑01` und die Ära‑Zeichenkette `R3年04月01日` ausgibt.  
3. Öffnen Sie die erzeugte Arbeitsmappe (wenn Sie `wb.Save("Demo.xlsx");` hinzufügen) in Microsoft Excel, um dieselbe Formatierung in den Zellen zu sehen.

### Automatisierungstipp

Wenn Sie einen großen Bereich von Ära‑Daten verarbeiten müssen (z. B. Spalte A enthält viele japanische Daten), kapseln Sie die Umwandlungslogik in einer Schleife:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Dieser Ansatz hält die **set cell number format**‑Operation schnell und speichereffizient.

## Fazit

Sie wissen jetzt, wie man mit Aspose.Cells in C# **Zellformat festlegt**, wie man **Excel‑Datumsformat** für japanische Ära‑Zeichenketten **anwendet** und wie man zuverlässige **C# Excel‑Datumsumwandlung** von Ära‑ zu gregorianischen Daten durchführt. Der vollständige, ausführbare Code demonstriert beide Ausgaben und hebt gängige Randfälle hervor.  

**Nächste Schritte**

* Weitere integrierte Format‑IDs erkunden


## Was Sie als Nächstes lernen sollten?


Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige, funktionierende Code‑Beispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, weitere API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [Excel‑Datumsformat in C# festlegen – Komplett‑Schritt‑für‑Schritt‑Leitfaden](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Wie man Zahlenformat in Excel mit Aspose.Cells anwendet](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [Wie man ein benutzerdefiniertes Zahlenformat in Excel in C# anwendet](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}