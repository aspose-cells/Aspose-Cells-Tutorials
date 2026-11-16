---
category: general
date: 2026-11-16
description: Hur du kopierar en pivottabell från en Excel-fil till en ny arbetsbok
  med C#. Lär dig att ladda arbetsboken, kopiera område och bevara pivottabeller.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new workbook
- load excel workbook c#
- Aspose.Cells copy pivot
- preserve pivot table C#
- Excel automation C#
language: sv
lastmod: 2026-11-16
og_description: Hur man kopierar en pivottabell från en befintlig arbetsbok till en
  ny arbetsbok med C#. Följ den här kompletta guiden för att ladda Excel‑arbetsboken,
  kopiera området och behålla pivottabellen intakt.
og_image_alt: how to copy pivot table example in C#
og_title: Hur man kopierar en pivottabell till en ny arbetsbok i C# – steg‑för‑steg‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  headline: How to copy a pivot table to a new workbook in C#
  type: TechArticle
- description: How to copy pivot table from one Excel file to a new workbook using
    C#. Learn to load workbook, copy range, and preserve pivot tables.
  name: How to copy a pivot table to a new workbook in C#
  steps:
  - name: Expected output
    text: 'Running the program produces `CopyWithPivot.xlsx`. Opening the file in
      Excel shows:'
  - name: Copying multiple pivot tables
    text: If your source sheet contains several pivots, expand the `CellArea` to cover
      the union of all ranges, or repeat the copy step for each distinct area.
  - name: Preserving styles and conditional formatting
    text: '`CopyRows` copies cell styles automatically. If you need to preserve workbook‑wide
      named styles or custom number formats, call `destWorkbook.Worksheets[0].CopyStyle`
      before saving.'
  - name: Working with large workbooks
    text: For files larger than 100 MB, consider using `Workbook.LoadOptions` with
      the `MemorySetting` set to `MemorySetting.MemoryPreference` to reduce memory
      pressure.
  - name: Next steps
    text: '* Explore **Aspose.Cells** features such as refreshing pivots programmatically.
      * Combine this approach with **ExcelPackage** (EPPlus) if you need an open‑source
      alternative. * Automate copying across multiple sheets by looping through `srcWorkbook.Worksheets`.'
  type: HowTo
- questions:
  - answer: Aspose.Cells can read macro‑enabled files (`.xlsm`), but the macro code
      isn’t copied. The pivot table itself is preserved because it’s part of the worksheet
      XML.
    question: Does this work with macros or VBA‑enabled workbooks?
  - answer: The copy operation includes the cached data only. If the destination workbook
      needs to refresh from the original source, you’ll have to re‑configure the data
      connection manually.
    question: What if the pivot uses an external data source?
  - answer: 'No. A pivot table needs its cache. The most reliable way is to copy the
      rows that contain the cache, as demonstrated. You can later hide those rows
      if you don’t want them visible. ## Conclusion You now know **how to copy pivot
      table** from one Excel file to another using C#. The tutorial covered **l'
    question: Can I copy the pivot without the underlying data rows?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: Hur man kopierar en pivottabell till en ny arbetsbok i C#
url: /sv/net/pivot-tables/how-to-copy-a-pivot-table-to-a-new-workbook-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar en pivottabell till en ny arbetsbok i C#

Om du behöver **how to copy pivot table** från en Excel‑fil till en ny arbetsbok, visar den här guiden de exakta stegen. Du får lära dig hur du **load excel workbook c#**, definierar källområdet och **copy range to new workbook** samtidigt som pivottabellen förblir intakt.

Att kopiera en pivottabell är ett vanligt krav när du vill återanvända en rapportmall, migrera data mellan projekt eller skapa en lättviktig fil för distribution. Kodexemplet nedan använder Aspose.Cells, ett helt hanterat .NET‑bibliotek som fungerar utan Microsoft Office installerat. I slutet av den här tutorialen har du ett körbart program som skapar en ny arbetsbok som innehåller den ursprungliga pivottabellen, redo för vidare bearbetning eller delning.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 SDK eller senare (exemplet fungerar med .NET Core och .NET Framework)
* Visual Studio 2022 eller någon annan C#‑editor du föredrar
* En Aspose.Cells for .NET‑licens (gratisprovversionen fungerar för utvärdering)
* En käll‑Excel‑fil (`Source.xlsx`) som innehåller minst en pivottabell

> **Proffstips:** Om du använder gratisprovet, sätt licensen i koden för att undvika utvärderingsvattenstämplar.

## Steg 1: Ladda källarboken (load excel workbook c#)

Den första åtgärden är att öppna arbetsboken som innehåller pivottabellen. Aspose.Cells läser filen till minnet och ger dig full åtkomst till kalkylblad, celler och pivottabell‑objekt.

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Load the source workbook that contains the pivot table
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");
```

*Varför detta är viktigt*: Att ladda arbetsboken är grunden för all Excel‑automation. Utan ett giltigt `Workbook`‑objekt kan du varken inspektera pivottabellen eller kopiera dess data.

## Steg 2: Definiera cellområdet som omger pivottabellen (copy range to new workbook)

En pivottabell lever i ett rektangulärt block av celler. Du måste ange detta block så att kopieringsoperationen vet vad som ska flyttas. `CellArea`‑konstruktorn använder noll‑baserade index: `StartRow, StartColumn, EndRow, EndColumn`.

```csharp
        // Define the cell range that encloses the pivot table, e.g., A1:K21
        // Row and column indexes start at 0, so A1 = (0,0)
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21
```

*Varför detta är viktigt*: Genom att explicit ange området undviker du att kopiera orelaterad data och du säkerställer att pivottabellens cache inkluderas. Området kan beräknas dynamiskt om du behöver hantera varierande pivottabell‑storlekar.

## Steg 3: Skapa en ny arbetsbok och hämta dess första kalkylblad

Skapa nu destinationsarbetsboken som ska ta emot de kopierade raderna. Aspose.Cells lägger automatiskt till ett standardkalkylblad, som vi använder som mål.

```csharp
        // Create a new workbook that will receive the copied range
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Varför detta är viktigt*: Att börja med en ren arbetsbok garanterar att endast pivottabellen (och dess stödjande rader) hamnar i filen, vilket håller utdata lättviktig.

## Steg 4: Kopiera rader från källområdet till destinationsbladet (how to copy pivot table)

`CopyRows`‑metoden kopierar hela rader och bevarar formler, formatering och – framför allt – pivottabeller. Metodens parametrar är: startrad, slutrad, mål‑cellkollektion och radindex i målet där kopieringen börjar (här `0` för att börja på första raden).

```csharp
        // Copy the rows that contain the pivot table.
        // Pivot tables inside the range are preserved automatically.
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);
```

*Varför detta är viktigt*: Att använda `CopyRows` istället för att kopiera enskilda celler säkerställer att pivottabellens cache förblir länkad till den kopierade datan. Aspose.Cells hanterar de underliggande XML‑strukturerna, så du behöver inte bygga om pivottabellen manuellt.

## Steg 5: Spara den resulterande arbetsboken (copy range to new workbook)

Till sist, skriv den nya filen till disk. Destinationsarboken innehåller nu en identisk pivottabell som fungerar oberoende av källfilen.

```csharp
        // Save the new workbook with the copied pivot table
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        // Optional: inform the user
        System.Console.WriteLine("Pivot table copied successfully!");
    }
}
```

### Förväntad utdata

När programmet körs skapas `CopyWithPivot.xlsx`. När du öppnar filen i Excel visas:

* Samma pivottabell‑layout som i `Source.xlsx`
* Alla källdata‑rader som ingick i pivottabellens cache
* Inga referenser till den ursprungliga arbetsboken (pivottabellen fungerar offline)

## Hantera vanliga variationer

### Kopiera flera pivottabeller

Om ditt källblad innehåller flera pivottabeller, utvidga `CellArea` så att det täcker unionen av alla områden, eller upprepa kopieringssteget för varje separat område.

```csharp
// Example: copy two separate ranges
CellArea firstPivot = new CellArea(0, 0, 20, 10);
CellArea secondPivot = new CellArea(25, 0, 45, 10);

destWorksheet.Cells.CopyRows(firstPivot.StartRow, firstPivot.EndRow, destWorksheet.Cells, 0);
destWorksheet.Cells.CopyRows(secondPivot.StartRow, secondPivot.EndRow, destWorksheet.Cells, 21); // start after first block
```

### Bevara stilar och villkorsstyrd formatering

`CopyRows` kopierar cellstilar automatiskt. Om du behöver bevara arbetsboks‑omfattande namngivna stilar eller anpassade talformat, anropa `destWorkbook.Worksheets[0].CopyStyle` innan du sparar.

### Arbeta med stora arbetsböcker

För filer större än 100 MB, överväg att använda `Workbook.LoadOptions` med `MemorySetting` satt till `MemorySetting.MemoryPreference` för att minska minnesbelastningen.

```csharp
LoadOptions loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeSrc = new Workbook(@"bigfile.xlsx", loadOptions);
```

## Fullständig källkod (klar att köra)

Nedan är hela programmet, inklusive `using`‑direktiv och kommentarer. Kopiera det till ett nytt konsolprojekt och ersätt `YOUR_DIRECTORY` med den faktiska sökvägen.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the source workbook (load excel workbook c#)
        // -------------------------------------------------
        Workbook srcWorkbook = new Workbook(@"YOUR_DIRECTORY\Source.xlsx");

        // -------------------------------------------------
        // Step 2: Define the area that contains the pivot table
        // -------------------------------------------------
        // Adjust the indices if your pivot occupies a different range.
        CellArea sourceRange = new CellArea(0, 0, 20, 10); // A1:K21

        // -------------------------------------------------
        // Step 3: Create the destination workbook
        // -------------------------------------------------
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.Worksheets[0];

        // -------------------------------------------------
        // Step 4: Copy rows (how to copy pivot table)
        // -------------------------------------------------
        destWorksheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            destWorksheet.Cells,
            0);

        // -------------------------------------------------
        // Step 5: Save the new file (copy range to new workbook)
        // -------------------------------------------------
        destWorkbook.Save(@"YOUR_DIRECTORY\CopyWithPivot.xlsx");

        Console.WriteLine("Pivot table copied successfully!");
    }
}
```

Kör programmet (`dotnet run` eller `Ctrl+F5` i Visual Studio). Efter körning, öppna `CopyWithPivot.xlsx` för att verifiera att pivottabellen beter sig exakt som originalet.

## Vanliga frågor

**Q: Fungerar detta med makron eller VBA‑aktiverade arbetsböcker?**  
A: Aspose.Cells kan läsa makro‑aktiverade filer (`.xlsm`), men makrokoden kopieras inte. Pivottabellen själv bevaras eftersom den är en del av kalkylbladets XML.

**Q: Vad händer om pivottabellen använder en extern datakälla?**  
A: Kopieringsoperationen inkluderar bara den cachade datan. Om destinationsarboken ska uppdateras från den ursprungliga källan måste du konfigurera datakopplingen manuellt.

**Q: Kan jag kopiera pivottabellen utan de underliggande dataraderna?**  
A: Nej. En pivottabell behöver sin cache. Det mest pålitliga sättet är att kopiera de rader som innehåller cachen, som demonstrerat. Du kan senare dölja dessa rader om du inte vill att de ska synas.

## Slutsats

Du vet nu **how to copy pivot table** från en Excel‑fil till en annan med C#. Tutorialen täckte **load excel workbook c#**, definierade **copy range to new workbook**, och använde Aspose.Cells `CopyRows`‑metod för att hålla pivottabellen intakt. Med det kompletta, körbara exemplet kan du integrera detta mönster i rapporterings‑pipelines, automatiserade exportverktyg eller vilket scenario som helst där en pivottabell måste flyttas mellan arbetsböcker.

### Nästa steg

* Utforska **Aspose.Cells**‑funktioner såsom att uppdatera pivottabeller programatiskt.  
* Kombinera detta tillvägagångssätt med **ExcelPackage** (EPPlus) om du behöver ett open‑source‑alternativ.  
* Automatisera kopiering över flera blad genom att loopa igenom `srcWorkbook.Worksheets`.  

Känn dig fri att experimentera med olika områden, lägga till anpassad formatering eller bädda in logiken i en större databehandlings‑tjänst. Lycka till med kodningen!


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create New Workbook in C# – Copy Pivot Table](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)
- [How to copy pivot table in Excel with C# and Aspose.Cells](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-excel-with-c-and-aspose-cells/)
- [Copy pivot table to new workbook, export shape to PowerPoint](/cells/english/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}