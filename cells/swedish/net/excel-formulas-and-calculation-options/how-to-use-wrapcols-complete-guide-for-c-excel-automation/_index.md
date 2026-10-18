---
category: general
date: 2026-07-13
description: Hur man använder WRAPCOLS i C# för att konvertera en array till kolumner,
  tillämpa en matrisformel i Excel och skapa en Excel-arbetsbok programmässigt – allt
  med tydliga steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert array to columns
- apply array formula excel
- create excel workbook programmatically
- evaluate excel formula c#
language: sv
lastmod: 2026-07-13
og_description: Hur du använder WRAPCOLS i C# låter dig snabbt konvertera en array
  till kolumner, tillämpa en arrayformel i Excel‑stil och utvärdera resultatet programatiskt.
og_image_alt: Screenshot showing how to use WRAPCOLS formula in a C# generated Excel
  sheet
og_title: Hur du använder WRAPCOLS i C# – Snabb skapning av Excel‑arbetsbok
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  headline: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  type: TechArticle
- description: How to use WRAPCOLS in C# to convert array to columns, apply array
    formula Excel, and create Excel workbook programmatically—all with clear steps.
  name: How to Use WRAPCOLS – Complete Guide for C# Excel Automation
  steps:
  - name: What if I need more than two columns?
    text: 'Just change the second argument of WRAPCOLS. For example, `=WRAPCOLS({1,2,3,4,5,6},3)`
      would produce three columns:'
  - name: Can I feed a dynamic range instead of a hard‑coded array?
    text: 'Absolutely. You can build the array string programmatically:'
  - name: What about error handling?
    text: 'If the formula is malformed, `Calculate()` will throw a `CellsException`.
      Wrap the calculation in a try/catch block and log the error:'
  - name: Does this work with older Excel versions?
    text: WRAPCOLS was introduced in Excel 365/2021. When you save the file as an
      older `.xls` format, the formula may be lost. Stick to `.xlsx` if you need the
      function to survive outside the C# engine.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hur man använder WRAPCOLS – Komplett guide för C# Excel‑automatisering
url: /sv/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man använder WRAPCOLS – Komplett guide för C# Excel‑automatisering

Har du någonsin undrat **hur man använder WRAPCOLS** när du behöver omvandla en platt lista till en prydlig tabell i en Excel‑fil som genereras från C#? Du är inte ensam. Oavsett om du bygger en rapporteringsmotor, exporterar enkätresultat eller bara leker med data, kan WRAPCOLS‑funktionen omedelbart omforma en array till det antal kolumner du anger.

I den här handledningen går vi igenom hela processen: från **skapa en Excel‑arbetsbok programatiskt** till **tillämpa en array‑formel i Excel‑stil**, och slutligen **utvärdera formeln med C#**. I slutet kommer du att kunna **konvertera en array till kolumner** i en enda kodrad, utan manuella cell‑för‑cell‑manövrar.

> **Vad du får:** ett körbart kodexempel, förklaring av varje steg, tips för vanliga fallgropar och förslag på hur du kan utöka lösningen.

---

## Förutsättningar

Innan vi dyker ner, se till att du har:

- .NET 6.0+ (eller någon nyare .NET‑runtime)
- En C#‑IDE (Visual Studio, Rider eller VS Code)
- **Aspose.Cells for .NET**‑biblioteket (gratis provversion fungerar bra) – det är det enklaste sättet att manipulera Excel‑filer utan att behöva Excel installerat.
- Grundläggande kunskap om C#‑syntax och Excel‑formler.

Om du föredrar ett annat bibliotek (t.ex. EPPlus eller ClosedXML) förblir kärnidén densamma – byt bara ut API‑anropen.

## Steg 1: Ställ in ditt projekt och lägg till Excel‑biblioteket

Först och främst, skapa en ny konsolapp och hämta Aspose.Cells via NuGet:

```bash
dotnet new console -n WrapColsDemo
cd WrapColsDemo
dotnet add package Aspose.Cells
```

> **Proffstips:** Använd flaggan `--version` för att låsa till en känd stabil version, t.ex. `Aspose.Cells 24.9`.

Öppna nu `Program.cs`. Vi börjar med att lägga till de nödvändiga namnrymderna:

```csharp
using System;
using Aspose.Cells;   // Main API for workbook manipulation
```

Att ha biblioteket refererat säkerställer att vi kan **skapa en Excel‑arbetsbok programatiskt** och arbeta med formler.

## Steg 2: Skapa en ny arbetsbok och målcell

Därefter, skapa en ny arbetsbok och välj cellen där WRAPCOLS‑formeln ska placeras. I Excel‑termer är cell **A1** rad 0, kolumn 0.

```csharp
// Step 2.1: Create a new workbook (blank Excel file)
Workbook workbook = new Workbook();

// Step 2.2: Grab the first worksheet (default)
Worksheet sheet = workbook.Worksheets[0];

// Step 2.3: Define the target cell (A1)
Cell targetCell = sheet.Cells[0, 0];
```

Varför gör vi detta? `Workbook`‑objektet är behållaren för alla blad, stilar och beräkningar. Genom att explicit referera till cellen håller vi koden tydlig och undviker “magiska tal” senare.

## Steg 3: Infoga WRAPCOLS‑array‑formeln

Nu kommer hjärtat i handledningen—**hur man använder WRAPCOLS**. Funktionen tar en array och ett kolumnantal, och returnerar ett två‑dimensionellt område. I Excel‑syntax ser det ut så här:

```
=WRAPCOLS({1,2,3,4}, 2)
```

Det säger åt Excel att ordna siffrorna 1‑4 i **2 kolumner**, vilket ger:

| A | B |
|---|---|
| 1 | 3 |
| 2 | 4 |

För att bädda in den formeln från C#:

```csharp
// Step 3: Apply the WRAPCOLS array formula to A1
targetCell.Formula = "=WRAPCOLS({1,2,3,4},2)";
```

Observera att vi använder en **string** som speglar vad du skulle skriva i Excels formelfält. Detta är steget **apply array formula excel**, och Aspose.Cells behandlar den automatiskt som en array‑formel eftersom WRAPCOLS returnerar ett område.

## Steg 4: Tvinga beräkning så formeln utvärderas

Excel beräknar normalt trögt—endast när du öppnar filen. Eftersom vi vill läsa resultatet omedelbart måste vi utlösa en beräkning:

```csharp
// Step 4: Calculate the workbook so the WRAPCOLS formula resolves
workbook.Calculate();
```

Att anropa `Calculate()` är handlingen **evaluate excel formula c#** som tvingar motorn att beräkna varje formel, inklusive vår WRAPCOLS‑array. Utan detta anrop skulle `targetCell.Value` fortfarande vara `null`.

## Steg 5: Hämta och verifiera resultatet

Nu när arbetsboken har beräknats kan vi hämta värdet/värdena från cellerna som arrayen upptog. Den övre vänstra cellen (A1) innehåller det första elementet, medan de intilliggande cellerna innehåller resten. Låt oss läsa hela 2 × 2‑blocket:

```csharp
// Step 5: Read the evaluated values from the resulting range
object[,] result = targetCell.GetArrayValue() as object[,];

// Simple sanity check: print the 2x2 matrix to console
if (result != null)
{
    for (int r = 0; r < result.GetLength(0); r++)
    {
        for (int c = 0; c < result.GetLength(1); c++)
        {
            Console.Write($"{result[r, c]}\t");
        }
        Console.WriteLine();
    }
}
else
{
    Console.WriteLine("No array result was returned.");
}
```

När du kör programmet bör konsolen visa:

```
1   3
2   4
```

Detta resultat bekräftar att vi framgångsrikt **convert array to columns** med WRAPCOLS.

## Steg 6: Spara arbetsboken (valfritt men praktiskt)

Om du vill öppna filen i Excel och se formeln i realtid, spara den bara:

```csharp
// Step 6: Persist the workbook to disk (optional)
workbook.Save("WrapColsDemo.xlsx");
Console.WriteLine("Workbook saved as WrapColsDemo.xlsx");
```

När du öppnar filen visas WRAPCOLS‑formeln i A1 och det fyllda 2‑kolumn‑området under. Detta steg är användbart för felsökning eller för att leverera filen till slutanvändare.

## Vanliga frågor & kantfall

### Vad händer om jag behöver fler än två kolumner?

Ändra bara det andra argumentet i WRAPCOLS. Till exempel, `=WRAPCOLS({1,2,3,4,5,6},3)` skulle producera tre kolumner:

| A | B | C |
|---|---|---|
| 1 | 3 | 5 |
| 2 | 4 | 6 |

Uppdatera C#‑raden därefter:

```csharp
targetCell.Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

### Kan jag mata in ett dynamiskt område istället för en hårdkodad array?

Absolut. Du kan bygga array‑strängen programatiskt:

```csharp
int[] numbers = Enumerable.Range(1, 10).ToArray();
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";
```

På så sätt kan du **apply array formula excel** i farten, perfekt för rapporter med variabel datastorlek.

### Vad händer med felhantering?

Om formeln är felaktig kommer `Calculate()` att kasta ett `CellsException`. Omge beräkningen med ett try/catch‑block och logga felet:

```csharp
try
{
    workbook.Calculate();
}
catch (CellsException ex)
{
    Console.Error.WriteLine($"Formula evaluation failed: {ex.Message}");
}
```

### Fungerar detta med äldre Excel‑versioner?

WRAPCOLS introducerades i Excel 365/2021. När du sparar filen som ett äldre `.xls`‑format kan formeln gå förlorad. Håll dig till `.xlsx` om du behöver att funktionen ska överleva utanför C#‑motorn.

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta, klar‑för‑kopiering‑och‑klistra‑in‑programmet:

```csharp
using System;
using System.Linq;
using Aspose.Cells;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];
            Cell targetCell = sheet.Cells[0, 0];

            // 2️⃣ Build a dynamic array (optional)
            int[] numbers = Enumerable.Range(1, 8).ToArray(); // {1,2,3,4,5,6,7,8}
            string arrayLiteral = "{" + string.Join(",", numbers) + "}";

            // 3️⃣ Apply WRAPCOLS – convert array to columns (2 columns in this case)
            targetCell.Formula = $"=WRAPCOLS({arrayLiteral},2)";

            // 4️⃣ Force calculation – evaluate excel formula c#
            try
            {
                workbook.Calculate();
            }
            catch (CellsException ex)
            {
                Console.Error.WriteLine($"Failed to evaluate formula: {ex.Message}");
                return;
            }

            // 5️⃣ Retrieve the 2‑column result
            object[,] result = targetCell.GetArrayValue() as object[,];
            if (result != null)
            {
                Console.WriteLine("WRAPCOLS result:");
                for (int r = 0; r < result.GetLength(0); r++)
                {
                    for (int c = 0; c < result.GetLength(1); c++)
                    {
                        Console.Write($"{result[r, c]}\t");
                    }
                    Console.WriteLine();
                }
            }

            // 6️⃣ Save the file for visual inspection (optional)
            workbook.Save("WrapColsDemo.xlsx");
            Console.WriteLine("\nWorkbook saved as WrapColsDemo.xlsx");
        }
    }
}
```

Kör `dotnet run` så bör du se matrisen skriven, följt av en bekräftelse på att `.xlsx`‑filen finns.

## Sammanfattning & nästa steg

Vi har gått igenom **how to use WRAPCOLS** för att **convert array to columns**, demonstrerat **apply array formula excel**‑tekniken från C#, tvingat en beräkning för att **evaluate excel formula c#**, och sparat resultatet för vidare konsumtion.

Om du vill ha mer:

- **Dynamiska kolumnantal:** låt kolumnnumret vara en användar‑inmatad variabel.
- **Formatera utskriften:** applicera teckensnitt, ramar eller villkorsstyrd formatering via Aspose.Cells efter beräkningen.
- **Kombinera med andra funktioner:** nästla WRAPCOLS i `LET` eller `FILTER`

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Aspose.Cells .NET: Hur man skapar och formaterar Excel‑arbetsböcker programatiskt](/cells/english/net/formatting/aspose-cells-net-create-style-excel-workbooks/)
- [Hur man skapar och sparar en Excel‑arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Hur man skapar arbetsboks‑omfattande namngivna områden i Excel med Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}