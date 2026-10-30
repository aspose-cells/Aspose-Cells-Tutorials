---
category: general
date: 2026-08-07
description: Skapa Excel från JSON med Aspose.Cells Smart Marker – lär dig hur du
  fyller i en Excel‑mall, använder dynamisk bladnamngivning och genererar flera kalkylblad.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- populate excel template
- dynamic sheet naming
- generate multiple worksheets
- aspose.cells smart marker
language: sv
lastmod: 2026-08-07
og_description: Skapa Excel från JSON med Aspose.Cells Smart Marker för att snabbt
  fylla i mallar, använda dynamisk bladnamngivning och generera flera kalkylblad.
og_image_alt: Screenshot of generated Excel workbook with multiple dynamically named
  sheets
og_title: Skapa Excel från JSON – Aspose.Cells Smart Marker‑guide
schemas:
- author: Aspose
  dateModified: '2026-08-07'
  description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  headline: Create Excel from JSON with Aspose.Cells Smart Marker
  type: TechArticle
- description: Create Excel from JSON using Aspose.Cells Smart Marker – learn how
    to populate an Excel template, apply dynamic sheet naming, and generate multiple
    worksheets.
  name: Create Excel from JSON with Aspose.Cells Smart Marker
  steps:
  - name: Define the JSON‑compatible source data
    text: '```csharp // Step 1: Define the source data that will be merged into the
      workbook var ordersData = new { Orders = new[] { new { Id = 1, Items = new[]
      { "Apple", "Banana" } }, new { Id = 2, Items = new[] { "Orange" } } } }; ```'
  - name: Prepare the workbook template and insert a Smart Marker
    text: '```csharp // Step 2: Create a new workbook and place a Smart Marker that
      references the data collection var workbook = new Workbook(); // creates an
      empty workbook workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}"); ```'
  - name: Configure dynamic sheet naming
    text: '```csharp // Step 3: Configure how duplicated detail sheets should be named
      during processing var smartMarkerOptions = new SmartMarkerOptions { // {0} will
      be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …) DetailSheetNewName
      = "DetailSheet_{0}" }; ```'
  - name: Process the template with the data and naming options
    text: '```csharp // Step 4: Process the workbook with the data and the naming
      options var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
      smartMarkerProcessor.Process(ordersData); ```'
  - name: Save the resulting workbook
    text: '```csharp // Step 5: Save the resulting workbook – the detail sheets are
      created automatically workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
      ```'
  - name: Populate Excel template with additional fields
    text: 'If your JSON includes more properties (e.g., `CustomerName`, `TotalAmount`),
      add corresponding markers to the template:'
  - name: Generate multiple worksheets from nested collections
    text: 'You can create a second level of duplication by placing a marker inside
      the detail sheet that references a nested collection, such as `Items`:'
  - name: Custom naming with data from the record
    text: '```csharp var smartMarkerOptions = new SmartMarkerOptions { DetailSheetNewName
      = "Order_{Id}" }; ```'
  - name: Next steps
    text: '* Explore **conditional formatting** inside the detail sheet to highlight
      high‑value orders. * Replace the anonymous object with a strongly typed model
      deserialized via `System.Text.Json`. * Combine Smart Markers with **PivotTable**
      generation for advanced reporting.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Skapa Excel från JSON med Aspose.Cells Smart Marker
url: /sv/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel från JSON med Aspose.Cells Smart Marker

Om du behöver **skapa Excel från JSON**, visar den här handledningen en komplett, produktionsklar lösning. Du kommer att se hur du **fyller i en Excel‑mall**, konfigurerar **dynamisk bladnamngivning** och **genererar flera arbetsblad** automatiskt med **Aspose.Cells Smart Marker**‑motorn.

Guiden går dig igenom varje nödvändigt steg, från att definiera JSON‑liknande källobjekt till att spara den slutliga arbetsboken. Inga externa skript behövs, och koden körs på .NET 6 eller senare.

## Vad du kommer att uppnå

* Läs in ett JSON‑liknande dataobjekt i minnet.  
* Infoga en Smart Marker‑platshållare i en arbetsboksmall.  
* Applicera ett namnmönster så att varje duplicerat detaljblad får ett unikt namn.  
* Bearbeta mallen för att skapa ett separat arbetsblad för varje order i samlingen.  
* Spara resultatet som en `.xlsx`‑fil klar för vidare konsumtion.

Förutsättningar: Visual Studio 2022 (eller någon C#‑IDE), .NET 6+ och **Aspose.Cells**‑NuGet‑paketet. Exemplet använder C#; samma koncept gäller för VB.NET eller andra .NET‑språk.

## Skapa Excel från JSON – övergripande arbetsflöde

Följande avsnitt delar upp arbetsflödet i fem logiska steg. Varje steg innehåller den exakta koden du behöver, en förklaring till varför det är viktigt och tips för att skala lösningen.

### Steg 1: Definiera den JSON‑kompatibla källdata

```csharp
// Step 1: Define the source data that will be merged into the workbook
var ordersData = new
{
    Orders = new[]
    {
        new { Id = 1, Items = new[] { "Apple", "Banana" } },
        new { Id = 2, Items = new[] { "Orange" } }
    }
};
```

**Varför detta är viktigt** – `ordersData`‑objektet speglar strukturen du skulle få från ett riktigt JSON‑API. Aspose.Cells Smart Marker läser offentliga egenskaper, så en anonym typ fungerar så länge egenskapsnamnen matchar markörtaggarna (`{{Orders}}`). När du senare ersätter den anonyma typen med ett deserialiserat JSON‑objekt krävs inga kodändringar.

### Steg 2: Förbered arbetsboksmallen och infoga en Smart Marker

```csharp
// Step 2: Create a new workbook and place a Smart Marker that references the data collection
var workbook = new Workbook();                     // creates an empty workbook
workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");
```

**Varför detta är viktigt** – Markören `{{Orders}}` talar om för processorn att iterera över `Orders`‑samlingen. Genom att placera markören i cell `A1` på det första bladet blir det bladet *master*-bladet. Processorn kommer att klona detta blad för varje order och bevara all formatering du lägger till senare.

> **Tips:** Om du har en fördesignad mall (t.ex. med rubriker, formler eller styling), ladda den med `new Workbook("Template.xlsx")` istället för att skapa en tom arbetsbok.

### Steg 3: Konfigurera dynamisk bladnamngivning

```csharp
// Step 3: Configure how duplicated detail sheets should be named during processing
var smartMarkerOptions = new SmartMarkerOptions
{
    // {0} will be replaced by an incremental index (DetailSheet_1, DetailSheet_2, …)
    DetailSheetNewName = "DetailSheet_{0}"
};
```

**Varför detta är viktigt** – Som standard namnger Aspose.Cells duplicerade blad `Sheet1`, `Sheet2` osv. Mönstret `DetailSheetNewName` infogar ett inkrementellt index (`{0}`) så att varje blad får ett meningsfullt namn. Du kan bädda in ytterligare platshållare (t.ex. `{Id}`) för att inkludera data från den aktuella posten.

> **Pro‑tips:** Använd `DetailSheetNewName = "Order_{Id}"` för att namnge blad efter orderidentifieraren, vilket gör navigeringen enklare i stora arbetsböcker.

### Steg 4: Bearbeta mallen med data och namngivningsalternativ

```csharp
// Step 4: Process the workbook with the data and the naming options
var smartMarkerProcessor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
smartMarkerProcessor.Process(ordersData);
```

**Varför detta är viktigt** – `SmartMarkerProcessor` sammanslår `ordersData` i arbetsboken, skapar ett nytt blad för varje element i `Orders` och tillämpar namnmönstret som definierades tidigare. Processorn expanderar också eventuella nästlade samlingar (t.ex. `Items`) om du lägger till ytterligare markörer i detaljbladet.

### Steg 5: Spara den resulterande arbetsboken

```csharp
// Step 5: Save the resulting workbook – the detail sheets are created automatically
workbook.Save("YOUR_DIRECTORY/SmartMarkerDupSheets.xlsx");
```

**Varför detta är viktigt** – `Save`‑metoden skriver den fullt ifyllda arbetsboken till disk. Filen innehåller nu ett master‑blad (som kan döljas eller tas bort) och en serie detaljblad namngivna `DetailSheet_1`, `DetailSheet_2`, …, där varje blad innehåller data för en enskild order.

#### Förväntad output

| Sheet name        | Innehåll (förenklat)                     |
|-------------------|------------------------------------------|
| DetailSheet_1     | Order Id = 1, Items: Apple, Banana       |
| DetailSheet_2     | Order Id = 2, Items: Orange              |

Alla blad behåller all formatering du applicerade på master‑bladet innan bearbetning.

## Avancerade variationer

### Fyll i Excel‑mall med ytterligare fält

Om ditt JSON innehåller fler egenskaper (t.ex. `CustomerName`, `TotalAmount`), lägg till motsvarande markörer i mallen:

```csharp
workbook.Worksheets[0].Cells["B1"].PutValue("{{CustomerName}}");
workbook.Worksheets[0].Cells["C1"].PutValue("{{TotalAmount}}");
```

Processorn kommer att ersätta varje markör med det matchande egenskapsvärdet.

### Generera flera arbetsblad från nästlade samlingar

Du kan skapa en andra nivå av duplicering genom att placera en markör i detaljbladet som refererar till en nästlad samling, såsom `Items`:

```csharp
// Inside the detail sheet (e.g., cell A2)
workbook.Worksheets[0].Cells["A2"].PutValue("{{Items}}");

// Inside the same sheet, cell B2 will list each item
workbook.Worksheets[0].Cells["B2"].PutValue("{{Items}}");
```

Under bearbetning skapar Aspose.Cells en rad för varje objekt i `Items`‑arrayen, vilket låter dig generera artikellistor per order.

### Anpassad namngivning med data från posten

```csharp
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheetNewName = "Order_{Id}"
};
```

Nu är bladen namngivna `Order_1`, `Order_2`, vilket matchar bladnamnet med affärsidentifieraren.

## Vanliga fallgropar och hur man undviker dem

| Fallgrop                              | Lösning |
|--------------------------------------|----------|
| Markörtext matchar inte egenskapsnamnet (skiftlägeskänsligt) | Se till att markören (`{{Orders}}`) matchar egenskapen exakt, inklusive skiftläge. |
| Mallen innehåller sammanslagna celler som sträcker sig över markörområdet | Ta bort sammanslagning av celler eller placera markören i en enskild, osammanslagen cell för att undvika oväntade layoutförändringar. |
| Stora JSON‑samlingar orsakar minnesbelastning | Bearbeta data i batcher eller strömma JSON till en `DataTable` och använd `SmartMarkerProcessor` med `DataSource`. |
| Sparad filsökväg är ogiltig | Använd `Path.Combine(Environment.CurrentDirectory, "output.xlsx")` eller verifiera skrivbehörigheter. |

## Fullt fungerande exempel

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1️⃣ Define JSON‑compatible data
        var ordersData = new
        {
            Orders = new[]
            {
                new { Id = 1, Items = new[] { "Apple", "Banana" } },
                new { Id = 2, Items = new[] { "Orange" } }
            }
        };

        // 2️⃣ Create workbook and add master Smart Marker
        var workbook = new Workbook();
        workbook.Worksheets[0].Cells["A1"].PutValue("{{Orders}}");

        // 3️⃣ Set up dynamic sheet naming
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheetNewName = "DetailSheet_{0}"
        };

        // 4️⃣ Process template with data
        var processor = new SmartMarkerProcessor(workbook, smartMarkerOptions);
        processor.Process(ordersData);

        // 5️⃣ Save the result
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "SmartMarkerDupSheets.xlsx");
        workbook.Save(outputPath);
    }
}
```

När programmet körs genereras en Excel‑fil på skrivbordet som innehåller två detaljblad (`DetailSheet_1` och `DetailSheet_2`). Varje blad återspeglar den motsvarande orderposten.

## Slutsats

Du vet nu hur du **skapar Excel från JSON** med **Aspose.Cells Smart Marker**, hur du **fyller i en Excel‑mall**, tillämpar **dynamisk bladnamngivning** och **genererar flera arbetsblad** automatiskt. Samma mönster kan skalas till dussintals eller tusentals poster, stöder nästlade samlingar och integreras sömlöst med vilket .NET‑JSON‑deserialiseringsbibliotek som helst.

### Nästa steg

* Utforska **villkorsstyrd formatering** i detaljbladet för att markera högvärdesordrar.  
* Ersätt det anonyma objektet med en starkt typad modell deserialiserad via `System.Text.Json`.  
* Kombinera Smart Markers med **PivotTable**‑generering för avancerad rapportering.  

Experimentera med namnmönstret, lägg till fler markörer och integrera detta arbetsflöde i dina befintliga data‑export‑pipelines. Lycka till med kodningen!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Generera dynamiska Excel‑rapporter med Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Fyll i Excel med data med Aspose.Cells och Smart Markers](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [Hur man skapar och slår ihop Excel‑arbetsböcker med Aspose.Cells för Java | Komplett guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}