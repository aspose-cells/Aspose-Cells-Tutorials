---
category: general
date: 2026-10-01
description: Leer hoe u aangepaste eigenschappen aan een Excel-werkmap kunt toevoegen
  met Aspose.Cells. Deze gids laat ook zien hoe u een project‑ID kunt toevoegen en
  aangepaste eigenschappen kunt lezen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: nl
lastmod: 2026-10-01
og_description: Voeg aangepaste eigenschappen toe aan een Excel-werkmap met Aspose.Cells.
  Volg deze volledige tutorial om een project-ID toe te voegen, reviewer‑informatie
  in te stellen en aangepaste eigenschappen programmatisch te lezen.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Aangepaste eigenschappen toevoegen aan Excel-werkmap – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe aangepaste eigenschappen aan een Excel-werkmap toe te voegen
url: /nl/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe aangepaste eigenschappen toe te voegen aan een Excel-werkmap

Als je **aangepaste eigenschappen** aan een Excel-werkmap moet toevoegen, laat deze gids je precies zien hoe je dat doet met Aspose.Cells for .NET. Je leert ook hoe je een project‑ID toevoegt, een beoordelaarnaam instelt, en later **aangepaste eigenschappen** weer uit het bestand **leest**.

Werken met aangepaste metadata stelt je in staat om bedrijfs‑specifieke informatie direct in de spreadsheet te embedden, waardoor het eenvoudig wordt om eigendom, versie of andere context bij te houden zonder een aparte database te onderhouden. De onderstaande stappen behandelen de volledige end‑to‑end workflow, van het maken van de werkmap tot het opslaan van de nieuwe eigenschappen.

## Prerequisites

Voordat je begint, zorg dat je het volgende hebt:

* .NET 6.0 of later geïnstalleerd  
* Een geldige Aspose.Cells for .NET‑licentie (of een gratis proefversie)  
* Visual Studio 2022 (of een andere C#‑IDE)  

Er zijn geen extra NuGet‑pakketten nodig naast `Aspose.Cells`.

## Step 1: Set up the project and import namespaces

Maak een nieuwe console‑applicatie en voeg de Aspose.Cells‑referentie toe:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

De `Aspose.Cells`‑namespace bevat de klassen `Workbook`, `Worksheet` en `CustomPropertyCollection` die we gaan gebruiken.

## Step 2: Load an existing workbook (or create a new one)

Je kunt beginnen met een bestaande `.xlsb`‑file of een nieuwe werkmap genereren. Het voorbeeld hieronder laadt een bestand met de naam **Data.xlsb** dat zich bevindt in een map genaamd `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Als het bestand niet bestaat, vervang dan de code door `new Workbook();` om een lege werkmap te maken.

## Step 3: Add custom properties to the first worksheet

De primaire handeling is om **aangepaste eigenschappen** aan een werkblad toe te voegen. Aspose.Cells slaat aangepaste eigenschappen op in een collectie die zich gedraagt als een woordenboek.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Waarom we `CustomProperties.Add` gebruiken in plaats van `CustomProperties["Name"] = value` is dat de `Add`‑methode het item maakt als het nog niet bestaat en garandeert dat het juiste gegevenstype wordt opgeslagen. Deze aanpak voorkomt onbedoelde type‑mismatches die later runtime‑fouten kunnen veroorzaken bij het lezen van de waarden.

## Step 4: Save the workbook with the new properties

Nadat je de metadata hebt geïnjecteerd, sla je de wijzigingen op in een nieuw bestand zodat het origineel onaangeroerd blijft.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Op dit moment bevat het Excel‑bestand de aangepaste metadata die je hebt gedefinieerd. Je kunt de eigenschappen verifiëren met de stappen in de volgende sectie.

## Step 5: Read custom properties from a workbook

Het lezen van **excel custom properties** volgt hetzelfde collectie‑patroon. Dit fragment toont hoe je de waarden die we zojuist hebben opgeslagen, kunt ophalen.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

De indexer van `CustomPropertyCollection` retourneert een `CustomProperty`‑object; door de `Value`‑eigenschap te benaderen krijg je de opgeslagen data in het oorspronkelijke type. Controleren op `null` vóór het casten voorkomt een `NullReferenceException` als een eigenschap ontbreekt.

### Expected console output

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

De tijdstempel zal het exacte moment weergeven waarop je `Add` in stap 3 hebt aangeroepen.

## Pro tip: Updating an existing custom property

Als je later **how to add custom** informatie moet toevoegen (bijvoorbeeld de beoordelaar wijzigen), gebruik dan de setter van `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Dit patroon zorgt ervoor dat de eigenschap wordt bijgewerkt of aangemaakt, wat nuttig is in iteratieve workflows zoals geautomatiseerde rapportgeneratie.

## Step 6: Verify the properties inside Excel (optional)

Je kunt de aangepaste eigenschappen ook direct in Excel bekijken:

1. Open het opgeslagen `DataWithProps.xlsb`‑bestand in Microsoft Excel.  
2. Ga naar **Bestand → Info → Eigenschappen → Geavanceerde eigenschappen**.  
3. Selecteer het tabblad **Aangepast**.  

Je ziet de items `ProjectId`, `Reviewer` en `CreatedOn` met hun respectieve waarden.

## Full working example

Hieronder staat het volledige, zelfstandige programma dat alle eerdere fragmenten combineert. Kopieer het naar `Program.cs` en voer het uit; de console zal de opgehaalde waarden weergeven.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Het uitvoeren van dit programma levert de eerder getoonde console‑output op en maakt `DataWithProps.xlsb` aan met de ingebedde metadata.

## Common questions and edge cases

| Question | Answer |
|---|---|
| **Can I store non‑primitive types?** | Aspose.Cells ondersteunt `string`, `int`, `double`, `DateTime` en `bool`. Voor complexe objecten serialiseer je ze eerst naar JSON of XML en sla je de string op. |
| **What if the workbook is password‑protected?** | Open de werkmap met een wachtwoord (`new Workbook(path, password)`) voordat je `CustomProperties` benadert. De eigenschappen blijven toegankelijk na ontcijferen. |
| **Do custom properties survive format conversion?** | Bij het opslaan naar een ander formaat (bijv. `.xlsx`) behoudt Aspose.Cells aangepaste eigenschappen zolang het doelformaat ze ondersteunt. |
| **How to delete a custom property?** | Gebruik `worksheet.CustomProperties.Remove("PropertyName");`. Hiermee wordt het item uit de collectie verwijderd. |

## Next steps

Nu je weet **add custom properties**, kun je gerelateerde onderwerpen verkennen, zoals:

* **excel custom properties** voor documentversiebeheer  
* **read custom properties** uit meerdere werkbladen in één werkmap  
* Het gebruik van **Aspose.Cells** om draaitabellen te maken die verwijzen naar aangepaste metadata  
* Het exporteren van de werkmap naar PDF terwijl aangepaste eigenschappen behouden blijven  

Experimenteer met verschillende gegevenstypen, combineer aangepaste eigenschappen met celopmerkingen, of integreer de metadata in een groter document‑beheersysteem.

---

**Ready to automate your Excel reporting?** Voeg de bovenstaande code toe aan je project, pas de eigenschapsnamen aan op basis van je zakelijke behoeften, en je hebt een zelf‑beschrijvende spreadsheet klaar voor downstream‑verwerking.

## What Should You Learn Next?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}