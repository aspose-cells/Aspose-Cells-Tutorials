---
category: general
date: 2026-07-14
description: Sla Excel snel op als HTML en leer hoe je Excel naar HTML kunt converteren
  met volledige opmaak. Exporteer Excel met opmaak met Aspose.Cells in enkele minuten.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: nl
lastmod: 2026-07-14
og_description: Sla Excel direct op als HTML. Deze gids laat zien hoe je Excel naar
  HTML converteert, terwijl je de stijlen behoudt en Grid.js-nummeropmaak inschakelt.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Excel opslaan als HTML – Stap‑voor‑stap export met volledige opmaak
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Excel opslaan als HTML – Complete gids voor het exporteren van Excel met opmaak
url: /nl/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel opslaan als HTML – Complete gids voor het exporteren van Excel met opmaak

Heb je je ooit afgevraagd hoe je **Excel als HTML kunt opslaan** zonder de kleuren, randen of getalopmaak te verliezen? Je bent niet de enige. In veel rapportagescenario's heb je een web‑klare weergave van een werkmap nodig, en de snelste manier is om het bestand direct naar HTML te exporteren.  

In deze tutorial lopen we de exacte stappen door om **Excel naar HTML te converteren** met Aspose.Cells, Grid.js getalopmaak in te schakelen, en ervoor te zorgen dat de output er precies uitziet als de oorspronkelijke spreadsheet. Aan het einde heb je een kant‑klaar HTML‑bestand dat je vanaf elke webserver kunt serveren.

## Wat je zult leren

- Voorvereisten en installatie van pakketten  
- Een bestaande werkmap laden (of er één on‑the‑fly maken)  
- `HtmlSaveOptions` configureren voor perfecte visuele getrouwheid  
- `GridJsOptions.EnableNumberFormat` inschakelen om numerieke opmaak intact te houden  
- Het bestand opslaan en het resultaat verifiëren  

Als je ooit hebt geprobeerd **Excel met opmaak te exporteren** met een generieke CSV‑dump, weet je hoe frustrerend het kan zijn wanneer getallen veranderen in platte tekst. Deze gids vermijdt die valkuil.

---

## Voorvereisten – Stel je ontwikkelomgeving in

Voordat we in de code duiken, zorg ervoor dat je het volgende hebt:

| Voorwaarde | Waarom het belangrijk is |
|-------------|--------------------------|
| .NET 6.0 of later (de tutorial gebruikt .NET 6) | Moderne API's en betere prestaties |
| Visual Studio 2022 (of VS Code met C#‑extensie) | Gemakkelijk bewerken en debuggen |
| Aspose.Cells for .NET NuGet‑pakket | De bibliotheek die `HtmlSaveOptions` en `GridJsOptions` aandrijft |
| Een voorbeeld‑Excel‑bestand (`sample.xlsx`) of een werkmap die je in code genereert | De bron die je gaat converteren |

Installeer Aspose.Cells met het volgende commando in de Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

> **Pro tip:** Als je op een CI‑pipeline werkt, voeg dan dezelfde `dotnet add package`‑regel toe aan je build‑script zodat de afhankelijkheid altijd aanwezig is.

---

## Stap 1: Een werkmap laden of maken

Je kunt een bestaand bestand laden of er één programmatisch opbouwen. Hier is een minimaal voorbeeld dat een werkmap maakt met een paar opgemaakte cellen zodat je de opmaak kunt zien overleven tijdens de export.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Waarom dit belangrijk is:** Door expliciet getalopmaak in te stellen, zul je later zien dat `GridJsOptions.EnableNumberFormat` die opmaak levend houdt in de HTML‑output.

---

## Stap 2: HTML‑opslaanopties configureren

Nu maken we een `HtmlSaveOptions`‑instantie. Dit object vertelt Aspose.Cells precies hoe je de HTML wilt laten renderen.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Grid.js getalopmaak inschakelen

Als je van plan bent de HTML in te sluiten in een pagina die **Grid.js** gebruikt voor interactieve tabellen, wil je dat de getallen opgemaakt blijven (bijv. valutasymbolen, duizendtallen). De volgende regel doet precies dat:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Wat gebeurt er onder de motorkap?** `EnableNumberFormat` injecteert een klein JavaScript‑fragment dat Grid.js vertelt het `data-format`‑attribuut van de cel te interpreteren, waardoor de Excel‑achtige opmaak in de browser behouden blijft.

---

## Stap 3: De werkmap opslaan als een HTML‑bestand

Met de werkmap klaar en de opties afgestemd, schrijft de laatste regel het HTML‑bestand naar schijf.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Het uitvoeren van het programma produceert een `gridjs.html`‑bestand dat er zo uitziet (vereenvoudigde weergave):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Open het bestand in een willekeurige browser en je ziet een mooi gestylede tabel, compleet met een lichtgrijze header‑achtergrond en valuta‑opmaak. Als je de pagina in een site plaatst die al Grid.js laadt, zullen de getallen automatisch worden weergegeven met de juiste komma's en symbolen.

---

## Veelvoorkomende valkuilen bij het **converteren van Excel naar HTML**

| Probleem | Waarom het gebeurt | Hoe te vermijden |
|----------|--------------------|------------------|
| **Formules verloren** | HTML is statisch; formules worden platte waarden. | Als je live berekeningen nodig hebt, houd de werkmap op de server en gebruik JavaScript‑bibliotheken zoals SheetJS. |
| **Ontbrekende afbeeldingen** | Afbeeldingen worden opgeslagen als afzonderlijke bronnen. | Stel `HtmlSaveOptions.ExportImagesAsBase64 = true` in om ze direct in te sluiten. |
| **Grote bestanden** | Grote werkmappen genereren enorme HTML + JS. | Gebruik `ExportOnlyVisibleSheets` of splits in meerdere pagina's via `HtmlSaveOptions.OnePagePerSheet`. |
| **Onjuiste getallen‑locale** | Excel slaat getallen op in een invariant culture, browsers kunnen lokale instellingen toepassen. | Stel expliciet `htmlOptions.Encoding = Encoding.UTF8` in en gebruik `GridJsOptions.EnableNumberFormat`. |

---

## Geavanceerd: Meerdere bladen exporteren met individuele Grid.js‑instanties

Als je werkmap meerdere bladen bevat en je wilt dat elk blad zijn eigen Grid.js‑tabel wordt, kun je door de werkbladen itereren en elk afzonderlijk opslaan:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Elk bestand zal zijn eigen `<table class="gridjs-table">`‑element bevatten, klaar voor onafhankelijke manipulatie.

---

## Output verifiëren – Snelle checklist

1. **Stijlen intact?** Vergelijk celachtergrondkleuren en randen met de originele Excel‑weergave.  
2. **Getalopmaak behouden?** Zoek naar het `data-format`‑attribuut op `<td>`‑elementen.  
3. **Afbeeldingen weergegeven?** Als je afbeeldingen als Base64 hebt geëxporteerd, zouden ze inline moeten verschijnen.  
4. **Browser‑console schoon?** Geen JavaScript‑fouten gerelateerd aan Grid.js.  

Als een van deze controles faalt, bekijk dan opnieuw de betreffende `HtmlSaveOptions`‑eigenschap — de meeste problemen komen voort uit een ontbrekende vlag.

---

## Conclusie

Je hebt nu een solide, productie‑klare methode om **Excel als HTML op te slaan** terwijl elke stijl, rand en numerieke weergave intact blijft. Door `HtmlSaveOptions` te configureren en `GridJsOptions.EnableNumberFormat` in te schakelen, heb je een statische spreadsheet omgevormd tot een web‑vriendelijke tabel die naadloos werkt met Grid.js.

Kort samengevat laat deze tutorial je zien hoe je **Excel naar HTML kunt converteren** en **Excel met opmaak kunt exporteren** met Aspose.Cells. Voel je vrij om te experimenteren: probeer verschillende thema's, voeg grafieken in, of serveer de HTML zelfs via een ASP.NET‑endpoint voor realtime conversie.

---

## Wat is het volgende?

- **Verken andere exportformaten**: PDF, PNG of CSV via `Workbook.Save`.  
- **Integreren met ASP.NET Core**: Retourneer de HTML‑string direct vanuit een controller‑actie.  
- **Combineren met SheetJS**: Laad de gegenereerde HTML terug in een JavaScript‑werkmap voor client‑side bewerking.  

Als je ergens tegenaan loopt, laat dan een reactie achter of raadpleeg de Aspose.Cells‑documentatie voor diepere configuratie‑opties. Veel plezier met coderen!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel naar HTML te exporteren met rasterlijnen met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Excel naar HTML exporteren met behoud van randstijlen met Aspose.Cells voor Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [HTML naar Excel converteren met Aspose.Cells .NET: Een uitgebreide gids](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}