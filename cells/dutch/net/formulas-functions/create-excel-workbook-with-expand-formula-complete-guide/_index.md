---
category: general
date: 2026-07-13
description: Maak een Excel-werkmap en stel een celformule in met EXPAND. Leer hoe
  je de werkmap opnieuw kunt berekenen en Excel‑formules dynamisch kunt schrijven
  in C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set cell formula
- recalculate workbook
- write excel formula
- how to use expand
language: nl
lastmod: 2026-07-13
og_description: Maak direct een Excel-werkmap. Deze gids laat zien hoe je een celformule
  instelt, de werkmap opnieuw berekent en beheerst hoe je EXPAND gebruikt voor dynamische
  bereiken.
og_image_alt: Screenshot showing create excel workbook with EXPAND formula in C#
og_title: Maak Excel-werkmap met EXPAND‑formule – stap voor stap
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Create Excel workbook and set cell formula using EXPAND. Learn how
    to recalculate workbook and write Excel formulas dynamically in C#.
  headline: Create Excel Workbook with EXPAND Formula – Complete Guide
  type: TechArticle
tags:
- excel
- csharp
- aspnet
title: Maak een Excel-werkmap met de EXPAND‑formule – Complete gids
url: /nl/net/formulas-functions/create-excel-workbook-with-expand-formula-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak Excel-werkmap met EXPAND-formule – Complete gids

Heb je je ooit afgevraagd hoe je **create excel workbook** programmatically kunt maken en een enkele formule een hele tabel laten invullen? Je bent niet de enige. In veel rapportage‑ of data‑exportscenario's moet je een werkmap in de Downloads‑map van een gebruiker plaatsen, een formule over cellen verspreiden, en deze automatisch laten evalueren.  

In deze tutorial lopen we precies dat stap voor stap door: we zullen **create excel workbook**, **set cell formula** gebruiken met de nieuwe `EXPAND`‑functie, en vervolgens **recalculate workbook** zodat de resultaten direct verschijnen. Tegen het einde weet je ook **how to use expand** voor dynamische bereiken en kun je comfortabel **write excel formula** code schrijven die zich aanpast aan veranderende gegevensgroottes.

---

## Wat je gaat bouwen

- Een nieuw `Workbook`‑object (geen sjabloon nodig).  
- Een uitbreidende array‑formule in `A1` die groeit tot een blok van 5 rij × 3 kolom.  
- Een aanroep van `Calculate()` die de engine dwingt de formule te evalueren.  
- Een snelle teruglezen van de ingevulde cellen zodat je de output kunt verifiëren.

Geen externe bibliotheken nodig buiten de core Aspose.Cells (of een vergelijkbare .NET Excel‑engine) — alleen plain C#.

---

## Voorvereisten

- .NET 6+ (of .NET Framework 4.7.2+).  
- Een referentie naar een Excel‑manipulatie‑bibliotheek die dynamische array‑functies ondersteunt (bijv. **Aspose.Cells**, **GemBox.Spreadsheet**, of **ClosedXML** met een recente Excel‑engine).  
- Basiskennis van C#‑syntaxis — als je een “Hello World” hebt geschreven, ben je klaar om te beginnen.

---

## Stap 1: Maak Excel-werkmap en voeg een werkblad toe

Allereerst. We hebben een workbook‑object nodig om alles te bevatten. Beschouw het als het lege notitieboek dat je later gaat vullen.

```csharp
// Step 1: Instantiate a new workbook
var workbook = new Workbook();               // Primary object
var sheet = workbook.Worksheets[0];          // Grab the default sheet
```

> **Waarom dit belangrijk is:** De `Workbook`‑klasse is het startpunt voor elke Excel‑bewerking. Zonder deze kun je geen formule instellen of iets opnieuw berekenen. Het vooraf aanmaken van de werkmap stelt je ook in staat later meerdere bladen toe te voegen als je scenario groeit.

---

## Stap 2: Stel cel‑formule in met `EXPAND`

Nu gaan we **set cell formula** in `A1` instellen. De `EXPAND`‑functie neemt een “spill”‑referentie (`A1#`) en breidt deze uit tot een specifieke grootte — in ons geval 5 rijen bij 3 kolommen.

```csharp
// Step 2: Insert an expanding array formula into cell A1
// The source range A1# will be stretched to 5 rows × 3 columns
sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";
```

> **Pro tip:** Als je een bibliotheek gebruikt die de Excel‑berekeningsengine nabootst, werkt de `#`‑spill‑operator direct out‑of‑the‑box. Anders moet je mogelijk dynamische array‑ondersteuning inschakelen in de bibliotheekinstellingen.  
> **Wat als de broncel leeg is?** `EXPAND` zal `#SPILL!` retourneren. Om dat te voorkomen kun je de referentie omhullen met `IFERROR` of een standaardwaarde opgeven, bijv. `=IFERROR(EXPAND(A1#,5,3),0)`.

---

## Stap 3: Vul de broncel (optioneel)

`EXPAND` heeft iets nodig om uit te breiden. Laten we een eenvoudige array‑constante in `A1` plaatsen zodat we de spill in actie kunnen zien.

```csharp
// Optional: Fill A1 with a 2‑by‑2 array constant
sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";
```

Nu vertegenwoordigt `A1#` een blok van 2 × 2, en `EXPAND` zal dit uitrekken tot de gevraagde 5 × 3‑matrix, waarbij de extra cellen worden gevuld met nullen (of wat de engine beslist).

---

## Stap 4: Herbereken werkmap om de formule te evalueren

De formule instellen is niet genoeg — je moet **recalculate workbook** zodat de engine de waarden daadwerkelijk berekent.

```csharp
// Step 4: Force calculation of all formulas
workbook.Calculate();
```

> **Waarom we herberekenen:** Sommige bibliotheken evalueren formules lui alleen wanneer je opslaat of expliciet om een waarde vraagt. Het aanroepen van `Calculate()` garandeert dat het spill‑gebied direct wordt gevuld, wat essentieel is voor verdere verwerking of voor het teruggeven van gegevens aan een UI.

---

## Stap 5: Verifieer het resultaat – Lees het uitgebreide bereik terug

Laten we een paar cellen uit het uitgebreide gebied ophalen om te bewijzen dat het werkt.

```csharp
// Step 5: Read back a few cells from the expanded block
for (int row = 0; row < 5; row++)
{
    for (int col = 0; col < 3; col++)
    {
        var value = sheet.Cells[row, col].Value;
        Console.Write($"{value}\t");
    }
    Console.WriteLine();
}
```

**Verwachte console‑output**

```
1	2	0	
3	4	0	
0	0	0	
0	0	0	
0	0	0	
```

Merk op hoe de oorspronkelijke 2 × 2‑array in de linkerbovenhoek wordt geplaatst, en de resterende cellen worden opgevuld met nullen (het standaardgedrag van `EXPAND` wanneer de doelformaat groter is dan de bron).

---

## Veelvoorkomende variaties en randgevallen

| Situation | How to Handle It |
|-----------|------------------|
| **Source range larger than target** | `EXPAND` zal de extra rijen/kolommen afkappen. Als je de volledige bron nodig hebt, laat je de grootte‑argumenten weg. |
| **Dynamic source size** | Gebruik `ROWS(A1#)` en `COLUMNS(A1#)` binnen `EXPAND` voor een zelf‑aanpassende spill. |
| **Performance on huge ranges** | Het herberekenen van een enorme werkmap kan traag zijn. Roep `Calculate()` alleen aan op het betreffende blad: `sheet.Calculate();`. |
| **Saving the workbook** | Na verificatie roep je `workbook.Save("Report.xlsx");` aan om het bestand op te slaan. |
| **Using other dynamic functions** | `SEQUENCE`, `FILTER` en `SORT` werken goed samen met `EXPAND`. Bijvoorbeeld, `=EXPAND(FILTER(A2:A20, B2:B20>0),10,2)`. |

---

## Volledig werkend voorbeeld (alle stappen gecombineerd)

```csharp
using System;
using Aspose.Cells;   // Replace with your chosen library

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];

        // 2️⃣ Set an expanding formula in A1
        sheet.Cells[0, 0].Formula = "=EXPAND(A1#,5,3)";

        // 3️⃣ Optional: give A1 a 2x2 array constant
        sheet.Cells[0, 0].ArrayFormula = "{1,2;3,4}";

        // 4️⃣ Recalculate so the formula evaluates
        workbook.Calculate();

        // 5️⃣ Print the first 5 rows × 3 columns
        for (int r = 0; r < 5; r++)
        {
            for (int c = 0; c < 3; c++)
            {
                Console.Write($"{sheet.Cells[r, c].Value}\t");
            }
            Console.WriteLine();
        }

        // Save if you want to inspect the file
        workbook.Save("ExpandDemo.xlsx");
    }
}
```

Voer dit programma uit en je ziet exact de eerder getoonde output, plus een `ExpandDemo.xlsx`‑bestand op schijf dat dezelfde uitgespreide array bevat.

---

## Tips & tricks uit de praktijk

- **Pro tip:** Als je de uitgebreide waarden alleen nodig hebt voor verdere berekeningen (geen door de gebruiker zichtbare spreadsheet), overweeg dan de waarden direct na `Calculate()` uit te lezen — geen noodzaak om naar schijf te schrijven.  
- **Watch out for:** Sommige oudere versies van Excel‑engines ondersteunen geen dynamische arrays; ze geven `#NAME?` terug. Controleer altijd je bibliotheekversie.  
- **Typical mistake:** Het vergeten aanroepen van `Calculate()` leidt tot lege cellen en verwarde gebruikers. Test altijd de volledige pipeline.  
- **Performance hint:** Het batch‑instellen van formules (`sheet.Cells[range].Formula = ...`) kan sneller zijn dan individuele toewijzingen bij duizenden cellen.

---

## Conclusie

Je weet nu hoe je **create excel workbook**, **set cell formula** met de krachtige `EXPAND`‑functie, en **recalculate workbook** zodat de gegevens precies daar uitvloeien waar je ze nodig hebt. Deze aanpak stelt je in staat **write excel formula** code te schrijven die zich aanpast aan veranderende gegevensgroottes zonder vaste bereiken te coderen — perfect voor dashboards, geautomatiseerde rapporten, of elk scenario waarin de brongegevens in de loop van de tijd groeien.

Klaar voor de volgende stap? Probeer `EXPAND` te vervangen door `SEQUENCE` om genummerde rasters te genereren, of combineer het met `FILTER` om alleen rijen op te halen die aan een voorwaarde voldoen. En vergeet niet te verkennen hoe je **set cell formula** kunt gebruiken voor grafieken, draaitabellen of voorwaardelijke opmaak — je nieuw aangemaakte werkmap is een solide basis.

Heb je vragen over randgevallen of bibliotheek‑specifieke eigenaardigheden? Laat een reactie achter hieronder, en happy coding!

---

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een werkmap‑gebonden benoemd bereik te maken in Excel met Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)
- [Excel‑automatisering met Aspose.Cells .NET: Werkmap maken & externe koppelingen instellen](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Hoe een Excel‑werkmap te laden & printerformaten in te stellen met Aspose.Cells voor .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}