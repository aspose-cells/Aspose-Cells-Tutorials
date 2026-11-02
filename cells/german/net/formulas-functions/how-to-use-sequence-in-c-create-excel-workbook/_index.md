---
category: general
date: 2026-07-03
description: Wie man SEQUENCE in C# verwendet, um inkrementelle Zahlen in Excel zu
  generieren. Lernen Sie, ein Excel‑Arbeitsbuch mit C# zu erstellen, und ASP.NET erzeugt
  eine Excel‑Datei mit nur wenigen Codezeilen.
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: de
og_description: Wie man SEQUENCE in C# verwendet, um fortlaufende Zahlen in Excel
  zu erzeugen. Schritt‑für‑Schritt‑Anleitung zum Erstellen einer Excel‑Arbeitsmappe
  mit C# und ASP.NET, um eine Excel‑Datei zu erstellen.
og_title: Wie man SEQUENCE in C# verwendet – Excel-Arbeitsmappe erstellen
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: Wie man SEQUENCE in C# verwendet – Excel-Arbeitsmappe erstellen
url: /de/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wie man SEQUENCE in C# verwendet – Excel-Arbeitsmappe erstellen

Haben Sie sich jemals gefragt, **wie man SEQUENCE** verwendet, um eine Liste von Zahlen in einem Excel‑Blatt aus C# auszugeben? Sie sind nicht der Einzige. Egal, ob Sie ein Reporting‑Dashboard erstellen, ein Data‑Grid füttern oder einfach nur schnell IDs generieren müssen, das Beherrschen dieses Tricks erspart Ihnen das Herumfummeln mit Schleifen.

In diesem Tutorial werden wir **eine Excel‑Arbeitsmappe in C# erstellen**, eine `SEQUENCE`‑Dynamik‑Array‑Formel in Zelle A1 einfügen und am Ende eine schöne Spalte mit fortlaufenden Zahlen erhalten. Wir zeigen auch, wie man diese Datei von einem ASP.NET‑Controller aus bereitstellt – ja, **ASP.NET create Excel file** wird ebenfalls behandelt. Am Ende können Sie **inkrementelle Zahlen im Excel‑Stil** mit einer einzigen Codezeile erzeugen.

## Was Sie benötigen

- .NET 6+ (der Code funktioniert auch unter .NET Framework 4.6+)
- Das **Aspose.Cells for .NET** NuGet‑Paket (oder jede Bibliothek, die `Workbook`/`Worksheet`‑Objekte bereitstellt)
- Ein einfaches ASP.NET‑Core‑ oder MVC‑Projekt, falls Sie den Web‑Download‑Teil ausprobieren möchten

Das war's. Kein zusätzliches COM‑Interop, keine Office‑Installation erforderlich.

---

## Wie man SEQUENCE verwendet, um inkrementelle Zahlen zu erzeugen

Die Excel‑Funktion `SEQUENCE(rows, [columns], [start], [step])` liefert einen **spill**‑Bereich. In unserem Fall wollen wir 5 Zeilen, 1 Spalte, Start bei 10, Schritt 2. Die Formel sieht so aus:

```excel
=SEQUENCE(5,1,10,2)
```

Wenn Excel sie auswertet, enthalten die Zellen A1:A5 **10, 12, 14, 16, 18**. Das Schöne ist, dass wir keine C#‑Schleifen schreiben müssen – die Formel übernimmt die schwere Arbeit.

Unten finden Sie das vollständige C#‑Snippet, das eine Arbeitsmappe erstellt, die Formel einfügt, die Berechnung erzwingt und die Datei speichert.

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Erwartete Ausgabe** – öffnen Sie *DynamicArray.xlsx* und Sie sehen:

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

Das ist die gesamte **how to use sequence**‑Geschichte in C#. Einfach, oder? Aber lassen Sie uns etwas tiefer einsteigen.

### Warum SEQUENCE statt einer Schleife verwenden?

- **Performance** – Excel führt die Berechnungen in seiner eigenen Engine aus, die stark optimiert ist.
- **Maintainability** – Die Formel ist selbsterklärend; jeder, der das Blatt öffnet, erkennt sofort die Absicht.
- **Dynamic resizing** – Ändern Sie das Argument `rows` und der Spill‑Bereich erweitert sich automatisch.

---

## Excel‑Arbeitsmappe in C# erstellen – Schritt für Schritt

Wenn Sie neu bei **create excel workbook c#** sind, hilft Ihnen die folgende Checkliste, häufige Fallstricke zu vermeiden.

1. **Add the Aspose.Cells package**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   (Sie können auch ClosedXML oder EPPlus verwenden, aber die gezeigte API entspricht dem obigen Code.)

2. **Set a license** (optional for trial).  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```

3. **Instantiate `Workbook`** – das erzeugt eine neue, leere Arbeitsmappe.

4. **Reference the worksheet** – `workbook.Worksheets[0]` ist das Standardblatt mit dem Namen *Sheet1*.

5. **Apply the SEQUENCE formula** – wie oben gezeigt.

6. **Calculate** – `workbook.CalculateFormula()` erzwingt den Spill; andernfalls würde die Datei nur die Formel enthalten.

7. **Save** – Sie können auf die Festplatte, in einen `MemoryStream` oder direkt in eine HTTP‑Antwort schreiben.

### Profi‑Tipp

Wenn Sie die Arbeitsmappe im Speicher benötigen (z. B. um sie über eine Web‑API zu senden), verwenden Sie einen `MemoryStream`:

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET Excel‑Datei erstellen – Streaming zum Browser

Jetzt, wo wir **create excel workbook c#** kennen, integrieren wir es in einen ASP.NET‑Core‑Controller, damit Benutzer die Datei on‑the‑fly herunterladen können.

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

Wenn ein Benutzer `/api/excel/download` aufruft, fordert der Browser den Download von *DynamicArray.xlsx* an. Die Datei enthält bereits die **generated incremental numbers excel**‑Spalte dank der `SEQUENCE`‑Formel.

### Was, wenn der Client eine ältere Excel‑Version verwendet?

Dynamische Arrays (einschließlich `SEQUENCE`) wurden in Excel 365/2019 eingeführt. Wenn Sie Rückwärtskompatibilität benötigen, greifen Sie zu einer manuellen Befüllung zurück:

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

Dieses Snippet zeigt den klassischen **generate incremental numbers excel**‑Ansatz, ohne die neue Funktion zu verwenden.

---

## Häufige Fragen & Sonderfälle

- **Muss ich iterative Berechnung aktivieren?**  
  Nein. `SEQUENCE` ist eine nicht‑iterative Funktion; ein einfacher Aufruf von `CalculateFormula()` reicht aus.

- **Was, wenn ich einen horizontalen Spill möchte?**  
  Ändern Sie das zweite Argument: `=SEQUENCE(1,5,10,2)` spaltet über B1:F1.

- **Kann ich SEQUENCE mit anderen Funktionen kombinieren?**  
  Absolut. Zum Beispiel kann `=INDEX(A:A, SEQUENCE(5,1,10,2))` Zeilen aus einer anderen Spalte ziehen.

- **Ist die Größe der Arbeitsmappe ein Problem?**  
  Der Einfluss einer Formel auf die Dateigröße ist vernachlässigbar. Nur wenn Sie Millionen von Zellen manuell füllen, wird die Größe relevant.

---

## Fazit

Wir haben **how to use sequence** in C# durchgegangen, um **create excel workbook c#** zu erstellen, diese Arbeitsmappe über **ASP.NET create excel file** bereitgestellt und einen sauberen Weg gezeigt, **generate incremental numbers excel** zu erzeugen, ohne Schleifen zu schreiben. Die wichtigste Erkenntnis: Lassen Sie die dynamische Array‑Engine von Excel das Zählen übernehmen und konzentrieren Sie Ihren .NET‑Code auf die Orchestrierung.

Fühlen Sie sich frei zu experimentieren – tauschen Sie die Argumente `rows`, `start` oder `step` aus, erzeugen Sie einen horizontalen Spill oder kombinieren Sie die Formel mit `IF` oder `FILTER` für anspruchsvollere Berichte. Wenn Sie bereit sind, versuchen Sie, mehrere Blätter zu verketten oder die Arbeitsmappe als CSV zu exportieren für nachgelagerte Systeme.

Haben Sie eine Variante, die Sie teilen möchten? Hinterlassen Sie unten einen Kommentar oder schreiben Sie mir auf GitHub. Viel Spaß beim Coden!

## Was sollten Sie als Nächstes lernen?

Die folgenden Tutorials behandeln eng verwandte Themen, die auf den in diesem Leitfaden gezeigten Techniken aufbauen. Jede Ressource enthält vollständige funktionierende Codebeispiele mit Schritt‑für‑Schritt‑Erklärungen, um Ihnen zu helfen, zusätzliche API‑Funktionen zu meistern und alternative Implementierungsansätze in Ihren eigenen Projekten zu erkunden.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}