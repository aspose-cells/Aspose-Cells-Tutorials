---
category: general
date: 2026-07-03
description: Skriv en matrisformel i C# för att skapa en tvåkolumnsmatris, beräkna
  en Excel‑cell och omvandla listan till kolumner. Följ detta steg‑för‑steg‑exempel
  med Aspose.Cells.
draft: false
keywords:
- write array formula
- calculate excel cell
- wrap list into columns
- create 2‑column array
- generate excel array
language: sv
og_description: Skriv en array‑formel i C# för att bygga en tvåkolumnsarray, beräkna
  en Excel‑cell och omsluta listan i kolumner. Lär dig hela processen med körbar kod.
og_title: Skriv arrayformel i C# – Steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  headline: Write array formula in C# – Complete Programming Guide
  type: TechArticle
- description: Write array formula in C# to create a 2‑column array, calculate Excel
    cell and wrap list into columns. Follow this step‑by‑step example using Aspose.Cells.
  name: Write array formula in C# – Complete Programming Guide
  steps:
  - name: What if I need a dynamic range rather than a hard‑coded list?
    text: 'You can construct the list part of the formula at runtime:'
  - name: Does `WRAPCOLS` work on older Excel versions?
    text: '`WRAPCOLS` is available starting with Excel 365/2019. If you target older
      versions, you’ll need to simulate the behavior with `INDEX` and `MOD` tricks,
      but that quickly becomes messy. Using Aspose.Cells lets you keep the modern
      formula and still produce a compatible file for most users.'
  - name: Can I write the formula to a range instead of a single cell?
    text: 'Yes—assign the same formula to the top‑left cell of the range, then call
      `Calculate()` on the range object:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- automation
title: Skriv arrayformel i C# – Komplett programmeringsguide
url: /sv/net/formulas-functions/write-array-formula-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skriv array‑formel i C# – Komplett programmeringsguide

Har du någonsin behövt **write array formula** i C# men varit osäker på hur du får Excel att leverera en snyggt insvept lista? Du är inte ensam. Många utvecklare stöter på problem när de försöker *generate Excel array* resultat utan att öppna UI. I den här handledningen går vi igenom ett koncist, end‑to‑end‑exempel som **writes an array formula**, **calculates Excel cell**, och **wraps list into columns** för att **create a 2‑column array** som du kan spara och inspektera.

## Vad du behöver

* .NET 6.0 eller senare (koden fungerar även på .NET Core)  
* En referens till **Aspose.Cells** (du kan hämta den från NuGet: `Install-Package Aspose.Cells`)  
* En mapp som du kan läsa/skriva Excel‑filer till – vi kallar den `YOUR_DIRECTORY` i exemplen  

Det är allt. Ingen extra Excel‑interop, ingen COM, bara ren hanterad kod.

![Exempel på att skriva array‑formel i C#](write-array-formula.png "Skärmdump som visar den genererade 2‑kolumns‑arrayen i Excel – write array formula in C#")

## Steg 1: Skriv array‑formel med Aspose.Cells

Det första vi måste göra är att **write array formula** i en cell. I Excels syntax tar funktionen `WRAPCOLS` en platt lista och omformar den till en matris. Så här gör du det programmässigt:

```csharp
// Step 1: Load the workbook (or create a new one)
var workbook = new Aspose.Cells.Workbook(); // creates a blank workbook

// Access the first worksheet – this is where we’ll work
var worksheet = workbook.Worksheets[0];

// Write array formula into A1 that wraps {1,2,3,4} into 2 columns
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";
```

**Varför detta är viktigt:** Egenskapen `Formula` lagrar den bokstavliga Excel‑formelsträngen. Genom att använda `WRAPCOLS` säger vi åt Excel att ta den linjära arrayen `{1,2,3,4}` och placera den i ett 2‑kolumns‑layout, vilket effektivt **creating a 2‑column array**. Formeln i sig är en *array formula*—du kommer att märka de krulliga parenteserna runt siffrorna.

## Steg 2: Beräkna Excel‑cell så att formeln utvärderas

Att skriva formeln räcker inte; vi måste **calculate Excel cell** så att motorn utvärderar den. Aspose.Cells kommer inte automatiskt att beräkna om du inte ber om det:

```csharp
// Step 2: Force calculation of the cell containing the array formula
worksheet.Cells["A1"].Calculate();
```

**Varför detta steg är avgörande:** Utan att anropa `Calculate()` förblir cellen i ett “pending”-tillstånd och arbetsboken du sparar kommer att innehålla den råa formeln, inte de beräknade värdena. Genom att explicit omberäkna säkerställer vi att utdata‑arrayen materialiseras i filen.

## Steg 3: Packa lista i kolumner – se resultatet

Vid detta tillfälle innehåller arbetsbladet nu ett 2‑kolumns‑block som börjar på `A1`. Om du öppnar filen ser du:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |

Det är den visuella representationen av **wrap list into columns** med hjälp av `WRAPCOLS`‑funktionen. Om du föredrar ett annat antal kolumner, ändra bara det andra argumentet:

```csharp
worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)"; // creates 3 columns
worksheet.Cells["A1"].Calculate();
```

Nu ser arrayen ut så här:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

**Proffstips:** När du hanterar större datamängder, bygg liststrängen dynamiskt (t.ex. med `string.Join(",", myNumbers)`) för att undvika hårdkodade värden.

## Steg 4: Spara arbetsboken och verifiera resultatet

Till sist sparar vi arbetsboken till disk så att du kan öppna den i Excel och bekräfta **generate excel array**‑arbetet:

```csharp
// Step 4: Save the workbook – you’ll see the calculated array in Excel
workbook.Save("YOUR_DIRECTORY/output.xlsx");
```

Öppna `output.xlsx` så ser du den 2‑kolumns‑arrayen exakt som beskrivet. Om du ändrar formeln och beräknar om, uppdateras den sparade filen automatiskt—ingen manuell uppdatering behövs.

## Fullt, körbart exempel

När vi sätter ihop allt, här är det kompletta programmet som du kan klistra in i en konsolapp:

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Load (or create) a workbook
        var workbook = new Workbook(); // blank workbook

        // 2️⃣ Access the first worksheet
        var worksheet = workbook.Worksheets[0];

        // 3️⃣ Write the array formula that wraps a list into 2 columns
        worksheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4},2)";

        // 4️⃣ Calculate the cell so the formula is evaluated
        worksheet.Cells["A1"].Calculate();

        // 5️⃣ (Optional) Save the workbook to view the result
        workbook.Save("YOUR_DIRECTORY/output.xlsx");

        Console.WriteLine("Workbook saved – check output.xlsx to see the 2‑column array.");
    }
}
```

**Förväntad output:** När du öppnar `output.xlsx` innehåller cellerna `A1:B2` siffrorna 1‑4 arrangerade i två kolumner. Konsolen skriver ut en vänlig bekräftelse.

## Kantfall & vanliga frågor

### Vad om jag behöver ett dynamiskt område istället för en hårdkodad lista?

Du kan konstruera listdelen av formeln vid körning:

```csharp
int[] values = { 10, 20, 30, 40, 50, 60 };
string list = "{" + string.Join(",", values) + "}";
worksheet.Cells["A1"].Formula = $"=WRAPCOLS({list},3)";
worksheet.Cells["A1"].Calculate();
```

Detta genererar fortfarande **generate excel array**‑output, men nu kommer källdata från din applikationslogik.

### Fungerar `WRAPCOLS` på äldre Excel‑versioner?

`WRAPCOLS` finns tillgänglig från och med Excel 365/2019. Om du riktar dig mot äldre versioner måste du simulera beteendet med `INDEX`‑ och `MOD`‑knep, men det blir snabbt rörigt. Att använda Aspose.Cells låter dig behålla den moderna formeln och ändå producera en kompatibel fil för de flesta användare.

### Kan jag skriva formeln till ett område istället för en enskild cell?

Ja—tilldela samma formel till den översta vänstra cellen i området, och anropa sedan `Calculate()` på område‑objektet:

```csharp
var range = worksheet.Cells.CreateRange("A1", 2, 2); // 2x2 block
range.Formula = "=WRAPCOLS({1,2,3,4},2)";
range.Calculate();
```

Resultatet är identiskt, men du får mer kontroll över var arrayen placeras.

## Prestandaöverväganden

När du **calculate excel cell** för många formler kan Aspose.Cells batcha beräkningar för hastighet. Om du genererar tusentals array‑er, anropa `workbook.CalculateFormula()` en gång efter att alla formler har satts, istället för `Calculate()` på varje cell. Detta minskar overheaden dramatiskt.

## Nästa steg

Nu när du vet hur du **write array formula**, **calculate Excel cell**, och **wrap list into columns** för att **create a 2‑column array**, kan du utforska:

* **Generate Excel array** för flik‑rapporter  
* Applicera styling (ramar, talformat) på det resulterande området  
* Exportera arbetsboken till PDF eller CSV för efterföljande bearbetning  
* Kombinera med datavalideringsregler för att skapa interaktiva kalkylblad  

Var och en av dessa bygger på den kärnteknik vi täckte, vilket låter dig automatisera komplexa Excel‑arbetsflöden helt från C#.

---

**Kort sagt**, den här guiden visade dig hur du **write array formula** i C# med Aspose.Cells, tvingar **calculate excel cell**‑steget, och **wrap list into columns** för att **create a 2‑column array** som du kan **generate excel array**‑filer med. Koden är fullt körbar, förklaringarna täcker *varför* bakom varje rad, och du har tips för skalning och hantering av kantfall.

Prova det, justera kolumnantalet, anslut din egen data, och låt Excel göra det tunga arbetet åt dig. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Behärska Excel‑array‑formler med Aspose.Cells Java: Förenkla beräkningar och formatering](/cells/english/java/formulas-functions/aspose-cells-java-array-formulas-custom-calculations/)
- [Skapa Excel‑listobjekt med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/tables-structured-references/create-excel-list-objects-aspose-cells-net/)
- [Importera flerdimensionell array till Excel med Aspose Cells Java](/cells/german/java/import-export/import-multi-dimensional-array-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}