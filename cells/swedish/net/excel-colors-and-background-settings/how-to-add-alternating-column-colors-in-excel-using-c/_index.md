---
category: general
date: 2026-10-01
description: alternerande kolumnfärger i Excel med C# – lär dig skapa en Excel‑fil
  från en DataTable, sätta cellbakgrundsfärg i C# och importera DataTable till Excel
  med stylade kolumner.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: sv
lastmod: 2026-10-01
og_description: Alternerande kolumnfärger i Excel gjort enkelt. Följ den här guiden
  för att skapa en Excel‑fil från en DataTable, sätta cellbakgrundsfärg i C#, och
  importera en DataTable till Excel med formaterade kolumner.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Lägg till alternerande kolumnfärger i Excel med C# – steg‑för‑steg guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Hur man lägger till alternerande kolumnfärger i Excel med C#
url: /sv/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man lägger till alternerande kolumnfärger i Excel med C#

Om du behöver **alternating column colors excel** i en rapport som genereras från din applikation, visar den här guiden en komplett lösning. Du kommer att se hur du skapar en Excel‑fil från en `DataTable`, sätter cellbakgrundsfärg C#‑stil, och importerar datatable till excel samtidigt som du tillämpar en distinkt stil på varje kolumn.

Tutorialen täcker allt du behöver: nödvändiga NuGet‑paket, ett komplett körbart kodexempel och förklaringar till varför varje steg är viktigt. I slutet har du en formaterad arbetsbok som kan öppnas direkt i Microsoft Excel.

## Förutsättningar

* .NET 6.0 (eller senare) SDK installerad  
* Visual Studio 2022 (eller någon C#‑kompatibel IDE)  
* Aspose.Cells for .NET‑biblioteket – installera det med  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells tillhandahåller klasserna `Workbook`, `Worksheet`, `Style` och `BackgroundType` som används i exemplet.

## Steg 1: Hämta källdata som en `DataTable`

Den första uppgiften är att hämta de data du vill exportera. I riktiga projekt kan du fylla `DataTable` från en databasfråga, ett API‑anrop eller någon in‑memory‑samling.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Varför detta är viktigt:**  
En `DataTable` är en universell behållare som mappar smidigt till ett Excel‑arbetsblad. Genom att använda en `DataTable` kan du **create excel file from datatable c#** utan att skriva anpassade loopar för varje kolumn.

## Steg 2: Skapa en ny arbetsbok och hämta dess första arbetsblad

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Förklaring:**  
`Workbook` är rotobjektet; `Worksheets[0]` ger dig standardbladet där data kommer att placeras.

## Steg 3: Förbered en distinkt stil för varje kolumn (alternerande bakgrundsfärger)

För att uppnå **alternating column colors excel** genererar vi en `Style` för varje kolumn och tilldelar en ljus bakgrundsfärg som växlar mellan två nyanser.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Varför vi använder en loop:**  
Loopen garanterar att **set cell background color c#** tillämpas konsekvent, även om antalet kolumner ändras vid körning. Detta gör lösningen robust för dynamiska rapporter.

## Steg 4: Importera `DataTable` till arbetsbladet och tillämpa kolumnstilarna

Aspose.Cells kan importera en `DataTable` direkt, och vi kan skicka in arrayen av stilar för att färga varje kolumn.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Vad som händer under huven:**  
`ImportDataTable` skriver rubrikraden, sedan varje datarad. Eftersom vi levererade `columnStyles` får varje cell i en given kolumn den motsvarande stilen, vilket ger oss de önskade alternerande färgerna.

## Steg 5: Spara den formaterade arbetsboken till en fil

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

När du öppnar *StyledTable.xlsx* i Excel kommer du att se varje kolumn skuggad alternerande, vilket gör tabellen lättare att läsa.

## Fullständigt, körbart exempel

När alla bitar sätts ihop, här är ett självständigt program som du kan kopiera, klistra in och köra.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Förväntat resultat

* En fil med namnet **StyledTable.xlsx** placerad i `C:\Temp\`.
* Arbetsbladet visar tre kolumner (`Id`, `Name`, `Score`) med alternerande bakgrundsfärger: kolumner 1 och 3 i *LightYellow*, kolumn 2 i *LightCyan*.
* Alla rader från `DataTable` visas under rubrikraden.

## Vanliga frågor och specialfall

| Fråga | Svar |
|-------|------|
| *Kan jag använda andra färger?* | Ja. Ersätt `System.Drawing.Color.LightYellow` och `LightCyan` med valfritt `System.Drawing.Color`‑värde. |
| *Vad händer om DataTable har många kolumner?* | Loopen skapar automatiskt en stil för varje kolumn, så mönstret skalar utan kodändringar. |
| *Behöver jag avyttra arbetsboken?* | Aspose.Cells implementerar `IDisposable`. Om du omsluter `Workbook` i ett `using`‑block frigörs resurserna omedelbart. |
| *Hur applicerar man samma alternerande färger på rader istället för kolumner?* | Skapa en `Style[]` för rader och anropa `worksheet.Cells.ImportDataTable(..., rowStyles)` – Aspose.Cells‑overloadar stödjer båda. |
| *Kan jag skriva filen direkt till en ström (t.ex. för ett web‑API)?* | Ja. Använd `workbook.Save(stream, SaveFormat.Xlsx);` istället för en filsökväg. |

## Tips från fältet

* **Pro tip:** Cacha stilobjekten om du genererar många arbetsblad i ett enda körning – att skapa en stil är relativt billigt, men återanvändning minskar minnesflödet.  
* **Watch out for:** När du använder `System.Drawing.Color` på icke‑Windows‑plattformar, lägg till `System.Drawing.Common`‑NuGet‑paketet och säkerställ att runtime stödjer GDI+.

## Slutsats

Du vet nu hur du **alternating column colors excel** genom att skapa en Excel‑fil från en `DataTable` i C#, sätta cellbakgrundsfärger med Aspose.Cells, och **import datatable to excel** med en stylad kolumnarray. Detta tillvägagångssätt är snabbt, underhållbart och fungerar med vilken datamängd som helst.

### Nästa steg

* Utforska **set cell background color c#** för villkorsstyrd formatering (t.ex. markera låga poäng).  
* Kombinera denna teknik med **create excel file from datatable c#** för att generera flikar‑rapporter.  
* Titta på Aspose.Cells‑diagram‑API för att lägga till visuella sammanfattningar i samma arbetsbok.

Känn dig fri att anpassa färgerna, filformatet eller datakällan för att passa ditt projekts behov. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Ställ in kolumnbakgrund i Excel med C# – Komplett guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Lägg till bakgrundsfärg excel – Alternerande radstilar i C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Skapa arbetsbok C# – Importera DataTable till Excel med stilar](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}