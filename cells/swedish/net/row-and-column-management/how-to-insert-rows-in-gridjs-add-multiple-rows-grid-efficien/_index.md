---
category: general
date: 2026-03-29
description: Lär dig hur du snabbt kan infoga rader i GridJs. Den här guiden täcker
  också hur du lägger till rader och lägger till flera rader i ett rutnät med en batchoperation.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: sv
og_description: Lär dig hur du snabbt kan infoga rader i GridJs. Den här guiden visar
  hur du lägger till rader, lägger till flera rader i ett rutnät och hanterar stora
  batchinfogningar.
og_title: Hur man infogar rader i GridJs – Lägg till flera rader i rutnätet effektivt
tags:
- GridJs
- C#
- data‑grid
title: Hur man infogar rader i GridJs – Lägg till flera rader i rutnätet effektivt
url: /sv/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man infogar rader i GridJs – Lägg till flera rader i rutnätet effektivt

Har du någonsin undrat **hur man infogar rader** i en enorm GridJs‑tabell utan att frysa UI‑t? Kanske har du stött på problem när du försöker **lägga till rader** en efter en och prestandan bara faller sönder. Den goda nyheten är att GridJs erbjuder ett batch‑API som låter dig **lägga till flera rader i rutnätet** i ett enda anrop, vilket håller allt snabbt även när du hanterar miljontals poster.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar exakt **hur man infogar rader** med `InsertRowsBatch`. Du får se varför batchning är viktigt, hur du verifierar resultatet och vad du bör vara uppmärksam på när det index du riktar in dig på är enormt. I slutet kommer du kunna lägga in tusen nya poster i vilken GridJs‑instans som helst med självförtroende.

## Förutsättningar

Innan vi dyker ner, se till att du har:

- .NET 6.0 eller senare (koden kompileras med alla moderna SDK:n)
- En referens till `GridJs`‑NuGet‑paketet (eller DLL‑filen om du använder en egen build)
- Grundläggande kunskaper i C# – du behöver inte vara en guru, bara vara bekväm med klasser och metoder
- En IDE eller editor du föredrar (Visual Studio, Rider, VS Code… alla fungerar)

> **Proffstips:** Om du planerar att arbeta med riktigt enorma rutnät (tiotals miljoner rader), aktivera `gridJs.EnableVirtualization = true;` för att hålla UI‑renderingen lätt.

## Steg 1: Skapa och konfigurera GridJs‑instansen

Först och främst: du behöver ett levande `GridJs`‑objekt. Tänk på det som duken där du ska måla rader.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Varför detta steg är viktigt:** Initiering av rutnätet och eventuellt förseeding av data speglar ett verkligt scenario där rutnätet redan innehåller en stor mängd information. Batch‑insättningen vi kommer att utföra senare måste respektera det nollbaserade indexet, så vi förhandsbefolkar för att illustrera exakt infogningspunkt.

## Steg 2: Använd `InsertRowsBatch` för att **lägga till flera rader i rutnätet**

Nu kommer kärnan i handledningen – anropet som faktiskt **lägger till rader** i bulk. Metodsignaturen är `InsertRowsBatch(int startIndex, int count)`. I vårt exempel börjar vi vid index 2 000 000 (vilket motsvarar den 2 000 001:a raden) och lägger till tio rader.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Hur det fungerar:** `InsertRowsBatch` allokerar det begärda antalet rader internt och skjuter befintliga rader nedåt. Eftersom operationen utförs i en enda transaktion, uppdateras UI bara en gång, vilket är anledningen till att denna metod är det rekommenderade sättet att **hur man lägger till rader** effektivt.

## Steg 3: Verifiera infogningen – hamnade raderna där du förväntade dig?

Efter batch‑operationen vill du vara säker på att raderna är där du tror att de är. Följande hjälpfunktion läser den första och sista raden i det nyss tillagda blocket och skriver ut dem till konsolen.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Förväntad utskrift**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

De tomma cellerna indikerar att raderna är platshållare som väntar på data. Du kan nu fylla dem individuellt eller köra en annan batch‑uppdatering.

> **Notering om kantfall:** Om `startIndex` överstiger det aktuella antalet rader, kommer GridJs automatiskt att lägga till de nya raderna i slutet. Omvänt, ett negativt index kastar ett `ArgumentOutOfRangeException`, så validera alltid användar‑angivna index.

## Steg 4: Fyll i de nya raderna (valfritt men vanligt)

Ofta vill du inte bara ha tomma rader; du behöver fylla dem med meningsfulla värden. Du kan loopa över det nyss skapade intervallet och anropa `SetCell` eller ett liknande API.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Du skulle kunna anropa `PopulateNewRows(gridJs, startIndex, rowsToAdd);` direkt efter batch‑insättningen om du behöver raderna klara för visning omedelbart.

## Steg 5: Prestandatips för mycket stora rutnät

När du hanterar **lägga till flera rader i rutnätet** i miljoner, håll dessa knep i åtanke:

1. **Batch‑storlek är viktig** – Att infoga 10 000 rader på en gång kan vara snabbare än tio separata batcher på 1 000 rader eftersom varje batch medför en enda UI‑uppdatering.
2. **Stäng av UI‑uppdateringar** – Vissa GridJs‑versioner exponerar `grid.SuspendLayout()` / `grid.ResumeLayout()`. Inneslut din batch i dessa anrop om du märker fördröjning.
3. **Använd virtualisering** – Som visat tidigare minskar `EnableVirtualization` dramatiskt minnesanvändning och renderingtid.
4. **Undvik djupa kopior** – Skicka enkla värdetyper eller lätta objekt till rutnätet; tunga objekt tvingar rutnätet att klona data, vilket försämrar prestandan.

## Fullständigt fungerande exempel

När vi sätter ihop allt, här är det kompletta programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Kör programmet, så ser du konsolutskriften som bekräftar att de tio raderna har infogats på rätt plats och sedan fyllts i.

## Slutsats

Vi har gått igenom **hur man infogar rader** i GridJs med batch‑API:t, demonstrerat **hur man lägger till rader** effektivt, och utforskat sätt att **lägga till flera rader i rutnätet** utan att hänga UI:t. De viktigaste slutsatserna är:

- Använd `InsertRowsBatch(startIndex, count)` för alla bulk‑operationer.
- Validera index och överväg virtualisering för massiva dataset.
- Fyll i raderna efter batchen om du behöver omedelbart innehåll.

Nästa steg kan vara att utforska **hur man tar bort rader**, implementera **undo/redo** för batch‑redigeringar, eller integrera GridJs med en back‑end‑tjänst som strömmar data på begäran. Alla dessa ämnen bygger direkt på de koncept du just har lärt dig.

Känn dig fri att experimentera—ändra batch‑storleken, prova att infoga i början av rutnätet, eller kombinera flera batcher i en enda transaktion. Ju mer du leker, desto bekvämare blir du med stora

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}