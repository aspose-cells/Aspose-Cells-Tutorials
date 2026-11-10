---
category: general
date: 2026-10-01
description: Lär dig hur du använder WRAPCOLS, tvingar formelberäkning, skriver Excel‑fil
  i C# och sparar arbetsboken till fil med Aspose.Cells i några enkla steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- force formula calculation
- write excel file c#
- save workbook to file
- how to add formula excel
language: sv
lastmod: 2026-10-01
og_description: Hur du använder WRAPCOLS i C# för att lägga till en formel, tvinga
  formelberäkning, skriva en Excel‑fil i C# och spara arbetsboken till en fil med
  Aspose.Cells.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in an Excel worksheet
  with Aspose.Cells
og_title: Hur man använder WRAPCOLS i C# – lägg till formler, tvinga beräkning och
  spara Excel
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to use WRAPCOLS, force formula calculation, write Excel file
    C# and save workbook to file with Aspose.Cells in a few easy steps.
  headline: How to use WRAPCOLS in C# for Excel arrays and workbook saving
  type: TechArticle
- description: Learn how to use WRAPCOLS, force formula calculation, write Excel file
    C# and save workbook to file with Aspose.Cells in a few easy steps.
  name: How to use WRAPCOLS in C# for Excel arrays and workbook saving
  steps:
  - name: '**Target the cell** – use `Cells["B2"]`, `Cells[1, 1]`, or a range name.'
    text: '**Target the cell** – use `Cells["B2"]`, `Cells[1, 1]`, or a range name.'
  - name: '**Assign the formula string** – remember to start with `=` and use US‑style
      separators (comma for arguments).'
    text: '**Assign the formula string** – remember to start with `=` and use US‑style
      separators (comma for arguments).'
  - name: '**Trigger calculation** if you need the result immediately.'
    text: '**Trigger calculation** if you need the result immediately.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man använder WRAPCOLS i C# för Excel‑arrayer och sparande av arbetsbok
url: /sv/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-for-excel-arrays-and-workbook-savin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS i C# – lägg till formler, tvinga beräkning och spara Excel

Om du behöver **how to use WRAPCOLS** i ett C#-projekt, visar den här guiden exakt det och varför det är viktigt. Du kommer också att lära dig hur du **force formula calculation**, **write Excel file C#**, och **save workbook to file** med hjälp av Aspose.Cells-biblioteket.

Att arbeta med Excel programatiskt innebär ofta att infoga formler, säkerställa att de utvärderas och slutligen spara resultatet. Denna handledning går igenom varje steg, så att du kan generera arrayresultat som `=WRAPCOLS({1,2,3,4},2)` utan att lämna din IDE.

## Vad du kommer att uppnå

* Infoga `WRAPCOLS`-funktionen i en cell (svarar på **how to add formula excel**).
* Utlösa beräkning så att arrayresultatet blir ett riktigt cellområde.
* Exportera arbetsboken till en `.xlsx`-fil på disk (**write Excel file C#** och **save workbook to file**).

### Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.6+).
* En giltig licens för **Aspose.Cells for .NET** – den kostnadsfria utvärderingen fungerar för testning.
* Visual Studio 2022 eller någon C#‑kompatibel editor.

---

## Så använder du WRAPCOLS med Aspose.Cells

`WRAPCOLS` skapar en tvådimensionell array från en endimensionell lista. I Aspose.Cells behandlar du den som vilken annan Excel-formel som helst—tilldela den till en cells `Formula`-egenskap.

```csharp
using Aspose.Cells;

class WrapColsExample
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty workbook
        Worksheet sheet = workbook.Worksheets[0];        // first (default) sheet

        // Step 2: Insert the WRAPCOLS formula into cell A1
        // The formula builds a 2‑column array from {1,2,3,4}
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // Step 3: Force calculation so the array result is materialized
        workbook.Calculate();

        // Step 4: Save the workbook to inspect the result
        workbook.Save("output.xlsx");
    }
}
```

**Varför detta fungerar:**  
*Att tilldela formeln* lagrar det textuella uttrycket i cellen. Arbetsboken **utvärderar inte** formler automatiskt när du anropar `Save`; du måste anropa `Calculate()` eller aktivera automatisk beräkning. Detta är kärnan i **force formula calculation**.

---

## Tvinga formelberäkning i arbetsboken

Aspose.Cells respekterar arbetsbokens `CalculationOptions`. Om du hoppar över det explicita anropet `Calculate()` kommer den sparade filen fortfarande att innehålla formeln, och Excel kommer att beräkna om den först när filen öppnas. För att garantera att arrayen redan är expanderad (t.ex. för efterföljande bearbetning) tvingar du beräkningen själv.

```csharp
// Force full calculation, including array formulas
workbook.Calculate(FormulaCalculationMode.Full);
```

*Tips:* Om du arbetar med stora arbetsböcker, använd `FormulaCalculationMode.Manual` och anropa `Calculate()` endast på de blad du behöver. Detta minskar minnesförbrukningen.

---

## Skriv Excel-fil i C# och spara arbetsbok till fil

Att spara arbetsboken är enkelt, men steget **save workbook to file** kan innebära ytterligare överväganden:

| Scenario                              | Rekommenderad metod                              |
|---------------------------------------|-------------------------------------------------|
| Default location (same folder)        | `workbook.Save("output.xlsx");`                 |
| Specific folder, ensure it exists     | `Directory.CreateDirectory(path); workbook.Save(Path.Combine(path, "output.xlsx"));` |
| Stream output (e.g., HTTP response)   | `using var ms = new MemoryStream(); workbook.Save(ms, SaveFormat.Xlsx);` |

```csharp
// Example: saving to a custom directory
string outputDir = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "AsposeDemo");
Directory.CreateDirectory(outputDir);
string filePath = Path.Combine(outputDir, "wrapcols_result.xlsx");
workbook.Save(filePath);
Console.WriteLine($"Workbook saved to {filePath}");
```

**Varför du bör specificera sökvägen** – Att hårdkoda `"output.xlsx"` fungerar bara när processen har skrivbehörighet till den aktuella katalogen. Att använda en absolut sökväg undviker behörighetsfel och gör handledningen reproducerbar på vilken maskin som helst.

---

## Så lägger du till Excel-formler i celler programatiskt

Utöver `WRAPCOLS` gäller samma mönster för vilken Excel-formel som helst:

1. **Måla cellen** – använd `Cells["B2"]`, `Cells[1, 1]` eller ett områdesnamn.
2. **Tilldela formelsträngen** – kom ihåg att börja med `=` och använda amerikanska separatorer (komma för argument).
3. **Utlösa beräkning** om du behöver resultatet omedelbart.

```csharp
// Adding a SUM formula to C1 that sums A1:B1
sheet.Cells["C1"].Formula = "=SUM(A1:B1)";
workbook.Calculate(); // ensures C1 now contains the computed sum
```

*Vanligt fallgropp:* Att glömma att escapera dubbla citationstecken i en formelsträng. Använd `\"` i C# eller den verbatim-stränglitteralen `@"..."`.

```csharp
// Correct way to embed a text constant in a formula
sheet.Cells["D1"].Formula = @"=IF(A1>0,""Positive"",""Zero or Negative"")";
```

---

## Särskilda fall och bästa praxis‑tips

| Situation                              | Rekommenderad hantering |
|----------------------------------------|--------------------------|
| **Large array formulas** (e.g., 10 000 elements) | Use `worksheet.Cells.SetArrayFormula` to write the array directly; avoid `WRAPCOLS` for massive data sets. |
| **Formula evaluation disabled** (some environments) | Set `workbook.Settings.CalcMode = CalculationMode.Manual;` then call `workbook.Calculate();` explicitly. |
| **Saving as CSV** | Formulas are lost; call `workbook.Save("file.csv", SaveFormat.Csv);` after calculation if you need the values. |
| **Thread‑safe execution** | Do not share a single `Workbook` instance across threads; instantiate a new workbook per request. |

---

## Fullständigt körbart exempel

Nedan är hela programmet som du kan kopiera‑klistra in i en konsolapplikation. Det inkluderar alla steg—**how to use WRAPCOLS**, **force formula calculation**, **write Excel file C#**, och **save workbook to file**—i ett sammanhängande flöde.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Add WRAPCOLS formula (answers how to add formula excel)
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 3️⃣ Force calculation so the array expands to A1:B2
        workbook.Calculate(FormulaCalculationMode.Full);

        // 4️⃣ Save the file (demonstrates write Excel file C# and save workbook to file)
        string outDir = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "AsposeDemo");
        Directory.CreateDirectory(outDir);
        string outPath = Path.Combine(outDir, "wrapcols_demo.xlsx");
        workbook.Save(outPath);
        Console.WriteLine($"Workbook with WRAPCOLS saved to: {outPath}");
    }
}
```

**Förväntat resultat i Excel**

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

`WRAPCOLS`-funktionen har tagit den platta listan `{1,2,3,4}` och omslagit den i två kolumner, exakt som formeln specificerar.

---

## Slutsats

Du vet nu **how to use WRAPCOLS** i C#, hur du **force formula calculation**, hur du **write Excel file C#**, och det korrekta sättet att **save workbook to file** med Aspose.Cells. Genom att följa stegen ovan kan du bädda in vilken Excel-formel som helst, få omedelbara resultat och spara arbetsboken för efterföljande bearbetning eller nedladdning av användaren.

### Vad blir nästa?

* Utforska andra array‑funktioner som `WRAPROWS` eller `SEQUENCE`.
* Kombinera `WRAPCOLS` med dynamiska områden med hjälp av `OFFSET` eller `INDEX`.
* Byt till det kostnadsfria **ClosedXML**-biblioteket om du behöver ett open‑source‑alternativ (API:et skiljer sig men koncepten att sätta en formel och anropa `Calculate()` förblir desamma).

Känn dig fri att experimentera med större dataset, olika arbetsboksinställningar eller export till PDF/CSV. Om du stöter på problem, dubbelkolla att du anropade `workbook.Calculate()` innan du sparar—det är nyckeln till pålitlig **force formula calculation**.

Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Skapa ny arbetsbok i C# – Lägg till formel och spara Excel‑fil](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Hur man beräknar cotangent i Excel med C# – Skapa arbetsbok, använd EXPAND,](/cells/english/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/)
- [Hur man sparar specifika sidor i en Excel‑fil som PDF med Aspose.Cells för .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}