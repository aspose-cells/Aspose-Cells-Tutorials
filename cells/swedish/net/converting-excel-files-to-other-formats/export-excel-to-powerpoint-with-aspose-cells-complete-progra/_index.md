---
category: general
date: 2026-08-14
description: Exportera Excel till PowerPoint med Aspose.Cells och lär dig hur du beräknar
  Excel‑formler i kod. Steg‑för‑steg C#‑exempel med fullständig källa.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: sv
lastmod: 2026-08-14
og_description: Exportera Excel till PowerPoint med Aspose.Cells och beräkna Excel‑formler
  i kod. Följ den här kompletta guiden för att skapa redigerbara PPTX‑filer från arbetsböcker.
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Exportera Excel till PowerPoint med Aspose.Cells – fullständig C#‑handledning
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Exportera Excel till PowerPoint med Aspose.Cells – komplett programmeringsguide
url: /sv/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera Excel till PowerPoint med Aspose.Cells – komplett programmeringsguide

Om du behöver **exportera Excel till PowerPoint** programatiskt visar den här guiden exakt hur du gör det med Aspose.Cells för .NET. Du kommer också att lära dig hur du **beräknar Excel-formler i kod**, kopierar pivottabeller utan att förlora definitioner och använder den nya Office‑365 EXPAND‑funktionen för dynamiska matriser.

I de följande avsnitten går vi igenom ett verkligt C#‑exempel, förklarar varför varje rad är viktig och tar upp vanliga fallgropar så att du kan anpassa lösningen till dina egna projekt.

## Vad den här handledningen täcker

* Laddar en befintlig arbetsbok (`input.xlsx`)  
* Kopierar ett område som innehåller en pivottabell samtidigt som definitionen bevaras  
* Exporterar arbetsboken till en PowerPoint (`.pptx`)-fil med redigerbara textrutor och former  
* Exporterar ett cellområde som strängar med anpassad logik  
* Beräknar Excel-formler i kod, inklusive Office‑365 EXPAND‑funktionen  
* Sparar den slutgiltiga arbetsboken med alla ändringar tillämpade  

**Förutsättningar**  
* .NET 6.0 eller senare (koden fungerar också med .NET Framework 4.7.2+)  
* Aspose.Cells för .NET v25.11 eller nyare (alternativet `CopyPivotTable` introducerades i v25.11)  
* Grundläggande förståelse för C# och Excel-koncept som områden, pivottabeller och formler  

> **Proffstips:** Installera Aspose.Cells via NuGet (`Install-Package Aspose.Cells`) för att hålla ditt projekt uppdaterat med de senaste funktionerna.

## Exportera Excel till PowerPoint med Aspose.Cells

Den första stora uppgiften är att konvertera arbetsboken till en PowerPoint‑presentation samtidigt som alla visuella element förblir redigerbara. Detta är avgörande när du vill generera bildspel automatiskt från finansiella rapporter eller instrumentpaneler.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### Varför detta fungerar

* **`Workbook`** laddar hela Excel‑filen i minnet och ger dig full API‑åtkomst.  
* **`CopyRange`** med `CopyPivotTable = true` säkerställer att pivottabellens datakälla, cache och layout dupliceras exakt—något äldre versioner av Aspose.Cells inte kunde göra.  
* Att lägga till ett nytt kalkylblad (`Copy`) låter dig behålla det ursprungliga bladet orört, vilket är användbart för revisionsspår.

## Exportera arbetsboken till PowerPoint med redigerbara objekt

Nu omvandlar vi arbetsboken till en PowerPoint‑fil. Genom att aktivera `ExportEditableObjects` blir varje diagram, form eller textruta ett inbyggt PowerPoint‑objekt som användare kan redigera direkt efter exporten.

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### Förklaring

* **`WorkbookDesigner`** är en hög‑nivå‑hjälpare som förbereder arbetsboken för export, hanterar Smart Markers, namngivna områden och layoutjusteringar.  
* Genom att sätta `ExportEditableObjects = true` instruerar du Aspose.Cells att översätta Excel‑ritningar till PowerPoint‑former snarare än att platta till dem till bilder. Detta ger en **fullt redigerbar** bildspelsuppsättning.

> **Särskilt fall:** Om din arbetsbok innehåller komplexa diagram som bygger på externa datakopplingar, se till att dessa kopplingar är lösta innan du anropar `ExportToPptx`, annars kan diagrammet visas tomt.

## Exportera ett område som strängar med anpassad logik

Ibland behöver du råa strängvärden för efterföljande bearbetning (t.ex. för att mata en CSV‑parser). Klassen `ExportTableOptions` låter dig styra hur varje cell konverteras.

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### Varför du kan vilja använda detta

* **Enhetlig datatyp:** Att exportera som strängar undviker typ‑mismatch‑fel när mottagaren förväntar sig text.  
* **Anpassad formatering:** Ersätt `value.ToString()` med någon anpassad formatterare (t.ex. `value.ToString("yyyy-MM-dd")` för datum).  

## Beräkna Excel-formler i kod

Ett vanligt krav är att **beräkna Excel-formler i kod** utan att öppna Excel. Aspose.Cells tillhandahåller en inbyggd beräkningsmotor som fungerar offline och stödjer de senaste Office‑365‑funktionerna, inklusive `EXPAND`.

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### Så fungerar beräkningsmotorn

* `Formula`‑egenskapen lagrar uttrycket exakt som du skulle skriva det i Excel.  
* `CalculateFormula()` utlöser en fullständig omberäkning av arbetsboken och respekterar beroenden mellan celler.  
* `EXPAND`‑funktionen (tillgänglig i Excel 365) returnerar ett spill‑område baserat på källcellen (`B1`) och de angivna raderna (`5`) och kolumnerna (`3`).  

> **Tip:** Om du bara behöver beräkna en delmängd av arbetsboken, använd `Worksheet.CalculateFormula()` för att begränsa omfattningen och förbättra prestandan.

## Spara arbetsboken med alla ändringar tillämpade

Slutligen skriver du den modifierade arbetsboken tillbaka till disk. Du kan spara i något av de stödda formaten (`.xlsx`, `.xls`, `.csv`, etc.) genom att ändra filändelsen.

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### Vad du ska verifiera

* Öppna `result.xlsx` i Excel för att bekräfta kopian av pivottabellen, `EXPAND`‑formelns resultat och eventuella anpassade exporterade strängar.  
* Öppna `output.pptx` i PowerPoint; du bör se en bild som speglar Excel‑layouten, och alla diagram/textrutor ska vara redigerbara.

## Vanliga frågor och felsökning

| Question | Answer |
|----------|--------|
| **Behöver jag en licens för att använda Aspose.Cells?** | Ja. En provversion fungerar för utvärdering, men en full licens tar bort vattenstämplar för utvärdering och låser upp `CopyPivotTable`‑funktionen. |
| **Vad händer om den exporterade PPTX-filen visar tomma former?** | Verifiera att arbetsbokens ritobjekt inte är dolda (`Visible = true`) och att eventuella externa bildlänkar är inbäddade innan export. |
| **Kan jag exportera flera kalkylblad till separata PPTX‑bilder?** | Använd `WorkbookDesigner.ExportToPptx` i en loop, ange olika `ExportOptions` för varje kalkylblad, eller kombinera dem till en enda presentation genom att manuellt lägga till bilder via Aspose.Slides. |
| **Är `CalculateFormula` trådsäker?** | Nej. Utför beräkningar på en enda tråd eller klona arbetsboken per tråd för att undvika race‑conditions. |

## Slutsats

Du har nu en **komplett, end‑to‑end‑lösning för att exportera Excel till PowerPoint** med Aspose.Cells, och du förstår hur du **beräknar Excel-formler i kod**—inklusive den moderna `EXPAND`‑funktionen. Handledningen täckte inläsning av en arbetsbok, kopiering av pivottabeller, export till redigerbar PowerPoint, anpassad strängexport, formelberäkning och slutlig sparning.

Från och med nu kan du:

* Utöka exporten för att inkludera flera bilder per kalkylblad (sekundärt nyckelord: *calculate Excel formulas in code* kan återanvändas vid generering av diagramdata).  
* Integrera Aspose.Slides för att lägga till animationer eller master‑bildlayouter.  
* Byt ut den enkla `CustomExport`‑delegaten mot lokalanpassad formatering för internationella projekt.  

Känn dig fri att experimentera med olika områden, utforska andra Office‑365‑funktioner (t.ex. `FILTER`, `SORT`), och kombinera detta arbetsflöde med automatiserad e‑postleverans för helt automatiserade rapporteringspipelines.

---


## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstrerats i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Automatisera export av Excel-data med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [Hur du exporterar Excel-diagram till PDF med Aspose.Cells för .NET: En steg‑för‑steg‑guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Exportera Excel-celler till bild med Aspose.Cells .NET: En steg‑för‑steg‑guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}