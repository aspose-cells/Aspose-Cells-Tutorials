---
category: general
date: 2026-09-15
description: Lär dig hur du kopierar pivottabell, kopierar kalkylblad med pivottabell
  och sparar arbetsboken som pptx med Aspose.Cells i C#. Komplett steg‑för‑steg‑guide.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: sv
lastmod: 2026-09-15
og_description: Hur man kopierar pivottabell, kopierar kalkylblad med pivot och sparar
  arbetsbok som pptx med Aspose.Cells. Följ de kompletta, körbara C#‑exemplen.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Hur man kopierar pivottabell och exporterar kalkylblad – fullständig C#‑guide
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  headline: How to copy pivot table while preserving worksheets
  type: TechArticle
- description: Learn how to copy pivot table, copy worksheet with pivot, and save
    workbook as pptx using Aspose.Cells in C#. Complete step‑by‑step guide.
  name: How to copy pivot table while preserving worksheets
  steps:
  - name: – Load the source workbook that holds the pivot table
    text: '```csharp // Load the workbook that contains the pivot table you want to
      copy Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx"); ```'
  - name: – Create an empty destination workbook
    text: '```csharp // Create a new, empty workbook that will receive the copied
      data Workbook destinationWorkbook = new Workbook(); ```'
  - name: – Copy the rows that include the pivot table
    text: '```csharp // Copy rows 0‑19 (A1:G20) from the first worksheet of the source
      sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20); ```'
  - name: – Copy the columns that contain the pivot table
    text: '```csharp // Copy columns 0‑6 (A‑G) from the same worksheet sourceWorkbook.Worksheets[0].Cells.CopyColumns(0,
      0, 7); ```'
  - name: – Transfer the prepared sheet into the destination workbook
    text: '```csharp // Move the fully prepared worksheet into the destination workbook
      sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]); ```'
  - name: – Save the result – the pivot table remains intact
    text: '```csharp // Save the destination workbook; the pivot table works exactly
      like the original destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
      ```'
  - name: – Load the workbook that includes the textbox
    text: '```csharp // Load the Excel file that contains an editable textbox shape
      Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
      ```'
  - name: – Configure PPTX save options
    text: '```csharp // Create PPTX save options and enable the editable textbox feature
      (available from v25.11) PptxSaveOptions pptxOptions = new PptxSaveOptions {
      ExportEditableTextBox = true }; ```'
  - name: – Save the workbook as PPTX
    text: '```csharp // Export the workbook to a PPTX file; the textbox stays editable
      in PowerPoint workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
      ```'
  - name: – Prepare the SmartMarkerProcessor
    text: '```csharp // Initialise the processor that will fill Smart Markers SmartMarkerProcessor
      smartMarkerProcessor = new SmartMarkerProcessor(); ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hur man kopierar pivottabell samtidigt som man bevarar kalkylblad
url: /sv/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så kopierar du pivottabell samtidigt som du bevarar kalkylblad

Om du behöver **how to copy pivot table** från en arbetsbok till en annan utan att förlora den underliggande pivotcachen, ger den här guiden en färdig‑att‑köra‑lösning. Du kommer också att se hur du **copy worksheet with pivot** och hur du **save workbook as pptx** samtidigt som redigerbara textrutor förblir intakta. Alla exempel använder den senaste Aspose.Cells för .NET, så du kan klistra in koden i vilket C#‑projekt som helst och se omedelbara resultat.

Att arbeta med Excel‑filer programatiskt innebär ofta att flytta data mellan arbetsböcker, exportera till presentationer eller infoga komplexa Smart Markers. De tre kodsnuttarna nedan täcker dessa vanliga scenarier och förklarar varför varje steg är viktigt.

## Förutsättningar

Innan du börjar, se till att du har:

* .NET 6.0 eller senare installerat  
* Aspose.Cells for .NET (version 25.11 eller nyare) refererad i ditt projekt  
* En mapp med namnet `YOUR_DIRECTORY` där exempel‑filerna kommer att läsas från och skrivas till  

Inga ytterligare NuGet‑paket krävs.

---

## Så kopierar du pivottabell med Aspose.Cells

Att kopiera ett område som innehåller en pivottabell samtidigt som pivotcachen bevaras är ett vanligt krav. Följande steg visar den exakta sekvensen du behöver.

### Steg 1 – Läs in källarboken som innehåller pivottabellen

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Varför*: Aspose.Cells läser in arbetsboken i minnet, vilket ger dig åtkomst till kalkylblad, celler och pivottabeller.

### Steg 2 – Skapa en tom destinationsarbok

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Varför*: Att börja med en tom arbetsbok garanterar att inga dolda format eller namngivna områden stör kopieringsoperationen.

### Steg 3 – Kopiera raderna som inkluderar pivottabellen

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Varför*: `CopyRows` kopierar de råa cellvärdena, formaten och underliggande pivotcache‑referenser. Området måste inkludera hela pivottabellens område.

### Steg 4 – Kopiera kolumnerna som innehåller pivottabellen

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Varför*: Pivottabeller sträcker sig över både rader och kolumner; att kopiera kolumner säkerställer att hela tabellens layout behålls.

### Steg 5 – Överför det förberedda bladet till destinationsarboken

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Varför*: Metoden `Copy` klonar kalkylbladet, inklusive pivotcachen, så att destinationsarboken visar en identisk pivottabell.

### Steg 6 – Spara resultatet – pivottabellen förblir intakt

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Varför*: Att spara arbetsboken skriver alla interna strukturer, vilket garanterar att pivottabellen kan uppdateras senare.

**Pro tip**: Efter kopiering kan du anropa `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` för att uppdatera data om källdata har förändrats.

---

## Kopiera kalkylblad med pivottabell – ett kortfattat alternativ

Om du bara behöver duplicera ett helt kalkylblad som redan innehåller en pivottabell kan du hoppa över rad‑/kolumnkopieringsstegen och använda kalkylblads‑nivåns `Copy`‑metod direkt.

```csharp
// Load source workbook
Workbook src = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

// Create destination workbook
Workbook dst = new Workbook();

// Copy the first worksheet (including its pivot table) to the destination
src.Worksheets[0].Copy(dst.Worksheets[0]);

// Save the new file
dst.Save("YOUR_DIRECTORY/WorksheetCopy.xlsx");
```

Denna metod är användbar när kalkylbladet inte innehåller extra data utanför pivotområdet. **copy worksheet with pivot**‑operationen bevarar automatiskt all formatering, namngivna områden och pivotcacher.

---

## Spara arbetsbok som PPTX med redigerbara textrutor

Att exportera ett Excel‑blad som innehåller en redigerbar textruta till PowerPoint kan krävas för rapporterings‑dashboards. Koden nedan visar **save workbook as pptx** samtidigt som textrutan förblir redigerbar.

### Steg 1 – Läs in arbetsboken som innehåller textrutan

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Steg 2 – Konfigurera PPTX‑spara‑alternativ

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Varför*: Genom att sätta `ExportEditableTextBox` instrueras Aspose.Cells att översätta Excel‑textrutan till en PowerPoint‑form som förblir redigerbar efter export.

### Steg 3 – Spara arbetsboken som PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Förväntat resultat**: Öppna `Result.pptx` i PowerPoint, markera textrutan och redigera dess innehåll precis som någon inbyggd form.

**Vanlig fråga**: *Vad händer om jag behöver låsa textrutan?*  
Sätt `pptxOptions.ExportEditableTextBox = false`; formen kommer då att konverteras till en statisk bild istället.

---

## Exportera en Smart Marker som innehåller en JSON‑array som ett enda cellvärde

Smart Markers låter dig fylla Excel‑mallar med komplexa datastrukturer. Nedan är ett komplett exempel som demonstrerar **how to copy pivot table**‑liknande databehandling samtidigt som en JSON‑array infogas i en enda cell.

### Steg 1 – Förbered SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Steg 2 – Infoga en Smart Marker i cell A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Steg 3 – Definiera datakällan med en JSON‑liknande array

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Steg 4 – Bearbeta arbetsboken

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Steg 5 – Spara den resulterande arbetsboken

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Resultatverifiering**: Öppna `JsonSingleCell.xlsx` och bekräfta att cell A1 visar `A,B,C`. Detta visar hur man behandlar en samling som ett enda cellvärde, ett mönster som ofta behövs vid export av data till efterföljande system.

---

## Fullt fungerande exempel

Nedan är ett enda program som kombinerar de tre scenarierna. Du kan kopiera koden till en konsolapp, justera filsökvägarna och köra den för att se alla tre resultat.

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1. How to copy pivot table (preserve pivot cache)
        // -------------------------------------------------
        Workbook srcPivot = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Workbook dstPivot = new Workbook();
        srcPivot.Worksheets[0].Cells.CopyRows(0, 0, 20);
        srcPivot.Worksheets[0].Cells.CopyColumns(0, 0, 7);
        srcPivot.Worksheets[0].Copy(dstPivot.Worksheets[0]);
        dstPivot.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");

        // -------------------------------------------------
        // 2. Save workbook as PPTX with editable textbox
        // -------------------------------------------------
        Workbook txtWorkbook = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
        PptxSaveOptions pptxOpts = new PptxSaveOptions { ExportEditableTextBox = true };
        txtWorkbook.Save("YOUR_DIRECTORY/Result.pptx", pptxOpts);

        // -------------------------------------------------
        // 3. Export Smart Marker containing a JSON array
        // -------------------------------------------------
        SmartMarkerProcessor smProcessor = new SmartMarkerProcessor();
        Workbook smWorkbook = new Workbook();
        smWorkbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
        var model = new { Orders = new[] { "A", "B", "C" } };
        smProcessor.Process(smWorkbook, model);
        smWorkbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
    }
}
```

När du kör detta program får du:

* `CopyWithPivot.xlsx` – en perfekt kopia av den ursprungliga pivottabellen.  
* `Result.pptx` – ett PowerPoint‑bildspel med en redigerbar textruta.  
* `JsonSingleCell.xlsx` – ett blad där JSON‑arrayen visas i en enda cell.

---

## Slutsats

Du vet nu hur du **how to copy pivot table** på ett säkert sätt, hur du **copy worksheet with pivot** i ett enda anrop, och hur du **save workbook as pptx** samtidigt som du bevarar redigerbara textrutor. Dessa mönster täcker de vanligaste Excel‑till‑PowerPoint‑ och Excel‑till‑JSON‑arbetsflöden du kommer att stöta på i företagsautomatiseringsprojekt.

Nästa steg, överväg att utforska:

* Uppdatera kopierade pivottabeller programatiskt (`PivotTable.Refresh()`)  
* Exportera till andra format som PDF eller HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Använda avancerade Smart Marker‑alternativ som anpassade funktioner eller villkorsstyrd formatering  

Känn dig fri att experimentera med olika områden, flera kalkylblad eller större JSON‑strukturer. Aspose.Cells‑API:et ger dig fin‑granulerad kontroll, så du kan anpassa dessa exempel till alla verkliga scenarier. Lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementeringsmetoder i dina egna projekt.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}