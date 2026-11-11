---
category: general
date: 2026-09-27
description: Lär dig hur du kopierar en pivottabell i C# med Aspose.Cells. Inkluderar
  att kopiera rader med formatering, kopiera pivottabellen till ett annat blad och
  exportera pivottabellen till en ny arbetsbok.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: sv
lastmod: 2026-09-27
og_description: Hur man kopierar en pivottabell i C# med Aspose.Cells. Följ den steg‑för‑steg‑guiden
  för att kopiera rader med formatering, flytta en pivottabell till ett annat blad
  och exportera den till en ny arbetsbok.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: Hur man kopierar en pivottabell i C# – komplett Aspose.Cells-guide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Hur man kopierar en pivottabell i C# med Aspose.Cells
url: /sv/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här kopierar du en pivottabell i C# med Aspose.Cells

Om du behöver **kopiera en pivottabell** från ett kalkylblad till ett annat, kan kunskap om **hur man kopierar pivottabell** i C# med Aspose.Cells spara dig timmar av manuellt arbete. Metoden låter dig också **kopiera rader med formatering**, behålla pivottabellscachen intakt och till och med **exportera pivottabell till en ny arbetsbok** när du behöver en fristående fil.

Denna handledning går igenom hela arbetsflödet:

* skapa en arbetsbok,  
* kopiera pivottabellens område samtidigt som formateringen bevaras,  
* placera de kopierade data på ett nytt blad, och  
* spara resultatet som en separat fil.

Du får se varför den inbyggda `CopyRows`‑metoden är det mest pålitliga sättet att **kopiera pivottabell till ett annat blad**, och du får tips för att hantera kantfall som dolda rader eller externa datakällor.

## Förutsättningar

Innan du börjar, se till att du har:

| Krav | Varför det är viktigt |
|------|------------------------|
| .NET 6.0 eller senare | Aspose.Cells stödjer .NET 6+ och ger bästa prestanda. |
| Visual Studio 2022 (eller någon C#‑IDE) | Du behöver en editor som kan återställa NuGet‑paket. |
| Aspose.Cells for .NET (NuGet‑paket `Aspose.Cells`) | Detta bibliotek tillhandahåller `CopyRows`‑API‑t som används i exemplet. |
| En käll‑Excel‑fil (`source.xlsx`) som innehåller en pivottabell i området `A1:G20` | Koden kopierar detta specifika område; justera området om din pivottabell är större. |

Installera biblioteket med NuGet‑CLI eller Package Manager Console:

```bash
dotnet add package Aspose.Cells
```

## Steg 1: Ladda arbetsboken som innehåller pivottabellen

Den första raden skapar ett `Workbook`‑objekt som representerar hela Excel‑filen. Att ladda filen en gång ger dig läs‑/skriv‑åtkomst till varje kalkylblad.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Varför detta steg är viktigt** – Utan att ladda arbetsboken kan inga av de efterföljande `CopyRows`‑anropen referera till källdata eller pivottabellens cache.

## Steg 2: Förbered käll‑ och destinationsarbetsblad

Du behöver ett destinationsblad där den kopierade pivottabellen ska ligga. Koden nedan hämtar det första kalkylbladet (där den ursprungliga pivottabellen finns) och lägger till ett nytt blad med namnet **Copy**.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Proffstips:** Om destinationsbladet redan finns, anropa `Worksheets.RemoveAt(index)` först för att undvika dubbla namn.

## Steg 3: Definiera cellområdet som omsluter pivottabellen

Ett `CellArea`‑objekt beskriver de övre‑vänstra och nedre‑högra cellerna i det område du vill flytta. I detta exempel upptar pivottabellen `A1:G20`. Justera koordinaterna för större tabeller.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Steg 4: Kopiera rader med formatering och bevara pivottabellens cache

`CopyRows`‑metoden kopierar **rader** från källbladet till destinationsbladet. Genom att skicka `CopyOptions.CopyAll` säkerställer du att värden, formatering, diagram och inbäddade objekt – allt som ingår i en pivottabell – överförs.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Varför `CopyRows` fungerar bättre än `Copy` för pivottabeller

* `CopyRows` respekterar den interna pivottabellscachen, så den kopierade pivottabellen förblir funktionell.
* Den bevarar **kopiera rader med formatering** exakt som de visas i originalbladet.
* Till skillnad från en enkel `Copy` av ett område, flyttar den även dolda rader och eventuella associerade slicers.

## Steg 5: Spara arbetsboken med den kopierade pivottabellen

Till sist skriver du den modifierade arbetsboken till disk. Den nya filen innehåller originalbladet plus ett **Copy**‑blad som innehåller en fullt funktionell duplicering av den ursprungliga pivottabellen.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Förväntat resultat

När du öppnar `pivot_copied.xlsx`:

* Blad **Sheet1** innehåller fortfarande originaldata och pivottabell.
* Blad **Copy** visar en identisk pivottabell med samma layout, filter och formatering.
* Alla formler och datakopplingar förblir intakta eftersom pivottabellscachen kopierades tillsammans med raderna.

## Hur man kopierar pivottabell till ett annat blad i samma arbetsbok

Om du bara behöver pivottabellen i ett annat befintligt blad (t.ex. “Report”), ersätt steget för att skapa destinationsbladet med en referens till målbladet:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Detta kodsnutt demonstrerar **kopiera pivottabell till ett annat blad** utan att skapa ett nytt arbetsblad.

## Exportera pivottabell till ny arbetsbok

Ibland vill du ha pivottabellen i en helt separat fil. Efter kopieringen kan du ta bort alla kalkylblad förutom det som innehåller den kopierade pivottabellen och sedan spara:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Nu innehåller `pivot_only.xlsx` ett enda blad med den duplicerade pivottabellen, vilket uppfyller kravet **exportera pivottabell till ny arbetsbok**.

## Hur man kopierar Excel‑rader utan att förlora formatering

Samma `CopyRows`‑anrop fungerar för vilket område som helst, inte bara pivottabeller. Om du behöver **kopiera excel rows** som inkluderar villkorsstyrd formatering, datavalidering eller sammanslagna celler, använd samma metod:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

Eftersom `CopyOptions.CopyAll` överför allt ser destinationsraderna exakt ut som källraderna.

## Vanliga fallgropar och hur man undviker dem

| Fallgrop | Symtom | Lösning |
|----------|--------|---------|
| Källområdet inkluderar inte hela pivottabellen | Den kopierade pivottabellen blir avkortad. | Verifiera att `CellArea` täcker alla rader/kolumner i pivottabellen. |
| Destinationsbladet innehåller redan data | Överskrivna rader orsakar dataförlust. | Välj ett tomt blad eller börja kopiera från ett högre radindex. |
| Pivottabellen använder en extern datakälla | Kopian förlorar sin anslutning. | Efter kopiering, anropa `pivotTable.RefreshData()` för att återupprätta länken. |
| Dolda rader utelämnas | Vissa rader försvinner i kopian. | `CopyRows` kopierar automatiskt dolda rader; se till att du inte använder `CopyOptions.CopyValuesOnly`. |

## Fullständigt, körbart exempel

Nedan är ett självständigt program du kan klistra in i ett nytt konsolprojekt. Det demonstrerar varje steg som diskuteras ovan.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**När programmet körs** skapas `pivot_copied.xlsx` med en duplicerad version av originalpivottabellen på ett nytt blad med namnet **Copy**.

## Slutsats

Du vet nu **hur man kopierar en pivottabell** i C# med

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger vidare på teknikerna i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Skapa ny arbetsbok – Hur man kopierar ett arbetsblad med en pivottabell](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Kopiera pivottabell i C# – Komplett steg‑för‑steg‑guide](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [Hur man kopierar område med pivottabeller i C# – Komplett guide](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}