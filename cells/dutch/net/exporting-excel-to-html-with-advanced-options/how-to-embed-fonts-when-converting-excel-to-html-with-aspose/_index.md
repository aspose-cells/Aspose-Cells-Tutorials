---
category: general
date: 2026-10-01
description: Leer hoe je lettertypen in HTML kunt insluiten tijdens het converteren
  van Excel naar HTML met Aspose.Cells. Exporteer Excel als HTML met ingesloten lettertypen
  in een paar stappen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to embed fonts
- convert excel to html
- embed fonts in html
- how to export excel
- export excel as html
language: nl
lastmod: 2026-10-01
og_description: Hoe lettertypen in HTML in te sluiten bij het exporteren van Excel‑bestanden.
  Volg deze stapsgewijze handleiding om Excel naar HTML te converteren met ingesloten
  lettertypen.
og_image_alt: Screenshot of Aspose.Cells code embedding fonts in exported HTML
og_title: Hoe lettertypen in HTML vanuit Excel in te sluiten – Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  headline: How to embed fonts when converting Excel to HTML with Aspose.Cells
  type: TechArticle
- description: Learn how to embed fonts in HTML while converting Excel to HTML using
    Aspose.Cells. Export Excel as HTML with embedded fonts in a few steps.
  name: How to embed fonts when converting Excel to HTML with Aspose.Cells
  steps:
  - name: 'Edge case: unsupported fonts'
    text: If the workbook uses a font that is not installed on the server, Aspose.Cells
      falls back to a default system font. To avoid this, install the required fonts
      on the server or embed them manually after export.
  - name: Converting multiple worksheets
    text: If you need to **convert Excel to HTML** for all worksheets, set `ExportActiveWorksheetOnly
      = false` (the default). Aspose.Cells will create a separate HTML file for each
      sheet.
  - name: Controlling CSS output
    text: 'You can reduce the HTML size by disabling inline CSS:'
  - name: Using a stream instead of a file
    text: 'When integrating into a web API, write the HTML to a `MemoryStream` and
      return it directly:'
  type: HowTo
tags:
- Aspose.Cells
- .NET
- Excel conversion
title: Hoe lettertypen inbedden bij het converteren van Excel naar HTML met Aspose.Cells
url: /nl/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-when-converting-excel-to-html-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe lettertypen inbedden bij het converteren van Excel naar HTML met Aspose.Cells

Hoe lettertypen in HTML inbedden bij het converteren van een Excel‑werkmap is essentieel om het oorspronkelijke uiterlijk in verschillende browsers te behouden. Als je Excel naar HTML wilt converteren en daarbij aangepaste lettertypen intact wilt houden, laat deze gids het volledige proces zien. Je ziet ook hoe je Excel als HTML kunt exporteren en waarom het inbedden van lettertypen in HTML belangrijk is voor consistente weergave.

Deze tutorial behandelt alles wat je moet weten: vereiste bibliotheken, code‑configuratie en verificatie van het gegenereerde HTML‑bestand. Aan het einde kun je Excel als HTML exporteren met ingebedde lettertypen in slechts een paar regels C#.

## Wat je nodig hebt

Voordat je begint, zorg dat je het volgende hebt:

* **.NET 6.0 of hoger** – de code richt zich op .NET 6, maar elke .NET‑versie die Aspose.Cells ondersteunt werkt.
* **Aspose.Cells for .NET** – verkrijg een licentie of gebruik de gratis evaluatie‑versie van de Aspose‑website.
* Een **C#‑ontwikkelomgeving** (Visual Studio, Rider of VS Code) – elke IDE die .NET‑projecten kan compileren.
* Een Excel‑werkmap (`Styled.xlsx`) die aangepaste lettertypen gebruikt die je wilt behouden.

## Stap 1: Aspose.Cells instellen in je .NET‑project

Voeg eerst het Aspose.Cells‑NuGet‑pakket toe aan je project:

```bash
dotnet add package Aspose.Cells
```

Voeg vervolgens de namespace toe aan de bovenkant van je C#‑bestand:

```csharp
using Aspose.Cells;
```

Het toevoegen van het pakket maakt de `Workbook`, `HtmlSaveOptions` en gerelateerde klassen beschikbaar.

## Stap 2: De Excel‑werkmap laden

Het laden van de werkmap is de eerste concrete stap in **hoe je Excel‑gegevens exporteert**. De `Workbook`‑constructor leest het bestand van de schijf:

```csharp
// Step 1: Load the Excel workbook
var workbook = new Workbook("YOUR_DIRECTORY/Styled.xlsx");
```

*Waarom dit belangrijk is:* Aspose.Cells parseert de werkmap, inclusief celstijlen, formules en lettertype‑informatie. Als het bestand niet gevonden kan worden, wordt er een uitzondering gegooid, dus zorg dat het pad correct is.

## Stap 3: HTML‑opslaan‑opties configureren om lettertypen in te bedden

De kern van **lettertypen inbedden in html** is de `HtmlSaveOptions`‑klasse. Stel `EmbedFonts` in op `true` zodat elk lettertype dat in de werkmap wordt gebruikt, wordt geschreven naar de HTML‑output als een Base64‑gecodeerde `@font-face`‑regel.

```csharp
// Step 2: Set HTML save options to embed fonts in the output
var htmlOptions = new HtmlSaveOptions
{
    EmbedFonts = true,
    // Optional: keep the original worksheet name as the HTML file name
    ExportActiveWorksheetOnly = true
};
```

*Waarom dit belangrijk is:* Standaard verwijst Aspose.Cells naar externe lettertypebestanden, die mogelijk niet beschikbaar zijn op de client‑machine. Het inschakelen van `EmbedFonts` garandeert dat de gerenderde HTML er identiek uitziet als het oorspronkelijke Excel‑blad, ongeacht welke lettertypen de kijker geïnstalleerd heeft.

### Randgeval: niet‑ondersteunde lettertypen

Als de werkmap een lettertype gebruikt dat niet op de server is geïnstalleerd, valt Aspose.Cells terug op een standaard systeemlettertype. Om dit te voorkomen, installeer de vereiste lettertypen op de server of embed ze handmatig na export.

## Stap 4: De werkmap opslaan als HTML met de geconfigureerde opties

Nu kun je het HTML‑bestand schrijven. De `Save`‑methode neemt het uitvoerpad en de `HtmlSaveOptions`‑instantie:

```csharp
// Step 3: Save the workbook as an HTML file using the configured options
workbook.Save("YOUR_DIRECTORY/Styled.html", htmlOptions);
```

Na uitvoering bevat `Styled.html` de spreadsheet‑gegevens en een `<style>`‑blok met Base64‑gecodeerde `@font-face`‑definities voor elk aangepast lettertype.

## Stap 5: De ingebedde lettertypen verifiëren

Open `Styled.html` in een browser. Inspecteer de `<head>`‑sectie; je zou iets moeten zien als:

```html
<style>
@font-face {
    font-family: 'Calibri';
    src: url(data:font/ttf;base64,AAEAAAARAQAABAA...);
}
...
</style>
```

Als de lettertypen correct verschijnen in de gerenderde tabel, is het inbedden gelukt. Als er tekens ontbreken, controleer dan nogmaals of de bron‑lettertypebestanden op de machine die de conversie uitvoert, geïnstalleerd zijn.

## Veelvoorkomende variaties en extra opties

### Meerdere werkbladen converteren

Als je **Excel naar HTML wilt converteren** voor alle werkbladen, stel `ExportActiveWorksheetOnly = false` in (de standaard). Aspose.Cells maakt een apart HTML‑bestand voor elk blad.

```csharp
htmlOptions.ExportActiveWorksheetOnly = false;
workbook.Save("YOUR_DIRECTORY/AllSheets.html", htmlOptions);
```

### CSS‑output beheersen

Je kunt de HTML‑grootte verkleinen door inline CSS uit te schakelen:

```csharp
htmlOptions.ExportCssSeparately = true; // Generates a .css file alongside the .html
```

### Een stream gebruiken in plaats van een bestand

Bij integratie in een web‑API kun je de HTML naar een `MemoryStream` schrijven en direct teruggeven:

```csharp
using var stream = new MemoryStream();
workbook.Save(stream, htmlOptions);
stream.Position = 0; // Reset for reading
// Return stream as a file download in ASP.NET Core
```

## Pro‑tip: Licentie het product om evaluatiewatermerken te verwijderen

Als je de evaluatie‑versie gebruikt, kan het gegenereerde HTML‑bestand een watermerk‑commentaar bevatten. Pas je Aspose.Cells‑licentie toe vóór het laden van de werkmap om schone output te produceren:

```csharp
var license = new License();
license.SetLicense("Aspose.Total.lic");
```

## Volledig werkend voorbeeld

Hieronder staat een compleet, uitvoerbaar programma dat **hoe je lettertypen inbedt**, **excel naar html converteert** en **excel als html exporteert** in één stap demonstreert:

```csharp
using System;
using Aspose.Cells;

class ExcelToHtmlWithEmbeddedFonts
{
    static void Main()
    {
        // Apply license if you have one (optional)
        // var license = new License();
        // license.SetLicense("Aspose.Total.lic");

        // 1️⃣ Load the Excel workbook
        var workbookPath = @"YOUR_DIRECTORY/Styled.xlsx";
        var workbook = new Workbook(workbookPath);

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportActiveWorksheetOnly = true, // Export only the first sheet
            ExportCssSeparately = false        // Keep CSS inline for a single file
        };

        // 3️⃣ Save as HTML
        var htmlPath = @"YOUR_DIRECTORY/Styled.html";
        workbook.Save(htmlPath, htmlOptions);

        Console.WriteLine($"Excel workbook '{workbookPath}' has been exported to HTML with embedded fonts at '{htmlPath}'.");
    }
}
```

**Verwachte output:** Na het uitvoeren van het programma verschijnt `Styled.html` in `YOUR_DIRECTORY`. Het openen van het bestand in een moderne browser toont de spreadsheet met dezelfde lettertypen als in het oorspronkelijke Excel‑bestand, zelfs op machines die die lettertypen niet hebben.

## Conclusie

Je weet nu **hoe je lettertypen inbedt** wanneer je **Excel naar HTML converteert** met Aspose.Cells, en je hebt de volledige workflow gezien van het laden van een werkmap tot het verifiëren van de ingebedde lettertypen. Deze aanpak zorgt ervoor dat de visuele getrouwheid van je Excel‑bestanden behouden blijft in de gegenereerde HTML, wat ideaal is voor web‑rapportage, e‑mail‑nieuwsbrieven of elke situatie waarin je **Excel als HTML moet exporteren** met aangepaste typografie.

Ga vervolgens verder met gerelateerde onderwerpen zoals **Excel exporteren als PDF**, **HTML‑output stylen met aangepaste CSS**, of **batch‑verwerking van meerdere werkboeken**. Elk van deze bouwt voort op hetzelfde `HtmlSaveOptions`‑patroon, zodat je de code met minimale aanpassingen kunt hergebruiken.

Happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Export Excel to HTML – Step‑by‑Step Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-export-excel-to-html-step-by-step-guide/)
- [How to Embed Fonts in HTML – Complete C# Guide](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/)
- [How to embed fonts when converting Excel to PDF – Step‑by‑Step Guide](/cells/english/net/conversion-to-pdf/how-to-embed-fonts-when-converting-excel-to-pdf-step-by-step/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}