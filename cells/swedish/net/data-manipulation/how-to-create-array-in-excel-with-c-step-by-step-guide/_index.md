---
category: general
date: 2026-02-28
description: Hur du skapar en array i Excel med C#. Lär dig att generera siffror,
  utvärdera en formel, skapa en Excel‑arbetsbok och spara Excel‑filen på några minuter.
draft: false
keywords:
- how to create array
- create excel workbook
- save excel file
- how to evaluate formula
- how to generate numbers
language: sv
og_description: Hur man skapar en array i Excel med C#. Denna handledning visar hur
  man genererar siffror, utvärderar en formel, skapar en arbetsbok och sparar filen.
og_title: Hur man skapar en array i Excel med C# – Komplett guide
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Hur man skapar en array i Excel med C# – Steg‑för‑steg‑guide
url: /sv/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar en array i Excel med C# – Komplett programmeringshandledning

Har du någonsin undrat **how to create array** i Excel programatiskt med C#? Du är inte ensam—utvecklare frågar ständigt efter ett snabbt sätt att generera ett block med siffror utan att skriva in dem manuellt. I den här guiden går vi igenom de exakta stegen för att **create excel workbook**, lägga in en formel som **generates numbers**, **evaluate the formula**, och slutligen **save excel file** så att du kan öppna den i Excel och se resultatet.

Vi kommer att använda Aspose.Cells-biblioteket eftersom det ger oss full kontroll över formler och beräkningar utan att behöva ha Excel installerat. Om du föredrar ett annat bibliotek förblir koncepten desamma—byt bara ut API-anropen.

## Vad den här handledningen täcker

- Ställa in ett C#-projekt med det erforderliga NuGet‑paketet.  
- Skapa en ny arbetsbok (det är *create excel workbook*-delen).  
- Skriva en formel som bygger en 4‑rad × 3‑kolumns array med `SEQUENCE` och `WRAPCOLS`.  
- Tvinga motorn att **evaluate the formula** så att arrayen materialiseras.  
- Spara arbetsboken till disk (**save excel file**) och kontrollera resultatet.  

I slutet kommer du att ha ett körbart program som producerar ett Excel‑blad som ser ut så här:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |
| 7 | 8 | 9 |
|10 |11 |12 |

![Hur man skapar array i Excel – resulterande blad efter att ha kört C#‑koden](image.png)

*(Bildens alt‑text innehåller huvudnyckelordet “how to create array” för SEO.)*

---

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar även på .NET Framework 4.6+).  
- Visual Studio 2022 eller någon annan editor du föredrar.  
- NuGet‑paket **Aspose.Cells** (gratis provversion tillgänglig).  

Ingen extra Excel‑installation krävs eftersom Aspose.Cells har beräkningsmotorn internt.

---

## Steg 1: Ställ in projektet och importera Aspose.Cells

För att börja, skapa en konsolapp och lägg till biblioteket:

```bash
dotnet new console -n ExcelArrayDemo
cd ExcelArrayDemo
dotnet add package Aspose.Cells
```

Öppna nu **Program.cs** och lägg till namnrymden:

```csharp
using Aspose.Cells;
```

*Varför detta är viktigt*: Att importera `Aspose.Cells` ger oss `Workbook`, `Worksheet` och beräkningsklasserna vi behöver för att **create excel workbook** och arbeta med formler.

---

## Steg 2: Skapa arbetsboken och målbladet

Vi behöver ett nytt workbook‑objekt; det första kalkylbladet (`Worksheets[0]`) kommer att hysa vår array.

```csharp
// Step 2: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = workbook.Worksheets[0];            // reference to Sheet1
```

*Förklaring*: Klassen `Workbook` representerar hela Excel‑filen. Som standard innehåller den ett blad, vilket är perfekt för en enkel demo. Om du någonsin behöver fler blad kan du anropa `workbook.Worksheets.Add()` senare.

---

## Steg 3: Skriv en formel som **generates numbers** och bildar en array

Excels dynamiska‑array‑funktioner (`SEQUENCE` och `WRAPCOLS`) låter oss producera ett block med värden med en enda formel. Här är den exakta strängen vi kommer att tilldela:

```csharp
// Step 3: Assign a formula that creates a 4‑row × 3‑col array
// SEQUENCE(12,1,1,1) generates numbers 1‑12; WRAPCOLS wraps them into 3 columns
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
```

*Varför detta fungerar*:  
- `SEQUENCE(12,1,1,1)` returnerar en vertikal lista med siffrorna 1‑12.  
- `WRAPCOLS(...,3)` tar den listan och fyller den över tre kolumner, och spillar automatiskt över till nästa rader.  

Om du öppnar arbetsboken i Excel **utan** att först utvärdera formeln, kommer du bara att se formeltexten i `A1`. Nästa steg tvingar beräkningen.

---

## Steg 4: **evaluate the formula** så att arrayen materialiseras

Aspose.Cells räknar inte automatiskt om formler vid skrivning, så vi anropar uttryckligen beräkningsmotorn:

```csharp
// Step 4: Evaluate the formula so the array is materialised in the sheet
workbook.Calculate();   // runs all pending formulas
```

*Vad som händer*: `Calculate()` går igenom varje cell som innehåller en formel, beräknar dess resultat och skriver tillbaka värdena. Detta är **how to evaluate formula**-delen i vår handledning. Efter detta anrop innehåller cellerna A1:C4 siffrorna 1‑12, precis som en inbyggd Excel‑spill.

---

## Steg 5: **save excel file** och verifiera resultatet

Slutligen sparar vi arbetsboken till disk:

```csharp
// Step 5: Save the workbook to view the result
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Öppna `output.xlsx` i Excel så ser du den 4 × 3‑array vi genererade. Om du använder en version av Excel äldre än 365/2019 kommer de dynamiska‑array‑funktionerna inte att kännas igen—Aspose.Cells kommer fortfarande att skriva de beräknade värdena, så filen förblir användbar.

*Pro‑tips*: Använd `SaveFormat.Xlsx` om du behöver tvinga ett specifikt format, t.ex. `workbook.Save(outputPath, SaveFormat.Xlsx);`.

---

## Fullt fungerande exempel (Klar att kopiera‑klistra in)

Nedan är det kompletta programmet. Klistra in det i **Program.cs**, kör `dotnet run`, så får du `output.xlsx` i projektmappen.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelArrayDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();               // in‑memory workbook
            Worksheet ws = workbook.Worksheets[0];            // default sheet (Sheet1)

            // 2️⃣ Drop the formula that builds a 4‑row × 3‑col array
            // SEQUENCE creates numbers 1‑12; WRAPCOLS arranges them into 3 columns
            ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";

            // 3️⃣ Force the calculation engine to evaluate the formula
            workbook.Calculate();   // now the array is "spilled" into A1:C4

            // 4️⃣ Save the file so you can open it in Excel
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Workbook saved to {outputPath}");
        }
    }
}
```

**Förväntad output** (konsol):

```
✅ Workbook saved to C:\Path\To\ExcelArrayDemo\output.xlsx
```

Öppna filen så ser du siffrorna 1‑12 ordnade exakt som visat tidigare.

---

## Variationer & kantfall

### 1. Äldre Excel‑versioner utan dynamiska arrayer  

Om din målgrupp använder Excel 2016 eller tidigare finns inte `SEQUENCE` och `WRAPCOLS`. En snabb lösning är att generera siffrorna i C# och skriva dem direkt:

```csharp
int value = 1;
for (int row = 0; row < 4; row++)
{
    for (int col = 0; col < 3; col++)
    {
        ws.Cells[row, col].PutValue(value++);
    }
}
```

Denna manuella loop efterliknar samma resultat, men med mer kod. Konceptet **how to generate numbers** förblir identiskt.

### 2. Ändra storleken på arrayen  

Vill du ha ett 5 × 5‑rutnät med siffrorna 1‑25? Justera bara argumenten i `SEQUENCE` och kolumnantalet i `WRAPCOLS`:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(25,1,1,1),5)";
```

### 3. Använda namngivna områden för återanvändning  

Du kan tilldela det spillade området ett namn för senare formler:

```csharp
ws.Cells["A1"].Formula = "=WRAPCOLS(SEQUENCE(12,1,1,1),3)";
workbook.Calculate(); // ensure the range exists
int lastRow = ws.Cells.GetLastDataRow(); // should be 3 (zero‑based)
int lastCol = ws.Cells.GetLastDataColumn(); // should be 2
string address = $"A1:{CellIndexToName(lastRow, lastCol)}";
ws.Workbook.Names.Add("MyArray", ws, address);
```

Nu kan vilket annat blad som helst referera till `MyArray` direkt.

---

## Vanliga fallgropar & hur man undviker dem

| Fallgrop | Varför det händer | Lösning |
|---|---|---|
| **Formeln spillar inte** | `Calculate()` utelämnad eller anropad innan formeln satts. | Anropa alltid `workbook.Calculate()` **efter** att formeln har tilldelats. |
| **Fil sparad men tom** | Använder `SaveFormat.Csv` av misstag. | Använd `SaveFormat.Xlsx` eller utelämna formatet så att Aspose kan avgöra. |
| **Dynamic

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}