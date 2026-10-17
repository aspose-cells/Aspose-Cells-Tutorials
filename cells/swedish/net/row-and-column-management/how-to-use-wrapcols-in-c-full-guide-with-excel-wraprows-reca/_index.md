---
category: general
date: 2026-06-27
description: Hur man använder wrapcols och wrap rows i Excel i C#. Lär dig att skapa
  en Excel‑arbetsbok i C# och omberäkna Excel‑formler med ett steg‑för‑steg‑exempel.
draft: false
keywords:
- how to use wrapcols
- wrap rows excel
- wrap columns excel
- recalculate excel formulas
- create excel workbook c#
language: sv
og_description: Hur man använder wrapcols och wrap rows i Excel med C#. Denna guide
  visar hur man skapar en Excel‑arbetsbok i C# och omräknar Excel‑formler på några
  minuter.
og_title: Hur man använder wrapcols i C# – Komplett guide för Excel-omslag
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  headline: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate
    Formulas
  type: TechArticle
- description: how to use wrapcols and wrap rows excel in C#. Learn to create excel
    workbook c# and recalculate excel formulas with a step‑by‑step example.
  name: how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas
  steps:
  - name: Expected Result
    text: '| A | B | C | |---|---|---| | 1 | A | 2 | | 2 | B | 3 | | 3 | C | 4 | |
      4 | D | 5 | | 5 | E | 6 | | 6 | F | 7 | | 7 | G | 8 | | 8 | H | 9 | | 9 | I
      | |'
  - name: What if the source range is empty?
    text: Both `WRAPCOLS` and `WRAPROWS` will simply return an empty array, resulting
      in a blank cell. It’s safe to call the functions even when you’re not sure about
      data presence.
  - name: Can I wrap more than one range at a time?
    text: Yes—just place additional formulas in other cells. Each formula works independently,
      so you could have `WRAPCOLS` in D1, `WRAPROWS` in E1, etc.
  - name: How does this differ from a simple copy‑paste transpose?
    text: '`WRAPCOLS`/`WRAPROWS` handle *pagination* automatically. If you have 20
      items and ask for 3 columns, the function creates the necessary number of rows
      (7 in this case) without you calculating the dimensions manually.'
  - name: Does the library support dynamic array formulas (Excel 365)?
    text: Aspose.Cells fully supports dynamic array functions, including `WRAPCOLS`
      and `WRAPROWS`. The calculation engine will spill the results just like native
      Excel.
  - name: What about performance on large datasets?
    text: For millions of rows, consider batching the calculation (`workbook.CalculateFormula(FormulaCalculationOptions)`)
      or disabling automatic calculation while you insert formulas, then re‑enable
      it before saving.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: hur man använder wrapcols i C# – fullständig guide med Excel WRAPROWS & omberäkna
  formler
url: /sv/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hur man använder wrapcols i C# – Fullständig guide med Excel WRAPROWS & Recalculate Formulas

Har du någonsin funderat **hur man använder wrapcols** när du behöver omforma en lång lista till ett prydligt rutnät? Kanske har du provat den manuella kopiera‑klistra‑tricket, men det är långsamt, felbenäget och ärligt talat en plåga. Den goda nyheten? Excels `WRAPCOLS` (och dess syster `WRAPROWS`) kan göra det tunga arbetet åt dig—*och* du kan styra dem från C#‑kod.

I den här handledningen går vi igenom hur du skapar en Excel‑arbetsbok i C#, applicerar `WRAPCOLS` och `WRAPROWS`, och slutligen **recalculate excel formulas** så att den omslagna datan visas omedelbart. När du är klar har du ett färdigt kodexempel som du kan klistra in i vilket .NET‑projekt som helst.

## Vad du kommer att lära dig

- Hur du **create excel workbook c#** med hjälp av Aspose.Cells‑biblioteket (ingen COM‑interop behövs).  
- Den exakta syntaxen för `WRAPCOLS`‑funktionen och hur den skiljer sig från `WRAPROWS`.  
- Varför du måste **recalculate excel formulas** efter att du har infogat funktionerna, och hur du gör det på ett effektivt sätt.  
- Ett komplett, körbart exempel som du kan kopiera‑klistra och se resultatet i en `.xlsx`‑fil.  

**Förutsättningar** – Du behöver .NET 6+ (eller .NET Framework 4.7+), Visual Studio 2022 eller någon annan IDE du föredrar, samt Aspose.Cells for .NET NuGet‑paketet. Om du är ny på Aspose.Cells, oroa dig inte; stegen är enkla och fullt förklarade.

---

## Steg 1: Ställ in projektet och installera Aspose.Cells

För att börja, skapa ett nytt konsolprojekt:

```bash
dotnet new console -n WrapDemo
cd WrapDemo
dotnet add package Aspose.Cells
```

> **Proffstips:** Om du använder Visual Studio, högerklicka på projektet → *Manage NuGet Packages* → sök efter **Aspose.Cells** och installera det.

Biblioteket ger oss klasserna `Workbook`, `Worksheet` och `Cell` som vi kommer att behöva för resten av handledningen.

## Steg 2: Skapa en Excel‑arbetsbok och fyll i exempeldata

Nu skapar vi en arbetsbok, hämtar det första kalkylbladet och fyller kolumn **A** och **B** med exempelnummer. Denna data kommer senare att omslutas till kolumner och rader.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Step 2‑1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2‑2: Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate A2:A10 with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate B2:B10 with letters A‑I (just for variety)
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // The rest of the steps follow…
```

> **Varför detta är viktigt:** Deterministisk data låter dig verifiera att `WRAPCOLS` och `WRAPROWS` gör exakt det du förväntar dig.

## Steg 3: Applicera `WRAPCOLS`‑funktionen – **how to use wrapcols**

`WRAPCOLS` tar ett endimensionellt område och sprider det över ett angivet antal kolumner, och lägger automatiskt till nya rader vid behov. Här är den exakta formeln vi injicerar i cell **A1**:

```csharp
        // Step 3: Insert WRAPCOLS formula – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";
```

> **Förklaring:** Det andra argumentet (`3`) säger åt Excel att skapa tre kolumner per rad. Så de första tre värdena (1, 2, 3) hamnar i A1:C1, de nästa tre (4, 5, 6) i A2:C2, och de återstående värdena fyller nästa rad.

## Steg 4: Applicera `WRAPROWS`‑funktionen – wrap rows excel

`WRAPROWS` gör motsatsen: den tar ett vertikalt område och ordnar det i ett bestämt antal rader per kolumn. Vi placerar denna formel i **B1**:

```csharp
        // Step 4: Insert WRAPROWS formula – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";
```

> **Förklaring:** Med `2` rader per kolumn går värdena “A, B” in i B1:B2, “C, D” in i C1:C2, och så vidare. Funktionen expanderar automatiskt bladet horisontellt.

## Steg 5: Återberäkna alla formler – **recalculate excel formulas**

När du sätter en formel programatiskt kommer Excel inte att beräkna resultatet förrän arbetsboken öppnas eller du uttryckligen ber biblioteket att utvärdera den. Det är här **recalculate excel formulas** kommer in:

```csharp
        // Step 5: Force calculation so the wrapped data appears immediately
        workbook.CalculateFormula();
```

> **Varför du behöver detta:** Utan att anropa `CalculateFormula()` kommer cellerna att visa den råa `=WRAPCOLS(...)`‑texten när du öppnar filen, vilket gör handledningens syfte meningslöst.

## Steg 6: Spara arbetsboken och verifiera resultatet

Till sist skriver vi arbetsboken till disk. Du kan öppna den resulterande filen i Excel för att se den omslagna layouten.

```csharp
        // Step 6: Save the workbook (adjust the path as needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see wrapcols and wraprows in action.");
    }
}
```

### Förväntat resultat

| A | B | C |
|---|---|---|
| 1 | A | 2 |
| 2 | B | 3 |
| 3 | C | 4 |
| 4 | D | 5 |
| 5 | E | 6 |
| 6 | F | 7 |
| 7 | G | 8 |
| 8 | H | 9 |
| 9 | I |   |

- **Kolumnerna A‑C** fylls av `WRAPCOLS`‑anropet (tre kolumner per rad).  
- **Raderna B‑I** fylls av `WRAPROWS`‑anropet (två rader per kolumn).  

Öppna `output.xlsx` så ser du exakt den layout som visas ovan. Om siffrorna inte stämmer, dubbelkolla formelsträngarna och se till att `CalculateFormula()` anropades.

---

## Vanliga frågor & kantfall

### Vad händer om källområdet är tomt?
Både `WRAPCOLS` och `WRAPROWS` returnerar helt enkelt en tom array, vilket resulterar i en tom cell. Det är säkert att anropa funktionerna även när du är osäker på om data finns.

### Kan jag omsluta mer än ett område åt gången?
Ja—placera bara ytterligare formler i andra celler. Varje formel fungerar oberoende, så du kan ha `WRAPCOLS` i D1, `WRAPROWS` i E1 osv.

### Hur skiljer sig detta från en enkel kopiera‑klistra‑transponering?
`WRAPCOLS`/`WRAPROWS` hanterar *paginering* automatiskt. Om du har 20 objekt och begär 3 kolumner skapar funktionen det nödvändiga antalet rader (7 i detta fall) utan att du själv måste räkna ut dimensionerna.

### Stöder biblioteket dynamiska array‑formler (Excel 365)?
Aspose.Cells har fullt stöd för dynamiska array‑funktioner, inklusive `WRAPCOLS` och `WRAPROWS`. Beräkningsmotorn spillar resultaten precis som i native Excel.

### Vad gäller prestanda för stora datamängder?
För miljontals rader, överväg att batcha beräkningen (`workbook.CalculateFormula(FormulaCalculationOptions)`) eller inaktivera automatisk beräkning medan du infogar formler, och återaktivera den innan du sparar.

---

## Fullständig källkod (Klar att köra)

Nedan är hela programmet—kopiera det till `Program.cs` och tryck **F5**.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate column A (A2:A10) with numbers 1‑9
        for (int i = 2; i <= 10; i++)
        {
            worksheet.Cells[$"A{i}"].PutValue(i - 1);
        }

        // Populate column B (B2:B10) with letters A‑I
        char letter = 'A';
        for (int i = 2; i <= 10; i++, letter++)
        {
            worksheet.Cells[$"B{i}"].PutValue(letter.ToString());
        }

        // Apply WRAPCOLS – wrap A2:A10 into 3 columns per row
        worksheet.Cells["A1"].Formula = "=WRAPCOLS(A2:A10, 3)";

        // Apply WRAPROWS – wrap B2:B10 into 2 rows per column
        worksheet.Cells["B1"].Formula = "=WRAPROWS(B2:B10, 2)";

        // Recalculate all formulas so the wrapped data appears
        workbook.CalculateFormula();

        // Save the workbook (adjust the folder if needed)
        string outputPath = "output.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the wrapped results.");
    }
}
```

---

## Slutsats

Du vet nu **hur man använder wrapcols** (och dess motsvarighet `WRAPROWS`) från C# för att omforma data i ett Excel‑ark, och du förstår varför **recalculate excel formulas** är ett obligatoriskt steg. Detta mönster—*create excel workbook c# → insert WRAP functions → recalculate*—är en solid grund för alla rapporterings‑ eller datapresentation‑uppgifter som kräver dynamiska kolumn‑ eller radlayouter.

Vad blir nästa steg? Prova att experimentera med:

- Olika kolumn‑/radantal (`WRAPCOLS(..., 5)` eller `WRAPROWS(..., 4)`).  
- Kombinera `WRAPCOLS` med andra dynamiska array‑funktioner som `FILTER` eller `SORT`.  
- Exportera arbetsboken till PDF med `workbook.Save("report.pdf", SaveFormat.Pdf)`.

Känn dig fri att justera exemplet, lägga till formatering, eller integrera det i en större automatiseringspipeline. Om du stöter på problem, lämna en kommentar nedan—lycka till med kodandet!

![Diagram som visar hur wrapcols och wraprows omvandlar en enda kolumn till ett rutnät – how to use wrapcols example](wrapcols-wraprows-diagram.png "how to use wrapcols example")


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger vidare på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man använder Aspose.Cells för .NET för att gruppera rader och kolumner i Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Hur man döljer rader och kolumner i Excel med Aspose.Cells .NET: En omfattande guide](/cells/english/net/range-management/aspose-cells-net-hide-rows-columns-excel/)
- [Hur man skapar och konfigurerar Excel‑arbetsböcker med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}