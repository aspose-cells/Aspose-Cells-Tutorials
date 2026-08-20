---
category: general
date: 2026-02-14
description: 'Automatiseer het genereren van facturen met SmartMarker: leer hoe je
  werkbladen kunt herhalen, ze dynamisch kunt benoemen en binnen enkele minuten meester
  wordt in dynamische werkbladnaamgeving.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: nl
og_description: Automatiseer factuurgeneratie met SmartMarker. Deze gids laat zien
  hoe je werkbladen kunt herhalen, ze dynamisch kunt benoemen en dynamische werkbladbenamingen
  onder de knie krijgt.
og_title: Factuurgeneratie automatiseren – Dynamische werkbladnaamgeving & herhaling
tags:
- C#
- SmartMarker
- Excel Automation
title: Factuurgeneratie automatiseren – Dynamische werkbladnaamgeving en herhaling
  in C#
url: /nl/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Factuurgeneratie automatiseren – Dynamische werkbladnaamgeving & herhalen in C#

Heb je je ooit afgevraagd hoe je **factuurgeneratie kunt automatiseren** zonder handmatig werkbladen te kopiëren voor elke bestelling? Je bent niet de enige. Veel ontwikkelaars lopen tegen een muur wanneer ze een apart werkblad per factuur nodig hebben, maar ook willen dat de bladnaam het ordernummer weergeeft. In deze tutorial lossen we dat probleem op met SmartMarker’s `SmartMarkerProcessor` en laten we je zien **hoe je werkbladen dynamisch kunt benoemen** terwijl we ook behandelen **hoe je een werkblad kunt herhalen** voor elk record. Aan het einde heb je een kant‑klaar C#‑voorbeeld dat een werkmap produceert waarin elke factuur op een eigen, mooi benoemde tab staat.

We lopen elke stap door – van het ophalen van bestellingen uit een gegevensbron tot het configureren van `SmartMarkerOptions` voor dynamische werkbladnaamgeving. Geen externe documentatie nodig; alles wat je nodig hebt staat hier. Een beetje voorkennis van C# en een verwijzing naar de Aspose.Cells‑bibliotheek (of een andere SmartMarker‑compatibele engine) is voldoende.

---

## Wat je gaat bouwen

- Een collectie orderobjecten ophalen.
- SmartMarker configureren om **een werkblad te herhalen** voor elke order.
- **Dynamische werkbladnaamgeving** toepassen met de `{OrderId}`‑placeholder.
- Een Excel‑bestand genereren waarbij elke tab `Invoice_12345`, `Invoice_67890`, enz. heet.
- De output verifiëren door de werkmap te openen.

---

## Vereisten

- .NET 6.0 of later (de code compileert ook met .NET 5+).
- Aspose.Cells for .NET (of een bibliotheek die SmartMarker implementeert). Installeer via NuGet:

```bash
dotnet add package Aspose.Cells
```

- Een eenvoudige `Order`‑klasse (je kunt deze vervangen door je eigen DTO).

---

## Stap 1: Het project en model opzetten

Maak eerst een nieuwe console‑app en definieer het datamodel dat een order vertegenwoordigt.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Pro tip:** Houd het model lichtgewicht voor de demo; je kunt later altijd regels, belastingdetails, enz. toevoegen.

---

## Stap 2: Het Excel‑sjabloon voorbereiden

SmartMarker werkt tegen een sjabloon‑werkmap. Maak een bestand genaamd `InvoiceTemplate.xlsx` met één werkblad genaamd `InvoiceTemplate`. Plaats in cel **A1** een SmartMarker‑placeholder zoals:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Je kunt de cellen op elke gewenste manier opmaken – vette koppen, valuta‑opmaak, enz. Sla het bestand op in de hoofdmap van het project.

> **Waarom een sjabloon?** Het scheidt de lay‑out van de code, zodat ontwerpers het uiterlijk kunnen aanpassen zonder de logica aan te raken.

---

## Stap 3: SmartMarker‑opties configureren – Werkblad herhalen & benoemen

Nu vertellen we SmartMarker om *het* sjabloon‑werkblad te *herhalen* voor elke order en elke kopie een naam te geven die het order‑ID bevat. Dit is de kern van **dynamische werkbladnaamgeving**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Hoe het werkt

- **`RepeatWorksheet = true`** vertelt de engine om het bronblad te dupliceren voor elk element in de `orders`‑collectie. Dit voldoet aan de **hoe je een werkblad herhaalt**‑vereiste.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** is een sjabloon‑string waarbij `{OrderId}` een placeholder is die SmartMarker vervangt door het huidige order‑ID. Dat is het antwoord op **hoe je werkbladen benoemt** en **dynamische werkbladnaamgeving**.
- De processor voegt de velden van elke order (`{{OrderId}}`, `{{Customer}}`, enz.) samen in het gedupliceerde blad, waardoor een volledig ingevulde factuur ontstaat.

---

## Stap 4: De applicatie uitvoeren en output verifiëren

Compileer en voer de console‑app uit:

```bash
dotnet run
```

Je zou een succesbericht in de console moeten zien. Open `GeneratedInvoices.xlsx` en je vindt drie tabbladen:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Elk blad bevat de ordergegevens die in de placeholders zijn ingevoegd. De lay‑out die je in het sjabloon hebt ontworpen blijft behouden, wat bewijst dat **factuurgeneratie automatiseren** end‑to‑end werkt.

### Verwachte screenshot (alt‑tekst voor SEO)

![voorbeeld van geautomatiseerde factuurgeneratie met drie dynamisch benoemde werkbladen](/images/invoice-automation.png)

> *De alt‑tekst van de afbeelding bevat het belangrijkste trefwoord om te voldoen aan SEO.*

---

## Stap 5: Randgevallen & Veelvoorkomende variaties

### Wat als een OrderId ongeldige tekens bevat?

Excel‑bladnamen mogen geen `\ / ? * [ ] :` bevatten. Als je ID’s die tekens kunnen bevatten, reinig ze dan:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Voeg een berekende eigenschap toe aan `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Het originele sjabloonblad behouden?

Stel `smartMarkerOptions.RemoveTemplate = false;` in (standaard is `true`). Hierdoor blijft `InvoiceTemplate` onaangeroerd als referentie.

### Facturen per klant groeperen?

Je kunt **herhaal‑groepen** nesten. Eerst per klant herhalen, daarna per order binnen elk klant‑werkblad. De syntaxis wordt iets complexer, maar het principe blijft hetzelfde – gebruik `RepeatWorksheet` en een naamgevingspatroon dat de hiërarchie weerspiegelt.

---

## Volledig werkend voorbeeld (Alle code op één plek)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Kopieer‑en‑plak dit in `Program.cs`, plaats `InvoiceTemplate.xlsx` ernaast, en je bent klaar om te gaan.

---

## Veelgestelde vragen

**V: Werkt deze aanpak met grote datasets (duizenden facturen)?**  
A: Ja. SmartMarker streamt gegevens efficiënt, maar houd het geheugenverbruik in de gaten. Als je limieten bereikt, overweeg dan om in batches te verwerken en elke batch naar een aparte werkmap te schrijven.

**V: Kan ik automatisch een logo aan elke factuur toevoegen?**  
A: Absoluut. Plaats de logo‑afbeelding op het sjabloonblad. Omdat het blad wordt gedupliceerd, verschijnt het logo op elke gegenereerde factuur zonder extra code.

**V: Wat als ik de werkbladen wil beveiligen?**  
A: Na het verwerken kun je door `wb.Worksheets` itereren en `ws.Protect(Password, ProtectionType.All)` aanroepen.

---

## Conclusie

We hebben zojuist **factuurgeneratie geautomatiseerd** door gebruik te maken van SmartMarker’s herhaal‑werkblad‑functie en een slimme naamgevingspatroon. De tutorial behandelde **hoe je werkbladen benoemt**, toonde **hoe je een werkblad herhaalt** voor elke order, en liet **dynamische werkbladnaamgeving** zien die je werkmap netjes en doorzoekbaar houdt.

Van het ophalen van data, het opzetten van een sjabloon, het configureren van `SmartMarkerOptions`, tot het afhandelen van randgevallen – je beschikt nu over een complete, uitvoerbare oplossing. Probeer nu lijn‑item‑tabellen toe te voegen, voorwaardelijke opmaak toe te passen, of dezelfde data naar PDF te exporteren voor een volledig geautomatiseerde facturatie‑pipeline.

Klaar om een stap hoger te gaan? Verken gerelateerde onderwerpen zoals “bulk Excel‑export met Aspose.Cells”, “PDF‑conversie van werkbladen”, of “facturen direct vanuit C# e‑mailen”. De mogelijkheden zijn eindeloos – happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}