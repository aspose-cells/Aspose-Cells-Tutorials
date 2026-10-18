---
category: general
date: 2026-10-10
description: Tillämpa talformat i Excel snabbt genom att importera en DataTable, ange
  datum‑ och valutformat samt bevara rubrikraden i Excel i ett enda steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: sv
lastmod: 2026-10-10
og_description: Tillämpa talformat i Excel i C# med Aspose.Cells. Lär dig att ställa
  in datumformat i Excel, ställa in valutformat i Excel och bevara rubrikraden i Excel
  när du importerar en DataTable.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: Använd talformat i Excel i C# – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Hur man tillämpar talformat i Excel med Aspose.Cells
url: /sv/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man tillämpar talformat i Excel med Aspose.Cells

Om du behöver **apply number format excel** medan du laddar data från en `DataTable`, visar den här guiden exakt hur. Du kommer också att lära dig hur du **set date format excel**, **set currency format excel**, och **preserve header row excel** under importen, så att det resulterande kalkylbladet ser professionellt ut utan extra efterbehandling.

Vi kommer att gå igenom allt från att installera biblioteket till att skriva ett komplett, körbart kodexempel. I slutet kommer du att kunna importera vilken `DataTable` som helst till en Excel-arbetsbok, automatiskt formatera numeriska kolumner och behålla rubrikraden intakt – allt på bara några rader C#.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.6+)
* Visual Studio 2022 (eller någon C#‑IDE du föredrar)
* **Aspose.Cells for .NET** – installera via NuGet:

```bash
dotnet add package Aspose.Cells
```

* En `DataTable`‑källa – exemplet använder en hjälpfunktion `GetTable()` som returnerar exempeldata.

> **Proffstips:** Aspose.Cells är ett kommersiellt bibliotek, men det erbjuder ett gratis utvärderingsläge som inaktiverar vattenstämpeln i upp till 30 dagar.

## Steg 1: Skapa en arbetsbok och få åtkomst till det första kalkylbladet

Workbook‑objektet är ingångspunkten för alla Excel‑operationer. Att skapa en ny arbetsbok ger dig ett standardkalkylblad på index 0.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Varför detta steg?*  
`Workbook` hanterar filformat, beräkningsmotor och stilarkiv. Att tidigt få åtkomst till `Worksheet` låter oss skicka målbladet till importmetoden senare.

## Steg 2: Hämta källdata som en DataTable

I riktiga projekt kommer data ofta från en databasfråga, en CSV‑parser eller ett API‑svar. För illustration genererar vi en enkel `DataTable` med tre kolumner: **Product**, **Price** och **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Varför detta steg?*  
En `DataTable` ger en tabellbaserad minnesrepresentation som Aspose.Cells kan importera direkt, och bevarar kolumnordning och datatyper.

## Steg 3: Förbered en `Style`‑array – en stil per kolumn

Aspose.Cells låter dig tillämpa en separat stil på varje kolumn under import genom att skicka en array av `Style`‑objekt. Arrayens längd måste matcha antalet kolumner i källtabellen.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Varför detta steg?*  
Om du hoppar över den explicita skapelsen (`CreateStyle()`), kommer ett försök att sätta `Number` att kasta ett `NullReferenceException`. Att initiera varje `Style` säkerställer att de senare tilldelningarna lyckas.

## Steg 4: Tilldela talformat – valuta och datum

Excel identifierar inbyggda talformat med ID.  
* **14** – Valuta (t.ex. `$1,234.00`)  
* **22** – Kort datum (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Obs:** Om du behöver ett anpassat format (t.ex. `"¥#,##0.00"`), använd `Style.Custom = "¥#,##0.00"` istället för ett inbyggt ID.

*Varför detta steg?*  
Att tillämpa rätt **number format** vid importen eliminerar behovet av ett andra pass som loopar igenom celler för att ändra formatering. Det garanterar också att **format excel cells date** och **set currency format excel** är konsekventa i alla rader.

## Steg 5: Importera DataTable samtidigt som rubrikraden bevaras

`ImportDataTable`‑metoden kan kopiera data, behålla den första raden som rubrik och tillämpa de kolumnstilar vi förberedde.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Förväntad utskrift** – Öppna `FormattedReport.xlsx` så ser du:

| Product | Price (currency) | ReleaseDate (date) |
|---------|------------------|--------------------|
| Widget A| $12.99           | 05/01/2023         |
| Widget B| $23.50           | 06/15/2023         |
| Widget C| $7.75            | 07/30/2023         |

Rubrikraden är intakt, **Price**‑kolumnen visar valutasymbolen och **ReleaseDate**‑kolumnen visar ett kort datumformat – allt utan ytterligare stilkod.

### Hantera vanliga kantfall

| Situation                               | Lösning |
|----------------------------------------|----------|
| **Fler kolumner än stilar**           | Se till att `columnStyles.Length` är lika med `sourceTable.Columns.Count`. Saknade poster får arbetsbokens standardstil som standard. |
| **Null‑värden i numeriska kolumner**   | Excel behandlar `null` som en tom cell; talformatet gäller fortfarande när ett värde senare matas in. |
| **Anpassad lokalspecifik valuta**      | Använd `columnStyles[i].Custom = "\"€\"#,##0.00"` och sätt `columnStyles[i].Number = -1` för att inaktivera det inbyggda ID‑talet. |
| **Stora tabeller ( > 100 000 rader )** | Överväg att använda `ImportDataTable`‑överladdning med `ImportTableOptions` för att strömma data och minska minnesbelastningen. |
| **Applicera samma stil på flera kolumner** | Återanvänd samma `Style`‑instans i arrayen (t.ex. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Använda en anpassad formatsträng

Om de inbyggda ID‑en inte uppfyller dina behov kan du definiera ett anpassat talformat:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Detta tillvägagångssätt ger dig full kontroll över **format excel cells date** och **set currency format excel** utöver de fördefinierade ID‑en.

## Slutsats

Du vet nu hur du **apply number format excel** effektivt när du importerar en `DataTable` med Aspose.Cells. Genom att skapa en per‑kolumn `Style`‑array, tilldela inbyggda eller anpassade tal‑ID:n, och använda `ImportDataTable`‑överladdningen som **preserve header row excel**, kan du generera färdiga arbetsblad i ett enda steg.

### Vad blir nästa?

* Utforska **set date format excel** med anpassade mönster som `"dddd, mmmm dd, yyyy"`.
* Kombinera denna teknik med **conditional formatting** för att markera värden utanför intervallet.
* Använd **format excel cells date** i pivottabeller eller diagram för dynamisk rapportering.

Känn dig fri att experimentera med olika tal‑ID:n eller anpassade strängar för att matcha din organisations stilguide. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [apply number format excel – Steg‑för‑steg‑guide för att formatera kolumner](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Skapa Excel‑arbetsbok C# – Tillämpa valutformat och importera DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Ställ in datumformat i Excel med C# – Full guide för importformatering](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}