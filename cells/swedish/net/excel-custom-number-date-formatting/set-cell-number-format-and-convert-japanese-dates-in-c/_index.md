---
category: general
date: 2026-11-19
description: Ställ in cellens talformat i C# och lär dig hur du använder Exceldatumformat
  för japanska era‑datum, vilket möjliggör pålitlig C# Excel‑datumkonvertering.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: sv
lastmod: 2026-11-19
og_description: Ställ in cellens talformat i C# och tillämpa Excel-datumformat på
  japanska era-datum. Följ den här kompletta guiden för exakt C# Excel-datumkonvertering.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: Ställ in cellens talformat och konvertera japanska datum i C# – steg‑för‑steg‑guide
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
title: Ställ in cellens talformat och konvertera japanska datum i C#
url: /sv/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in cellens talformat och konvertera japanska datum i C#

Om du behöver **ställa in cellens talformat** i ett C#‑Excel‑automatiseringsprojekt visar den här guiden hur du **tillämpar Excel‑datumformat** och utför **C#‑Excel‑datumkonvertering** för japanska era‑datum. Du får ett komplett, körbart exempel som konverterar en Reiwa‑era‑sträng (t.ex. `R3/04/01`) till det gregorianska datumet `2021‑04‑01`.

## Vad du kommer att lära dig

* Hur du skapar en arbetsbok och får åtkomst till dess första kalkylblad.  
* Hur du **ställer in cellens talformat** så att Excel behandlar värdet som ett datum.  
* Hur du **tillämpar Excel‑datumformat** som känner igen japanska era‑strängar.  
* Hur du triggar **C#‑Excel‑datumkonvertering** genom att omberäkna formler.  
* Förväntad utdata och felsökningstips för kantfall.

**Förutsättningar**

* .NET 6 eller senare (koden fungerar också med .NET Framework 4.6+).  
* Aspose.Cells för .NET 2024 eller nyare – installera via NuGet: `dotnet add package Aspose.Cells`.  
* Grundläggande kunskap om C# och Excel‑datumhantering.

> **Proffstips:** Aspose.Cells fungerar utan att Microsoft Office är installerat, vilket gör det idealiskt för server‑sidig automatisering.

## Ställ in cellens talformat med Aspose.Cells i C#

Det första steget är att berätta för Excel att cellen innehåller ett datum. Excel lagrar datum som serienummer, så vi måste tillämpa ett inbyggt datum‑talformat (ID 14) på mål‑cellen.

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

### Varför detta fungerar

* `Style.Number = 14` motsvarar Excels *Kort datum*‑format (`mm/dd/yyyy` som standard).  
* När cellen innehåller en japansk era‑sträng som `R3/04/01` känner Aspose.Cells interna parser igen eran och konverterar den till motsvarande gregorianskt serienummer under `CalculateFormula()`.  
* Efter beräkningen returnerar `StringValue` det formaterade gregorianska datumet.

## Tillämpa Excel‑datumformat för japanska era‑datum

Om du vill att cellen ska visa den japanska eran istället för det gregorianska datumet kan du använda ett anpassat talformat som inkluderar era‑koden. Detta demonstrerar **apply excel date format**‑kapaciteten.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` tvingar den japanska lokalen.  
* `ggg` representerar erans namn (t.ex. `R` för Reiwa).  
* Att lägga till bokstavliga tecken (`年`, `月`, `日`) skapar en bekant japansk datumlayout.

### När du ska använda ett anpassat format

* Rapporter avsedda för japanska mottagare.  
* När du behöver bevara den ursprungliga erainformationen för juridiska dokument.  
* I instrumentpaneler där både gregorianska och era‑datum visas sida‑vid‑sida.

## C#‑Excel‑datumkonvertering – hantera japanska era‑datum

**c# excel date conversion**‑processen kan delas in i tre logiska delar:

1. **Parse the era string** – Aspose.Cells identifierar automatiskt `R` (Reiwa), `H` (Heisei), `S` (Showa) osv.  
2. **Convert to a serial number** – Excel lagrar datum som dagar sedan 1899‑12‑30.  
3. **Format the serial number** – antingen med ett inbyggt format (ID 14) eller ett anpassat japanskt format.

### Fullständigt end‑to‑end‑exempel

Nedan är ett självständigt program som demonstrerar både de gregorianska och era‑utdata i ett körning.

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

**Förväntad konsolutskrift**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Kantfall & vanliga fallgropar

| Situation                              | Vad du bör hålla utkik efter                                   | Fix / Rekommendation                                   |
|----------------------------------------|---------------------------------------------------------------|--------------------------------------------------------|
| Tom eller felaktig era‑sträng          | `PutValue` lagrar den bokstavliga texten; konverteringen misslyckas | Validera indata med ett reguljärt uttryck innan du skriver till cellen. |
| Lokalmismatch                         | Anpassat format visar västerländska siffror istället för japanska tecken | Säkerställ att `Custom`‑formatet inkluderar `[$-ja-JP]` eller sätt `Workbook.Settings.CultureInfo` till `ja-JP`. |
| Arbetsboken innehåller formler som refererar till datumcellen | Omberäkning kan skriva över formelresultat | Anropa `CalculateFormula` **efter** alla formateringssteg, eller använd `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` om du vill hoppa över fel. |
| Använder äldre versioner av Aspose.Cells | Stöd för japanska era‑datum lades till i 2022 Q3               | Uppgradera till den senaste NuGet‑paketet.            |

## Testa lösningen

1. **Kör programmet** från Visual Studio eller `dotnet run`.  
2. Verifiera att konsolen skriver ut det gregorianska datumet `2021‑04‑01` och era‑strängen `R3年04月01日`.  
3. Öppna den genererade arbetsboken (om du lägger till `wb.Save("Demo.xlsx");`) i Microsoft Excel för att se samma formatering tillämpad på cellerna.

### Automatiseringstips

Om du behöver bearbeta ett stort intervall av era‑datum (t.ex. kolumn A innehåller många japanska datum), omslut konverteringslogiken i en loop:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Detta tillvägagångssätt håller **set cell number format**‑operationen snabb och minnes‑effektiv.

## Slutsats

Du vet nu hur du **ställer in cellens talformat** i C# med Aspose.Cells, hur du **tillämpar Excel‑datumformat** för japanska era‑strängar, och hur du utför pålitlig **C#‑Excel‑datumkonvertering** från era till gregorianska datum. Den kompletta, körbara koden demonstrerar båda utdata och belyser vanliga kantfall.  

**Nästa steg**

* Utforska andra inbyggda format‑ID:n


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [set excel date format in C# – Complete Step‑by‑Step Guide](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [How to apply number format excel with Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [How to apply a custom number format excel in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}