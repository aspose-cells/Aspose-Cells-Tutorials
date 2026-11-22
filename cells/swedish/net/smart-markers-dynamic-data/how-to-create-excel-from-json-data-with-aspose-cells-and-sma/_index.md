---
category: general
date: 2026-11-22
description: Lär dig att skapa Excel från JSON‑data i C# med Aspose.Cells Smart Marker.
  En steg‑för‑steg‑guide täcker mallutformning, JSON‑hantering och filexport.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel from json data
- Aspose.Cells
- Smart Marker
- C# Excel generation
- JSON to Excel
- Excel template
language: sv
lastmod: 2026-11-22
og_description: Skapa Excel från JSON‑data med Aspose.Cells Smart Marker. Följ den
  här kortfattade handledningen för att generera en fullt formaterad arbetsbok från
  en JSON‑array.
og_image_alt: Screenshot showing Excel workbook created from JSON data using Aspose.Cells
og_title: Skapa Excel från JSON-data i C# – komplett guide till Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn to create Excel from JSON data in C# using Aspose.Cells Smart
    Marker. Step‑by‑step guide covers template design, JSON handling, and file export.
  headline: How to create Excel from JSON data with Aspose.Cells and Smart Marker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man skapar Excel från JSON-data med Aspose.Cells och Smart Marker
url: /sv/net/smart-markers-dynamic-data/how-to-create-excel-from-json-data-with-aspose-cells-and-sma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man skapar Excel från JSON-data med Aspose.Cells och Smart Marker

Om du behöver **skapa Excel från JSON-data** i en .NET-applikation, visar den här handledningen en komplett, produktionsklar lösning. Du kommer att se hur du bäddar in en JSON-array i en enda cell, använder **Smart Marker**-funktionen i **Aspose.Cells**, och genererar en slutgiltig arbetsbok utan manuell cell‑för‑cell‑kodning.

Metoden fungerar för vilken JSON‑payload som helst—oavsett om du exporterar API‑resultat, serialiserar objekt eller bygger rapporter. I slutet av guiden har du ett färdigt C#‑projekt som läser en JSON‑sträng, applicerar den på en **Excel‑mall**, och sparar resultatet som en ny fil.

## Förutsättningar

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)
- Visual Studio 2022 (eller någon IDE som stödjer C#)
- **Aspose.Cells for .NET** NuGet‑paket (version 23.10 eller nyare)
- En enkel Excel‑mallfil som innehåller Smart Marker‑taggen `<%=Fruits:ArrayAsSingle%>` i mål‑cellen

> **Pro tip:** Håll mallen i en mapp som din applikation kan komma åt vid körning (t.ex. `Resources` eller en konfigurerbar sökväg).  

## Steg 1: Förbered JSON‑payloaden

Först definierar du JSON‑arrayen som du vill infoga i kalkylbladet. I det här exemplet använder vi en lista med fruktnamn.

```csharp
// Step 1 – JSON array that will be placed in a single cell
string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";
```

JSON‑strängen kan genereras dynamiskt (t.ex. `JsonSerializer.Serialize(myList)`) eller läsas från en extern källa såsom ett REST‑API. Det viktiga är att strängen måste vara en giltig JSON‑array eftersom **Smart Marker** förväntar sig en JSON‑representation när `ArrayAsSingle`‑alternativet används.

## Steg 2: Bygg Smart Marker‑datakällan

Aspose.Cells Smart Marker‑motor arbetar med vilket .NET‑objekt som helst. Vi skapar ett anonymt objekt som innehåller JSON‑strängen under en egenskap med namnet `Fruits`. Egendomsnamnet måste matcha marker‑namnet som används i mallen.

```csharp
// Step 2 – Anonymous object serving as the Smart Marker data source
var dataSource = new
{
    Fruits = fruitsJson   // Property name "Fruits" matches the marker <%=Fruits...%>
};
```

> **Varför ett anonymt objekt?** Det låter dig skicka en lättviktig databehållare utan att definiera en dedikerad klass, vilket snabbar upp prototypandet. För större projekt kan du ersätta det med en starkt‑typad DTO.

## Steg 3: Designa Excel‑mallen med en Smart Marker‑platshållare

Skapa en Excel‑fil (`SmartMarkerTemplate.xlsx`) som innehåller platshållaren där JSON‑värdet ska visas. Placera följande marker i önskad cell (t.ex. **A1**):

```
<%=Fruits:ArrayAsSingle%>
```

- `Fruits` – matchar egenskapsnamnet i datakällan.  
- `ArrayAsSingle` – talar om för Smart Marker att skriva hela JSON‑arrayen som en enda sträng, med hakparenteser och citattecken bevarade.

![Excel template with Smart Marker placeholder](excel-template.png){alt="Excel‑mall som innehåller <%=Fruits:ArrayAsSingle%> för att skapa Excel från JSON-data"}

## Steg 4: Läs in arbetsboken och initiera Smart Marker‑processorn

Läs nu in mallfilen i en `Aspose.Cells.Workbook`‑instans och skapa en `SmartMarkerProcessor` som hanterar ersättningen.

```csharp
// Step 4 – Load the template workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

// Initialise the Smart Marker processor with the loaded workbook
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);
```

Att läsa in arbetsboken en gång och återanvända samma `SmartMarkerProcessor`‑instans är mer effektivt än att skapa en ny processor för varje cell.

## Steg 5: Applicera datakällan för att ersätta markern

`ApplyTemplate`‑metoden skannar arbetsboken efter alla markörer och ersätter dem med värden från det angivna objektet.

```csharp
// Step 5 – Replace the Smart Marker with the JSON content
smartMarkerProcessor.ApplyTemplate(dataSource);
```

Eftersom vi använde `ArrayAsSingle` innehåller cellen nu den råa JSON‑strängen:

```
["Apple","Banana","Cherry"]
```

Om du behöver ett annat format (t.ex. en kommaseparerad lista) kan du använda `ArrayAsCommaSeparated` istället för `ArrayAsSingle`.

## Steg 6: Spara den bearbetade arbetsboken

Skriv slutligen den modifierade arbetsboken till en ny fil. Du kan välja vilket som helst av de stödjade formaten (`.xlsx`, `.xls`, `.csv`, osv.).

```csharp
// Step 6 – Save the workbook with the JSON inserted
workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
```

Den resulterande filen `JsonExported.xlsx` kan öppnas i Excel, Google Sheets eller någon kompatibel visare, och den visar JSON‑arrayen exakt som den infördes.

## Fullt fungerande exempel

Att sätta ihop alla delar ger dig ett självständigt konsolprogram:

```csharp
using Aspose.Cells;

class SmartMarkerJsonDemo
{
    static void Main()
    {
        // 1️⃣ Define the JSON array
        string fruitsJson = "[\"Apple\",\"Banana\",\"Cherry\"]";

        // 2️⃣ Create the data source object
        var dataSource = new
        {
            Fruits = fruitsJson
        };

        // 3️⃣ Load the Excel template that contains <%=Fruits:ArrayAsSingle%>
        Workbook workbook = new Workbook("YOUR_DIRECTORY/SmartMarkerTemplate.xlsx");

        // 4️⃣ Initialise the Smart Marker processor
        SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor(workbook);

        // 5️⃣ Apply the data source – the marker is replaced with the JSON string
        smartMarkerProcessor.ApplyTemplate(dataSource);

        // 6️⃣ Save the result
        workbook.Save("YOUR_DIRECTORY/JsonExported.xlsx");
    }
}
```

### Förväntad utdata

| A                                   |
|-------------------------------------|
| `["Apple","Banana","Cherry"]`       |

JSON‑strängen visas exakt som en sträng i cell **A1** i `JsonExported.xlsx`.

## Hantera vanliga variationer och kantfall

| Situation                                 | Rekommenderad justering |
|-------------------------------------------|--------------------------|
| **Stora JSON‑objekt** (nästlade ordböcker) | Använd `ArrayAsJson` för att bädda in hela objekt‑hierarkin, eller mappa JSON‑en till en starkt‑typad modell och använd nästlade markörer (`<%=Parent.Child%>`). |
| **Flera JSON‑arrayer** i olika celler      | Lägg till ytterligare egenskaper i det anonyma objektet (t.ex. `Vegetables = vegJson`) och motsvarande markörer (`<%=Vegetables:ArrayAsSingle%>`). |
| **Behov av att dela upp arrayen i rader** | Ersätt `ArrayAsSingle` med `Array` – Smart Marker skapar en ny rad för varje element. |
| **Mall lagrad som en inbäddad resurs**    | Läs in arbetsboken från en ström: `Assembly.GetExecutingAssembly().GetManifestResourceStream("Namespace.Template.xlsx")`. |
| **Kör i ASP.NET Core**                    | Använd `IWebHostEnvironment.ContentRootPath` för att bygga den fullständiga sökvägen till mallen och utdatafilerna. |

## Prestandaöverväganden

- **Återanvänd `Workbook`‑objektet** när du bearbetar många poster i ett batch‑jobb; skapa processorn en gång per arbetsbok.  
- **Inaktivera beräkning** (`workbook.CalculateFormula = false`) om mallen innehåller tunga formler som inte behövs för JSON‑infogningssteget.  
- **Strömspara** (`workbook.Save(stream, SaveFormat.Xlsx)`) minskar I/O‑belastning när filen skickas direkt som svar till en klient.

## Slutsats

Du vet nu hur du **skapar Excel från JSON-data** i C# med **Aspose.Cells** och **Smart Marker**‑funktionen. Handledningen täckte JSON‑förberedelse, skapande av datakälla, mall‑design, marker‑bearbetning och fil‑sparande—allt i ett enda körbart program.

Härifrån kan du:

- Utöka mallen med ytterligare **Smart Marker**‑taggar för rikare rapporter.  
- Byta till `Array` eller `ArrayAsJson` för att skriva ut JSON som rader eller nästlade strukturer.  
- Kombinera denna teknik med **C# Excel generation**‑bibliotek som EPPlus eller ClosedXML om du behöver ett gratis alternativ.

Lycka till med kodningen, och njut av att förvandla JSON till snygga Excel‑arbetsböcker!

## Vad bör du lära dig härnäst?

De följande handledningarna behandlar närliggande ämnen som bygger vidare på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationssätt i dina egna projekt.

- [Importera JSON‑data till Excel med Aspose.Cells Java: En omfattande guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Aspose Cells GridJs‑handledning – Exportera Excel‑data till JSON med lazy loading](/cells/english/python/import-and-export/aspose-cells-gridjs-tutorial-export-excel-data-to-json-with/)
- [Skapa Excel från JSON med Smart Marker i Aspose.Cells](/cells/spanish/net/smart-markers-dynamic-data/create-excel-from-json-with-aspose-cells-smart-marker/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}