---
category: general
date: 2026-06-08
description: Hoe werkbladen in Excel te koppelen met SmartMarkerProcessor voor master‑detailrapporten.
  Vul het masterblad in en genereer moeiteloos een master‑detail Excel‑rapport.
draft: false
keywords:
- how to link sheets
- populate master sheet
- create master detail excel
- generate master detail report
language: nl
og_description: Hoe je bladen in Excel koppelt met SmartMarkerProcessor. Leer hoe
  je het mastersheet vult en binnen enkele minuten een master‑detailrapport genereert.
og_title: Hoe bladen in Excel te koppelen met SmartMarker – Stap voor stap
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  headline: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  type: TechArticle
- description: How to link sheets in Excel using SmartMarkerProcessor for master‑detail
    reports. Populate master sheet and generate a master detail Excel report effortlessly.
  name: How to Link Sheets in Excel with SmartMarker – Step‑by‑Step Guide
  steps:
  - name: Multiple Detail Rows per Master
    text: If a master row has several related details, SmartMarker repeats the master
      row once and then writes *all* matching detail rows beneath it. No extra code
      is needed—just ensure your `Details` collection contains every row.
  - name: Missing Details
    text: When a master entry has no matching detail rows, the detail sheet simply
      skips that section. If you need a placeholder (e.g., “No items”), you can add
      a calculated column in the template that uses an Excel formula like `=IF(COUNTA(A2:B2)=0,"No
      items","")`.
  - name: Large Datasets
    text: 'Processing tens of thousands of rows can be memory‑intensive. To keep performance
      snappy:'
  - name: Custom Column Mapping
    text: If your property names don’t line up (`MasterKey` vs `Id`), you can use
      the `SmartMarkerProcessor.Map` method to create an alias before processing.
  type: HowTo
tags:
- Excel
- SmartMarker
- C#
- master‑detail
title: Hoe werkbladen in Excel koppelen met SmartMarker – Stapsgewijze gids
url: /nl/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe werkbladen in Excel koppelen met SmartMarker – Stapsgewijze gids

Heb je je ooit afgevraagd **hoe je werkbladen** in Excel kunt koppelen zonder handmatig rijen te kopiëren of eindeloze VBA‑lussen te schrijven? Je bent niet de enige. De meeste ontwikkelaars lopen tegen een muur aan wanneer ze een overzichtelijk master‑detail‑rapport nodig hebben dat synchroon blijft terwijl de gegevens veranderen. Het goede nieuws? SmartMarkerProcessor doet het zware werk voor je en verandert een paar regels C# in een volledig master‑detail‑werkboek.

In deze tutorial lopen we de exacte stappen door om **master sheet te vullen**, het detailblad in te stellen, en uiteindelijk **een master‑detail‑rapport te genereren** dat automatisch wordt bijgewerkt. Aan het einde heb je een herbruikbaar patroon dat je in elk .NET‑project kunt gebruiken.

> **Voorwaarde:** Je hebt GrapeCity Documents for Excel (GcExcel) versie 2024 of later nodig, een .NET‑ontwikkelomgeving (Visual Studio 2022 werkt uitstekend), en basiskennis van C#. Er zijn geen extra NuGet‑pakketten nodig naast GcExcel.

---

## Overzicht van de oplossing

Before we duiken in de code, laten we uiteenzetten wat “werkbladen koppelen” eigenlijk betekent in de context van SmartMarker:

1. **Master sheet** – Bevat één rij per entiteit (bijv. een lijst met klanten).
2. **Detail sheet** – Bevat rijen die behoren tot een master‑rij (bijv. bestellingen voor elke klant).
3. **SmartMarker syntax** – Een kleine opmaaktaal (`{MasterSheet}#master;{DetailSheet}#detail`) die de processor vertelt hoe de twee datatabellen te binden.
4. **Processor options** – Het inschakelen van `MasterDetail` zorgt ervoor dat de engine automatisch de master‑rijen herhaalt en de gerelateerde detail‑rijen eronder invoegt.

Het begrijpen van deze onderdelen helpt je later de aanpak aan te passen — misschien heb je een drie‑niveau nesting of voorwaardelijke opmaak nodig. Houd dit mentale model bij de hand terwijl we de implementatie stap voor stap doorlopen.

## Stap 1: Hiërarchische gegevens voorbereiden voor Master‑Detail verwerking

Het eerste wat je nodig hebt is een gegevensbron die de master‑detail‑relatie weerspiegelt. In de meeste real‑world scenario's komt dit uit een database, maar voor de duidelijkheid gebruiken we een anonieme object‑literal.

```csharp
// Step 1: Prepare hierarchical data for master‑detail processing
var sampleData = new
{
    // Master collection – one row per category
    Master = new[]
    {
        new { Id = 1, Name = "A" },
        new { Id = 2, Name = "B" }
    },

    // Detail collection – rows reference MasterId
    Details = new[]
    {
        new { MasterId = 1, Item = "Item1" },
        new { MasterId = 2, Item = "Item2" }
    }
};
```

**Waarom dit belangrijk is:** SmartMarker raadt relaties niet magisch; het zoekt naar overeenkomende eigenschapsnamen (`MasterId` → `Id`). Door de gegevens op deze manier te structureren geven we de processor een duidelijke kaart, wat de hoeksteen is van **hoe je werkbladen koppelt**.

> **Pro tip:** Als je gegevens zich in `DataTable`‑objecten bevinden, exposeer ze dan gewoon als eigenschappen met dezelfde namen — SmartMarker werkt met elke doorzoekbare collectie.

## Stap 2: Een werkboek maken en een sjabloon laden

SmartMarker werkt tegen een bestaand Excel‑werkboek, meestal een sjabloon dat al de bladnamen en placeholder‑markers bevat. Laten we een werkboek in het geheugen maken en twee lege werkbladen toevoegen met de namen *MasterSheet* en *DetailSheet*.

```csharp
using GrapeCity.Documents.Excel;

// Step 2: Create a workbook and add template sheets
IWorkbook wb = new Workbook();

// Create the master sheet and add a header row
IWorksheet masterSheet = wb.Worksheets.Add("MasterSheet");
masterSheet.Range["A1"].Value = "ID";
masterSheet.Range["B1"].Value = "Name";

// Create the detail sheet and add its header
IWorksheet detailSheet = wb.Worksheets.Add("DetailSheet");
detailSheet.Range["A1"].Value = "Master ID";
detailSheet.Range["B1"].Value = "Item";
```

Je kunt ook een `.xlsx`‑bestand van de schijf laden (`wb.Open("Template.xlsx")`) als je de lay-out eerst in Excel wilt ontwerpen. Het belangrijke is dat de bladnamen overeenkomen met die je in de SmartMarker‑string zult refereren.

## Stap 3: SmartMarkerProcessor instantiëren en Master‑Detail‑modus inschakelen

Nu brengen we de engine binnen die de markers leest en de gegevens plakt. De `SmartMarkerProcessor` neemt het werkboek als constructor‑argument, en de `Options.MasterDetail`‑vlag vertelt hem om de `#master`‑ en `#detail`‑markers als een gekoppeld paar te behandelen.

```csharp
// Step 3: Create a SmartMarkerProcessor for the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

// Enable master‑detail mode on the processor options
processor.Options.MasterDetail = true;
```

**Waarom `MasterDetail` inschakelen?** Zonder deze vlag zou de processor `{MasterSheet}#master` en `{DetailSheet}#detail` als onafhankelijke bewerkingen behandelen, waardoor de cruciale relatie tussen rijen verloren gaat. Het instellen van de vlag is de enige regel die **hoe je werkbladen koppelt** daadwerkelijk laat werken.

## Stap 4: De SmartMarker‑string definiëren en de processor uitvoeren

De marker‑string vertelt SmartMarker welk blad de master is en welk blad het detail is. De syntaxis is eenvoudig: `{SheetName}#master;{SheetName}#detail`. Je kunt ook extra markers toevoegen (bijv. `#header`), maar die zijn niet nodig voor een basisrapport.

```csharp
// Step 4: Execute the smart‑marker processing, linking master and detail sheets
string marker = "{MasterSheet}#master;{DetailSheet}#detail";
processor.Process(marker, sampleData);
```

Wanneer `Process` draait, doet de engine:

1. Schrijft elke master‑rij naar *MasterSheet* beginnend bij de eerste lege rij na de koptekst.
2. Voor elke master‑rij scant het de `Details`‑collectie, selecteert rijen waar `MasterId` overeenkomt met de master `Id`, en schrijft ze direct onder de corresponderende master‑invoer in *DetailSheet*.

## Stap 5: Het resulterende werkboek opslaan of exporteren

Op dit punt heb je een volledig gevuld werkboek. Je kunt het opslaan op schijf, streamen naar een webclient, of zelfs converteren naar PDF.

```csharp
// Save the workbook to a file (you could also stream it to a response)
wb.Save("MasterDetailReport.xlsx");
```

Open het bestand en je ziet twee bladen: *MasterSheet* toont `A` en `B`, terwijl *DetailSheet* `Item1` onder master `1` en `Item2` onder master `2` laat zien. Dat is de essentie van **master sheet vullen** en **een master‑detail‑rapport genereren** in één keer.

## Visueel overzicht

![Diagram dat laat zien hoe je werkbladen in Excel koppelt met SmartMarkerProcessor](https://example.com/diagram.png "Diagram hoe werkbladen koppelen")

Het diagram (alt‑tekst bevat het primaire zoekwoord) toont de gegevensstroom van C#‑objecten → SmartMarkerProcessor → gekoppelde Excel‑bladen.

## Veelvoorkomende randgevallen behandelen

### Meerdere detailrijen per master

Als een master‑rij meerdere gerelateerde details heeft, herhaalt SmartMarker de master‑rij één keer en schrijft vervolgens *alle* overeenkomende detailrijen eronder. Er is geen extra code nodig — zorg er alleen voor dat je `Details`‑collectie elke rij bevat.

### Ontbrekende details

Wanneer een master‑invoer geen overeenkomende detailrijen heeft, slaat het detailblad die sectie simpelweg over. Als je een placeholder nodig hebt (bijv. “Geen items”), kun je een berekende kolom toevoegen in de sjabloon die een Excel‑formule gebruikt zoals `=IF(COUNTA(A2:B2)=0,"No items","")`.

### Grote datasets

Het verwerken van tienduizenden rijen kan veel geheugen verbruiken. Om de prestaties vlot te houden:

- Gebruik `processor.Options.EnableStreaming = true` (beschikbaar in GcExcel 2025+).
- Verdeel de gegevens in stukken en verwerk elk stuk afzonderlijk, en voeg daarna de werkboeken samen.

### Aangepaste kolomtoewijzing

Als je eigenschapsnamen niet overeenkomen (`MasterKey` vs `Id`), kun je de `SmartMarkerProcessor.Map`‑methode gebruiken om vóór het verwerken een alias te maken.

```csharp
processor.Map("MasterId", "Id"); // tells the engine that MasterId maps to Id
```

## Volledig werkend voorbeeld

Alles samenvoegend, hier is een compleet, kant‑klaar programma dat je direct kunt uitvoeren.



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Externe koppelformules in Excel met Aspose.Cells voor Java](/cells/english/java/formulas-functions/aspose-cells-java-external-link-formulas-excel/)
- [Dynamische Excel‑bladen in Java met Aspose.Cells: Een uitgebreide gids](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamische Excel‑rapporten met Aspose.Cells Java: benoemde bereiken & complexe formules](/cells/english/java/templates-reporting/dynamic-excel-reports-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}