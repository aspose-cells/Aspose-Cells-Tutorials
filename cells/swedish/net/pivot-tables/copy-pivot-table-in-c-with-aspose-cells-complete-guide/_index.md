---
category: general
date: 2026-08-11
description: Kopiera pivottabell med C# och Aspose.Cells. Lär dig hur du laddar en
  Excel‑arbetsbok, duplicerar en pivottabell och bevarar dess formatering snabbt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- duplicate pivot table excel
- move pivot table cell
- load excel workbook c#
- preserve pivot formatting
language: sv
lastmod: 2026-08-11
og_description: Kopiera pivottabell i C# med Aspose.Cells. Den här guiden visar hur
  du laddar en Excel-arbetsbok, duplicerar en pivottabell och behåller all formatering
  intakt.
og_image_alt: Excel worksheet after copy pivot table operation
og_title: Kopiera pivottabell i C# – steg‑för‑steg Aspose.Cells‑handledning
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  headline: Copy pivot table in C# with Aspose.Cells – complete guide
  type: TechArticle
- description: Copy pivot table using C# and Aspose.Cells. Learn how to load an Excel
    workbook, duplicate a pivot table, and preserve its formatting quickly.
  name: Copy pivot table in C# with Aspose.Cells – complete guide
  steps:
  - name: Load Excel workbook C#
    text: Loading the workbook is the first action when you **load excel workbook
      c#**. Aspose.Cells reads the file into memory, giving you access to worksheets,
      cells, and pivot tables.
  - name: Identify and copy the pivot table range
    text: A pivot table lives inside a rectangular cell range. To **move pivot table
      cell** safely, you must copy the whole range, not just individual cells.
  - name: Save the workbook with the copied pivot table
    text: After copying, you simply save the workbook. The new file will contain both
      the original and the duplicated pivot table.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: Kopiera pivottabell i C# med Aspose.Cells – komplett guide
url: /sv/net/pivot-tables/copy-pivot-table-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy pivot table in C# with Aspose.Cells – complete guide

Om du behöver **copy pivot table** från en plats till en annan i en Excel-arbetsbok med C#, visar den här handledningen hur du gör. Du får se en kortfattad, end‑to‑end‑lösning som laddar arbetsboken, duplicerar pivottabellen och bevarar varje formateringsdetalj.

Att arbeta med Excel programatiskt innebär ofta att hantera komplexa objekt som pivottabeller. I den här guiden lär du dig att **duplicate pivot table excel** stil utan att förlora filter, beräknade fält eller formatering. Det enda förutsättningen är en referens till Aspose.Cells‑biblioteket, som ger dig full kontroll över Excel‑filer från .NET.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också på .NET Framework 4.7+)
* En giltig Aspose.Cells för .NET-licens (du kan använda den kostnadsfria utvärderingsversionen för testning)
* En Excel‑fil (`Source.xlsx`) som innehåller en pivottabell du vill kopiera
* En utvecklingsmiljö såsom Visual Studio 2022

## Så kopierar du pivottabell med Aspose.Cells

De grundläggande stegen är:

1. **Load Excel workbook C#** – öppna källfilen.
2. **Select the range that contains the pivot table** – inkludera hela pivottabellområdet.
3. **Copy the range to a new location** – pivottabellen förblir intakt.
4. **Save the workbook** – den nya filen innehåller den duplicerade pivottabellen.

Varje steg förklaras nedan med fullständig kod.

### Steg 1: Load Excel workbook C#

Att ladda arbetsboken är den första åtgärden när du **load excel workbook c#**. Aspose.Cells läser filen till minnet och ger dig åtkomst till arbetsblad, celler och pivottabeller.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Path to the source workbook that holds the original pivot table
        string sourcePath = @"C:\Data\Source.xlsx";

        // Load the workbook into memory
        Workbook workbook = new Workbook(sourcePath);
```

> **Why this matters:** Laddning av arbetsboken skapar ett `Workbook`‑objekt som representerar hela Excel‑filen. Alla efterföljande operationer arbetar på denna in‑memory‑representation, vilket är snabbare än att upprepade gånger komma åt filsystemet.

### Steg 2: Identify and copy the pivot table range

En pivottabell finns inom ett rektangulärt cellområde. För att **move pivot table cell** på ett säkert sätt måste du kopiera hela området, inte bara enskilda celler.

```csharp
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.Worksheets[0];

        // Define the range that encloses the pivot table.
        // Adjust "A1:G20" to match your actual pivot area.
        Range sourceRange = worksheet.Cells.CreateRange("A1:G20");

        // Copy the range to a new location, e.g., starting at I1.
        // The copy operation keeps the pivot table definition and formatting.
        sourceRange.Copy(worksheet.Cells, "I1");
```

> **Why this works:** `Range.Copy` duplicerar inte bara cellvärdena utan även den underliggande pivottabellcachen och formateringen. Detta är det rekommenderade sättet att **duplicate pivot table excel** utan att bygga om pivottabellen manuellt.

### Steg 3: Save the workbook with the copied pivot table

Efter kopieringen sparar du helt enkelt arbetsboken. Den nya filen kommer att innehålla både den ursprungliga och den duplicerade pivottabellen.

```csharp
        // Path for the new workbook that will contain the copied pivot table
        string destinationPath = @"C:\Data\CopyPivot.xlsx";

        // Save the workbook; all pivot information is preserved.
        workbook.Save(destinationPath);

        Console.WriteLine("Pivot table copied successfully to " + destinationPath);
    }
}
```

> **Why you should preserve formatting:** Kravet `preserve pivot formatting` uppfylls automatiskt eftersom Aspose.Cells behåller stilinformation under kopieringsoperationen. Ingen extra formateringskod behövs.

### Fullt fungerande exempel

Att sätta ihop de tre stegen ger dig ett komplett, körbart program:

```csharp
using System;
using Aspose.Cells;

class CopyPivotTableDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that contains the pivot table
        string sourceFile = @"C:\Data\Source.xlsx";
        Workbook workbook = new Workbook(sourceFile);

        // 2️⃣ Identify the pivot table range and copy it
        Worksheet sheet = workbook.Worksheets[0];
        Range pivotRange = sheet.Cells.CreateRange("A1:G20"); // adjust as needed
        pivotRange.Copy(sheet.Cells, "I1"); // copies the pivot table intact

        // 3️⃣ Save the workbook with the duplicated pivot table
        string targetFile = @"C:\Data\CopyPivot.xlsx";
        workbook.Save(targetFile);

        Console.WriteLine($"Copy pivot table operation completed. File saved at: {targetFile}");
    }
}
```

**Expected result:**  
Öppna `CopyPivot.xlsx` i Excel. Du kommer att se den ursprungliga pivottabellen oförändrad och en andra, identisk pivottabell som börjar i cell `I1`. Alla filter, beräknade fält och visuella stilar matchar källan.

## Vanliga variationer och edge cases

| Situation | How to handle it |
|-----------|------------------|
| **Pivot table spans a dynamic range** | Använd `PivotTable.PivotTableRange` för att hämta den exakta adressen vid körning istället för att hårdkoda `"A1:G20"`. |
| **You need to move the pivot table to another worksheet** | Anropa `sourceRange.Copy(otherWorksheet.Cells, "A1")` efter att ha skapat `Worksheet otherWorksheet = workbook.Worksheets[workbook.Worksheets.Add()]`. |
| **Preserving only formatting, not data** | Efter kopiering, rensa datavärdena med `targetRange.Clear(ClearOptions.Contents)` medan stilarna lämnas orörda. |
| **Large workbooks cause memory pressure** | Använd `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` för att låta Aspose.Cells strömma data. |
| **You want to rename the duplicated pivot table** | Få åtkomst till den nya pivottabellen via `sheet.PivotTables[sheet.PivotTables.Count - 1]` och sätt dess `Name`‑egenskap. |

Dessa tips hjälper dig att **move pivot table cell** positioner, **duplicate pivot table excel**‑filer, och behålla kravet **preserve pivot formatting** intakt.

## Pro‑tips för pålitlig kopiering

* **Pro tip:** Verifiera alltid att källområdet inkluderar hela pivottabellcachen. En saknad kolumn kan bryta den kopierade pivottabellen.
* **Watch out for merged cells** inside the range; they may cause `Copy` to throw an exception. Dela upp dem innan du kopierar eller justera området.
* **Performance tip:** Om du bara behöver kopiera pivottabellens definition (utan data), använd `PivotTable.Clone` istället för att kopiera hela området.

## Slutsats

Du vet nu hur du **copy pivot table** programatiskt i C# med Aspose.Cells samtidigt som du **preserve pivot formatting**, **load excel workbook c#**, och även **move pivot table cell** positioner över arbetsblad. Den kompletta lösningen laddar arbetsboken, duplicerar pivottabellsområdet och sparar en ny fil med båda tabellerna intakta.

Nästa steg kan vara att utforska **duplicate pivot table excel**‑scenarier såsom kopiering mellan olika arbetsböcker, eller automatisering av rapportgenerering med flera pivottabeller. För djupare anpassning, kolla in Aspose.Cells’ PivotTable‑API för att ändra filter, beräknade fält eller diagramkopplingar.

Lycka till med kodandet, och var gärna fri att experimentera med koden för att passa dina specifika Excel‑automatiseringsbehov!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig behärska ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Skapa ny Excel-arbetsbok – Kopiera & duplicera pivottabell](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Skapa en pivottabell i Excel med Aspose.Cells för .NET](/cells/english/net/pivot-tables/create-pivot-table/)
- [Effektivt ändra Excel-pivottabellslayouter med Aspose.Cells för .NET](/cells/english/net/data-analysis/change-excel-pivot-table-layouts-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}