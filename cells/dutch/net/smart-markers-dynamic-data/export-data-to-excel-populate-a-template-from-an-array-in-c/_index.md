---
category: general
date: 2026-02-21
description: Exporteer gegevens naar Excel door een Excel‑sjabloon te laden en Smart
  Markers te gebruiken om een Excel‑rapport uit een array te genereren. Leer hoe je
  een Excel‑sjabloon snel kunt invullen.
draft: false
keywords:
- export data to excel
- populate excel template
- load excel template
- generate excel report
- create excel from array
language: nl
og_description: Exporteer gegevens naar Excel met een SmartMarker‑sjabloon. Deze gids
  laat zien hoe je een Excel‑sjabloon laadt, een Excel‑bestand maakt vanuit een array
  en een Excel‑rapport genereert.
og_title: Gegevens exporteren naar Excel – Een sjabloon vullen vanuit een array
tags:
- C#
- Excel Automation
- Smart Markers
title: 'Gegevens exporteren naar Excel: Een sjabloon vullen vanuit een array in C#'
url: /nl/net/smart-markers-dynamic-data/export-data-to-excel-populate-a-template-from-an-array-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gegevens exporteren naar Excel: Een sjabloon vullen vanuit een array in C#

Heb je ooit **gegevens naar Excel moeten exporteren** maar wist je niet hoe je een eenvoudige array omtovert tot een mooi opgemaakt werkboek? Je bent niet de enige—de meeste ontwikkelaars lopen tegen die muur aan wanneer ze voor het eerst data willen delen met niet‑technische belanghebbenden. Het goede nieuws is dat je met een paar regels C# een **Excel‑sjabloon kunt laden**, je data kunt toevoegen en direct een **professioneel uitziend Excel‑rapport** kunt **genereren**.

In deze tutorial lopen we stap voor stap door een volledig, uitvoerbaar voorbeeld dat een **Excel‑sjabloon vult** met behulp van Aspose.Cells Smart Markers. Aan het einde kun je **Excel maken vanuit een array**, het resultaat opslaan en het bestand openen om de gevulde rijen te zien. Geen ontbrekende stukjes, alleen een zelfstandige oplossing die je kunt copy‑pasten in je project.

## Wat je zult leren

- Hoe je een **excel‑sjabloon laadt** dat al Smart Marker‑plaatsaanduidingen bevat zoals `${OrderId}` en `${OrderItems:ItemName}`.  
- Hoe je je gegevensbron structureert zodat de SmartMarkerProcessor over collecties kan itereren.  
- Hoe je een **excel‑sjabloon vult** met een geneste array en een voltooid **excel‑rapport genereert**.  
- Tips voor het omgaan met randgevallen zoals lege collecties of grote datasets.  

**Voorwaarden**: .NET 6+ (of .NET Framework 4.6+) en het Aspose.Cells for .NET NuGet‑pakket. Als je al Visual Studio gebruikt, voeg je het pakket toe via de NuGet‑manager—geen extra configuratie nodig.

![Export data to Excel process diagram](https://example.com/export-data-diagram.png "Export data to Excel workflow")

## Gegevens exporteren naar Excel met een SmartMarker‑sjabloon

Het eerste wat we nodig hebben is een werkboek dat fungeert als skelet voor ons rapport. Zie het als een Word‑document met samenvoegvelden, maar dan een Excel‑bestand en de velden heten **Smart Markers**.  

```csharp
// Step 1: Load the Excel template that contains Smart Markers (${OrderId}, ${OrderItems:ItemName})
var workbook = new Aspose.Cells.Workbook("YOUR_DIRECTORY/template.xlsx");
```

Waarom een sjabloon laden? Omdat de lay‑out—kolombreedtes, kopstijlen, formules—niet in code opnieuw opgebouwd hoeft te worden. Je ontwerpt het één keer in Excel, plaatst de markers, en laat de bibliotheek het zware werk doen.

## Laad het Excel‑sjabloon en bereid de omgeving voor

Voordat we iets kunnen verwerken, moeten we de Aspose.Cells‑namespace refereren en ervoor zorgen dat het sjabloonbestand bestaat.  

```csharp
using Aspose.Cells;

// Verify template existence (optional but helpful)
if (!System.IO.File.Exists("YOUR_DIRECTORY/template.xlsx"))
{
    throw new System.IO.FileNotFoundException("Template file not found. Ensure the path is correct.");
}
```

> **Pro tip:** Plaats je sjabloon in een `Resources`‑map en stel de eigenschap *Copy to Output Directory* van het bestand in op *Copy always*; zo werkt het pad zowel tijdens ontwikkeling als na publicatie.

## Bereid je gegevensbron voor (Excel maken vanuit een array)

Nu volgt het deel waarin we **excel maken vanuit een array**. De SmartMarkerProcessor verwacht een enumerable‑object, dus een eenvoudige anonieme type werkt prima.  

```csharp
// Step 2: Prepare the data source – an array of orders, each with an ID and a list of item names
var orderData = new[]
{
    new
    {
        OrderId = 1,
        OrderItems = new[]
        {
            new { ItemName = "Pen" },
            new { ItemName = "Paper" }
        }
    },
    new
    {
        OrderId = 2,
        OrderItems = new[]
        {
            new { ItemName = "Notebook" },
            new { ItemName = "Marker" },
            new { ItemName = "Eraser" }
        }
    }
};
```

Let op de geneste `OrderItems`‑array—dit weerspiegelt de `${OrderItems:ItemName}`‑marker in het sjabloon. De processor zal de rij voor elk item herhalen en automatisch de `ItemName`‑kolom invullen.

Als je al een `List<Order>` of een DataTable hebt, geef die dan gewoon door aan de processor; het belangrijkste is dat de eigenschapsnamen overeenkomen met de markers.

## Verwerk het sjabloon om Excel te vullen

Met het werkboek en de data klaar, instantieren we de `SmartMarkerProcessor` en laten we deze de data samenvoegen.  

```csharp
// Step 3: Create a SmartMarkerProcessor for the loaded workbook
var processor = new Aspose.Cells.SmartMarkerProcessor(workbook);

// Step 4: Populate the template by processing the Smart Markers with the data source
processor.Process(orderData);
```

Waarom `SmartMarkerProcessor` gebruiken? Het is sneller dan handmatig cel‑voor‑cel schrijven en respecteert Excel‑features zoals formules, samengevoegde cellen en voorwaardelijke opmaak. Bovendien breidt het automatisch rijen uit voor collecties—perfect voor **excel‑sjabloon vullen** scenario's.

## Sla het gegenereerde Excel‑rapport op

Tot slot schrijven we het gevulde werkboek naar schijf.  

```csharp
// Step 5: Save the populated workbook to a new file
string outputPath = "YOUR_DIRECTORY/output.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Excel report generated at: {outputPath}");
```

Na het uitvoeren van het programma, open `output.xlsx`. Je zou iets moeten zien als:

| OrderId | ItemName |
|---------|----------|
| 1       | Pen      |
| 1       | Paper    |
| 2       | Notebook |
| 2       | Marker   |
| 2       | Eraser   |

Dat is een volledig **gegenereerd excel‑rapport** gebouwd vanuit een in‑memory array, zonder dat je zelf loops hoeft te schrijven.

## Randgevallen en veelvoorkomende valkuilen

- **Lege collecties** – Als `OrderItems` leeg is voor een bepaalde order, slaan Smart Markers de rij simpelweg over. Als je een placeholder‑rij nodig hebt, voeg dan een conditionele marker toe zoals `${OrderItems?ItemName:"(no items)"}`.  
- **Grote datasets** – Voor duizenden rijen kun je overwegen de output te streamen (`workbook.Save(outputPath, SaveFormat.Xlsx)` is al geoptimaliseerd, maar je kunt ook `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` inschakelen).  
- **Sjabloon‑updates** – Wanneer je marker‑namen wijzigt, werk je de eigenschapsnamen van het anonieme type bij; anders negeert de processor de niet‑overeenkomende velden stilzwijgend.  
- **Datum‑/nummeropmaak** – De celopmaak van het sjabloon heeft voorrang. Als je cultuur‑specifieke opmaak nodig hebt, stel dan de `NumberFormat` van de cel in vóór verwerking.

## Volledig werkend voorbeeld (Klaar om te copy‑pasten)

Hieronder staat het complete programma dat je in een console‑app kunt plaatsen. Het bevat alle using‑statements, foutafhandeling en commentaren.

```csharp
using System;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load the Excel template that contains Smart Markers
            // -------------------------------------------------
            string templatePath = "YOUR_DIRECTORY/template.xlsx";
            if (!System.IO.File.Exists(templatePath))
            {
                Console.WriteLine("Template not found. Please place template.xlsx in the specified folder.");
                return;
            }

            var workbook = new Workbook(templatePath);

            // -------------------------------------------------
            // 2️⃣ Prepare the data source – create excel from array
            // -------------------------------------------------
            var orderData = new[]
            {
                new
                {
                    OrderId = 1,
                    OrderItems = new[]
                    {
                        new { ItemName = "Pen" },
                        new { ItemName = "Paper" }
                    }
                },
                new
                {
                    OrderId = 2,
                    OrderItems = new[]
                    {
                        new { ItemName = "Notebook" },
                        new { ItemName = "Marker" },
                        new { ItemName = "Eraser" }
                    }
                }
            };

            // -------------------------------------------------
            // 3️⃣ Process the template – populate excel template
            // -------------------------------------------------
            var processor = new SmartMarkerProcessor(workbook);
            processor.Process(orderData);

            // -------------------------------------------------
            // 4️⃣ Save the generated Excel report
            // -------------------------------------------------
            string outputPath = "YOUR_DIRECTORY/output.xlsx";
            workbook.Save(outputPath);
            Console.WriteLine($"✅ Export data to Excel completed. File saved at: {outputPath}");
        }
    }
}
```

Voer het programma uit, open `output.xlsx`, en je ziet de data netjes ingevuld. Dat is alles—je **export data to excel** workflow is nu volledig geautomatiseerd.

## Conclusie

We hebben zojuist een volledige oplossing doorlopen voor **export data to Excel** met een vooraf ontworpen sjabloon, een eenvoudige array als gegevensbron, en Aspose.Cells Smart Markers om **excel‑sjabloon automatisch te vullen**. In een handvol stappen kun je **excel‑sjabloon laden**, elke collectie omzetten in een gepolijst **excel‑rapport genereren**, en **excel maken vanuit een array** zonder low‑level celcode te schrijven.

Wat nu? Probeer het anonieme type te vervangen door een echte `Order`‑klasse, voeg complexere markers toe zoals `${OrderDate:MM/dd/yyyy}`, of integreer deze logica in een Web API die het bestand on‑demand retourneert. Hetzelfde patroon werkt voor facturen, voorraadbladen, of elke tabeloutput die je moet delen.

Heb je vragen of een lastig scenario? Laat een reactie achter, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}