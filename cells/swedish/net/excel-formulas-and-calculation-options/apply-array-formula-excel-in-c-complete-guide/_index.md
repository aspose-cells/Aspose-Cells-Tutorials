---
category: general
date: 2026-06-24
description: Använd matrisformel i Excel med C#. Lär dig hur du sparar Excel‑fil i
  C# och skapar Excel‑arbetsbok i C# med Expand‑funktionen samt genererar en Excel‑fil
  med formler.
draft: false
keywords:
- apply array formula excel
- save excel file c#
- create excel workbook c#
- use expand function excel
- generate excel file with formulas
language: sv
og_description: Använd arrayformel i Excel i C# och lär dig hur du snabbt sparar Excel-filen
  i C#. Denna guide visar hur du skapar en Excel-arbetsbok i C# och använder expand-funktionen
  i Excel.
og_title: Tillämpa matrisformel i Excel med C# – Steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  headline: Apply Array Formula Excel in C# – Complete Guide
  type: TechArticle
- description: Apply array formula excel using C#. Learn how to save excel file c#
    and create excel workbook c# with the Expand function and generate excel file
    with formulas.
  name: Apply Array Formula Excel in C# – Complete Guide
  steps:
  - name: What if the target folder doesn’t exist?
    text: '`Workbook.Save` will throw a `DirectoryNotFoundException`. A quick fix
      is to ensure the directory exists before calling `Save`:'
  - name: Can I apply the array formula to a range other than A1?
    text: 'Absolutely. Just change the cell address:'
  - name: Does the calculation engine respect Excel’s precision settings?
    text: Aspose.Cells follows IEEE‑754 double‑precision arithmetic, which matches
      Excel’s default. If you need custom precision, you can tweak the `CalculationOptions`
      object before calling `CalculateFormula`.
  - name: What about older Excel versions that don’t support `EXPAND`?
    text: 'If you need backward compatibility, replace `EXPAND` with a combination
      of `INDEX` and `SEQUENCE` or simply write the values directly via C# loops.
      The library also lets you write values without formulas:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
title: Tillämpa Arrayformel i Excel i C# – Komplett guide
url: /sv/net/excel-formulas-and-calculation-options/apply-array-formula-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tillämpa Array‑formel Excel i C# – Komplett programmeringstutorial

Har du någonsin behövt **apply array formula excel** men varit osäker på hur du gör det från C#‑kod? Du är inte ensam. Många utvecklare stöter på problem när de försöker skapa ett kalkylblad som innehåller dynamiska array‑formler som `EXPAND` eller `COT`.  

I den här tutorialen går vi igenom ett praktiskt exempel som **creates an excel workbook c#**, injicerar en array‑formel, använder `EXPAND`‑funktionen och slutligen **save excel file c#** så att du kan öppna den i Excel och se resultaten. I slutet kommer du också att veta hur du **generate excel file with formulas** på ett produktionsklart sätt.

> **Pro tip:** Tillvägagångssättet som visas här fungerar med de senaste versionerna av Excel som stödjer dynamiska array‑funktioner (Office 365, Excel 2021+). Om du behöver bakåtkompatibilitet måste du återgå till äldre formeltekniker.

![Skärmdump av Excel som visar resultatet av array‑formeln – apply array formula excel](apply-array-formula-excel.png)

*(Bildtext: apply array formula excel – skärmdump av Excel‑arbetsbok med dynamisk array‑formel)*

## Vad du behöver

- **.NET 6+** (eller någon nyare .NET‑runtime) – koden kompileras med både .NET Core och .NET Framework.  
- **Aspose.Cells for .NET** (gratis provversion eller licensierad version). Detta bibliotek låter dig manipulera Excel‑filer utan att ha Excel installerat.  
- En favorit‑IDE (Visual Studio, Rider, VS Code).  
- Grundläggande C#‑kunskaper – inget avancerat, bara tillräckligt för att följa koden.

Om du redan har dem, bra – låt oss dyka ner.

---

## Steg 1 – Apply Array Formula Excel: Skapa arbetsboken

Det första vi gör är att **create excel workbook c#** med Aspose.Cells. Detta ger oss ett rent arbetsboksobjekt som vi senare kan fylla med formler.

```csharp
using System;
using Aspose.Cells;

namespace ExcelArrayFormulaDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create a new workbook
            Workbook workbook = new Workbook();

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];
```

> **Varför detta är viktigt:** Att instansiera ett `Workbook`‑objekt är startpunkten för all Excel‑automatisering. Det representerar hela filen, och det första kalkylbladet är ett bekvämt ställe att börja testa formler.

---

## Steg 2 – Use Expand Function Excel för att fylla en array

Nu **use expand function excel** för att omvandla en enkel statisk array `{1,2,3}` till ett vertikalt spill på fem rader. `EXPAND`‑funktionen är en del av Excels dynamiska array‑motor och fyller automatiskt intervallet.

```csharp
            // Set a formula that expands an array into 5 rows, 1 column
            // The formula will spill into A1:A5
            worksheet.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";
```

> **Förklaring:**  
> - `{1,2,3}` är en litteral array‑konstant.  
> - `5` instruerar Excel att returnera fem rader, medan `1` håller den till en enda kolumn.  
> - När du öppnar filen kommer cellerna A1 till A5 att visa `1, 2, 3, 0, 0` (de extra raderna fylls med nollor).

---

## Steg 3 – Lägg till en klassisk matematikformel (Cotangent)

Dynamiska arrayer är inte de enda formlerna du kan bädda in. Låt oss också **generate excel file with formulas** som beräknar cotangenten av π/4. Detta visar att vanliga formler fungerar sida‑vid‑sida med dynamiska.

```csharp
            // Set a formula that calculates the cotangent of π/4 (≈1)
            worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

> **Varför inkludera detta?** Det visar att du kan blanda äldre och nya funktioner utan någon extra konfiguration. `COT`‑funktionen finns i alla moderna Excel‑versioner.

---

## Steg 4 – Räkna om alla formler i arbetsboken

Aspose.Cells utvärderar inte automatiskt formler när du sätter dem. Du måste be motorn att **recalculate** innan du sparar, annars kommer filen bara att innehålla de råa formlerna.

```csharp
            // Force calculation of all formulas
            workbook.CalculateFormula();
```

> **Vad händer under huven?** Biblioteket parsar varje formel, bygger ett uttrycksträd och utvärderar det med sin egen beräkningsmotor. Detta steg är avgörande om du vill att den genererade filen ska visa värden omedelbart efter öppning.

---

## Steg 5 – Save Excel File C# – Spara resultaten

Till sist **save excel file c#** till disk. Du kan välja vilken mapp du vill; se bara till att applikationen har skrivbehörighet.

```csharp
            // Define the output path (adjust as needed)
            string outputPath = @"C:\Temp\output.xlsx";

            // Save the workbook – this writes the calculated values into the file
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

När du öppnar `output.xlsx` i Excel bör du se:

| A   | B |
|-----|---|
| 1   | 1 |
| 2   |   |
| 3   |   |
| 0   |   |
| 0   |   |

- Kolumn **A** visar den spillade arrayen som produceras av `EXPAND`.  
- Cell **B1** visar `1`, resultatet av `COT(π/4)`.

Det är hela **generate excel file with formulas**‑arbetsflödet.

---

## Vanliga frågor & kantfall

### Vad händer om målmappen inte finns?

`Workbook.Save` kommer att kasta ett `DirectoryNotFoundException`. En snabb lösning är att säkerställa att katalogen finns innan du anropar `Save`:

```csharp
if (!System.IO.Directory.Exists(System.IO.Path.GetDirectoryName(outputPath)))
{
    System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath));
}
```

### Kan jag tillämpa array‑formeln på ett annat område än A1?

Absolut. Ändra bara celladressen:

```csharp
worksheet.Cells["D4"].Formula = "=EXPAND({10,20,30},3,1)";
```

Spillet kommer att börja på D4 och fylla D4:D6.

### Respekterar beräkningsmotorn Excels precisioninställningar?

Aspose.Cells följer IEEE‑754 dubbelprecision‑aritmetik, vilket matchar Excels standard. Om du behöver anpassad precision kan du justera `CalculationOptions`‑objektet innan du anropar `CalculateFormula`.

```csharp
var options = new CalculationOptions { PrecisionAsDisplayed = true };
workbook.CalculateFormula(options);
```

### Vad händer med äldre Excel‑versioner som inte stödjer `EXPAND`?

Om du behöver bakåtkompatibilitet, ersätt `EXPAND` med en kombination av `INDEX` och `SEQUENCE` eller skriv helt enkelt värdena direkt via C#‑loopar. Biblioteket låter dig också skriva värden utan formler:

```csharp
object[] values = { 1, 2, 3, 0, 0 };
for (int i = 0; i < values.Length; i++)
{
    worksheet.Cells[i, 0].PutValue(values[i]); // Column A
}
```

---

## Pro‑tips för att arbeta med formler i C#

- **Batch‑beräkningar:** Om du infogar hundratals formler, anropa `CalculateFormula` en gång efter alla insättningar. Detta minskar CPU‑belastningen.  
- **Undvik volatila funktioner:** Funktioner som `NOW()` beräknas om vid varje öppning, vilket kan sakta ner stora arbetsböcker.  
- **Använd namngivna områden:** De gör formler lättare att läsa och underhålla, särskilt när du genererar dem programatiskt.  
- **Håll biblioteket uppdaterat:** Aspose.Cells‑utgåvor innehåller ofta prestandaförbättringar och stöd för nya Excel‑funktioner (t.ex. `XLOOKUP`, `FILTER`).  

---

## Sammanfattning – Vad vi gick igenom

Vi började med att **apply array formula excel** i en ny arbetsbok, sedan **use expand function excel** för att spilla en statisk array över fem rader. Därefter lade vi till en klassisk `COT`‑beräkning, tvingade en fullständig omräkning och slutligen **save excel file c#** till disk. Resultatet är ett färdigt kalkylblad som visar både dynamiskt array‑beteende och vanlig formelutvärdering – en solid grund för alla **generate excel file with formulas**‑projekt.

---

## Nästa steg

- **Styla utskriften:** Applicera teckensnitt, kantlinjer eller villkorsstyrd formatering via Aspose.Cells för att göra bladet snyggt.  
- **Lägg till diagram:** Använd bibliotekets diagram‑API för att automatiskt visualisera array‑data.  
- **Exportera till andra format:** Samma arbetsbok kan sparas som CSV, PDF eller HTML med ett enda metodanrop (`workbook.Save("output.pdf")`).  
- **Integrera i ASP.NET:** Leverera den genererade filen direkt till användare via en web‑API‑endpoint.

Känn dig fri att experimentera—byt ut `EXPAND` mot `SEQUENCE`, prova flerkolumn‑spill eller generera hela instrumentpaneler programatiskt. Himlen är gränsen när du vet hur du **apply array formula excel** från C#.

Lycka till med kodandet! 🚀


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa och spara Excel‑fil Aspose Cells .NET](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [Hur du sparar specifika sidor i en Excel‑fil som PDF med Aspose.Cells för .NET](/cells/english/net/workbook-operations/save-specific-excel-pages-pdf-aspose-cells-net/)
- [Hur du skapar och sparar en Excel‑arbetsbok som ODS med Aspose.Cells för .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}