---
category: general
date: 2026-02-28
description: Maak een master‑detailrapport in C# en leer hoe je een Excel‑sjabloon
  kunt vullen, gegevens kunt samenvoegen in Excel en een Excel‑werkmap kunt laden
  in C# in slechts een paar stappen.
draft: false
keywords:
- create master detail report
- populate excel template
- merge data into excel
- load excel workbook c#
- how to create master detail
language: nl
og_description: Maak een master‑detailrapport in C# met Aspose.Cells SmartMarker.
  Leer hoe je een Excel‑werkmap in C# laadt, gegevens samenvoegt in Excel en een Excel‑sjabloon
  invult.
og_title: Maak master‑detailrapport in C# – Vul Excel‑sjabloon in
tags:
- C#
- Aspose.Cells
- Excel automation
- SmartMarker
title: Maak master‑detailrapport in C# – Populeer Excel‑sjabloon met SmartMarker
url: /nl/net/smart-markers-dynamic-data/create-master-detail-report-in-c-populate-excel-template-wit/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak master‑detailrapport in C# – Populeer Excel‑sjabloon met SmartMarker

Heb je ooit een **master‑detailrapport** in C# moeten maken, maar wist je niet hoe je de gegevens in een Excel‑bestand krijgt? Je bent niet de enige. In deze gids lopen we de exacte stappen door om **Excel‑sjabloon te vullen**, **gegevens in Excel te combineren**, en **Excel‑werkmap te laden in C#‑stijl**, zodat je eindigt met een gepolijst master‑detailrapport klaar voor distributie.

We gebruiken Aspose.Cells SmartMarker, een krachtige engine die master‑detailrelaties direct begrijpt. Aan het einde van de tutorial heb je een volledig, uitvoerbaar voorbeeld dat je in elk .NET‑project kunt plaatsen. Geen vage “zie de docs” shortcuts—maar een zelfstandige oplossing die je kunt copy‑paste en uitvoeren.

## Wat je zult leren

- Hoe je **master‑detail**‑datastructuren in C# maakt die direct op een Excel‑sjabloon aansluiten.
- De exacte manier om **Excel‑werkmap te laden in C#** code die een `.xlsx`‑bestand opent met SmartMarker‑tags.
- Het proces om **Excel‑sjabloon te vullen** door `SmartMarkerProcessor` uit te voeren.
- Tips voor het omgaan met randgevallen, zoals ontbrekende tags of grote datasets.
- Hoe je het resultaat verifieert en hoe het uiteindelijke **master‑detailrapport** eruitziet.

### Vereisten

- .NET 6.0 of later (de code werkt ook op .NET Framework 4.8).
- Aspose.Cells voor .NET (je kunt een gratis proef‑NuGet‑pakket pakken: `Install-Package Aspose.Cells`).
- Een basis‑Excel‑bestand (`template.xlsx`) dat SmartMarker‑tags bevat (we laten de minimale markup zien die je nodig hebt).

Als je deze klaar hebt, laten we erin duiken.

## Stap 1 – Maak de master‑detail gegevensbron *(hoe master‑detail te maken)*

Het eerste wat je nodig hebt, is een C#‑object dat de master‑rijen (orders) en hun onderliggende rijen (orderitems) vertegenwoordigt. SmartMarker leest deze hiërarchie automatisch wanneer `MasterDetail` op `true` is gezet.

```csharp
using System;

// Step 1: Build the master‑detail data object
var orderData = new
{
    // Master collection – each order is a row in the master table
    Orders = new[]
    {
        new
        {
            Id = 1,
            // Detail collection – items belonging to order 1
            Items = new[] { new { Sku = 101, Qty = 2 }, new { Sku = 102, Qty = 1 } }
        },
        new
        {
            Id = 2,
            Items = new[] { new { Sku = 202, Qty = 1 } }
        }
    }
};
```

**Waarom dit belangrijk is:**  
SmartMarker zoekt naar een eigenschap met de naam `Orders` (de master) en vervolgens zoekt het voor elke order naar een collectie genaamd `Items`. Door die namen te laten overeenkomen krijg je automatisch een **master‑detailrapport** zonder zelf loops te schrijven.

> **Pro tip:** Houd de eigenschapsnamen kort en betekenisvol; ze worden de placeholders in je Excel‑sjabloon.

## Stap 2 – Configureer SmartMarker‑opties voor master‑detail verwerking

Vertel de engine dat je een master‑detail scenario behandelt en geef het de naam van het detailblad dat de onderliggende rijen zal ontvangen.

```csharp
using Aspose.Cells;

// Step 2: Set up SmartMarker options
SmartMarkerOptions options = new SmartMarkerOptions
{
    // Enables master‑detail processing
    MasterDetail = true,
    // The sheet in the template that holds the detail rows
    DetailSheetName = "OrderDetail"
};
```

**Waarom dit belangrijk is:**  
Als je `MasterDetail = true` weglaat, zal SmartMarker de data als een platte lijst behandelen en zullen de detailrijen nooit verschijnen. `DetailSheetName` moet overeenkomen met de bladnaam die je in het sjabloon hebt aangemaakt (hoofdlettergevoelig).

## Stap 3 – Laad de Excel‑werkmap in C#‑stijl

Nu openen we het sjabloon dat de SmartMarker‑tags bevat. Dit is de **load Excel workbook C#** stap waar veel ontwikkelaars over struikelen omdat ze de juiste bestands‑pad vergeten of de werkmap niet correct vrijgeven.

```csharp
using System.IO;

// Step 3: Load the workbook that holds the SmartMarker tags
string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
Workbook workbook = new Workbook(templatePath);
```

**Waarom dit belangrijk is:**  
Aspose.Cells leest de volledige werkmap in het geheugen, dus het bestand kan op schijf staan, ingebed zijn als resource, of zelfs gestreamd worden vanuit een webservice. Zorg er alleen voor dat het pad naar een geldig `.xlsx`‑bestand wijst dat de tags bevat die we straks bespreken.

## Stap 4 – Voeg SmartMarker‑tags toe aan het sjabloon (populate Excel template)

Als je nu `template.xlsx` opent, zie je twee bladen:

- **Orders** – het master‑blad met een rij zoals `&=Orders.Id`.
- **OrderDetail** – het detail‑blad met rijen zoals `&=Items.Sku` en `&=Items.Qty`.

Hier is een minimale weergave van de markup:

| Blad | Cel A1 | Cel B1 |
|-------|---------|---------|
| Orders | `&=Orders.Id` | *(empty)* |
| OrderDetail | `&=Items.Sku` | `&=Items.Qty` |

Je hoeft geen code te schrijven voor de tags—ze staan in het Excel‑bestand. De **populate Excel template** stap is simpelweg het aanroepen van de processor:

```csharp
// Step 4: Run SmartMarker to merge data into Excel
new SmartMarkerProcessor().Process(workbook, orderData, options);
```

**Waarom dit belangrijk is:**  
De processor scant elk blad, vervangt de `&=` placeholders door echte waarden, en breidt rijen uit voor elk master‑ en detailrecord. Omdat `MasterDetail` is ingeschakeld, maakt het automatisch een nieuwe rij voor elk item onder de juiste order.

## Stap 5 – Sla het master‑detailrapport op

Tot slot schrijf je de gevulde werkmap naar schijf. Dit is het moment waarop je een kant‑klaar **master‑detailrapport** krijgt.

```csharp
// Step 5: Save the populated workbook
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);

// Optional: open the file automatically (Windows only)
System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo
{
    FileName = outputPath,
    UseShellExecute = true
});
```

**Verwachte output:**  

- **Orders** blad toont twee rijen: `1` en `2` (order‑ID’s).  
- **OrderDetail** blad toont drie rijen:  
  - SKU 101 Qty 2  
  - SKU 102 Qty 1  
  - SKU 202 Qty 1  

Dat is een volledig functioneel **create master detail report** dat je kunt e‑mailen, afdrukken, of in een ander systeem kunt voeren.

## Randgevallen & veelgestelde vragen

### Wat als het sjabloon een tag mist?

SmartMarker negeert onbekende tags stilletjes, maar je krijgt lege cellen. Controleer de tag‑spelling dubbel en zorg ervoor dat de eigenschapsnamen in je C#‑object exact overeenkomen.

### Hoe gaat het om met grote datasets?

De processor streamt rijen, dus zelfs duizenden detailrecords zullen het geheugen niet overbelasten. Voor extreem grote bestanden wil je echter misschien de `MemorySetting` in `LoadOptions` verhogen.

```csharp
var loadOptions = new LoadOptions(LoadFormat.Xlsx)
{
    MemorySetting = MemorySetting.MemoryPreference
};
Workbook largeWorkbook = new Workbook(templatePath, loadOptions);
```

### Kan ik een andere bladnaam gebruiken voor de master?

Ja—hernoem gewoon het blad in het sjabloon en pas `DetailSheetName` aan als je een detailblad hebt. De master‑bladnaam wordt afgeleid van de placeholder (`&=Orders.Id`).

### Wat als ik een totalen‑rij moet toevoegen?

Voeg een reguliere Excel‑formule toe in het sjabloon (bijv. `=SUM(B2:B{#})`). SmartMarker behoudt de formule na het invoegen van data.

## Volledig uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt copy‑paste in een console‑applicatie. Het bevat alle `using`‑directives, het datamodel, de opties en bestandsafhandeling.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace MasterDetailReportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Create master‑detail data ----------
            var orderData = new
            {
                Orders = new[]
                {
                    new
                    {
                        Id = 1,
                        Items = new[]
                        {
                            new { Sku = 101, Qty = 2 },
                            new { Sku = 102, Qty = 1 }
                        }
                    },
                    new
                    {
                        Id = 2,
                        Items = new[]
                        {
                            new { Sku = 202, Qty = 1 }
                        }
                    }
                }
            };

            // ---------- Step 2: SmartMarker options ----------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                MasterDetail = true,
                DetailSheetName = "OrderDetail"
            };

            // ---------- Step 3: Load the template ----------
            string templatePath = Path.Combine(Environment.CurrentDirectory, "template.xlsx");
            Workbook workbook = new Workbook(templatePath);

            // ---------- Step 4: Process the template ----------
            new SmartMarkerProcessor().Process(workbook, orderData, options);

            // ---------- Step 5: Save the result ----------
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Master detail report generated at: {outputPath}");
        }
    }
}
```

Voer het programma uit, open `output.xlsx`, en je ziet de master‑detaildata prachtig ingevuld.

## Visuele referentie

![Screenshot van master‑detailrapport uitvoer](https://example.com/images/master-detail-report.png "Voorbeeld van master‑detailrapport")

*De afbeelding toont het Orders‑blad met ID’s 1 en 2, en het OrderDetail‑blad met de drie SKU‑Qty‑rijen.*

## Conclusie

Je weet nu **hoe je een master‑detailrapport maakt** in C# met Aspose.Cells SmartMarker, van het bouwen van de gegevensbron tot **loading Excel workbook C#**, **populating Excel template**, en uiteindelijk

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}