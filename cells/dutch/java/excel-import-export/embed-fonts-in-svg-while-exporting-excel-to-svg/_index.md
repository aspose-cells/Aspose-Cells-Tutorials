---
category: general
date: 2026-08-14
description: Lettertypen insluiten in SVG bij het exporteren van Excel naar SVG met
  Aspose.Cells. Leer hoe u het afdrukgebied instelt, afdrukopties configureert en
  de WRAPCOLS-functie gebruikt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: nl
lastmod: 2026-08-14
og_description: Lettertypen insluiten in SVG bij het exporteren van Excel naar SVG
  met Aspose.Cells. Deze gids laat zien hoe je het afdrukgebied instelt, afdrukopties
  configureert en de WRAPCOLS‑functie toepast.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Lettertypen insluiten in SVG bij het exporteren van Excel naar SVG – stap
  voor stap
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Lettertypen insluiten in SVG bij het exporteren van Excel naar SVG
url: /nl/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lettertypen insluiten in SVG bij het exporteren van Excel naar SVG

Als je **lettertypen in SVG wilt insluiten bij het exporteren van Excel naar SVG**, laat deze tutorial je precies zien hoe je dat doet met Aspose.Cells for Java. We behandelen ook hoe je **een afdrukgebied instelt**, **afdrukopties configureert**, en **de WRAPCOLS‑functie gebruikt** om gegevens te formatteren zonder de lay-out te verliezen.

Je doorloopt een volledig, uitvoerbaar voorbeeld dat een bestaande werkmap laadt, de `WRAPCOLS`‑formule toepast, SVG‑specifieke afbeeldingsopties configureert, het afdrukgebied definieert en uiteindelijk het bestand opslaat als een SVG met ingesloten lettertypen. Geen externe documentatie nodig—kopieer gewoon de code, voer deze uit en inspecteer de resulterende SVG.

## Lettertypen insluiten in SVG – configureren van ImageOrPrintOptions

Het insluiten van lettertypen zorgt ervoor dat de SVG exact wordt weergegeven zoals in Excel, zelfs op machines die de oorspronkelijke lettertypen niet geïnstalleerd hebben.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Waarom dit belangrijk is*: Wanneer `setEmbedFonts(true)` is ingeschakeld, schrijft Aspose.Cells de lettertype‑data rechtstreeks in de `<defs>`‑sectie van de SVG. Het resultaat is een zelfstandig bestand dat er identiek uitziet in alle browsers en op alle platforms.

## Exporteren van Excel naar SVG – volledige workflow

De volgende stappen illustreren het end‑to‑end proces, van het laden van de werkmap tot het opslaan van het SVG‑bestand.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Verwacht resultaat**: `output.svg` verschijnt in `YOUR_DIRECTORY`. Het openen in een browser toont het werkblad met alle ingesloten lettertypen, de gegevens verpakt in drie kolommen (dankzij `WRAPCOLS`), en alleen de cellen binnen `A1:H30` worden weergegeven.

## Afdrukgebied instellen voor het werkblad

Het definiëren van een afdrukgebied beperkt de geëxporteerde SVG tot een specifiek bereik, waardoor de bestandsgrootte afneemt en de kijker zich richt op de relevante gegevens.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Tip*: Het bereik volgt de A1‑notatie van Excel. Als je een dynamisch bereik nodig hebt, kun je dit programmatisch berekenen met `ws.getCells().getMaxDisplayRange()`.

## Afdrukopties instellen voor SVG‑output

Afdrukopties bepalen hoe Aspose.Cells het werkblad omzet naar een afbeelding. Naast het insluiten van lettertypen kun je resolutie, schaal en paginalay-out aanpassen.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Waarom je afdrukopties moet instellen*: Zonder expliciete opties gebruikt Aspose.Cells standaardinstellingen die het insluiten van lettertypen kunnen weglaten of een ongewenste schaalfactor toepassen, wat leidt tot onscherpe of onjuist gestylede SVG’s.

## WRAPCOLS‑functie gebruiken om kolomgegevens te verpakken

`WRAPCOLS` is een Excel‑formule die een verticale reeks verdeelt over een opgegeven aantal kolommen. Handig wanneer je een lange lijst compact wilt weergeven.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Wanneer de werkmap wordt opgeslagen, evalueert Aspose.Cells de formule en produceert een lay-out van drie kolommen binnen het gedefinieerde afdrukgebied. Deze techniek werkt voor elk bereik—pas simpelweg het tweede argument aan naar het gewenste aantal kolommen.

## Volledig uitvoerbaar voorbeeld

Hieronder staat het volledige Java‑programma dat je in elke IDE kunt plakken. Zorg ervoor dat de Aspose.Cells for Java‑bibliotheek op je classpath staat.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Verificatiestappen**

1. Voer het programma uit.  
2. Open `output.svg` in een webbrowser.  
3. Controleer of de tekst dezelfde lettertype gebruikt als het originele Excel‑bestand (lettertypen zijn ingesloten).  
4. Verifieer dat alleen de cellen binnen `A1:H30` verschijnen en dat de gegevens van `A2:A10` in drie kolommen worden weergegeven.

## Veelvoorkomende valkuilen en hoe ze te vermijden

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Lettertypen ontbreken in de SVG | `setEmbedFonts(false)` of het lettertype‑bestand is niet toegankelijk | Zorg voor `setEmbedFonts(true)` en dat het lettertype geïnstalleerd is op de machine die de code uitvoert |
| WRAPCOLS wordt niet geëvalueerd | Rekengine uitgeschakeld | Roep `workbook.calculateFormula()` aan vóór het exporteren, of laat Aspose.Cells tijdens het opslaan evalueren |
| Geëxporteerde SVG is leeg | Afdrukgebied omvat geen gegevens | Controleer het bereik dat aan `setPrintArea` wordt doorgegeven |
| SVG‑bestand is enorm | Geen schaal toegepast, hoge resolutie | Pas `imgOptions.setResolution(96)` of een vergelijkbare instelling aan om de DPI te regelen |

## Pro‑tip: ImageOrPrintOptions hergebruiken voor meerdere werkbladen

Als je werkmap meerdere bladen bevat die identieke SVG‑instellingen nodig hebben, maak dan één `ImageOrPrintOptions`‑instantie aan en wijs deze toe aan de `PageSetup` van elk werkblad. Dit vermindert het geheugenverbruik en garandeert consistente insluiting van lettertypen in alle geëxporteerde bestanden.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Volgende stappen

* **Exporteren naar andere vectorformaten** – Verander `ImageFormat.SVG` naar `ImageFormat.PDF` voor PDF’s van hoge kwaliteit.  
* **Batchverwerking** – Loop door een map met `.xlsx`‑bestanden en genereer automatisch SVG’s.  
* **Aangepaste lettertype‑afhandeling** – Gebruik `FontSettings` om lettertypen uit een specifieke map te laden wanneer de systeembrede lettertypen ontoereikend zijn.  

Door **lettertypen in SVG in te sluiten**, **Excel naar SVG te exporteren**, **een afdrukgebied in te stellen**, **afdrukopties te configureren** en **de WRAPCOLS‑functie te gebruiken**, kun je geautomatiseerd SVG‑generatie van hoge kwaliteit realiseren voor rapporten, dashboards en webvisualisaties direct vanuit Excel‑gegevens. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}