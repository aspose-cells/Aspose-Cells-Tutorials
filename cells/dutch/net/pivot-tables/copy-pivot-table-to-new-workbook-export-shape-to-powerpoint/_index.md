---
category: general
date: 2026-10-20
description: Kopieer draaitabel naar nieuw werkboek met Aspose.Cells en leer hoe je
  een bewerkbare vorm naar PowerPoint kunt exporteren in één gids.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: nl
lastmod: 2026-10-20
og_description: Kopieer draaitabel naar nieuw werkboek met Aspose.Cells en exporteer
  een bewerkbare vorm naar PowerPoint—stap‑voor‑stap code die je vandaag kunt uitvoeren.
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: Kopieer draaitabel naar een nieuwe werkmap, exporteer vorm naar PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: Kopieer draaitabel naar nieuw werkboek, exporteer vorm naar PowerPoint
url: /nl/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel naar nieuw werkboek, exporteer vorm naar PowerPoint

Als je een **draaitabel kunt kopiëren naar nieuw werkboek** moet uitvoeren terwijl je de functionaliteit behoudt, laat deze gids je precies zien hoe je dit doet met Aspose.Cells. Je ziet ook de snelste manier om een **bewerkbare vorm te exporteren naar PowerPoint**, zodat het tekstvak bewerkbaar blijft na de conversie.

Veel ontwikkelaars gaan ervan uit dat het kopiëren van een bereik dat een draaitabel bevat, de draaitabel‑logica verliest, of dat vormen statische afbeeldingen worden wanneer ze als PPTX worden opgeslagen. Deze tutorial weerlegt die mythes en biedt een betrouwbare, productie‑klare oplossing.

In de volgende secties zul je:

* Een bronwerkboek laden en een bereik kopiëren dat een draaitabel bevat.
* Een doelwerkboek maken dat dezelfde draaitabel bevat.
* Een tekstvakvorm toevoegen, de tekst wijzigen, en het werkboek opslaan als een PowerPoint‑presentatie waarbij het tekstvak bewerkbaar blijft.
* Begrijpen waarom elke API‑aanroep nodig is en hoe je veelvoorkomende valkuilen kunt vermijden.

**Voorvereisten**

* .NET 6.0 of later (de code werkt ook met .NET Framework 4.7+).
* Aspose.Cells voor .NET geïnstalleerd (`Install-Package Aspose.Cells`).
* Basiskennis van C# en Visual Studio (of een IDE naar keuze).

---

## Draaitabel kopiëren naar nieuw werkboek

Deze stap‑voor‑stap sectie laat zien hoe je een bereik dat een draaitabel bevat kopieert en de draaitabeldefinitie behoudt in het nieuwe bestand.

### Stap 1 – Laad het bronwerkboek en selecteer het eerste werkblad

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*Waarom?*  
`Workbook` is het toegangspunt voor elke Excel‑manipulatie in Aspose.Cells. Het selecteren van het juiste werkblad zorgt ervoor dat we met de exacte locatie van de draaitabel werken.

### Stap 2 – Definieer het celgebied dat de draaitabel omvat

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*Waarom?*  
De draaitabel bevindt zich binnen een specifiek blok cellen. Door een `CellArea` op te geven die de draaitabel volledig omsluit, weet Aspose.Cells dat het ook de onderliggende pivot‑cache moet kopiëren.

### Stap 3 – Maak het doelwerkboek aan en haal het eerste werkblad op

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*Waarom?*  
Een nieuw werkboek garandeert dat er geen conflicterende benoemde bereiken of bestaande draaitabellen zijn, waardoor de kopieerbewerking schoon is.

### Stap 4 – Kopieer de rijen van het brongebied naar het doelblad

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*Waarom?*  
`CopyRows` maakt deel uit van de **Aspose.Cells copy rows** API. Het kopieert zowel celwaarden als de verborgen pivot‑cache, zodat de draaitabel functioneel blijft na de verplaatsing.

### Stap 5 – Sla het nieuwe werkboek op

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Resultaat*  
Open `CopyWithPivot.xlsx` in Excel. De draaitabel verschijnt precies zoals in het bronbestand, en je kunt deze normaal vernieuwen of aanpassen.

---

## Bewerkbare vorm exporteren naar PowerPoint

Nu voegen we een tekstvakvorm toe, wijzigen we de inhoud, en slaan we het werkboek op als een PPTX‑bestand. De vorm blijft volledig bewerkbaar wanneer deze in PowerPoint wordt geopend.

### Stap 1 – Maak een nieuw werkboek aan en krijg toegang tot het eerste werkblad

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Stap 2 – Voeg een tekstvakvorm toe aan het werkblad

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*Waarom?*  
`AddTextBox` maakt een **bewerkbare tekstvak in PowerPoint**‑compatibele vorm. De coördinaten zijn in punten; pas ze aan om bij je lay‑out te passen.

### Stap 3 – Haal de vorm op en wijzig de tekst

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*Waarom?*  
Direct toegang tot het `Shape`‑object stelt je in staat eigenschappen zoals `Text`, `Font` of `Fill` te wijzigen. Deze stap toont hoe je programmatically de initiële inhoud kunt instellen.

### Stap 4 – Sla het werkboek op als een PowerPoint‑presentatie

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Resultaat*  
Open `Presentation.pptx` in Microsoft PowerPoint. Het tekstvak verschijnt op de eerste dia, en je kunt er dubbel‑klikken om de tekst te bewerken, net als elke native PowerPoint‑vorm.

## Verwachte output

| File | Wat je zult zien |
|------|-----------------|
| `CopyWithPivot.xlsx` | Een werkblad met de originele draaitabel, volledig functioneel (verversen werkt). |
| `Presentation.pptx` | Een enkele dia met een bewerkbaar tekstvak met de tekst “Change me in PowerPoint”. |

---

## Veelvoorkomende valkuilen en best‑practice tips

* **Pivot cache loss** – Als je alleen celwaarden kopieert (bijv. met `CopyRows` en de `PasteOptions`‑vlag ingesteld op `PasteValues`), wordt de pivot‑cache weggelaten en wordt de tabel statisch. Gebruik altijd de standaard `CopyRows`‑overload zoals getoond.
* **Shape positioning** – `AddTextBox` gebruikt punt‑eenheden, niet Excel‑celindices. Test de coördinaten op een voorbeeldbestand om plaatsing buiten de dia te voorkomen.
* **File format mismatch** – Een werkboek opslaan als PPTX met `SaveFormat.Pptx` converteert automatisch alle ondersteunde vormen. Proberen op te slaan als `Pdf` rastert de vorm, waardoor deze niet bewerkbaar is.

---

## Conclusie

Je weet nu hoe je een **draaitabel kunt kopiëren naar een nieuw werkboek** en hoe je een **bewerkbare vorm kunt exporteren naar PowerPoint** met Aspose.Cells voor .NET. De volledige, uitvoerbare code‑voorbeelden behandelen elke benodigde API‑aanroep, leggen uit waarom elke stap belangrijk is, en tonen de verwachte resultaten.

Vervolgens kun je verkennen:

* **Working with charts** – grafieken kopiëren samen met draaitabellen (`Aspose.Cells copy rows between worksheets`).
* **

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Nieuw Werkboek maken – Hoe een werkblad met een draaitabel kopiëren](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Draaitabel kopiëren en Excel exporteren naar PPTX met Aspose.Cells](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [Nieuw Werkboek maken in C# – Draaitabel kopiëren](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}