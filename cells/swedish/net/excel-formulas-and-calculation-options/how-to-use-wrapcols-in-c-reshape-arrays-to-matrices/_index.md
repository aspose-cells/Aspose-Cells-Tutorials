---
category: general
date: 2026-05-23
description: Hur man använder WRAPCOLS i C# för att omforma en 1D-array till en 2D-matris.
  Lär dig wrap‑columns‑funktionen, skriv formeln till cellen och konvertera 1D till
  2D enkelt.
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: sv
og_description: Att använda WRAPCOLS i C# gör att du kan omvandla en 1D‑array till
  en 2D‑matris med en enda formel. Följ den här guiden för att skriva formeln i en
  cell och behärska wrap‑columns‑funktionen.
og_title: Hur man använder WRAPCOLS i C# – Omforma arrayer till matriser
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Hur man använder WRAPCOLS i C# – Omforma arrayer till matriser
url: /sv/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så använder du WRAPCOLS i C# – Omforma arrayer till matriser

Har du någonsin undrat **hur man använder WRAPCOLS** när du behöver omvandla en platt lista med siffror till en prydlig tabell? Du är inte ensam—många utvecklare stöter på problem när de försöker konvertera en 1‑dimensionell lista till ett 2‑dimensionellt rutnät utan att skriva mycket loop‑kod. Den goda nyheten? WRAPCOLS‑funktionen (ibland kallad wrap columns‑funktionen) gör det tunga arbetet i en enda rad, och du kan lägga in den direkt i en Excel‑arbetsbok från C#.

I den här handledningen går vi igenom hela processen: från att skapa en arbetsbok, till **write formula to cell**, till **reshape array to matrix**, och slutligen till **convert 1d to 2d** med WRAPCOLS‑formeln. I slutet har du ett återanvändbart kodsnutt som fungerar med vilken numerisk array som helst, och du kommer att förstå varför wrap columns‑funktionen ofta är ett renare alternativ till manuell omformning av arrayer.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar även på .NET Framework 4.6+).  
* **Aspose.Cells for .NET**‑biblioteket (gratis provversion eller licensierad kopia) – det är komponenten som ger oss `Workbook`, `Worksheet` och `Cell`‑objekten som används nedan.  
* En grundläggande förståelse för C#‑syntax—ingen avancerad Excel‑kunskap krävs.

Har du det? Bra—låt oss sätta igång.

![Resulting 2x3 matrix after using WRAPCOLS function in C# – how to use WRAPCOLS](https://example.com/images/wrapcols-result.png "How to use WRAPCOLS – resulting 2x3 matrix")

## Steg 1: Ställ in projektet och lägg till Aspose.Cells

### Varför detta är viktigt

Du skulle kunna försöka skriva din egen matrislogik, men **wrap columns‑funktionen** hanterar redan kantfall som ojämn division och tomma inmatningar. Genom att lägga till Aspose.Cells‑NuGet‑paketet får vi ett rent API för att interagera med Excel‑formler direkt från C#.

```bash
dotnet add package Aspose.Cells
```

*Pro tip:* Om du använder Visual Studio, högerklicka på projektet → **Manage NuGet Packages** → sök efter **Aspose.Cells** och installera den senaste stabila versionen.

## Steg 2: Skapa en ny arbetsbok (eller ladda en befintlig)

Nu när biblioteket är på plats kan vi skapa ett workbook‑objekt. Det är här steget **write formula to cell** kommer att ske.

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

Här har vi skapat en helt ny arbetsbok; du kan också ladda en befintlig fil med `new Workbook("path/to/file.xlsx")` om du behöver infoga matrisen i en förformat mall.

## Steg 3: Infoga WRAPCOLS‑formeln i en cell

### Kärnan i “hur man använder WRAPCOLS”

**WRAPCOLS**‑funktionen tar två argument: en array (eller ett område) och antalet kolumner du vill ha per rad. I vårt fall kommer vi att omforma den bokstavliga arrayen `{1,2,3,4,5,6}` till **2 rader × 3 kolumner**.

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

Observera hur formeln speglar vad du skulle skriva i Excel själv. Genom att placera den i `Cells[0,0]` (cell **A1**) **skrivs formeln till en cell** utan någon extra kod.

## Steg 4: Tvinga beräkning så formeln utvärderas

Aspose.Cells utvärderar inte formler automatiskt om du inte säger åt den. Detta steg säkerställer att arbetsboken faktiskt innehåller den omformade matrisen.

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

Om du hoppar över den här raden kommer cellerna fortfarande att visa formeltexten istället för de beräknade värdena.

## Steg 5: Läs tillbaka resultatet (valfritt, men praktiskt för verifiering)

Du kanske vill bekräfta att operationen **reshape array to matrix** lyckades. Här är en snabb loop som skriver ut det resulterande 2‑x‑3‑rutnätet till konsolen.

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### Förväntad utskrift

```
1   2   3
4   5   6
```

Konsolen visar exakt samma layout som du skulle se i Excel efter att WRAPCOLS‑formeln körts. Det är **convert 1d to 2d**‑transformeringen i praktiken.

## Steg 6: Hantera kantfall – Vad händer om array‑längden inte är en multipel av kolumner?

Om källarrayen har, säg, 7 element och du begär 3 kolumner, kommer WRAPCOLS att skapa den sista raden med de återstående elementen och lämna de övriga cellerna tomma. Här är en snabb justering för att demonstrera:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

Resultat:

```
1   2   3
4   5   6
7       
```

**wrap columns‑funktionen** fyller smidigt den sista raden med tomma celler, så du behöver ingen extra kod för att hantera ojämna storlekar.

## Steg 7: Använda WRAPCOLS med dynamisk data

I riktiga projekt kommer du sällan att hårdkoda arrayen. Istället bygger du en strängrepresentation från en C#‑samling:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

Nu har du **converted 1d to 2d** för vilken längd som helst, och du får fortfarande samma rena matrisutdata. Formeln byggs vid körning, men den underliggande **wrap columns‑funktionen** förblir densamma.

## Vanliga fallgropar och pro‑tips

| Fallgrop | Varför det händer | Lösning |
|---------|-------------------|--------|
| Glömmer `workbook.CalculateFormula()` | Aspose.Cells lämnar formler oberäknade | Anropa alltid metoden efter att du har satt någon formel |
| Använder en icke‑numerisk array‑literal | WRAPCOLS förväntar sig tal eller strängar som kan omvandlas | Säkerställ att litteralen bara innehåller tal (eller citerade strängar) |
| Skriver över befintlig data av misstag | Placera formeln i en cell som redan innehåller data | Välj en tom cell (t.ex. A1) eller rensa området först |
| Refererar inte till rätt arbetsblad‑index | `Worksheets[0]` är det första bladet, men du kan ha lagt till andra | Verifiera `worksheet = workbook.Worksheets["SheetName"];` om det behövs |

## Varför WRAPCOLS slår manuella loopar

* **Readability** – En rad formel ersätter dussintals `for`‑loopar.  
* **Performance** – Excels inbyggda motor är starkt optimerad för array‑formler.  
* **Maintainability** – Framtida utvecklare kan omedelbart se avsikten: “wrap these values into columns”.  
* **Portability** – Samma formel fungerar om du exporterar arbetsboken till Google Sheets eller LibreOffice—ingen C#‑specifik logik behövs.

## Fullt fungerande exempel (klar att kopiera och klistra in)



## Relaterade handledningar

- [Hur man använder Aspose.Cells för .NET för att visa cellområden som datamärkningar i diagram](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [Hur man använder Aspose.Cells för .NET för att gruppera rader och kolumner i Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [Hur man använder Excel IF‑funktionen](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}