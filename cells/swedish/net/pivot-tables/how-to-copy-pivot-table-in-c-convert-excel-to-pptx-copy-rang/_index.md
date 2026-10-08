---
category: general
date: 2026-01-14
description: Hur man kopierar en pivottabell med Aspose.Cells och också lär sig att
  konvertera Excel till PPTX, kopiera ett område till en annan arbetsbok och göra
  en textruta redigerbar i PPTX i en enda handledning.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: sv
og_description: Hur man kopierar pivottabell och sedan konverterar Excel till PPTX,
  kopierar område till en annan arbetsbok och gör textrutan redigerbar i PPTX—allt
  med Aspose.Cells.
og_title: Hur man kopierar en pivottabell i C# – Komplett guide för Excel till PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Hur man kopierar pivottabell i C# – Konvertera Excel till PPTX, kopiera område
  och gör textrutan redigerbar
url: /sv/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man kopierar pivottabell i C# – Komplett guide för Excel till PPTX

Att kopiera en pivottabell från en arbetsbok till en annan är en vanlig fråga när du automatiserar Excel‑drivna rapporter. I den här handledningen går vi igenom tre verkliga scenarier med **Aspose.Cells for .NET**: kopiera ett pivottabell‑område, exportera ett kalkylblad till en PPTX‑fil med en redigerbar textruta och fylla i en enda cell med en JSON‑array via Smart Markers.  

Du kommer också att se hur du **konverterar Excel till PPTX**, **kopierar ett område till en annan arbetsbok** och **gör textrutan redigerbar i PPTX** utan att förstöra någon formatering. I slutet har du en färdig kodbas som du kan lägga in i vilket .NET‑projekt som helst.

> **Proffstips:** Alla exempel är riktade mot Aspose.Cells 23.12, men samma koncept gäller för tidigare versioner med mindre API‑justeringar.

![Diagram som visar hur en pivottabell kopieras, ett kalkylblad exporteras till PPTX och en JSON‑array infogas – arbetsflöde för att kopiera pivottabell](how-to-copy-pivot-table-diagram.png)

---

## Vad du behöver

- Visual Studio 2022 (eller någon C#‑IDE)
- .NET 6.0 eller senare runtime
- Aspose.Cells for .NET NuGet‑paket  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Två exempel‑Excel‑filer (`source.xlsx`, `chartWithTextbox.xlsx`) placerade i en mapp du kontrollerar (byt ut `YOUR_DIRECTORY` mot din faktiska sökväg).

Inga ytterligare bibliotek krävs; samma `Aspose.Cells`‑assembly hanterar Excel, PPTX och Smart Markers.

---

## Så kopierar du pivottabell och bevarar dess data

När du kopierar ett område som innehåller en pivottabell är standardbeteendet att bara klistra in **värdena**. För att behålla pivottabellens definition intakt måste du aktivera flaggan `CopyPivotTable`.

### Steg‑för‑steg

1. **Läs in källarboken** som innehåller pivottabellen.  
2. **Skapa en tom målarbok** – den kommer att ta emot det kopierade området.  
3. **Använd `CopyRange` med `CopyPivotTable = true`** så att pivottabellens definition följer med data.  
4. **Spara målfilen** där du behöver den.

#### Fullständigt kodexempel

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Varför detta fungerar:**  
`CopyOptions.CopyPivotTable` instruerar Aspose.Cells att klona det underliggande `PivotTable`‑objektet snarare än bara dess renderade värden. Målarboken innehåller nu en fullt funktionell pivottabell som du kan uppdatera eller ändra programmässigt.

**Edge‑case:** Om källarboken använder externa datakällor kan du behöva bädda in data eller justera anslutningssträngarna efter kopiering, annars kommer pivottabellen att visa “#REF!”.

---

## Konvertera Excel till PPTX och gör textrutan redigerbar

Att exportera ett kalkylblad till PowerPoint är praktiskt för att skapa bildspel direkt från data. Som standard blir den exporterade textrutan en statisk form, men genom att sätta `IsTextBoxEditable` ändras beteendet.

### Steg‑för‑steg

1. **Öppna arbetsboken** som innehåller diagrammet och textrutan du vill exportera.  
2. **Konfigurera `ImageOrPrintOptions`** med `SaveFormat = SaveFormat.Pptx`.  
3. **Definiera ett utskriftsområde** som inkluderar textrutan.  
4. **Aktivera `IsTextBoxEditable`** så att texten kan redigeras efter att PPTX‑filen öppnats.  
5. **Spara PPTX‑filen**.

#### Fullständigt kodexempel

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Resultat:** Öppna `result.pptx` i PowerPoint – textrutan du placerade i Excel blir nu en vanlig textruta som du kan skriva i. Ingen anledning att återskapa den manuellt.

**Vanligt fallgropp:** Om kalkylbladet innehåller sammanslagna celler som skär igenom utskriftsområdet kan den resulterande bilden flyttas. Justera utskriftsområdet eller dela upp cellerna innan export.

---

## Kopiera område till en annan arbetsbok med Smart Markers (JSON → En cell)

Ibland behöver du bädda in en JSON‑array i en enda Excel‑cell, till exempel när du skickar data till efterföljande system som förväntar sig en JSON‑sträng. Aspose.Cells Smart Markers kan serialisera en array som en enda cell när du sätter `ArrayAsSingle = true`.

### Steg‑för‑steg

1. **Läs in en mallarbok** som innehåller en Smart Marker‑platshållare (t.ex. `&=Items.Name`).  
2. **Förbered dataobjektet** – en anonym typ med en `Items`‑array.  
3. **Skapa en `SmartMarkerProcessor`** och tillämpa data med `ArrayAsSingle`.  
4. **Spara den fyllda arbetsboken**.

#### Fullständigt kodexempel

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Förklaring:**  
När `ArrayAsSingle` är true, konkatenerar Aspose.Cells varje element i `Items.Name` till en JSON‑liknande sträng (`["A","B"]`) och skriver den i cellen som innehöll smart‑markören. Detta undviker att skapa en separat rad per array‑element.

**När du bör använda den:** Perfekt för att exportera konfigurationstabeller, API‑payloads eller vilket scenario som helst där mottagaren förväntar sig en kompakt JSON‑sträng snarare än en tabelluppställning.

---

## Ytterligare tips & Edge‑Case‑hantering

| Scenario | Vad att hålla utkik efter | Föreslagen åtgärd |
|----------|---------------------------|-------------------|
| **Stora pivottabeller** | Minnesanvändning ökar kraftigt när stora pivottabellscachar kopieras. | Använd `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` innan du läser in. |
| **Export till PPTX med bilder** | Bilder kan rasteriseras med låg DPI. | Sätt `pptxOptions.ImageResolution = 300` för skarpare bilder. |
| **Smart Marker JSON‑formatering** | Specialtecken (`"` , `\`) bryter JSON. | Escape dem manuellt eller använd `JsonSerializer` för att förserialisera innan du matar in i Smart Markers. |
| **Kopiera område över olika Excel‑versioner** | Äldre `.xls`‑filer kan förlora formatering. | Spara målet som `.xlsx` för att bevara moderna funktioner. |

---

## Sammanfattning – Så kopierar du pivottabell och mycket mer

Vi började med att svara på **hur man kopierar pivottabell** samtidigt som funktionaliteten bevaras, sedan visade vi hur du **konverterar Excel till PPTX**, **gör textrutan redigerbar i PPTX**, och slutligen hur du **kopierar ett område till en annan arbetsbok** med Smart Markers för att bädda in en JSON‑array i en enda cell.

Alla tre kodsnuttar är självständiga; du kan klistra in dem i en ny konsolapp, justera filsökvägarna och köra dem idag.

---

## Vad blir nästa?

- **Utforska andra exportformat** – Aspose.Cells stödjer även PDF, XPS och HTML.  
- **Uppdatera pivottabeller programmässigt** med `PivotTable.RefreshData()` efter kopiering.  
- **Kombinera Smart Markers med diagram** för att generera dynamiska instrumentpaneler som uppdateras automatiskt.  

Om du är intresserad av att **spara arbetsbok som PPTX** med anpassade bildlayouter, kolla in Aspose.Cells‑dokumentationen om `SlideOptions`.  

Känn dig fri att experimentera—byt ut utskriftsområdet, prova olika `CopyOptions` eller mata in en mer komplex JSON‑payload. API‑et är tillräckligt flexibelt för de flesta rapporteringspipeline.

---

### Vanliga frågor

**Q: Kopierar `CopyPivotTable` också slicers?**  
A: Inte direkt. Slicers är separata objekt; efter kopiering måste du återskapa dem eller kopiera dem via samlingen `Worksheet.Shapes`.

**Q: Kan jag exportera flera kalkylblad till en enda PPTX‑presentation?**  
A: Ja. Loopa igenom varje kalkylblad, anropa `Save` med samma `ImageOrPrintOptions` och sätt `pptxOptions.StartSlideNumber` för att fortsätta numreringen.

**Q: Vad händer om min JSON‑array innehåller nästlade objekt?**  
A: Sätt `ArrayAsSingle = false` och använd en anpassad mall som itererar över

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}