---
category: general
date: 2026-09-18
description: Lär dig hur du expanderar en matris i Excel med EXPAND‑funktionen, fyller
  i en Excel‑mall och skapar ett dynamiskt område i ett Excel‑ark med C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- populate excel template
- dynamic range excel
- use expand function
- expand array formula
language: sv
lastmod: 2026-09-18
og_description: Hur man expanderar en matris i Excel med EXPAND‑funktionen, fyller
  i en Excel‑mall och bygger en dynamisk områdeslösning i Excel med C#‑kod.
og_image_alt: Excel worksheet showing expanded 5x5 array and Smart Markers result
og_title: Hur man expanderar en matris i Excel och fyller i en mall
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to expand array in Excel using the EXPAND function, populate
    an Excel template, and create a dynamic range Excel worksheet with C#.
  headline: How to expand array in Excel and populate a template
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Hur man expanderar en matris i Excel och fyller i en mall
url: /sv/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här expanderar du en array i Excel och fyller i en mall

Om du behöver **expanda en array** i Excel medan du fyller i en fördesignad mall, visar den här guiden en komplett, end‑to‑end‑lösning. Genom att använda `EXPAND`‑funktionen tillsammans med Aspose.Cells Smart Markers kan du förvandla en enda cellreferens till ett 5 × 5‑område och automatiskt ersätta markörer som `{IsActive}` med levande data.

Du får se hur du **populerar excel‑mall**, skapar ett **dynamiskt område i Excel**, och korrekt **använder expand‑funktionen** i ett C#‑projekt. I slutet av tutorialen har du ett körbart program som laddar en `.xlsx`‑fil, expanderar en array‑formel, applicerar Smart Markers och sparar resultatet.

## Förutsättningar

* .NET 6.0 eller senare (koden fungerar också med .NET Core 3.1+)
* Aspose.Cells for .NET (NuGet‑paket `Aspose.Cells`)
* En Excel‑arbetsbok som innehåller en platshållar‑formelcell (t.ex. `B2`) och en Smart Marker som `{IsActive}`
* Grundläggande kunskap om C# och Excel‑formler

> **Pro‑tips:** `EXPAND`‑funktionen finns endast i Excel för Microsoft 365 och Excel 2021+. Äldre versioner ger ett `#NAME?`‑fel.

## Steg 1: Så här expanderar du en array med EXPAND‑funktionen

Det första steget är att ladda arbetsboken och skriva en `EXPAND`‑formel som förvandlar en enda källcell till en större matris.  

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the workbook that contains the template layout
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Apply the EXPAND function to cell B2.
        // =EXPAND(A2,5,5) expands the array that starts at A2 into a 5‑row by 5‑column range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";
```

Varför detta är viktigt: `EXPAND` tar bort behovet av att manuellt kopiera formler över rader och kolumner. När källcellen (`A2`) ändras uppdateras hela 5 × 5‑blocket automatiskt, vilket ger dig ett **dynamiskt område i Excel** som reagerar på datakörningar.

## Steg 2: Populera Excel‑mall med Smart Markers

Smart Markers låter dig bädda in platshållare i mallen som ersätts med värden från ett C#‑objekt. Detta är det smidigaste sättet att **populera excel‑mall** utan att skriva kod cell‑för‑cell.

```csharp
        // Prepare an anonymous object that matches the marker names in the template.
        var data = new { IsActive = true };

        // Apply Smart Markers. The marker {IsActive} inside a formula like
        // =IF({IsActive}, "Active", "Inactive") will be replaced with the value from the object.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);
```

Anropet `SmartMarkersProcessor().Apply` skannar hela bladet, hittar `{IsActive}` och injicerar det booleska värdet. Formeln utvärderas då automatiskt till `"Active"` eller `"Inactive"`.

## Steg 3: Verifiera det expanderade området och det populära resultatet

Efter att både `EXPAND`‑formeln och Smart Markers har applicerats kan du programatiskt läsa några celler för att säkerställa att allt fungerade som förväntat.

```csharp
        // Optional: read a cell from the expanded block to confirm the value.
        var sampleValue = ws.Cells["B2"].Value; // top‑left cell of the expanded range
        Console.WriteLine($"Top‑left of expanded range: {sampleValue}");

        // Read the marker result cell (assume it is C2)
        var status = ws.Cells["C2"].StringValue;
        Console.WriteLine($"Status from Smart Marker: {status}");
```

När programmet körs bör det skriva ut det ursprungliga värdet från `A2` (eller array‑resultatet) samt antingen **Active** eller **Inactive** beroende på `IsActive`‑flaggan.

## Steg 4: Spara arbetsboken – det slutgiltiga resultatet

Till sist skriver du den modifierade arbetsboken till disk. Detta steg demonstrerar hela flödet från laddning, expansion, populering till lagring av filen.

```csharp
        // Save the workbook with the expanded array and populated markers.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Den sparade `output.xlsx` innehåller nu en 5 × 5‑matris genererad av `EXPAND`‑formeln och en cell som speglar värdet av `{IsActive}`. Öppna filen i Excel för att se det dynamiska området i aktion.

## Edge cases och bästa praxis

| Situation                              | Rekommendation                                                                 |
|----------------------------------------|--------------------------------------------------------------------------------|
| Excel‑version stöder inte `EXPAND`    | Falla tillbaka till klassiska `=OFFSET`‑ eller `=INDEX`‑formler, eller uppgradera till Office 365. |
| Behöver expandera till variabel storlek| Använd `ROWS(source)` och `COLUMNS(source)` inuti `EXPAND` för sann dynamik.   |
| Flera Smart Markers i samma blad       | Anropa `SmartMarkersProcessor().Apply` en gång med ett sammansatt dataobjekt.      |
| Stora arbetsböcker ( > 10 000 rader)   | Inaktivera beräkning medan formler skrivs (`workbook.Settings.CheckFormula = false`). |

## Fullt fungerande exempel

Nedan är det kompletta, självständiga programmet som du kan kopiera‑och‑klistra in i ett nytt konsolprojekt.

```csharp
using System;
using Aspose.Cells;

class ExpandArrayDemo
{
    static void Main()
    {
        // 1️⃣ Load the workbook that serves as the template.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Write the EXPAND formula to create a 5x5 dynamic range.
        ws.Cells["B2"].Formula = "=EXPAND(A2,5,5)";

        // 3️⃣ Prepare data for Smart Markers.
        var data = new { IsActive = true };

        // 4️⃣ Apply Smart Markers – replaces {IsActive} in any formula or text.
        workbook.Worksheets[0].SmartMarkersProcessor().Apply(data);

        // 5️⃣ (Optional) Verify a couple of cells.
        Console.WriteLine($"Expanded top‑left: {ws.Cells["B2"].Value}");
        Console.WriteLine($"Marker result: {ws.Cells["C2"].StringValue}");

        // 6️⃣ Save the final workbook.
        workbook.Save("YOUR_DIRECTORY/output.xlsx");
        Console.WriteLine("Workbook saved successfully.");
    }
}
```

**Förväntad utskrift när du kör programmet** (förutsatt att `A2` innehåller talet `42`):

```
Expanded top‑left: 42
Marker result: Active
Workbook saved successfully.
```

När du öppnar `output.xlsx` visas ett 5 × 5‑block fyllt med värden härledda från `A2` samt en cell som visar **Active**.

## Slutsats

Du vet nu **hur du expanderar en array** i Excel med `EXPAND`‑funktionen, hur du **populerar excel‑mall** med Smart Markers, och hur du bygger ett **dynamiskt område i Excel** som automatiskt anpassar sig efter källdata. Exemplet visar också det korrekta sättet att **använda expand‑funktionen** och **expandera array‑formeln** i ett verkligt C#‑automatiseringsscenario.

Nästa steg, överväg att utöka lösningen:

* Ersätt de fasta `5,5`‑dimensionerna med `ROWS(A2:A10), COLUMNS(A2:E2)` för riktigt variabla områden.
* Kombinera flera Smart Markers för att generera fullständiga rapporter (t.ex. medarbetarlistor, försäljningstabeller).
* Utforska Aspose.Cells‑styling‑API för att automatiskt formatera det expanderade blocket.

Känn dig fri att experimentera med olika källarrayar, markörnamn och arbetsbokslayouter. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

De följande tutorialerna täcker närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Export Data to Excel: Populate a Template from an Array in C#](/cells/english/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/)
- [How to create array in Excel with C# – Step-by-Step Guide](/cells/english/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/)
- [Processing Data Using Array Function in Excel](/cells/english/net/excel-formulas-and-calculation-options/processing-data-using-array-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}