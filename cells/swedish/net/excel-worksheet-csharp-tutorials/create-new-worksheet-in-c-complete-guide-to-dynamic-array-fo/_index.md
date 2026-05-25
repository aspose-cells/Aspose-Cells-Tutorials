---
category: general
date: 2026-05-23
description: Skapa ett nytt kalkylblad i C# med en steg‑för‑steg‑handledning. Lär
  dig hur du skapar en arbetsbok, använder en dynamisk array‑formel, exporterar sorterade
  data och sparar arbetsboken.
draft: false
keywords:
- create new worksheet
- how to create workbook
- how to save workbook
- export sorted data
- dynamic array formula
language: sv
og_description: Skapa ett nytt kalkylblad i C# med Aspose.Cells. Den här guiden visar
  hur du skapar en arbetsbok, tillämpar en dynamisk matrisformel, exporterar sorterade
  data och sparar arbetsboken.
og_title: Skapa nytt kalkylblad i C# – Fullständig programmeringsgenomgång
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create new worksheet in C# with a step‑by‑step tutorial. Learn how
    to create workbook, use a dynamic array formula, export sorted data and save workbook.
  headline: Create New Worksheet in C# – Complete Guide to Dynamic Array Formulas
  type: TechArticle
- questions:
  - answer: The file will open, but the `SORT` formula will appear as text and show
      a `#NAME?` error. For backward compatibility, generate the sorted list in code
      and write the values directly.
    question: Does this work on older Excel versions that don’t support dynamic arrays?
  - answer: Absolutely. Use `=SORT(A2:C10, {1,2}, {1,-1})` where the second argument
      specifies the column indices and the third the sort order.
    question: Can I sort by multiple columns?
  - answer: 'After saving the workbook, load it again and call `worksheet.Cells.ExportDataTableAsString`
      or use `CsvSaveOptions` if your library provides one. --- ## Next Steps - **Explore
      other dynamic array functions** such as `FILTER`, `UNIQUE`, and `SEQUENCE`.
      - **Automate chart creation** on the same worksh'
    question: What if I need to export the sorted data to CSV?
  type: FAQPage
tags:
- C#
- Excel Automation
- Aspose.Cells
- Spreadsheet
title: Skapa ett nytt kalkylblad i C# – Fullständig guide till dynamiska matrisformler
url: /sv/net/excel-worksheet-csharp-tutorials/create-new-worksheet-in-c-complete-guide-to-dynamic-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa nytt kalkylblad i C# – Komplett guide till dynamiska array‑formler

Har du någonsin funderat på hur man **skapar ett nytt kalkylblad** i C# utan att öppna Excel manuellt? Du är inte ensam. Många utvecklare behöver generera rapporter, sortera data i farten och skicka resultatet som en .xlsx‑fil – allt från kod.  

I den här handledningen går vi igenom precis det: vi visar **hur man skapar en arbetsbok**, lägger in en **dynamisk array‑formel** i ett helt nytt blad, **exporterar sorterade data**, och slutligen **hur man sparar arbetsboken** så att du kan dela den med vem som helst. Inga onödiga detaljer, bara ett gediget, körbart exempel som du kan kopiera och klistra in idag.

## Vad du kommer att lära dig

- Förutsättningarna för att använda Aspose.Cells (eller något liknande .NET Excel‑bibliotek).  
- Hur man **skapar ett nytt kalkylblad**, skriver en `SORT`‑formel och låter Excels spill‑område fyllas automatiskt.  
- Tips för att hantera kantfall som tomma källområden eller stora datamängder.  
- Hur man **exporterar sorterade data** till en ny fil och verifierar resultatet.  
- En snabb titt på alternativa tillvägagångssätt om du föredrar `OpenXML` eller `EPPlus`.  

När du är klar med den här guiden har du ett fristående program som producerar en sorterad lista i ett nytt kalkylblad, redo för vidare bearbetning.

---

## Steg 1: Ställ in ditt projekt – Hur man skapar en arbetsbok

Först, låt oss förbereda miljön. Vi kommer att använda **Aspose.Cells for .NET** eftersom det stödjer hela Excels beräkningsmotor, inklusive de senaste **dynamiska array‑formlerna** som `SORT`. Om du använder ett annat bibliotek är koncepten desamma – byt bara namnrymden.

```csharp
// Add the Aspose.Cells NuGet package
//   dotnet add package Aspose.Cells
using Aspose.Cells;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or load an existing one)
            Workbook workbook = new Workbook();   // <-- this is how we **how to create workbook**
```

**Varför detta är viktigt:**  
Att skapa ett `Workbook`‑objekt startar upp en minnesrepresentation av en Excel‑fil. Ingen COM‑interop, ingen Excel‑installation krävs. Detta gör lösningen portabel över Windows, Linux och Docker‑behållare.

> **Proffstips:** Om du redan har en mallfil, skicka dess sökväg till `new Workbook("template.xlsx")` istället för att börja från början.

## Steg 2: Lägg till ett nytt blad – Skapa nytt kalkylblad

Nu när vi har en arbetsbok behöver vi en plats att lägga våra data. Som standard skapar Aspose ett enda blad som heter “Sheet1”. Vi lägger till ett till så att exemplet blir prydligt.

```csharp
            // Step 2: Add a new worksheet to hold the sorted output
            int newSheetIndex = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[newSheetIndex];   // <-- **create new worksheet**
```

**Vad händer under huven?**  
`Worksheets.Add()` returnerar det nollbaserade indexet för det nyss tillagda bladet. Vi hämtar sedan `Worksheet`‑objektet så att vi kan manipulera celler direkt.

> **Observera:** Om du anropar `Add()` upprepade gånger utan att lagra indexet kan du tappa bort vilket blad du skriver till. Behåll alltid en referens.

## Steg 3: Fyll i exempeldata (valfritt)

För att `SORT`‑formeln ska ha något att arbeta med behöver vi ett källområde. Låt oss fylla `A2:A6` med några osorterade värden.

```csharp
            // Populate source data (A2:A6) – this mimics a raw data table
            string[] rawValues = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < rawValues.Length; i++)
            {
                sheet.Cells[i + 1, 0].PutValue(rawValues[i]); // Row i+1, Column 0 (A column)
            }
```

Varför placera data på *samma* blad? Eftersom `SORT`‑funktionen kan referera till ett område på samma kalkylblad; detta håller demonstrationen kompakt. I verkliga scenarier kan du läsa från en databas, CSV eller ett annat blad.

## Steg 4: Skriv den dynamiska array‑formeln – Exportera sorterade data

Här är kärnan i handledningen: vi injicerar en **dynamisk array‑formel** som automatiskt spillar den sorterade listan i intilliggande celler.

```csharp
            // Step 4: Write a SORT formula into cell A1 (row 0, column 0)
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";   // <-- **dynamic array formula**
```

När Excel utvärderar `=SORT(A2:A6)` producerar den en vertikal array av värdena i alfabetisk ordning. Tack vare spill‑beteendet som introducerades i Excel 365, fyller resultaten automatiskt `A1:A5`.

> **Vanlig fråga:** *Vad händer om källområdet är tomt?*  
> Formeln returnerar ett `#SPILL!`‑fel. Skydda mot detta genom att kontrollera `rawValues.Length` innan du skriver formeln, eller omslut den i `IFERROR(SORT(...), "")`.

## Steg 5: Tvinga beräkning – Låt formeln köras

Aspose.Cells räknar inte om formler automatiskt efter att du har satt dem, så vi måste be motorn att utföra beräkningarna.

```csharp
            // Recalculate the workbook so the spill range is populated
            workbook.CalculateFormula();   // <-- triggers **export sorted data**
```

**Bakom kulisserna:** Beräkningsmotorn parsar formelträdet, löser cellreferenser och skriver tillbaka den resulterande arrayen till bladet. Detta steg är avgörande; annars skulle du se den råa texten `=SORT(A2:A6)` i filen.

## Steg 6: Spara filen – Hur man sparar arbetsboken

Till sist sparar vi arbetsboken till disk. Du kan välja vilken mapp du vill; se bara till att processen har skrivbehörighet.

```csharp
            // Step 6: Save the workbook to view the result
            string outputPath = @"YOUR_DIRECTORY\sorted_output.xlsx";
            workbook.Save(outputPath);   // <-- **how to save workbook**
            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**Varför använda `Save` istället för `SaveCopyAs`?**  
`Save` skriver över målfilen, vilket är okej för en engångsexport. Om du behöver behålla originalet orört, anropa `workbook.SaveCopyAs("backup.xlsx")` först.

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta programmet som du kan kompilera direkt nu:

```csharp
using Aspose.Cells;
using System;

namespace WorksheetDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Add a fresh worksheet
            int sheetIdx = workbook.Worksheets.Add();
            Worksheet sheet = workbook.Worksheets[sheetIdx];

            // 3️⃣ Seed unsorted data (A2:A6)
            string[] values = { "Delta", "Alpha", "Echo", "Bravo", "Charlie" };
            for (int i = 0; i < values.Length; i++)
                sheet.Cells[i + 1, 0].PutValue(values[i]);

            // 4️⃣ Insert the SORT dynamic array formula in A1
            sheet.Cells[0, 0].Formula = "=SORT(A2:A6)";

            // 5️⃣ Calculate so the spill range fills
            workbook.CalculateFormula();

            // 6️⃣ Save the workbook
            string outFile = @"C:\Temp\sorted_output.xlsx";
            workbook.Save(outFile);
            Console.WriteLine($"✅ Workbook saved – open {outFile} to see the sorted list.");
        }
    }
}
```

### Förväntat resultat

När du öppnar `sorted_output.xlsx` kommer cell **A1** att innehålla “Alpha”, **A2** “Bravo”, **A3** “Charlie”, **A4** “Delta” och **A5** “Echo”. Den ursprungliga osorterade listan finns kvar i **A2:A6** (källområdet), vilket bevisar att **den dynamiska array‑formeln** framgångsrikt exporterade sorterade data.

## Hantera kantfall & variationer

| Situation | Vad man ska göra |
|-----------|-------------------|
| **Källområde större än 1 048 576 rader** | Excels radgräns gäller; dela upp data över flera blad eller använd en databas för tunga operationer. |
| **Blandade datatyper (nummer + text)** | `SORT` placerar som standard siffror före text. Använd `SORTBY` med en anpassad sorteringsnyckel om du behöver en annan ordning. |
| **Du behöver de sorterade värdena som ett statiskt område** | Efter beräkning, kopiera spill‑området och klistra in endast värden (`PasteSpecial`), ta sedan bort formeln. |
| **Använda OpenXML/EPPlus istället för Aspose** | Stegen är identiska; byt bara ut `Workbook`/`Worksheet` mot bibliotekets motsvarigheter och anropa `Package.Save()`. |

## Vanliga frågor

**Q: Fungerar detta i äldre Excel‑versioner som inte stödjer dynamiska arrayer?**  
A: Filen öppnas, men `SORT`‑formeln visas som text och visar ett `#NAME?`‑fel. För bakåtkompatibilitet, generera den sorterade listan i kod och skriv värdena direkt.

**Q: Kan jag sortera efter flera kolumner?**  
A: Absolut. Använd `=SORT(A2:C10, {1,2}, {1,-1})` där det andra argumentet anger kolumnindexen och det tredje sorteringsordningen.

**Q: Vad händer om jag behöver exportera de sorterade data till CSV?**  
A: Efter att ha sparat arbetsboken, ladda den igen och anropa `worksheet.Cells.ExportDataTableAsString` eller använd `CsvSaveOptions` om ditt bibliotek erbjuder det.

## Nästa steg

- **Utforska andra dynamiska array‑funktioner** såsom `FILTER`, `UNIQUE` och `SEQUENCE`.  
- **Automatisera skapandet av diagram** på samma kalkylblad för att visualisera de sorterade resultaten.  
- **Integrera med ASP.NET Core** för att låta användare ladda ner den genererade filen direkt från ett webb‑API.  

Var och en av dessa ämnen bygger på grunderna som täcks här – att skapa en arbetsbok, lägga till ett blad, applicera formler och spara filen.

## Slutsats

Vi har just demonstrerat hur man **skapar ett nytt kalkylblad** i C#, lägger in en **dynamisk array‑formel**, **exporterar sorterade data**, och slutligen **hur man sparar arbetsboken**. Tillvägagångssättet är enkelt, kräver bara några få kodrader och fungerar pålitligt över plattformar.  

Prova det, justera källområdet, byt `SORT` mot `FILTER`, eller skicka utdata till en rapporttjänst. Himlen är gränsen när du behärskar grunderna i programmatisk Excel‑manipulation.

Lycklig kodning, och må dina kalkylblad alltid förbli sorterade!

## Relaterade handledningar

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Style Excel Tables Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}