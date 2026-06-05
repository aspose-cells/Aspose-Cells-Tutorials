---
category: general
date: 2026-06-05
description: Schakel de optie voor geneste bereiken in Aspose.Cells SmartMarkerProcessor
  in om hiërarchische Excel‑gegevens moeiteloos te verwerken. Leer over smart markers,
  geneste bereiken en best practices.
draft: false
keywords:
- enable nested range option
- SmartMarkerProcessor
- nested range handling
- Excel smart markers
- Aspose.Cells
language: nl
og_description: Schakel de geneste bereikoptie in Aspose.Cells SmartMarkerProcessor
  in om met hiërarchische gegevens te werken. Complete gids met code, tips en valkuilen.
og_title: Geneste bereikoptie inschakelen in Aspose.Cells SmartMarker
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Enable nested range option in Aspose.Cells SmartMarkerProcessor to
    handle hierarchical Excel data effortlessly. Learn smart markers, nested ranges,
    and best practices.
  headline: Enable Nested Range Option in Aspose.Cells SmartMarker
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Smart Markers
title: Geneste bereikoptie inschakelen in Aspose.Cells SmartMarker
url: /nl/net/smart-markers-dynamic-data/enable-nested-range-option-in-aspose-cells-smartmarker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enable Nested Range Option in Aspose.Cells SmartMarker

Heb je je ooit afgevraagd hoe je de **nested range option** kunt **inschakelen** in Aspose.Cells SmartMarkerProcessor? Het inschakelen van deze functie stelt je in staat om met hiërarchische gegevens zoals bestellingen en regelitems te werken zonder problemen.  

In deze tutorial lopen we een real‑world scenario door: een bestellijst met geneste items voeden in een Excel‑sjabloon met behulp van smart markers. Aan het einde heb je een volledig functionele werkmap, begrijp je **SmartMarkerProcessor**, en weet je waarom de **nested range handling**‑vlag belangrijk is.

We behandelen:

* Het voorbereiden van een C# anoniem object dat master‑detail data nabootst.  
* Het inschakelen van de **nested range**‑vlag op de processor.  
* Het uitvoeren van de processor op een werkmap en het verifiëren van het resultaat.  

Geen fancy frameworks nodig—alleen .NET 6+ en de Aspose.Cells for .NET bibliotheek. Als je ooit moeite hebt gehad met rijen die zich herhalen binnen andere herhalende rijen, is deze gids voor jou.

---

## Prepare Hierarchical Data for Excel Smart Markers

Eerst hebben we een gegevensbron nodig die een ouder‑kindrelatie weerspiegelt. Het voorbeeld hieronder maakt een anoniem object met één bestelling die twee items bevat.

```csharp
// Step 1: Define hierarchical data with orders and their items
var orderData = new
{
    Orders = new[]
    {
        new
        {
            Id = 1,
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        }
    }
};
```

**Waarom deze structuur?**  
Smart markers lezen de eigenschapsnamen (`Orders`, `Items`) en genereren automatisch geneste bereiken wanneer de processor correct is geconfigureerd. Beschouw het als een mini‑database waar het Excel‑sjabloon overheen itereren zal.

> **Pro tip:** Gebruik betekenisvolle eigenschapsnamen die overeenkomen met de markers die je in het sjabloon hebt geplaatst (bijv. `&=Orders.Id&`, `&=Items.Name&`). Niet‑overeenkomende namen zijn een veelvoorkomende oorzaak van “no data”‑fouten.

---

## Configure SmartMarkerProcessor and Enable Nested Range

Nu maken we de processor aan en zetten we de **NestedRange**‑schakelaar om. Deze ene regel vertelt Aspose.Cells om kindcollecties te behandelen als innerlijke tabellen.

```csharp
// Step 2: Create a SmartMarkerProcessor and enable nested range handling
SmartMarkerProcessor processor = new SmartMarkerProcessor();
processor.Options.NestedRange = true;   // <‑‑ enable nested range option
```

**Wat doet `NestedRange = true` eigenlijk?**  
Wanneer ingesteld, bouwt de processor een apart bereik voor elke kindcollectie en nestelt dit binnen het ouder‑bereik. Zonder deze instelling zou alleen de bovenliggende collectie (`Orders`) worden gerenderd, en zouden de innerlijke `Items`‑rijen worden genegeerd.

> **Let op:** Als je geneste bereiken inschakelt maar vergeet het kind‑bereik in het sjabloon te markeren (met `&=Items.Start&` / `&=Items.End&`), zal de processor een `SmartMarkerException` gooien. Controleer altijd je marker‑syntaxis dubbel.

---

## Load or Create the Workbook Template

Voor de demo genereren we een eenvoudige werkmap on‑the‑fly, maar in productie begin je meestal met een bestaand `.xlsx`‑bestand dat al smart markers bevat.

```csharp
// Step 3: Create a workbook with a simple template
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Header row
ws.Cells["A1"].PutValue("Order ID");
ws.Cells["B1"].PutValue("Item Name");

// Smart marker row for Orders (parent)
//   &amp;=Orders.Start&amp; and &amp;=Orders.End&amp; define the range for each order.
ws.Cells["A2"].PutValue("&=Orders.Start&");
ws.Cells["A2"].PutValue("&=Orders.Id&");
ws.Cells["B2"].PutValue("&=Orders.End&");

// Smart marker row for Items (child)
//   Nested inside the Orders range.
ws.Cells["A3"].PutValue("&=Items.Start&");
ws.Cells["A3"].PutValue("&=Items.Name&");
ws.Cells["B3"].PutValue("&=Items.End&");
```

Let op de `&=Orders.Start&` / `&=Orders.End&`‑markers—deze geven de processor aan waar elk bestelblok begint en eindigt. Hetzelfde patroon geldt voor het kind‑`Items`‑bereik.

---

## Process Workbook with Smart Markers

Met gegevens en processor klaar, is de laatste stap een één‑regel die alles samenvoegt.

```csharp
// Step 4: Apply the data to the workbook using smart markers
processor.Process(wb, orderData);
```

Na deze aanroep zal de werkmap bevatten:

| Order ID | Item Name |
|----------|-----------|
| 1        | A         |
| 1        | B         |

Je kunt het resultaat opslaan op schijf of terugsturen als stream naar een client:

```csharp
wb.Save("NestedRangeResult.xlsx");
```

---

## Verify Output and Handle Common Pitfalls

### Expected Result

Open `NestedRangeResult.xlsx` en je zou twee rijen onder de enkele bestellingskop moeten zien, elk met de itemnaam (`A` en `B`). De order‑ID wordt herhaald voor elke kind‑rij—precies wat geneste bereiken moeten doen.

### Typical Issues

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| No child rows appear | `NestedRange` left as `false` | Set `processor.Options.NestedRange = true`. |
| Markers show up as plain text | Marker syntax typo (`&=Orders.Start&` vs `&=Orders.Start`) | Ensure both `&=` and trailing `&` are present. |
| Duplicate rows for each order | Missing `&=Orders.End&` marker | Add the closing marker to bound the parent range. |

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Define hierarchical data
        var orderData = new
        {
            Orders = new[]
            {
                new
                {
                    Id = 1,
                    Items = new[]
                    {
                        new { Name = "A" },
                        new { Name = "B" }
                    }
                }
            }
        };

        // 2️⃣ Create processor and enable nested range option
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Options.NestedRange = true;   // enable nested range option

        // 3️⃣ Build a simple workbook template with smart markers
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("Order ID");
        ws.Cells["B1"].PutValue("Item Name");

        // Parent range markers
        ws.Cells["A2"].PutValue("&=Orders.Start&");
        ws.Cells["A2"].PutValue("&=Orders.Id&");
        ws.Cells["B2"].PutValue("&=Orders.End&");

        // Child range markers (nested)
        ws.Cells["A3"].PutValue("&=Items.Start&");
        ws.Cells["A3"].PutValue("&=Items.Name&");
        ws.Cells["B3"].PutValue("&=Items.End&");

        // 4️⃣ Process the workbook
        processor.Process(wb, orderData);

        // 5️⃣ Save the result
        wb.Save("NestedRangeResult.xlsx");
        Console.WriteLine("Workbook generated – check NestedRangeResult.xlsx");
    }
}
```

Voer het programma uit, open het gegenereerde bestand, en je zult de geneste rijen precies zoals in de tabel hierboven ingevuld zien.

---

## Conclusion

Je hebt zojuist geleerd hoe je de **nested range option** kunt **inschakelen** in Aspose.Cells SmartMarkerProcessor, waardoor een platte Excel‑sjabloon wordt omgevormd tot een krachtige master‑detail rapportgenerator. Door `processor.Options.NestedRange = true` in te stellen, maakt de bibliotheek automatisch innerlijke tabellen voor kindcollecties, waardoor je handmatige rij‑invoerlussen bespaart.

Wat nu? Probeer een tweede niveau van nesting toe te voegen (bijv. order → items → sub‑components), experimenteer met het stylen van de gegenereerde rijen, of schakel over naar een vooraf ontworpen sjabloon dat grafieken en formules bevat. De **Excel smart markers** en **nested range handling**‑combinatie vormt een solide basis voor elke geautomatiseerde rapportageoplossing.

Heb je vragen of een lastig scenario? Laat een reactie achter hieronder, en happy coding!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Handle Nested Objects with Smart Markers Aspose.Cells](/cells/english/net/smart-markers-dynamic-data/nested-objects-smart-markers/)
- [Populate Excel with Nested Data Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)
- [Populate Excel Nested Data Aspose Cells Java](/cells/german/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}