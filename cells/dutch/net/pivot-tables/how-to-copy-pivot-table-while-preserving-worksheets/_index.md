---
category: general
date: 2026-09-15
description: Leer hoe je een draaitabel kopieert, een werkblad met draaitabel kopieert
  en een werkmap opslaat als pptx met Aspose.Cells in C#. Volledige stapsgewijze handleiding.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy worksheet with pivot
- save workbook as pptx
language: nl
lastmod: 2026-09-15
og_description: Hoe een draaitabel te kopiëren, een werkblad met draaitabel te kopiëren
  en een werkmap op te slaan als pptx met Aspose.Cells. Volg de volledige, uitvoerbare
  C#‑voorbeelden.
og_image_alt: Screenshot showing how to copy pivot table in a C# code editor
og_title: Hoe een draaitabel te kopiëren en werkbladen te exporteren – volledige C#‑gids
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
title: How to copy pivot table while preserving worksheets
url: /nl/net/pivot-tables/how-to-copy-pivot-table-while-preserving-worksheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren terwijl werkbladen behouden blijven

Als je **hoe je een draaitabel moet kopiëren** van het ene werkboek naar het andere zonder de onderliggende draaitabelcache te verliezen, biedt deze gids een kant‑klaar oplossing. Je ziet ook hoe je **werkblad met draaitabel kunt kopiëren** en hoe je **werkboek als pptx kunt opslaan** terwijl bewerkbare tekstvakken intact blijven. Alle voorbeelden gebruiken de nieuwste Aspose.Cells voor .NET, zodat je de code in elk C#‑project kunt plaatsen en direct resultaten ziet.

Werken met Excel‑bestanden via code houdt vaak in dat je gegevens tussen werkboeken verplaatst, exporteert naar presentaties, of complexe Smart Markers invoegt. De drie code‑fragmenten hieronder behandelen die veelvoorkomende scenario’s en leggen uit waarom elke stap belangrijk is.

## Prerequisites

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later geïnstalleerd  
* Aspose.Cells for .NET (versie 25.11 of nieuwer) toegevoegd aan je project  
* Een map genaamd `YOUR_DIRECTORY` waar de voorbeeldbestanden worden gelezen en geschreven  

Er zijn geen extra NuGet‑pakketten vereist.

---

## Hoe een draaitabel te kopiëren met Aspose.Cells

Het kopiëren van een bereik dat een draaitabel bevat terwijl de draaitabelcache behouden blijft, is een veelvoorkomende eis. De volgende stappen tonen de exacte volgorde die je nodig hebt.

### Step 1 – Load the source workbook that holds the pivot table

```csharp
// Load the workbook that contains the pivot table you want to copy
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
```

*Waarom*: Aspose.Cells leest het werkboek in het geheugen, waardoor je toegang krijgt tot werkbladen, cellen en draaitabellen.

### Step 2 – Create an empty destination workbook

```csharp
// Create a new, empty workbook that will receive the copied data
Workbook destinationWorkbook = new Workbook();
```

*Waarom*: Beginnen met een leeg werkboek garandeert dat er geen verborgen stijlen of benoemde bereiken interfereren met de kopieeractie.

### Step 3 – Copy the rows that include the pivot table

```csharp
// Copy rows 0‑19 (A1:G20) from the first worksheet of the source
sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 0, 20);
```

*Waarom*: `CopyRows` kopieert de ruwe celwaarden, opmaak en onderliggende draaitabelcache‑referenties. Het bereik moet het volledige draaitabelgebied omvatten.

### Step 4 – Copy the columns that contain the pivot table

```csharp
// Copy columns 0‑6 (A‑G) from the same worksheet
sourceWorkbook.Worksheets[0].Cells.CopyColumns(0, 0, 7);
```

*Waarom*: Draaitabellen beslaan zowel rijen als kolommen; kolommen kopiëren zorgt ervoor dat de volledige tabelindeling behouden blijft.

### Step 5 – Transfer the prepared sheet into the destination workbook

```csharp
// Move the fully prepared worksheet into the destination workbook
sourceWorkbook.Worksheets[0].Copy(destinationWorkbook.Worksheets[0]);
```

*Waarom*: De `Copy`‑methode kloont het werkblad, inclusief de draaitabelcache, zodat het doelwerkboek een identieke draaitabel toont.

### Step 6 – Save the result – the pivot table remains intact

```csharp
// Save the destination workbook; the pivot table works exactly like the original
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Waarom*: Het opslaan van het werkboek schrijft alle interne structuren weg, waardoor de draaitabel later kan worden vernieuwd.

**Pro tip**: Na het kopiëren kun je `destinationWorkbook.Worksheets[0].PivotTables[0].Refresh()` aanroepen om de gegevens bij te werken als de brondata is gewijzigd.

---

## Werkblad met draaitabel kopiëren – een beknopt alternatief

Als je simpelweg een heel werkblad dat al een draaitabel bevat wilt dupliceren, kun je de rij‑/kolom‑kopieerstappen overslaan en direct de werkblad‑niveau `Copy`‑methode gebruiken.

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

Deze aanpak is handig wanneer het werkblad geen extra gegevens buiten het draaitabelgebied bevat. De **copy worksheet with pivot**‑operatie behoudt automatisch alle opmaak, benoemde bereiken en draaitabelcaches.

---

## Werkboek opslaan als PPTX met bewerkbare tekstvakken

Het exporteren van een Excel‑blad dat een bewerkbaar tekstvak bevat naar PowerPoint kan nodig zijn voor rapportagedashboards. De code hieronder toont **save workbook as pptx** terwijl het tekstvak bewerkbaar blijft.

### Step 1 – Load the workbook that includes the textbox

```csharp
// Load the Excel file that contains an editable textbox shape
Workbook workbookWithTextbox = new Workbook("YOUR_DIRECTORY/DocWithTextbox.xlsx");
```

### Step 2 – Configure PPTX save options

```csharp
// Create PPTX save options and enable the editable textbox feature (available from v25.11)
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableTextBox = true
};
```

*Waarom*: Het instellen van `ExportEditableTextBox` vertelt Aspose.Cells om het Excel‑tekstvak te vertalen naar een PowerPoint‑vorm die na export bewerkbaar blijft.

### Step 3 – Save the workbook as PPTX

```csharp
// Export the workbook to a PPTX file; the textbox stays editable in PowerPoint
workbookWithTextbox.Save("YOUR_DIRECTORY/Result.pptx", pptxOptions);
```

**Verwacht resultaat**: Open `Result.pptx` in PowerPoint, selecteer het tekstvak en bewerk de inhoud net als elke native vorm.

**Veelgestelde vraag**: *Wat als ik het tekstvak vergrendeld wil houden?*  
Stel `pptxOptions.ExportEditableTextBox = false`; de vorm wordt dan omgezet naar een statische afbeelding.

---

## Een Smart Marker exporteren die een JSON‑array bevat als enkele celwaarde

Smart Markers laten je Excel‑templates vullen met complexe datastructuren. Hieronder staat een volledig voorbeeld dat **hoe je een draaitabel moet kopiëren**‑achtige gegevensverwerking demonstreert terwijl een JSON‑array in één cel wordt ingevoegd.

### Step 1 – Prepare the SmartMarkerProcessor

```csharp
// Initialise the processor that will fill Smart Markers
SmartMarkerProcessor smartMarkerProcessor = new SmartMarkerProcessor();
```

### Step 2 – Insert a Smart Marker into cell A1

```csharp
// The marker ${Orders:ArrayAsSingle} tells the processor to write the whole array into one cell
Workbook workbook = new Workbook();
workbook.Worksheets[0].Cells["A1"].PutValue("${Orders:ArrayAsSingle}");
```

### Step 3 – Define the data source with a JSON‑style array

```csharp
// Anonymous object that mimics a JSON array
var dataModel = new { Orders = new[] { "A", "B", "C" } };
```

### Step 4 – Process the workbook

```csharp
// Fill the Smart Marker with the array data; the array becomes a comma‑separated string
smartMarkerProcessor.Process(workbook, dataModel);
```

### Step 5 – Save the resulting workbook

```csharp
// Persist the workbook; cell A1 now contains "A,B,C"
workbook.Save("YOUR_DIRECTORY/JsonSingleCell.xlsx");
```

**Result verification**: Open `JsonSingleCell.xlsx` en controleer dat cel A1 `A,B,C` weergeeft. Dit laat zien hoe je een collectie als één celwaarde kunt behandelen, een patroon dat vaak nodig is bij het exporteren van data voor downstream‑systemen.

---

## Volledig werkend voorbeeld

Hieronder staat één programma dat de drie scenario’s combineert. Kopieer de code naar een console‑app, pas de bestandspaden aan, en voer het uit om alle drie de uitkomsten te zien.

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

Het uitvoeren van dit programma levert:

* `CopyWithPivot.xlsx` – een perfecte kopie van de originele draaitabel.  
* `Result.pptx` – een PowerPoint‑dia met een bewerkbaar tekstvak.  
* `JsonSingleCell.xlsx` – een blad waarop de JSON‑array in één cel verschijnt.

---

## Conclusie

Je weet nu **hoe je een draaitabel veilig kunt kopiëren**, hoe je **werkblad met draaitabel in één stap kunt kopiëren** en hoe je **werkboek als pptx kunt opslaan** terwijl bewerkbare tekstvakken behouden blijven. Deze patronen dekken de meest voorkomende Excel‑naar‑PowerPoint en Excel‑naar‑JSON‑workflows die je tegenkomt in enterprise‑automatiseringsprojecten.

Vervolgens kun je overwegen om te verkennen:

* Het programmatic vernieuwen van gekopieerde draaitabellen (`PivotTable.Refresh()`)  
* Exporteren naar andere formaten zoals PDF of HTML (`PdfSaveOptions`, `HtmlSaveOptions`)  
* Geavanceerde Smart Marker‑opties zoals aangepaste functies of voorwaardelijke opmaak  

Voel je vrij om te experimenteren met verschillende bereiken, meerdere werkbladen, of grotere JSON‑structuren. De Aspose.Cells‑API geeft je fijnmazige controle, zodat je deze voorbeelden kunt aanpassen aan elke real‑world‑situatie. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step‑By‑Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}