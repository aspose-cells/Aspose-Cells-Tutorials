---
category: general
date: 2026-11-16
description: Skapa Excel från JSON med SmartMarker. Lär dig hur du konverterar JSON
  till Excel, bäddar in JSON i Excel och sparar arbetsboken som xlsx på några minuter.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json
- convert json to excel
- embed json in excel
- save workbook xlsx
language: sv
lastmod: 2026-11-16
og_description: Skapa Excel från JSON snabbt. Den här handledningen visar hur du konverterar
  JSON till Excel, bäddar in JSON i Excel och sparar arbetsboken som xlsx med Aspose.Cells.
og_image_alt: Screenshot of an Excel worksheet showing JSON data inserted into a single
  cell
og_title: Skapa Excel från JSON med SmartMarker – steg‑för‑steg C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  headline: Create Excel from JSON with SmartMarker in C#
  type: TechArticle
- description: Create Excel from JSON using SmartMarker. Learn how to convert JSON
    to Excel, embed JSON in Excel, and save workbook xlsx in minutes.
  name: Create Excel from JSON with SmartMarker in C#
  steps:
  - name: Build and run the console app (`dotnet run`).
    text: Build and run the console app (`dotnet run`).
  - name: Verify the console prints the full path to the generated file.
    text: Verify the console prints the full path to the generated file.
  - name: Open the file in Excel or any spreadsheet viewer.
    text: Open the file in Excel or any spreadsheet viewer.
  - name: Confirm that cell A1 holds the JSON array string exactly as shown above.
    text: Confirm that cell A1 holds the JSON array string exactly as shown above.
  type: HowTo
tags:
- SmartMarker
- Aspose.Cells
- C#
- JSON
title: Skapa Excel från JSON med SmartMarker i C#
url: /sv/net/smart-markers-dynamic-data/create-excel-from-json-with-smartmarker-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel från JSON med SmartMarker i C#

Om du behöver **skapa Excel från JSON** i ett .NET‑projekt visar den här guiden en komplett, körbar lösning. Med Aspose.Cells Smart Marker‑processorn kan du **konvertera JSON till Excel**, bädda in JSON‑strängen direkt i en cell och **spara arbetsbok xlsx** utan att skriva någon manuell parsningkod.

Du kommer att se hur du registrerar en JSON‑datakälla, infogar en Smart Marker som skriver ut hela arrayen som en enda JSON‑sträng, bearbetar kalkylbladet och slutligen skriver filen till disk. I slutet av handledningen kan du generera en Excel‑fil som innehåller den ursprungliga JSON‑payloaden i cell A1, redo för efterföljande bearbetning eller rapportering.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7+)
- Aspose.Cells för .NET (NuGet‑paketet `Aspose.Cells`)
- Grundläggande kunskap om C# och JSON‑formatering
- En IDE såsom Visual Studio eller VS Code

## Steg 1: Ställ in projektet och importera namnrymder

Skapa en ny konsolapplikation och lägg till Aspose.Cells‑paketet:

```bash
dotnet new console -n JsonToExcelDemo
cd JsonToExcelDemo
dotnet add package Aspose.Cells
```

Inkludera sedan de nödvändiga namnrymderna högst upp i `Program.cs`:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
```

**Varför?**  
`Aspose.Cells` tillhandahåller arbetsboksmodellen, medan `Aspose.Cells.SmartMarkers` innehåller klassen `SmartMarkerProcessor` som tolkar `&=`‑markörerna i kalkylbladet.

## Steg 2: Definiera JSON‑datakällan

Placera JSON‑strängen i en variabel. I det här exemplet har vi en array av beställningar:

```csharp
// Step 2: Define the JSON data source
string json = @"{
    ""Orders"": [
        { ""Id"": 1, ""Amount"": 100 },
        { ""Id"": 2, ""Amount"": 150 }
    ]
}";
```

**Varför?**  
Smart Marker fungerar med vilken välformad JSON som helst. Att hålla JSON i en sträng låter dig registrera den direkt utan att behöva en fil på disk.

## Steg 3: Registrera JSON‑data med SmartMarkerProcessor

Skapa en `SmartMarkerProcessor`‑instans och associera JSON‑strängen med ett namn som du senare kommer att referera till i kalkylbladet:

```csharp
// Step 3: Register the JSON data with the Smart Marker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.RegisterJsonDataSource("OrdersJson", json);
```

**Varför?**  
`RegisterJsonDataSource` parsar JSON‑en och gör dess hierarki tillgänglig för Smart Markers. Namnet `"OrdersJson"` blir rotobjektet i marköruttrycken.

## Steg 4: Skapa en arbetsbok och infoga Smart Marker

Instansiera en ny arbetsbok, hämta dess första kalkylblad och skriv en Smart Marker i cell A1 som kommer att skriva ut hela `Orders`‑arrayen som en enda JSON‑sträng:

```csharp
// Step 4: Create a workbook and get the first worksheet
Worksheet ws = new Workbook().Worksheets[0];

// Insert a Smart Marker that outputs the whole array as a single JSON string
ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");
```

**Varför?**  
Uttrycket `OrdersJson.Orders.ArrayAsSingle` instruerar Smart Marker att ta `Orders`‑arrayen och serialisera den tillbaka till JSON, och placera resultatet i målcell. Detta är det enklaste sättet att **bädda in JSON i Excel**.

## Steg 5: Bearbeta kalkylbladet

Kör processorn så att den ersätter markören med den faktiska JSON‑strängen:

```csharp
// Step 5: Process the worksheet – the marker is replaced with the JSON array string
processor.Process(ws);
```

**Varför?**  
Bearbetning granskar varje cell för `&=`‑markörer, utvärderar dem mot de registrerade datakällorna och skriver tillbaka det utvärderade värdet till kalkylbladet.

## Steg 6: Spara arbetsboken som en .xlsx‑fil

Skriv slutligen arbetsboken till disk. Anpassa sökvägen till en mapp du har skrivrättighet till:

```csharp
// Step 6: Save the workbook
string outputPath = Path.Combine(
    Environment.CurrentDirectory,
    "JsonArraySingleCell.xlsx");

ws.Workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to: {outputPath}");
```

**Varför?**  
`SaveFormat.Xlsx` säkerställer att filen lagras i det moderna Office Open XML‑formatet, vilket uppfyller kravet **save workbook xlsx**.

## Fullständig källkod

När alla bitar sätts ihop, här är det kompletta, färdiga programmet:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // Step 2: Define the JSON data source
        string json = @"{
            ""Orders"": [
                { ""Id"": 1, ""Amount"": 100 },
                { ""Id"": 2, ""Amount"": 150 }
            ]
        }";

        // Step 3: Register the JSON data with the Smart Marker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.RegisterJsonDataSource("OrdersJson", json);

        // Step 4: Create a workbook and get the first worksheet
        Worksheet ws = new Workbook().Worksheets[0];

        // Insert a Smart Marker that will output the whole array as a single JSON string
        ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSingle");

        // Step 5: Process the worksheet – the marker is replaced with the JSON array string
        processor.Process(ws);

        // Step 6: Save the workbook
        string outputPath = Path.Combine(
            Environment.CurrentDirectory,
            "JsonArraySingleCell.xlsx");
        ws.Workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Förväntad utdata i Excel

Öppna `JsonArraySingleCell.xlsx`. Cell A1 kommer att innehålla:

```
[{"Id":1,"Amount":100},{"Id":2,"Amount":150}]
```

JSON‑strängen är en kompakt representation av den ursprungliga `Orders`‑arrayen, vilket gör den enkel att transportera eller konsumera i efterföljande Excel‑baserade arbetsflöden.

## Vanliga variationer och specialfall

| Situation | Justering |
|-----------|------------|
| **Flera JSON‑objekt** | Registrera varje objekt med ett unikt namn (t.ex. `processor.RegisterJsonDataSource("CustomerJson", customerJson);`) och referera till dem med separata markörer. |
| **Pretty‑printad JSON i en cell** | Använd alternativet `ArrayAsSinglePretty`: `ws.Cells["A1"].PutValue("&=OrdersJson.Orders.ArrayAsSinglePretty");` |
| **Stora JSON‑payloads** | Överväg att skriva JSON till ett dolt blad eller använda `DataTable`‑konvertering för bättre prestanda. |
| **Bädda in JSON i flera celler** | Placera olika markörer i andra celler, t.ex. `&=OrdersJson.Orders[0].Id` för att hämta enskilda fält. |

**Pro tip:** När du hanterar mycket stora JSON‑filer, öka arbetsbokens minnesbuffert (`WorkbookSettings.MemorySetting`) för att undvika `OutOfMemoryException`.

## Testa lösningen

1. Bygg och kör konsolappen (`dotnet run`).  
2. Verifiera att konsolen skriver ut hela sökvägen till den genererade filen.  
3. Öppna filen i Excel eller någon annan kalkylbladsvisare.  
4. Bekräfta att cell A1 innehåller JSON‑array‑strängen exakt som visat ovan.

Om cellen innehåller markörtexten (`&=OrdersJson...`) istället för JSON, dubbelkolla att processorn anropades **efter** att markören placerades och att JSON‑strängen är giltig.

## Slutsats

Du vet nu hur du **skapar Excel från JSON** med Aspose.Cells Smart Markers, hur du **konverterar JSON till Excel**, bäddar in JSON‑payloaden direkt i en cell och **sparar arbetsbok xlsx** med en enda kodrad. Detta tillvägagångssätt eliminerar manuell parsning, fungerar med vilken JSON‑struktur som helst och producerar en ren, standard‑kompatibel Excel‑fil.

### Nästa steg

- Utforska **Smart Marker‑loopar** (`&=OrdersJson.Orders`) för att generera en rad för varje beställning istället för en enda JSON‑sträng.  
- Kombinera denna teknik med **Excel‑formler** för att beräkna totalsummor från den inbäddade datan.  
- Titta på **att läsa JSON tillbaka från Excel** med `Workbook.Load` och `SmartMarkerProcessor` i omvänd riktning.

Känn dig fri att experimentera med olika JSON‑strukturer, flera kalkylblad eller export till andra format som CSV eller PDF. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Create Excel from JSON with Aspose.Cells Smart Marker](/cells/english/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)
- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}