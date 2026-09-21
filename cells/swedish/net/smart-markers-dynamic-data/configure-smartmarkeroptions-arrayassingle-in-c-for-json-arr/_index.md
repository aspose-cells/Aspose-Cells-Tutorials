---
category: general
date: 2026-09-21
description: Konfigurera SmartMarkerOptions ArrayAsSingle i C# för att exportera JSON‑arrayer
  som ett enda cellvärde i en Excel‑arbetsbok.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: sv
lastmod: 2026-09-21
og_description: Konfigurera SmartMarkerOptions ArrayAsSingle i C# för att exportera
  JSON‑arrayer som ett enda cellvärde. Lär dig den kompletta steg‑för‑steg‑lösningen.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Konfigurera SmartMarkerOptions ArrayAsSingle i C# – fullständig guide
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Konfigurera SmartMarkerOptions ArrayAsSingle i C# för JSON‑arrayer
url: /sv/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konfigurera SmartMarkerOptions ArrayAsSingle i C# för JSON‑arrayer

Om du behöver **konfigurera SmartMarkerOptions ArrayAsSingle** när du genererar Excel‑filer med Aspose.Cells, visar den här guiden exakt hur du gör det. Du kommer att se hur du behåller en JSON‑array intakt i en cell istället för att sprida dess element över flera rader.

Att arbeta med JSON‑data i kalkylblad innebär ofta att välja mellan en platt vy och en kompakt representation. I många rapporteringsscenarier—som att lagra en lista med taggar eller en uppsättning identifierare—vill du att hela JSON‑strängen ska ligga i en enda cell. **ArrayAsSingle**‑flaggan i `SmartMarkerOptions` gör detta möjligt.

I den här handledningen kommer du att:

* Skapa en `DataTable` som innehåller en JSON‑array i en kolumn.
* Placera Smart Markers i ett Excel‑arbetsblad.
* **Konfigurera SmartMarkerOptions ArrayAsSingle** så att JSON‑arrayen behandlas som ett enda cellvärde.
* Bearbeta markörerna och spara arbetsboken.
* Verifiera resultatet.

> **Förutsättningar** – Du behöver Aspose.Cells för .NET‑biblioteket (v23.12 eller senare) och en .NET‑utvecklingsmiljö (Visual Studio 2022 rekommenderas). Grundläggande kunskap om C# och DataTables förutsätts.

---

## Steg 1: Förbered datakällan med en JSON‑array

Först, bygg en `DataTable` som efterliknar de data du skulle få från en tjänst eller en databas. Kolumnen **Names** innehåller en JSON‑kodad sträng som representerar en array av namn.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Varför detta steg?*  
Smart Markers läser data direkt från .NET‑objekt. Genom att placera JSON‑arrayen i en strängkolumn bevarar du den exakta JSON‑syntaksen, som senare kan skrivas till en cell oförändrad.

---

## Steg 2: Infoga Smart Markers i en ny arbetsbok

Skapa en ny arbetsbok, välj det första kalkylbladet och skriv Smart Markers som refererar till hela tabellen och den specifika **Names**‑kolumnen.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Markören `&=dataTable.Names` talar om för Aspose.Cells att ersätta cellen med värdet från **Names**‑kolumnen för varje rad i `dataTable`. Eftersom vi bara har en rad kommer markören att bearbetas en gång.

---

## Steg 3: **Konfigurera SmartMarkerOptions ArrayAsSingle**

Som standard expanderar Aspose.Cells en array‑liknande sträng till separata rader. Att sätta `ArrayAsSingle` till `true` åsidosätter detta beteende och tvingar hela JSON‑strängen att stanna i en enda cell.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Varför aktivera `ArrayAsSingle`?*  
När `ArrayAsSingle` är `false` tolkar motorn `["Alice","Bob"]` som två separata värden och skriver dem till intilliggande rader. Att sätta den till `true` behandlar strängen som ett atomärt värde, vilket är avgörande för att bevara JSON‑formatet i Excel.

---

## Steg 4: Bearbeta Smart Markers med de konfigurerade alternativen

Kör nu Smart Marker‑motorn och skicka med det alternativobjekt du just konfigurerat.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Under bearbetningen läser Aspose.Cells `dataTable`, applicerar markörerna och respekterar `ArrayAsSingle`‑flaggan, så att JSON‑arrayen förblir orörd.

---

## Steg 5: Spara arbetsboken och verifiera resultatet

Skriv slutligen arbetsboken till disk. Öppna den genererade filen i Excel eller någon annan kalkylbladsvisare för att bekräfta att cell **A2** innehåller exakt JSON‑strängen.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Förväntat resultat

| A   |
|-----|
| **["Alice","Bob"]** |

Cell **A2** visar JSON‑arrayen som ett enda textvärde, exakt som den lagras i `DataTable`. Inga extra rader skapas.

---

## Vanliga variationer och hantering av kantfall

| Situation | Hur man anpassar |
|-----------|------------------|
| **Flera rader med JSON‑arrayer** | Samma `ArrayAsSingle`‑inställning fungerar; varje rads JSON‑array stannar i sin egen cell. |
| **Olika JSON‑strukturer (objekt, nästlade arrayer)** | Så länge JSON är en sträng behåller `ArrayAsSingle` den intakt. För komplexa objekt kan du behöva escapera citattecken. |
| **Använda en annan datakälla (t.ex. List\<T\>)** | Ersätt `DataTable` med någon enumererbar samling; markörsyntaxen (`&=myList.Property`) förblir densamma. |
| **Exportera till CSV istället för XLSX** | `ArrayAsSingle` gäller fortfarande, men kom ihåg att CSV inte bevarar cellformatering; du kan behöva omge JSON med citattecken. |

**Proffstips:** Sätt alltid `ArrayAsSingle` *innan* du anropar `ProcessSmartMarkers`. Att ändra flaggan efter bearbetning har ingen effekt på redan genererade celler.

---

## Fullt, körbart exempel

Nedan är det kompletta programmet som du kan kopiera‑klistra in i en konsolapplikation. Det innehåller alla `using`‑direktiv och kommentarer för tydlighet.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Kör programmet, öppna `SmartMarkerJson.xlsx`, så ser du att JSON‑arrayen bevaras i cell **A2**.

---

## Slutsats

Du vet nu hur du **konfigurerar SmartMarkerOptions ArrayAsSingle** i C# för att hålla en JSON‑array som ett enda cellvärde när du använder Aspose.Cells smart markers. Stegen—att förbereda en `DataTable`, infoga markörer, sätta `ArrayAsSingle`‑flaggan, bearbeta och spara—utgör ett återanvändbart mönster som du kan tillämpa i alla scenarier där kompakt JSON‑representation i Excel krävs.

Nästa steg kan vara att utforska:

* **Aspose.Cells smart markers** för att loopa över samlingar.
* Export av **nästlade JSON‑objekt** genom att anpassa cellformatering.
* Kombinera **villkorlig formatering** med smart markers för rikare rapporter.

Experimentera gärna med olika datastrukturer och dela dina resultat. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

De följande handledningarna täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Create Configure Excel Workbook Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}