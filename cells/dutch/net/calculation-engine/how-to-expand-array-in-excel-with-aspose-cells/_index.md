---
category: general
date: 2026-11-16
description: Leer hoe je een array in Excel kunt uitbreiden met Aspose.Cells, dynamische
  array‑functies en een lambda‑reducer, en vervolgens het Excel‑bestand vanuit C#
  kunt schrijven.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: nl
lastmod: 2026-11-16
og_description: Hoe een array uit te breiden in Excel met Aspose.Cells, dynamische
  array‑functies en een lambda‑reducer. Volg het volledige C#‑voorbeeld om het Excel‑bestand
  te schrijven.
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Hoe een array uit te breiden in Excel met Aspose.Cells – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Hoe een array in Excel uit te breiden met Aspose.Cells
url: /nl/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een array uit te breiden in Excel met Aspose.Cells

Als je **hoe een array uit te breiden** in een Excel-werkblad vanuit C# nodig hebt, laat deze tutorial de exacte stappen zien. Je maakt een Excel-werkmap, gebruikt dynamische array‑functies zoals `EXPAND` en `REDUCE`, past een **lambda**‑accumulator toe, en **schrijft het Excel‑bestand** uiteindelijk naar schijf. De aanpak werkt met Aspose.Cells 23.10 of later en vereist geen handmatige Excel‑installatie.

Aan het einde van deze gids heb je een volledig functioneel `ExpandReduceDemo.xlsx` dat de kracht van dynamische array‑formules in een programmeercontext demonstreert.

## Wat je nodig hebt

- .NET 6.0 (of elke .NET‑versie die door Aspose.Cells wordt ondersteund)
- Aspose.Cells for .NET‑pakket (`dotnet add package Aspose.Cells`)
- Een code‑editor of IDE (Visual Studio, VS Code, Rider, enz.)

Er is geen extra COM‑interop of Office‑installatie vereist omdat Aspose.Cells het bestandsformaat intern afhandelt.

## Stap 1: Excel‑werkmap maken

De eerste taak is om **excel‑werkmap** in het geheugen te **creëren**. Aspose.Cells biedt de `Workbook`‑klasse, die een volledig XLSX‑bestand vertegenwoordigt.

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **Waarom dit belangrijk is:** Het instantieren van een `Workbook` geeft je een schoon canvas. Het standaard werkblad is al aanwezig, dus je hoeft er geen handmatig één toe te voegen tenzij je meerdere bladen wilt.

## Stap 2: Een verticale array‑constante invoegen

De dynamische array‑engine van Excel kan werken met letterlijke array‑constanten. We plaatsen de verticale array `{1;2;3;4;5}` in cel **A1**.

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **Tip:** Het puntkomma (`;`) scheidt rijen in de constante, terwijl een komma (`,`) kolommen zou scheiden. Dit weerspiegelt de eigen syntaxis van Excel.

## Stap 3: De array uitbreiden naar een matrix

Nu beantwoorden we de kernvraag – **hoe een array uit te breiden** – met de `EXPAND`‑functie. De formule breidt de één‑kolom‑array uit tot een matrix van 5 rij × 2 kolom, beginnend bij **B1**.

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **Waarom EXPAND?** `EXPAND(source, rows, cols)` dwingt het bronbereik om de opgegeven grootte in te nemen, met lege cellen op te vullen indien nodig. Het is de meest leesbare manier om een grotere matrix te genereren vanuit één array.

## Stap 4: De matrix reduceren met een lambda‑accumulator

De `REDUCE`‑functie doorloopt een bereik en aggregeert waarden met een **lambda**‑expressie. Hier sommeren we elke kolomwaarde in één kolom en plaatsen het resultaat in **D1**.

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **Hoe lambda te gebruiken:** De `LAMBDA(acc, val, acc+val)` ontvangt de huidige accumulator (`acc`) en de volgende celwaarde (`val`). Het retourneert de nieuwe accumulator, waardoor een lopende som ontstaat. Dit demonstreert **hoe lambda te gebruiken** in Excel‑formules vanuit code.

## Stap 5: Formules berekenen zodat resultaten verschijnen

Aspose.Cells evalueert formules niet automatisch wanneer je ze instelt. Het aanroepen van `CalculateFormula` dwingt de engine om elke formule in de werkmap te berekenen.

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **Opmerking:** Als je het gegenereerde bestand in Excel opent, zijn de waarden al zichtbaar omdat ze vooraf zijn berekend.

## Stap 6: Excel‑bestand naar schijf schrijven

Tot slot **schrijf je het excel‑bestand** met de `Save`‑methode. Kies een map waarvoor je schrijfrechten hebt.

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### Verwacht resultaat

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **Kolom B** en **C** bevatten de 5 × 2‑matrix die door `EXPAND` is geproduceerd.
- **Cel D1** toont `15`, de som van alle getallen, berekend door de `REDUCE` + **lambda**‑formule.

## Veelgestelde vragen en randgevallen

- **Kan ik uitbreiden naar meer kolommen dan de bron biedt?**  
  Ja. `EXPAND` vult ontbrekende kolommen met lege cellen. Hetzelfde geldt voor rijen.

- **Wat als de bronarray horizontaal is (`{1,2,3,4,5}`)?**  
  `EXPAND` behandelt de bron als één rij; je kunt nog steeds rijen en kolommen opgeven om deze te herschikken.

- **Werkt `REDUCE` met niet‑numerieke gegevens?**  
  De lambda moet een waarde retourneren die compatibel is met het type van de accumulator. Voor tekstconcatenatie kun je `LAMBDA(acc, val, acc & val)` gebruiken.

- **Moet ik `CalculateFormula` voor elke wijziging aanroepen?**  
  Alleen wanneer je de berekende waarden nodig hebt vóór het opslaan. Excel zal bij het openen opnieuw berekenen als je dit overslaat.

## Pro‑tips

- **Prestaties:** Voor grote werkmappen roep je `workbook.CalculateFormula` één keer aan nadat alle formules zijn ingesteld, in plaats van na elke cel.
- **Versie‑veiligheid:** `EXPAND` en `REDUCE` zijn beschikbaar in Excel 365 en later. Aspose.Cells implementeert ze ongeacht de doel‑Excel‑versie omdat de berekeningsengine ingebouwd is.
- **Formules debuggen:** Gebruik `sheet.Cells["B1"].Formula` om de exacte string die je hebt ingesteld terug te lezen; dit helpt bij het dynamisch opbouwen van formules.

## Conclusie

Je weet nu **hoe een array uit te breiden** in Excel met Aspose.Cells, dynamische array‑functies te benutten, een **lambda** toe te passen met `REDUCE`, en **excel‑bestand** te **schrijven** vanuit C#. Dit end‑to‑end‑voorbeeld kan worden aangepast voor complexere datatransformaties, zoals matrix‑transponeren, cumulatieve totalen of aangepaste aggregaties.

---

*Volgende stappen:*  
- Verken andere dynamische functies zoals `FILTER`, `SORT` en `UNIQUE`.  
- Combineer meerdere `LAMBDA`‑expressies om herbruikbare gebruikers‑gedefinieerde functies te bouwen.  
- Integreer de werkmapgeneratie in ASP.NET Core‑API’s voor on‑the‑fly rapportcreatie.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een Excel‑werkmap te maken in C# met een dynamische array‑formule](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [Hoe een array uit te breiden in Excel en een sjabloon te vullen](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [Hoe een array uit te breiden in C# met Aspose.Cells – Stapsgewijze gids](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}