---
category: general
date: 2026-05-30
description: Leer hoe je afwisselende rijkleuren kunt toevoegen in C#‑werkbladen,
  de celachtergrond kunt instellen met een effen vulpatroon en de stijl van werkbladcellen
  moeiteloos kunt aanpassen.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: nl
og_description: Afwisselende rijkleuren in C#‑werkbladen eenvoudig gemaakt. Leer hoe
  je de celachtergrond instelt, een effen vulpatroon gebruikt en de celstijl van het
  werkblad onder de knie krijgt.
og_title: Afwisselende rijkleuren in C#‑werkbladen – Complete gids
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Afwisselende rijkleuren in C#-werkbladen – Complete gids
url: /nl/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Afwisselende Rijkleuren in C# Werkbladen – Complete Gids

Heb je je ooit afgevraagd hoe je je Excel-export er gepolijst uit kunt laten zien door **afwisselende rijkleuren** te gebruiken? Je bent niet de enige—ontwikkelaars vragen voortdurend hoe ze *achtergrondkleur toevoegen* aan rijen kunnen *toevoegen* zonder een miljoen regels code te schrijven.  

In deze tutorial lopen we een eenvoudige manier door om **set cell background** per rij, een **solid fill pattern** toe te passen, en de **worksheet cell style** te beheersen zodat het resultaat zowel leesbaar als visueel aantrekkelijk is.

## Wat je zult leren

- Haal gegevens op in een `DataTable` (of een andere tabelbron).  
- Bouw een array van `Style`-objecten die afwisselen tussen twee kleuren.  
- Importeer de `DataTable` in een werkblad terwijl je die stijlen toepast.  
- Controleer de output en pas de kleuren of patronen aan indien nodig.  

Er zijn geen externe tools nodig buiten een .NET-omgeving en een spreadsheetbibliotheek (we gebruiken **Aspose.Cells** in de voorbeelden). Aan het einde heb je een herbruikbare methode die je in elke rapportage‑pipeline kunt plaatsen.

---

## Stap 1: Haal de brongegevens op als een `DataTable`

Allereerst—zonder gegevens is er niets om te stijlen. Hieronder staat een kleine helper die een `DataTable` met voorbeeldrijen maakt. In een echt project zou je dit vervangen door een database‑aanroep of CSV‑parser.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Waarom dit belangrijk is:** Het hebben van de gegevens in een `DataTable` laat de werkbladengine ze *importeren* in één oproep, waarbij kolomnamen en gegevenstypen automatisch behouden blijven.

## Stap 2: Maak **Alternating Row Colors**-stijlen

Nu genereren we een array van `Style`-objecten—één per rij—zodat even rijen een lichtgele tint krijgen terwijl oneven rijen een zacht cyaan ontvangen. Dit is de kern van de **alternating row colors**‑techniek.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Waarom een **Solid Fill Pattern** gebruiken?

De `Pattern`‑eigenschap vertelt de engine hoe de kleur moet worden weergegeven. Een `Solid`‑vulling garandeert dat de volledige celachtergrond wordt geschilderd, waardoor eventuele vage rasterlijnen die anders zichtbaar zouden zijn, verdwijnen. Dit is de meest voorkomende manier om **set cell background** toe te passen wanneer je een nette uitstraling wilt.

## Stap 3: Importeer de `DataTable` met de voorbereide stijlen

Met de stijl‑array klaar, wordt de importaanroep een één‑regel‑code. Aspose.Cells past automatisch de overeenkomstige stijl toe op elke rij.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Wat er onder de motorkap gebeurt?**  
> De bibliotheek doorloopt elke rij, kopieert de waarden naar cellen, en past vervolgens de overeenkomende `Style` uit `rowStyles` toe. Omdat we al een **solid fill pattern** hebben gedefinieerd, erft elke cel in een rij dezelfde achtergrondkleur, waardoor je perfecte **alternating row colors** krijgt.

## Stap 4: Sla de werkmap op en controleer het resultaat

Een snelle opslaan stelt je in staat het bestand te openen in Excel (of een andere compatibele viewer) en het effect te zien.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Wanneer je het bestand opent, zullen rijen 1, 3, 5… lichtgeel zijn, terwijl rijen 2, 4, 6… lichtcyaan zijn. De kolomkoppen blijven wit, waardoor de gegevens opvallen.

![Werkblad met afwisselende rijkleuren](/images/alternating-row-colors.png "Schermafbeelding van werkblad met afwisselende rijkleuren")

*Afbeeldings‑alt‑tekst:* **alternating row colors** schermafbeelding van een werkblad waarbij de achtergrond van elke rij afwisselt tussen lichtgeel en lichtcyaan.

## Stap 5: Verder aanpassen (optioneel)

### Verander de kleuren

Als je merk andere tinten gebruikt, vervang dan gewoon `Color.LightYellow` en `Color.LightCyan` door elke `System.Drawing.Color` die je verkiest. Bijvoorbeeld:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Gebruik een ander **Background Type**

Hoewel `BackgroundType.Solid` het meest gangbaar is, kun je experimenteren met `BackgroundType.Gray125`, `BackgroundType.Horizontal`, of elk patroon dat de bibliotheek ondersteunt. Dit verandert de visuele textuur terwijl je nog steeds **adding background color**.

### Pas een **Worksheet Cell Style** toe op specifieke kolommen

Soms wil je het afwisselende effect alleen op datakolommen toepassen, terwijl de eerste kolom (bijv. ID's) onaangeroerd blijft. Maak een aparte stijl voor die kolom en wijs deze toe na de import:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Conclusie

Je hebt nu een complete, herbruikbare oplossing voor **alternating row colors** in C#‑werkbladen. Door een array van `Style`‑objecten te bouwen, **set cell background** met een **solid fill pattern**, en een `DataTable` in één oproep te importeren, kun je professionele rapporten maken met minimale code.  

Vanuit hier kun je:

- Voeg **adding background color** toe aan header‑rijen voor extra nadruk.  
- Combineer de techniek met conditionele opmaak voor dynamische visuele aanwijzingen.  
- Ontdek andere **worksheet cell style**‑eigenschappen zoals lettertypen, randen of getalformaten.

Probeer het in je volgende export‑routine—je gebruikers zullen je dankbaar zijn voor de nettere, beter leesbare spreadsheets. Veel plezier met coderen!

## Wat moet je hierna leren?

- [Rijhoogte instellen in werkblad met Aspose.Cells voor .NET](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Excel-celnamen omzetten naar rij‑ en kolomindices met Aspose.Cells voor .NET](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Werkblad‑tabkleuren instellen in Excel met Aspose.Cells .NET – Een uitgebreide gids](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}