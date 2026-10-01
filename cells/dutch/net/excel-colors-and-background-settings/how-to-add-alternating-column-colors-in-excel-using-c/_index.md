---
category: general
date: 2026-10-01
description: afwisselende kolomkleuren Excel met C# – leer een Excel‑bestand te maken
  vanuit een DataTable, celachtergrondkleur instellen in C#, en een DataTable importeren
  naar Excel met gestylede kolommen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: nl
lastmod: 2026-10-01
og_description: Afwisselende kolomkleuren Excel eenvoudig gemaakt. Volg deze gids
  om een Excel‑bestand te maken vanuit een DataTable, de celachtergrondkleur in C#
  in te stellen en een DataTable naar Excel te importeren met gestylede kolommen.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: Voeg afwisselende kolomkleuren toe in Excel met C# – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: Hoe afwisselende kolomkleuren in Excel toe te voegen met C#
url: /nl/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe wisselende kolomkleuren toe te voegen in Excel met C#

Als je **alternating column colors excel** nodig hebt in een rapport dat door je applicatie wordt gegenereerd, laat deze gids je een volledige oplossing zien. Je ziet hoe je een Excel‑bestand maakt vanuit een `DataTable`, celachtergrondkleur instelt in C#‑stijl, en een datatable naar Excel importeert terwijl je een onderscheidende stijl op elke kolom toepast.

De tutorial behandelt alles wat je nodig hebt: vereiste NuGet‑pakketten, een volledige, uitvoerbare code‑voorbeeld, en uitleg waarom elke stap belangrijk is. Aan het einde heb je een gestylede werkmap die direct in Microsoft Excel kan worden geopend.

## Vereisten

* .NET 6.0 (of later) SDK geïnstalleerd  
* Visual Studio 2022 (of een C#‑compatibele IDE)  
* De **Aspose.Cells for .NET** bibliotheek – installeer deze met  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells levert de `Workbook`, `Worksheet`, `Style` en `BackgroundType` klassen die in het voorbeeld worden gebruikt.

## Stap 1: Haal de brongegevens op als een `DataTable`

De eerste taak is de gegevens die je wilt exporteren te verkrijgen. In echte projecten kun je de `DataTable` vullen vanuit een database‑query, een API‑aanroep, of een willekeurige in‑memory collectie.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Waarom dit belangrijk is:**  
Een `DataTable` is een universele container die netjes naar een Excel‑werkblad kan worden gemapt. Het gebruik van een `DataTable` stelt je in staat om **create excel file from datatable c#** te maken zonder aangepaste loops voor elke kolom te schrijven.

## Stap 2: Maak een nieuwe werkmap en haal het eerste werkblad op

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Uitleg:**  
`Workbook` is het hoofdobject; `Worksheets[0]` geeft je het standaardblad waarop de gegevens worden geplaatst.

## Stap 3: Bereid een onderscheidende stijl voor elke kolom voor (wisselende achtergrondkleuren)

Om **alternating column colors excel** te bereiken, genereren we een `Style` voor elke kolom en wijzen we een lichte achtergrondkleur toe die tussen twee tinten wisselt.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Waarom we een lus gebruiken:**  
De lus garandeert dat **set cell background color c#** consistent wordt toegepast, zelfs als het aantal kolommen tijdens runtime verandert. Dit maakt de oplossing robuust voor dynamische rapporten.

## Stap 4: Importeer de `DataTable` in het werkblad, waarbij je de kolomstijlen toepast

Aspose.Cells kan een `DataTable` direct importeren, en we kunnen de array met stijlen doorgeven om elke kolom te kleuren.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Wat er onder de motorkap gebeurt:**  
`ImportDataTable` schrijft de koprij, daarna elke gegevensrij. Omdat we `columnStyles` hebben opgegeven, krijgt elke cel in een bepaalde kolom de overeenkomstige stijl, waardoor we de gewenste wisselende kleuren krijgen.

## Stap 5: Sla de gestylede werkmap op naar een bestand

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

Wanneer je *StyledTable.xlsx* in Excel opent, zie je elke kolom afwisselend gekleurd, waardoor de tabel makkelijker leesbaar is.

## Volledig, uitvoerbaar voorbeeld

Alle onderdelen bij elkaar gezet, hier is een zelfstandige programma dat je kunt kopiëren, plakken en uitvoeren.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Verwachte output

* Een bestand genaamd **StyledTable.xlsx** geplaatst in `C:\Temp\`.
* Het werkblad toont drie kolommen (`Id`, `Name`, `Score`) met afwisselende achtergrondkleuren: kolommen 1 en 3 in *LightYellow*, kolom 2 in *LightCyan*.
* Alle rijen uit de `DataTable` verschijnen onder de koprij.

## Veelgestelde vragen en randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Kan ik andere kleuren gebruiken?* | Ja. Vervang `System.Drawing.Color.LightYellow` en `LightCyan` door elke `System.Drawing.Color` waarde. |
| *Wat als de DataTable veel kolommen heeft?* | De lus maakt automatisch een stijl voor elke kolom, zodat het patroon schaalt zonder code‑wijzigingen. |
| *Moet ik de werkmap vrijgeven?* | Aspose.Cells implementeert `IDisposable`. Als je de `Workbook` in een `using`‑blok plaatst, worden de bronnen direct vrijgegeven. |
| *Hoe pas ik dezelfde afwisselende kleuren toe op rijen in plaats van kolommen?* | Maak een `Style[]` voor rijen en roep `worksheet.Cells.ImportDataTable(..., rowStyles)` aan – Aspose.Cells‑overloads ondersteunen beide. |
| *Kan ik het bestand direct naar een stream schrijven (bijv. voor een web‑API)?* | Ja. Gebruik `workbook.Save(stream, SaveFormat.Xlsx);` in plaats van een bestandspad. |

## Tips uit de praktijk

* **Pro tip:** Cache de stijlobjecten als je veel werkbladen in één run genereert – een stijl aanmaken is relatief goedkoop, maar hergebruik vermindert geheugen‑churn.  
* **Let op:** Bij gebruik van `System.Drawing.Color` op niet‑Windows platformen, voeg het `System.Drawing.Common` NuGet‑pakket toe en zorg dat de runtime GDI+ ondersteunt.

## Conclusie

Je weet nu hoe je **alternating column colors excel** kunt realiseren door een Excel‑bestand te maken vanuit een `DataTable` in C#, celachtergrondkleuren in te stellen met Aspose.Cells, en **import datatable to excel** met een gestylede kolomarray. Deze aanpak is snel, onderhoudbaar, en werkt met elke omvang van dataset.

### Volgende stappen

* Verken **set cell background color c#** voor voorwaardelijke opmaak (bijv. lage scores markeren).  
* Combineer deze techniek met **create excel file from datatable c#** om multi‑sheet rapporten te genereren.  
* Bekijk de chart‑API van Aspose.Cells om visuele samenvattingen toe te voegen aan dezelfde werkmap.

Voel je vrij om de kleuren, bestandsformaat of gegevensbron aan te passen aan de behoeften van je project. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Kolomachtergrond instellen in Excel met C# – Complete gids](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Achtergrondkleur toevoegen in Excel – Wisselende rijstijlen in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Werkmap maken C# – DataTable importeren naar Excel met stijlen](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}