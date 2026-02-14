---
category: general
date: 2026-02-14
description: Maak snel een kortingssjabloon en leer hoe je korting toepast in een
  spreadsheet, gegevens in het sjabloon injecteert en een variabel voorvoegsel definieert
  voor slimme markers.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: nl
og_description: Maak een kortingssjabloon met C#. Leer hoe je korting toepast in een
  spreadsheet, gegevens in het sjabloon injecteert, en een variabel voorvoegsel definieert
  voor slimme markers.
og_title: Maak kortingssjabloon – Volledige C#‑handleiding
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Maak kortingssjabloon in C# – Stapsgewijze handleiding
url: /nl/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

Make sure we didn't translate any code block placeholders or shortcodes.

Now produce final output with all translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Kortingssjabloon – Volledige C# Uitleg

Heb je ooit een **create discount template** nodig gehad voor een verkooprapport, maar wist je niet hoe je de cijfers automatisch in een spreadsheet kon invoeren? Je bent niet de enige. In deze tutorial laten we je precies zien hoe je **create discount template**, vervolgens **apply discount in spreadsheet** cellen, **inject data into template**, en zelfs **define variable prefix** voor je smart markers—alles met nette C# code.

We beginnen met het schetsen van het probleem, en springen dan direct naar een werkende oplossing die je kunt copy‑paste. Aan het einde heb je een herbruikbaar patroon dat werkt, of je nu facturen, prijslijsten, of een willekeurige spreadsheet genereert die dynamische kortingen nodig heeft.

---

## Wat je zult leren

- Hoe je een korting‑bewust spreadsheet‑sjabloon ontwerpt.
- Hoe je een aangepaste `VariablePrefix` / `VariableSuffix` configureert zodat markers gemakkelijk te vinden zijn.
- Hoe je een anoniem object (`discountData`) doorgeeft aan de `SmartMarkerProcessor`.
- Hoe de resulterende formule (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) automatisch de eindprijs berekent.
- Tips voor het omgaan met randgevallen zoals nul‑kortingsrijen of meerdere kortingsniveaus.

**Prerequisites** – een recente .NET runtime (≥ .NET 6), een referentie naar de `Aspose.Cells` (of een vergelijkbare) bibliotheek die `SmartMarkerProcessor` levert, en een basisbegrip van C#-syntaxis. Niets exotisch.

---

## Stap 1: Maak een kortingssjabloon in je spreadsheet

Open eerst een nieuw werkboek (of gebruik een bestaand) en plaats een tijdelijke aanduiding waar de korting wordt toegepast. Beschouw het sjabloon als een eenvoudig Excel‑bestand met “smart markers” die door de processor worden vervangen.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** Door `#Discount#` in de formule te embedden, vertellen we de processor precies waar de kortingswaarde moet komen. De `SmartMarkerProcessor` zal `#Discount#` vervangen door het getal dat je later opgeeft, terwijl de rest van de formule onaangeroerd blijft.

---

## Stap 2: Definieer variabele prefix voor Smart Markers

Standaard zoeken veel bibliotheken naar `${Variable}` of `{{Variable}}`. In ons geval willen we een nette, menselijk leesbare marker, dus **define variable prefix** en suffix expliciet.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Het gebruik van `#` houdt de markers kort en gemakkelijk te vinden in de formulebalk van Excel. Als je ooit conflicten met bestaande Excel‑functies wilt vermijden, kies dan een ander paar (bijv. `[[` en `]]`).

---

## Stap 3: Voeg gegevens toe aan sjabloon met SmartMarkerProcessor

Nu voeren we de daadwerkelijke kortingswaarde in. De processor scant het werkblad, vindt elke `#Discount#`, en vervangt deze door de waarde uit het anonieme object dat we doorgeven.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Na deze aanroep wordt de formule in `B2`

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Wanneer het werkboek berekent, toont `B2` **90**, d.w.z. een korting van 10 % toegepast op de oorspronkelijke prijs van 100.

**Why it works:** `StartSmartMarkerProcessing` doorloopt elke cel, zoekt naar het `#Discount#`‑token, en vervangt het door de numerieke waarde. Omdat het token zich binnen een `IF`‑statement bevindt, behandelt de spreadsheet nog steeds gevallen waarin de korting nul kan zijn.

---

## Stap 4: Pas korting toe in spreadsheet – Verifieer het resultaat

Laten we de berekening activeren en de eindprijs naar de console outputten. Deze stap bewijst dat de **apply discount in spreadsheet** workflow geslaagd is.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Verwachte output**

```
Original: 100
Discounted (10%): 90
```

Als je `discountData.Discount` verandert naar `0.25` en de processor opnieuw uitvoert, zal de output automatisch een korting van 25 % weergeven—geen extra code nodig.

---

## Stap 5: Randgevallen en meerdere kortingen afhandelen

### Nul‑kortingsrijen

Soms is een product niet in de uitverkoop. Om de formule robuust te houden, dekt de `IF` die je eerder plaatste dit scenario al: wanneer `#Discount#` `0` is, wordt de oorspronkelijke prijs ongewijzigd doorgegeven.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Meerdere kortingskolommen

Als je per rij afzonderlijke kortingen nodig hebt, geef elke rij zijn eigen marker, bv. `#Discount1#`, `#Discount2#`, en geef een collectie door:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

De processor matcht markers opeenvolgend, zodat elke rij de juiste waarde krijgt.

---

## Volledig werkend voorbeeld

Hieronder staat het volledige, kant‑klaar programma dat elke stap hierboven bevat. Sla het op als `Program.cs`, voeg een referentie toe aan `Aspose.Cells`, en voer uit.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Het uitvoeren hiervan print de verwachte getallen en maakt een `DiscountedPricing.xlsx`‑bestand aan dat je in Excel kunt openen om de formule al opgelost te zien.

---

## Conclusie

Je weet nu hoe je **create discount template**, **apply discount in spreadsheet**, **inject data into template**, en **define variable prefix** voor smart markers kunt gebruiken—alles met een handvol beknopte C#‑regels. Het patroon schaalt—verander simpelweg het anonieme object of voer een collectie in voor bulk‑updates, en hetzelfde sjabloon zal elk kortingsscenario aan kunnen.

Klaar voor het volgende niveau? Probeer:

- Belastingberekeningen toevoegen naast kortingen.
- Kortingspercentages uit een database halen in plaats van ze hard‑coded op te geven.
- Voorwaardelijke opmaak gebruiken om rijen met hoge kortingen te markeren.

Die uitbreidingen behouden de kernidee, terwijl ze de bruikbaarheid van je kortingssjabloon uitbreiden.

Heb je vragen of een cool use‑case? Laat een reactie achter hieronder, en happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}