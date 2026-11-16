---
category: general
date: 2026-11-16
description: Lär dig hur du expanderar en matris i Excel med Aspose.Cells, dynamiska
  matrisfunktioner och en lambda‑reducerare, och sedan skriver du Excel‑filen från
  C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: sv
lastmod: 2026-11-16
og_description: Hur man expanderar en matris i Excel med Aspose.Cells, dynamiska matrisfunktioner
  och en lambda‑reducerare. Följ det kompletta C#‑exemplet för att skriva Excel‑filen.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Hur man utökar en matris i Excel med Aspose.Cells – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man utökar en matris i Excel med Aspose.Cells
url: /sv/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man expanderar array i Excel med Aspose.Cells

Om du behöver **how to expand array** i ett Excel‑blad från C#, visar den här handledningen de exakta stegen. Du kommer att skapa en Excel‑arbetsbok, använda dynamiska array‑funktioner som `EXPAND` och `REDUCE`, tillämpa en **lambda**‑ackumulator och slutligen **write Excel file** till disk. Metoden fungerar med Aspose.Cells 23.10 eller senare och kräver ingen manuell Excel‑installation.

I slutet av den här guiden kommer du att ha en fullt fungerande `ExpandReduceDemo.xlsx` som demonstrerar kraften i dynamiska array‑formler i ett programmeringssammanhang.

## Vad du behöver

- .NET 6.0 (eller någon .NET‑version som stöds av Aspose.Cells)
- Aspose.Cells for .NET‑paketet (`dotnet add package Aspose.Cells`)
- En kodredigerare eller IDE (Visual Studio, VS Code, Rider, etc.)

Ingen extra COM‑interop eller Office‑installation krävs eftersom Aspose.Cells hanterar filformatet internt.

## Steg 1: Skapa Excel‑arbetsbok

Den första uppgiften är att **create excel workbook** i minnet. Aspose.Cells tillhandahåller `Workbook`‑klassen, som representerar en hel XLSX‑fil.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Why this matters:** Att instansiera en `Workbook` ger dig en ren arbetsyta. Standard‑arbetsbladet är redan förberett, så du behöver inte lägga till ett manuellt om du inte vill ha flera blad.

## Steg 2: Infoga en vertikal array‑konstant

Excels dynamiska array‑motor kan arbeta med bokstavliga array‑konstanter. Vi placerar den vertikala arrayen `{1;2;3;4;5}` i cell **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tip:** Semikolon (`;`) separerar rader i konstanten, medan ett kommatecken (`,`) skulle separera kolumner. Detta speglar Excels egen syntax.

## Steg 3: Expandera arrayen till en matris

Nu besvarar vi huvudfrågan – **how to expand array** – med hjälp av `EXPAND`‑funktionen. Formeln expanderar den enkla kolumn‑arrayen till en 5‑rad × 2‑kolumn‑matris, med start i **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Why EXPAND?** `EXPAND(source, rows, cols)` tvingar källområdet att fylla den angivna storleken, med ifyllning av tomma celler om det behövs. Det är det mest läsbara sättet att generera en större matris från en enda array.

## Steg 4: Reducera matrisen med en lambda‑ackumulator

`REDUCE`‑funktionen itererar över ett område och aggregerar värden med en **lambda**‑uttryck. Här summerar vi varje kolumnvärde till en enda kolumn och placerar resultatet i **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **How to use lambda:** `LAMBDA(acc, val, acc+val)` tar emot den aktuella ackumulatorn (`acc`) och nästa cellvärde (`val`). Den returnerar den nya ackumulatorn, vilket effektivt utför en löpande summa. Detta demonstrerar **how to use lambda** i Excel‑formler från kod.

## Steg 5: Beräkna formler så resultaten visas

Aspose.Cells utvärderar inte automatiskt formler när du sätter dem. Att anropa `CalculateFormula` tvingar motorn att beräkna varje formel i arbetsboken.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Note:** Om du öppnar den genererade filen i Excel kommer värdena redan att vara synliga eftersom de har för‑beräknats.

## Steg 6: Skriv Excel‑fil till disk

Slutligen, **write excel file** med `Save`‑metoden. Välj en mapp som du har skrivbehörighet till.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Förväntat resultat

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Column B** och **C** innehåller den 5 × 2‑matris som produceras av `EXPAND`.
- **Cell D1** visar `15`, summan av alla tal, beräknad av `REDUCE` + **lambda**‑formeln.

## Vanliga frågor och edge cases

- **Can I expand to more columns than the source provides?**  
  Ja. `EXPAND` fyller saknade kolumner med tomma celler. Detsamma gäller rader.

- **What if the source array is horizontal (`{1,2,3,4,5}`)?**  
  `EXPAND` kommer att behandla källan som en enda rad; du kan fortfarande ange rader och kolumner för att omforma den.

- **Does `REDUCE` work with non‑numeric data?**  
  Lambda‑uttrycket måste returnera ett värde som är kompatibelt med ackumulatorns typ. För textkonkatenering kan du använda `LAMBDA(acc, val, acc & val)`.

- **Do I need to call `CalculateFormula` for every change?**  
  Endast när du behöver de beräknade värdena innan du sparar. Excel kommer att omberäkna vid öppning om du hoppar över det.

## Pro‑tips

- **Performance:** För stora arbetsböcker, anropa `workbook.CalculateFormula` en gång efter att alla formler har satts, snarare än efter varje cell.
- **Version safety:** `EXPAND` och `REDUCE` finns i Excel 365 och senare. Aspose.Cells implementerar dem oavsett mål‑Excel‑version eftersom beräkningsmotorn är inbyggd.
- **Debugging formulas:** Använd `sheet.Cells["B1"].Formula` för att läsa tillbaka den exakta strängen du satte; detta hjälper när du bygger formler dynamiskt.

## Slutsats

Du vet nu **how to expand array** i Excel med Aspose.Cells, utnyttja **dynamic array functions**, tillämpa en **lambda** med `REDUCE` och **write excel file** från C#. Detta helhets‑exempel kan anpassas till mer komplexa datatransformationer, såsom matris‑transponering, kumulativa summor eller egna aggregationer.

---

*Nästa steg:*  
- Utforska andra dynamiska funktioner som `FILTER`, `SORT` och `UNIQUE`.  
- Kombinera flera `LAMBDA`‑uttryck för att bygga återanvändbara användardefinierade funktioner.  
- Integrera arbetsboks‑genereringen i ASP.NET Core‑API:er för rapportgenerering i realtid.

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Hur man skapar Excel‑arbetsbok C# med en dynamisk array‑formel](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Hur man expanderar en array i Excel och fyller i en mall](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Hur man expanderar en array i C# med Aspose.Cells – Steg‑för‑steg‑guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}