---
category: general
date: 2026-10-26
description: Inaktivera autofilter i Excel med C#. Den här handledningen visar hur
  man tar bort autofilter från en Excel‑tabell programatiskt och innehåller ett komplett
  fungerande exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- disable autofilter in excel
- remove autofilter from excel table
- Excel automation C#
- Aspose.Cells filter handling
- programmatic Excel editing
language: sv
lastmod: 2026-10-26
og_description: Inaktivera autofilter i Excel snabbt. Följ den här guiden för att
  ta bort autofilter från en Excel-tabell med C# och Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet where the autofilter has been disabled
og_title: Inaktivera autofilter i Excel med C# – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  headline: How to disable autofilter in Excel with C# – complete guide
  type: TechArticle
- description: disable autofilter in Excel using C#. This tutorial shows how to remove
    autofilter from Excel table programmatically and includes a full working example.
  name: How to disable autofilter in Excel with C# – complete guide
  steps:
  - name: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
    text: Open the saved file (`Sample_NoFilter.xlsx`) in Microsoft Excel.
  - name: Click any column header – you should **not** see the drop‑down filter arrow.
    text: Click any column header – you should **not** see the drop‑down filter arrow.
  - name: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
    text: 'If you still see arrows, double‑check that the table you targeted is indeed
      the one with the filter. You can list all tables with:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Hur man inaktiverar autofilter i Excel med C# – komplett guide
url: /sv/net/excel-autofilter-validation/how-to-disable-autofilter-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man inaktiverar autofilter i Excel med C# – komplett guide

Om du behöver **inaktivera autofilter i Excel**, visar den här guiden exakt hur du gör det från C#. Oavsett om du rensar upp en rapport innan publicering eller automatiserar en data‑exportpipeline, säkerställer borttagning av filtret att kalkylbladet visar varje rad. Du kommer också att lära dig hur du **tar bort autofilter från Excel‑tabell** i ett enda, pålitligt anrop.

Vi kommer att använda det populära **Aspose.Cells for .NET**‑biblioteket eftersom det fungerar utan att Excel måste vara installerat på servern. I slutet av den här handledningen har du en självständig konsolapplikation som laddar en arbetsbok, hittar den första tabellen och inaktiverar dess autofilter. Lösningen fungerar med .xlsx‑filer skapade av Excel 2007 eller nyare.

## Vad du behöver

| Förutsättning | Varför det är viktigt |
|--------------|-----------------------|
| .NET 6.0 or later | Tillhandahåller runtime för C#‑koden. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Ger programmatisk åtkomst till kalkylblad, tabeller och autofilter. |
| En exempel‑Excel‑fil (`Sample.xlsx`) som innehåller minst en tabell med ett autofilter tillämpat | Koden arbetar på den första tabellen; att ha en tabell låter oss demonstrera inaktivering av filtret. |
| Visual Studio 2022 (or any C# IDE) | Gör det enkelt att bygga och felsöka konsolappen. |

> **Proffstips:** Om du föredrar ett gratisalternativ kan du anpassa koden för att använda **ClosedXML** eller **EPPlus**; huvudidén—att sätta tabellens `AutoFilter`‑egenskap till `null`—förblir densamma.

## Steg 1: Skapa ett nytt konsolprojekt

Öppna en terminal eller Visual Studio-kommandoprompten och kör:

```bash
dotnet new console -n ExcelFilterDemo
cd ExcelFilterDemo
dotnet add package Aspose.Cells
```

## Steg 2: Ladda arbetsboken och hitta det första kalkylbladet

Den första logiska operationen är att öppna arbetsboksfilen. Aspose.Cells läser filen till ett `Workbook`‑objekt som ger dig direkt åtkomst till kalkylblad och tabeller.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the Excel file you want to modify
        const string inputPath = "Sample.xlsx";

        // Load the workbook into memory
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Varför detta steg?** Att ladda arbetsboken krävs innan du kan manipulera några Excel‑objekt. Att använda det första kalkylbladet (`Worksheets[0]`) speglar det vanliga scenariot där huvuddata finns på det första bladet.

## Steg 3: Hämta den första tabellen som definierats på kalkylbladet

Excel‑tabeller (även kallade ListObjects) är behållare som håller strukturerad data. Varje tabell kan ha sitt eget autofilter. För att ta bort filtret behöver vi först en referens till tabellobjektet.

```csharp
        // Get the first table on the worksheet.
        // If the worksheet has no tables, this will throw an IndexOutOfRangeException.
        Table table = worksheet.Tables[0];
```

> **Edge case:** Om arbetsboken kan innehålla kalkylblad utan tabeller, omslut åtkomsten med en `if (worksheet.Tables.Count > 0)`‑kontroll. Detta förhindrar körfel och gör lösningen robust.

## Steg 4: Inaktivera autofiltret för tabellen

Den faktiska inaktiveringen är en enda rad: tilldela `null` till `AutoFilter`‑egenskapen på `Table`‑objektet. Detta rensar alla filterkriterier och tar bort rullgardinspilarna från rubrikraden.

```csharp
        // Disable the autofilter – this clears any applied filter.
        table.AutoFilter = null;
```

Efter att denna rad har körts beter sig tabellen som ett vanligt område utan filter‑UI.

## Steg 5: Spara den modifierade arbetsboken

Slutligen skriver du tillbaka ändringarna till disk. Du kan skriva över originalfilen eller skapa en ny för att behålla källfilen intakt.

```csharp
        // Save the workbook. Use a new file name to avoid overwriting the original.
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

### Fullständig källkod

När alla bitar sätts ihop ser det kompletta programmet ut så här:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the original Excel file
        const string inputPath = "Sample.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);

        // Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (worksheet.Tables.Count == 0)
        {
            System.Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Get the first table
        Table table = worksheet.Tables[0];

        // Disable the autofilter – clears any applied filter
        table.AutoFilter = null;

        // Save the modified workbook
        const string outputPath = "Sample_NoFilter.xlsx";
        wb.Save(outputPath);

        System.Console.WriteLine($"Autofilter disabled. Saved to {outputPath}");
    }
}
```

Kör programmet med `dotnet run`. Efter körning, öppna `Sample_NoFilter.xlsx` i Excel; du kommer att se att filterpilarna har försvunnit och alla rader är synliga.

## Verifiera att autofiltret verkligen är borta

1. Öppna den sparade filen (`Sample_NoFilter.xlsx`) i Microsoft Excel.  
2. Klicka på någon kolumnrubrik – du bör **inte** se den nedrullningsbara filterpilen.  
3. Om du fortfarande ser pilar, dubbelkolla att tabellen du riktade in dig på faktiskt är den med filtret. Du kan lista alla tabeller med:

```csharp
foreach (var tbl in worksheet.Tables)
{
    System.Console.WriteLine($"Table name: {tbl.Name}, Has AutoFilter: {tbl.AutoFilter != null}");
}
```

Konsolutdata bör rapportera `Has AutoFilter: False` för den tabell du modifierade.

## Vanliga fallgropar och hur man undviker dem

| Symptom | Trolig orsak | Lösning |
|---------|--------------|---------|
| `IndexOutOfRangeException` at `worksheet.Tables[0]` | Kalkylbladet har inga tabeller. | Lägg till en kontroll `if (worksheet.Tables.Count == 0)` innan åtkomst. |
| Saved file still shows filters | Du redigerade fel kalkylblad eller fel tabell. | Använd `wb.Worksheets["SheetName"]` eller iterera genom `wb.Worksheets` för att hitta rätt tabell. |
| The program crashes on older .NET versions | Aspose.Cells kräver .NET 6.0+ för det senaste paketet. | Uppgradera mål‑frameworket i `.csproj`‑filen. |
| NullReferenceException when `table.AutoFilter` is already null | Du anropade koden två gånger på samma fil utan att ladda om. | Läs in arbetsboken igen eller kontrollera `if (table.AutoFilter != null)` innan tilldelning. |

## Utöka lösningen

Nu när du vet hur man **inaktiverar autofilter i Excel**, kanske du vill:

* **Ta bort autofilter från Excel‑tabell** endast när ett specifikt villkor är uppfyllt (t.ex. när en användarflagga är satt). Lägg till ett `if`‑uttryck runt `table.AutoFilter = null;`.
* **Applicera ett nytt filter** programatiskt efter att det gamla har rensats, med `table.AutoFilter.Range` och `table.AutoFilter.AddFilterColumn(...)`.
* **Bearbeta flera tabeller** i samma arbetsbok genom att loopa igenom `worksheet.Tables` och inaktivera varje filter.

Dessa utökningar följer samma mönster som demonstrerats ovan och håller kodbasen ren.

## Slutsats

Du har nu en kortfattad, produktionsklar metod för att **inaktivera autofilter i Excel** med C#. Genom att ladda arbetsboken, komma åt den första tabellen och sätta `table.AutoFilter = null`, tar du effektivt **bort autofilter från Excel‑tabell** utan manuell interaktion. Det kompletta exemplet kompilerar, körs och producerar en ren fil som är klar för vidare automatisering eller distribution.

Känn dig fri att experimentera med ytterligare tabeller, villkorlig logik eller alternativa bibliotek. Om du stöter på några edge cases, gå tillbaka till felsökningsavsnittet eller utforska Aspose.Cells omfattande dokumentation för avancerad filterhantering. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man tar bort autofilter från Excel‑tabeller med C#](/cells/english/net/excel-autofilter-validation/how-to-remove-autofilter-from-excel-tables-using-c/)
- [Rensa filter‑UI i Excel med C# – Ta bort AutoFilter‑knappen](/cells/english/net/excel-autofilter-validation/clear-filter-ui-in-excel-with-c-remove-autofilter-button/)
- [Hur man använder AutoFilter i C# Excel‑automatisering – Fullständig steg‑för‑steg‑guide](/cells/english/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}