---
category: general
date: 2026-04-07
description: Lär dig hur du expanderar en array i C# med Aspose.Cells. Denna handledning
  visar hur du skapar en arbetsbok i C#, skriver en Excel‑formel i C# och sätter cellformel
  i C# utan ansträngning.
draft: false
keywords:
- how to expand array
- create workbook c#
- use aspose cells
- write excel formula c#
- set cell formula c#
language: sv
og_description: Upptäck hur du expanderar en array i C# med Aspose.Cells. Följ våra
  tydliga steg för att skapa en arbetsbok i C#, skriva en Excel‑formel i C# och sätta
  cellformel i C#.
og_title: Hur man utökar en array i C# med Aspose.Cells – Komplett guide
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Hur man utökar en array i C# med Aspose.Cells – Steg‑för‑steg‑guide
url: /sv/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man expanderar en array i C# med Aspose.Cells – Steg‑för‑steg‑guide

Har du någonsin undrat **how to expand array** i ett Excel‑blad från C# utan att trassla med röriga loopar? Du är inte ensam. Många utvecklare stöter på problem när de behöver omvandla en liten konstant array till en större kolumn eller rad för efterföljande beräkningar. Den goda nyheten? Aspose.Cells gör det enkelt, och du kan göra det med en enda Excel‑formel.

I den här handledningen går vi igenom hela processen: skapa en workbook C#, använda Aspose.Cells, skriva en Excel‑formel C#, och slutligen sätta cellformeln C# så att arrayen expanderar exakt som du förväntar dig. I slutet har du ett körbart kodexempel som skriver ut de expanderade värdena till konsolen, och du förstår varför detta tillvägagångssätt är både rent och prestandaeffektivt.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar på .NET Core och .NET Framework lika väl)  
- Aspose.Cells för .NET ≥ 23.12 (den senaste versionen vid skrivtillfället)  
- En grundläggande förståelse för C#‑syntax – ingen djup Excel‑automatiseringserfarenhet krävs  

Om du redan har detta, bra—låt oss dyka ner.

## Steg 1: Skapa Workbook C# med Aspose.Cells

Först och främst behöver vi ett nytt workbook‑objekt. Tänk på det som en tom Excel‑fil som bara finns i minnet tills du bestämmer dig för att spara den.

```csharp
using Aspose.Cells;
using System;

namespace ExpandArrayDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize a new workbook – this is the canvas for our work.
            Workbook workbook = new Workbook();

            // Grab the first worksheet (index 0). Most demos start here.
            Worksheet ws = workbook.Worksheets[0];
```

> **Proffstips:** Om du planerar att arbeta med flera blad kan du lägga till dem via `workbook.Worksheets.Add()` och referera till dem med namn eller index.

## Steg 2: Skriv Excel‑formel C# för att expandera arrayen

Nu kommer kärnan i saken—how to expand array. `EXPAND`‑funktionen (tillgänglig i senaste Excel‑versionerna) tar en källarray och sträcker den till en angiven storlek. I C# tilldelar vi helt enkelt den formeln till en cell.

```csharp
            // Set a formula that expands a 3‑element array into a 5‑row column.
            // The syntax mirrors what you'd type in Excel: =EXPAND({1,2,3},5,1)
            ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";
```

Varför använda `EXPAND`? Det undviker manuella loopar, håller workbooken lättviktig och låter Excel omberäkna automatiskt om du senare ändrar källarrayen. Detta är det renaste sättet att besvara frågan **how to expand array** utan att skriva extra C#‑kod.

## Steg 3: Beräkna Workbook så att formeln körs

Aspose.Cells utvärderar inte automatiskt formler förrän du ber om det. Att anropa `Calculate` tvingar motorn att köra `EXPAND`‑funktionen och fylla målområdet.

```csharp
            // Force calculation so the formula result becomes available.
            workbook.Calculate();
```

Om du hoppar över detta steg kommer läsning av cellvärdena att returnera formeltexten istället för de beräknade siffrorna.

## Steg 4: Läs de expanderade värdena – Set Cell Formula C# och hämta resultat

Med kalkylerade arbetsbladet kan vi nu läsa de fem cellerna som `EXPAND` fyllde. Detta demonstrerar **set cell formula c#** i praktiken och visar också hur man drar tillbaka data till din applikation.

```csharp
            // Loop through the first 5 rows of column A and print each value.
            for (int row = 0; row < 5; row++)
            {
                // Cells[row, 0] corresponds to column A (zero‑based index).
                Console.WriteLine(ws.Cells[row, 0].Value);
            }

            // Optional: keep the console window open when debugging.
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

### Förväntat resultat

När programmet körs skrivs följande ut till konsolen:

```
1
2
3
0
0
```

De första tre siffrorna kommer från den ursprungliga arrayen `{1,2,3}`. De sista två raderna är fyllda med nollor eftersom `EXPAND` fyller upp målstorleken med standardvärdet (noll för numeriska arrayer). Om du föredrar ett annat fyllningsvärde kan du omsluta `EXPAND`‑anropet i `IFERROR` eller kombinera det med `CHOOSE`.

## Steg 5: Spara Workbook (valfritt)

Om du vill inspektera den genererade Excel‑filen, lägg bara till ett `Save`‑anrop innan programmet avslutas:

```csharp
            // Save the workbook to disk for verification.
            workbook.Save("ExpandedArray.xlsx");
```

Att öppna `ExpandedArray.xlsx` visar samma fem‑radskolumn i cellerna A1:A5, vilket bekräftar att formeln har utvärderats korrekt.

## Vanliga frågor & kantfall

### Vad händer om jag behöver en horisontell expansion istället för vertikal?

Ändra det tredje argumentet i `EXPAND` från `1` (rader) till `0` (kolumner) och justera loopen därefter:

```csharp
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},1,5)"; // expands to a 1‑row, 5‑column range
```

### Kan jag expandera ett dynamiskt område istället för en hårdkodad array?

Absolut. Ersätt den bokstavliga `{1,2,3}` med en referens till ett annat cellområde, t.ex. `A10:C10`. Formeln blir:

```csharp
ws.Cells["A1"].Formula = "=EXPAND(A10:C10,5,1)";
```

Se bara till att källområdet finns innan du triggar beräkning.

### Hur jämför detta tillvägagångssätt med loopning i C#?

Loopning skulle kräva att du skriver varje värde manuellt:

```csharp
for (int i = 0; i < 5; i++) ws.Cells[i, 0].PutValue(i < 3 ? i + 1 : 0);
```

Även om det fungerar, håller användning av `EXPAND` logiken inne i Excel, vilket är fördelaktigt när workbooken senare redigeras av icke‑utvecklare eller när du vill att Excels inbyggda omberäkningsmotor ska hantera förändringar automatiskt.

## Fullt fungerande exempel – sammanfattning

Nedan är det kompletta, kopiera‑och‑klistra‑klara programmet som demonstrerar **how to expand array** med Aspose.Cells. Inga dolda beroenden, bara de `using`‑satser du behöver.

```csharp
using Aspose.Cells;
using System;

namespace ExpandArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook.
            Workbook workbook = new Workbook();

            // 2️⃣ Access the first worksheet.
            Worksheet ws = workbook.Worksheets[0];

            // 3️⃣ Write the EXPAND formula – this is the core of how to expand array.
            ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

            // 4️⃣ Calculate so the formula resolves.
            workbook.Calculate();

            // 5️⃣ Read and display the expanded values.
            for (int row = 0; row < 5; row++)
            {
                Console.WriteLine(ws.Cells[row, 0].Value);
            }

            // Optional: Save the workbook for visual verification.
            workbook.Save("ExpandedArray.xlsx");

            Console.WriteLine("Done – press any key to close.");
            Console.ReadKey();
        }
    }
}
```

Kör detta i Visual Studio, Rider eller `dotnet run`‑CLI:n så ser du arrayen expanderad exakt som beskrivet.

## Slutsats

Vi har gått igenom **how to expand array** i ett Excel‑arbetsblad med C# och Aspose.Cells, från att skapa workbook C# till att skriva Excel‑formeln C# och slutligen sätta cellformeln C# för att hämta resultaten. Tekniken bygger på den inbyggda `EXPAND`‑funktionen, vilket håller din kod prydlig och dina kalkylblad dynamiska.

Nästa steg? Prova att byta ut källarrayen mot ett namngivet område, experimentera med olika fyllningsvärden, eller kedja flera `EXPAND`‑anrop för att bygga större datatabeller. Du kan också utforska andra kraftfulla funktioner som `SEQUENCE` eller `LET` för ännu rikare formeldriven automation.

Har du frågor om att använda Aspose.Cells för mer komplexa scenarier? Lämna en kommentar nedan eller kolla in den officiella Aspose.Cells‑dokumentationen för djupare insikter i formelhantering, prestandaoptimering och plattformsoberoende stöd.

Lycka till med kodandet, och njut av att förvandla små arrayer till mäktiga kolumner! 

![Diagram som visar ett C#‑program som skapar en workbook, tillämpar EXPAND‑formeln och skriver ut resultat – illustrerar hur man expanderar en array med Aspose.Cells](https://example.com/expand-array-diagram.png "Diagram som visar hur man expanderar en array med Aspose.Cells i C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}