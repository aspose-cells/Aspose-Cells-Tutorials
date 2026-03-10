---
category: general
date: 2026-02-15
description: Hoe valuta snel te formatteren met set column number format en een aangepast
  numeriek formaat toe te passen in C#. Leer een kolom op naam op te halen en de uitlijning
  van de gridkolom in te stellen.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: nl
og_description: hoe valuta te formatteren in een rasterkolom met C#. Deze tutorial
  laat zien hoe je een kolom op naam kunt ophalen, het getalformaat van de kolom kunt
  instellen, een aangepast numeriek formaat kunt toepassen en de uitlijning van de
  rasterkolom kunt instellen.
og_title: Hoe valuta te formatteren in een gridkolom – volledige gids
tags:
- C#
- GridFormatting
- UI
title: Hoe valuta te formatteren in een gridkolom – Stapsgewijze gids
url: /nl/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

formatting.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# hoe valuta te formatteren in een Grid‑kolom – Complete Programmeertutorial

Heb je je ooit afgevraagd **hoe je valuta moet formatteren** in een grid‑kolom zonder je haar uit te trekken? Je bent niet de enige. Als je naar een simpel getal kijkt zoals `1234.5` en je wilt dat het magisch verschijnt als `$1,234.50`, is het antwoord meestal slechts een paar regels configuratie.  

In deze gids gaan we **een kolom op naam ophalen**, **het getalformaat van de kolom instellen**, en **een aangepast numeriek formaat toepassen** dat de typische boekhoudkundige lay‑out respecteert. Onderweg zetten we ook **de uitlijning van de grid‑kolom** en voegen we een subtiele rand toe zodat de UI er gepolijst uitziet.

> **TL;DR** – Aan het einde heb je een kant‑klaar‑snippet dat ruwe decimalen omzet in prachtig geformatteerde valutawaarden binnen elk `GridJs`‑achtig controle‑element.

---

## Wat je nodig hebt

- Een .NET‑project (elke versie die C# 8.0+ ondersteunt – Visual Studio 2022 werkt uitstekend).  
- Een grid‑component die een `Columns`‑collectie blootlegt (het voorbeeld gebruikt een fictieve `GridJs`‑klasse, maar de concepten zijn toepasbaar op DevExpress, Telerik of Syncfusion grids).  
- Basiskennis van C#‑syntaxis – geen geavanceerde trucjes nodig.

Als je die al hebt, prima. Zo niet, maak dan een console‑app; de grid kan voor illustratie gemockt worden.

---

## Stapsgewijze implementatie

Onder elke stap zie je een compact code‑blok, een korte uitleg **waarom** de regel belangrijk is, en een tip om veelvoorkomende valkuilen te vermijden.

### ## Stap 1 – Haal de “Amount”‑kolom op op naam

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Waarom dit belangrijk is:**  
De meeste grid‑API’s bieden kolommen via een dictionary‑achtige indexer. De kolom ophalen op basis van de headernaam (`"Amount"`) stelt je in staat het uiterlijk te manipuleren zonder de onderliggende gegevensbron aan te raken.  

**Pro tip:** Bescherm altijd tegen een `null`‑terugkeer – een typefout in de kolomnaam of een dynamische schema‑wijziging kan anders een `NullReferenceException` veroorzaken tijdens runtime.

---

### ## Stap 2 – Stel het kolom‑getalformaat in met een aangepast valutamasker

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Waarom dit belangrijk is:**  
De opmaakstring volgt de accounting‑conventies van Excel:

- `_(* #,##0.00_)` → Positieve getallen, rechts‑uitgelijnd met een spatie vóór het valutateken.  
- `_(* (#,##0.00)` → Negatieve getallen tussen haakjes.  
- `_(* \"-\"??_)` → Nulwaarden weergegeven als een streepje.  
- `_(@_)` → Tekstwaarden blijven ongewijzigd.

Door **een aangepast numeriek formaat toe te passen** krijg je volledige controle over duizendtallen‑scheidingstekens, decimalen en de plaatsing van het valutateken.  

**Randgeval:** Als je applicatie een andere locale moet respecteren (bijv. Euro in plaats van USD), vervang dan de spatie door het juiste symbool of gebruik `CultureInfo`‑gevoelige opmaak in de gegevensbron.

---

### ## Stap 3 – Lijn de kolominhoud rechts uit voor leesbaarheid

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Waarom dit belangrijk is:**  
Valutawaarden zijn makkelijker te scannen wanneer ze op de decimale separator uitgelijnd staan. Het instellen van **set grid column alignment** op `Right` bootst de manier na waarop spreadsheets monetaire data weergeven.  

**Gotcha:** Sommige grids negeren uitlijning op cellen die aangepaste templates bevatten. Als je merkt dat de uitlijning niet werkt, controleer dan of de kolom geen aangepaste cel‑renderer gebruikt.

---

### ## Stap 4 – Voeg een dunne grijze rand toe rond de kolomcellen

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Waarom dit belangrijk is:**  
Een subtiele rand scheidt de “Amount”‑kolom van zijn buren, vooral wanneer de grid afwisselende rij‑kleuren heeft. Het is een visueel signaal dat de data een afzonderlijk financieel cijfer vertegenwoordigt.  

**Tip:** Als je een dikkere lijn nodig hebt voor afdrukken, verhoog `BorderLineStyle` naar `Medium` of wijzig `Color` naar `Color.Black`.

---

## Volledig werkend voorbeeld

Hier is het volledige snippet dat je in een WinForms‑ of WPF‑project kunt plaatsen dat een `GridJs`‑achtig controle‑element gebruikt. Het voorbeeld print ook de geformatteerde waarden naar de console zodat je de output kunt verifiëren zonder UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Verwachte console‑output**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Let op hoe het positieve getal rechts‑uitgelijnd is, het negatieve getal tussen haakjes staat, en nul een streepje toont – precies wat de aangepaste opmaakstring bepaalt.

---

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|----------|--------|
| *Wat als de grid een andere cultuur gebruikt (bijv. € in plaats van $)?* | Vervang de spatie in de opmaakstring door het gewenste symbool of laat de gegevensbron een vooraf geformatteerde string genereren met `CultureInfo.CurrentCulture`. |
| *Kan ik hetzelfde formaat hergebruiken voor meerdere kolommen?* | Absoluut. Bewaar de opmaakstring in een constante (`const string CurrencyMask = "...";`) en wijs deze toe waar je valuta nodig hebt. |
| *Wat gebeurt er als de kolom een string‑waarde bevat?* | De opmaakstring beïnvloedt alleen numerieke types. Strings worden onveranderd doorgegeven, wat de reden is dat het laatste deel van het masker (`_(@_)`) bestaat – het behoudt niet‑numerieke inhoud. |
| *Is er een prestatie‑impact?* | Verwaarloosbaar. Het formaat wordt toegepast tijdens het renderen, niet tijdens het ophalen van data. Tenzij je duizenden rijen per frame rendert, zul je geen merkbare vertraging merken. |
| *Hoe maak ik de rand dikker voor afgedrukte rapporten?* | Vervang `BorderLineStyle.Thin` door `BorderLineStyle.Medium` of `BorderLineStyle.Thick`. Sommige bibliotheken laten je ook een pixel‑breedte direct specificeren. |

---

## Afsluiting

We hebben stap voor stap **hoe je valuta formatteert** in een grid‑kolom behandeld: de kolom op naam ophalen, het getalformaat instellen, een aangepast numeriek formaat toepassen, de cellen uitlijnen en een smaakvolle rand toevoegen. Het volledige voorbeeld werkt direct en laat het exacte visuele resultaat zien dat je kunt verwachten.

Als je klaar bent om verder te gaan, probeer dan:

- **Dynamische culturen** – wissel de opmaakstring op basis van de locale van de gebruiker.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}