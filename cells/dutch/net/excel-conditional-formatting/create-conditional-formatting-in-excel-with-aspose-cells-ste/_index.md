---
category: general
date: 2026-06-30
description: Maak voorwaardelijke opmaak in een Excel-werkmap met Aspose.Cells. Leer
  hoe u de celachtergrond instelt, cellen rangschikt en het bestand via code opbouwt.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: nl
og_description: Maak voorwaardelijke opmaak in een Excel-werkmap met Aspose.Cells.
  Volg deze volledige tutorial om de celachtergrond in te stellen, cellen te rangschikken
  en Excel te automatiseren.
og_title: Maak voorwaardelijke opmaak in Excel met Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Voorwaardelijke opmaak maken in Excel met Aspose.Cells – Stapsgewijze handleiding
url: /nl/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maak voorwaardelijke opmaak in Excel met Aspose.Cells – Stapsgewijze gids

Heb je je ooit afgevraagd hoe je **voorwaardelijke opmaak** in een Excel‑bestand kunt **maken** zonder de UI te openen? Je bent niet de enige. Veel ontwikkelaars moeten **excel‑workbooks** on‑the‑fly **maken**, en dit programmatically bespaart uren handmatig werk. In deze tutorial laten we je precies zien hoe je **voorwaardelijke opmaak** **maakt**, cellen stijlt, en zelfs de topwaarden rangschikt – alles met de krachtige Aspose.Cells‑bibliotheek voor .NET.

We lopen door een praktijkvoorbeeld: een scoreblad genereren, hoge scores in lichtgroen markeren, en een gouden achtergrond geven aan de top‑3 presteerders. Aan het einde weet je **hoe je celachtergrond instelt**, **hoe je cellen rangschikt**, en **hoe je Aspose** gebruikt voor geavanceerde Excel‑automatisering. Geen poespas, alleen een complete, uitvoerbare oplossing die je in elk C#‑project kunt plaatsen.

## Wat je gaat leren

- Hoe je een **excel‑workbook** maakt met Aspose.Cells  
- Hoe je een bereik vult met willekeurige gegevens (scores)  
- Hoe je **celachtergrond instelt** met effen kleuren  
- Hoe je een formule‑gebaseerde regel toepast om **cell‑ranking** te doen en de beste drie te markeren  
- Hoe je het resultaat opslaat als een .xlsx‑bestand  

Voorvereisten: .NET 6+ (of .NET Framework 4.6+), Visual Studio (of een andere C#‑IDE), en een referentie naar het Aspose.Cells‑NuGet‑pakket. Als je nog nooit met Aspose hebt gewerkt, geen zorgen – we behandelen **hoe je Aspose gebruikt** vanaf nul.

---

![Create conditional formatting example](https://example.com/images/create-conditional-formatting.png "Screenshot showing conditional formatting in the generated Excel file")

*Afbeeldings‑alt‑tekst: voorbeeld van voorwaardelijke opmaak in een Excel‑workbook gegenereerd met Aspose.Cells.*

## Hoe een Excel‑workbook te maken met Aspose.Cells

Allereerst heb je een workbook‑object nodig om mee te werken. Aspose.Cells maakt dit een één‑regelige code.

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

Waarom hernoemen we het blad? Een duidelijke naam (zoals **Scores**) maakt het later makkelijker om te refereren, vooral wanneer je het bestand deelt met niet‑technische gebruikers.  

Nu het workbook bestaat, vullen we kolom A met willekeurige scores.

## Hoe gegevens te vullen – Willekeurige scores maken

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

Een korte opmerking: `PutValue` detecteert automatisch het gegevenstype, dus je hoeft niet te casten naar `int`. De lus start bij `i = 0` maar schrijft naar rij `i + 1` omdat Excel‑rijen 1‑gebaseerd zijn terwijl de `Cells`‑collectie 0‑gebaseerd is.

## Hoe celachtergrond in te stellen voor hoge scores

Nu **maken we voorwaardelijke opmaak** die elke score ≥ 80 in een lichtgroene tint kleurt.

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

De eigenschap `ForegroundColor` bepaalt de vulkleur, terwijl `Pattern = BackgroundType.Solid` Excel vertelt een effen vulling te gebruiken in plaats van een verloop of patroon. Dit is de kern van **hoe je celachtergrond instelt** op basis van een numerieke drempel.

## Hoe cellen te rangschikken en de top‑3 te markeren

Rangschikken is iets ingewikkelder omdat we een formule nodig hebben die elke cel evalueert ten opzichte van het volledige bereik. Aspose.Cells laat je dezelfde Excel‑formulesyntax gebruiken die je in de UI zou typen.

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

Waarom `A2` in de formule? Aspose evalueert de formule relatief ten opzichte van elke cel in het bereik, dus `A2` verschuift automatisch naar `A3`, `A4`, enz., terwijl de regel rij‑voor‑rij wordt toegepast. De functie `RANK` geeft de positie van een waarde binnen het opgegeven bereik terug, en het deel `<=3` zorgt ervoor dat alleen de drie hoogste scores de gouden vulling krijgen.

## Hoe het workbook op te slaan

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Vervang `YOUR_DIRECTORY` door een absoluut of relatief pad waar je applicatie naar kan schrijven. Na het uitvoeren van de methode, open je het bestand in Excel en zie je:

- Lichtgroene cellen voor elke score ≥ 80  
- Gouden cellen voor de drie hoogste scores, ongeacht of ze ook ≥ 80 zijn  

Dat is de volledige **create conditional formatting**‑pipeline.

---

## Volledig, uitvoerbaar voorbeeld

Hier is de volledige methode nogmaals, klaar om te copy‑pasten in een console‑applicatie of een willekeurige C#‑klasse:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### Verwacht resultaat

Wanneer je `Scores_ConditionalFormatting.xlsx` opent:

- Cellen met waarden **80** of hoger lichten lichtgroen op.  
- De drie hoogste getallen (zelfs als ze onder 80 liggen) krijgen een **gouden** achtergrond.  
- Alle andere cellen behouden de standaard witte achtergrond.

Die visuele aanwijzing vertelt een manager in één oogopslag wie de top‑presteerders zijn, zonder handmatig te sorteren.

---

## Veelgestelde vragen & randgevallen

**Wat als ik meer dan drie top‑scores nodig heb?**  
Verander simpelweg het `<=3`‑deel van de formule naar `<=5` (of elk ander getal). De regel past zich automatisch aan.

**Kan ik meerdere opmaak‑bereiken toepassen?**  
Zeker. Roep opnieuw `sheet.ConditionalFormattings.Add` aan met een ander bereik, en voeg vervolgens voorwaarden toe aan dat nieuwe `ConditionalFormatting`‑object.

**Hoe zit het met oudere Excel‑versies?**  
Aspose.Cells slaat standaard op in het moderne `.xlsx`‑formaat, dat compatibel is met Excel 2007 en later. Als je `.xls` nodig hebt, geef je `SaveFormat.Excel97To2003` door aan de `Save`‑methode.

**Is er een prestatie‑impact bij grote bladen?**  
Voorwaardelijke opmaak wordt opgeslagen als metadata, dus het beïnvloedt de bestandsgrootte niet significant. Het genereren van honderdduizenden rijen kan echter het geheugenverbruik verhogen – overweeg batchverwerking.

---

## Volgende stappen

Nu je **hoe je voorwaardelijke opmaak maakt** onder de knie hebt, kun je verder verkennen:

- **Hoe je Excel‑grafieken maakt** programmatically (een andere Aspose.Cells‑parel)  
- **Hoe je celachtergrond instelt** op basis van tekstwaarden (bijv. “Pass/Fail”)  
- **Hoe je Aspose.Cells gebruikt voor gegevensvalidatie** en keuzelijsten  

Elk van deze onderwerpen bouwt voort op dezelfde basisprincipes die je net geleerd hebt, dus je voelt je meteen thuis.

---

## Samenvatting

We hebben zojuist een compleet, end‑to‑end‑voorbeeld doorlopen van hoe je **voorwaardelijke opmaak** maakt in een Excel‑workbook met Aspose.Cells. Van het initialiseren van het workbook, het vullen van gegevens, **celachtergrond instellen**, de top‑presteerders rangschikken, tot het uiteindelijk opslaan van het bestand, elke stap werd behandeld met zowel **hoe je cellen rangschikt** als **hoe je Aspose gebruikt** in gedachten.  

Probeer de code, pas de drempels aan, en zie hoe snel je gepolijste rapporten kunt genereren voor elke zakelijke situatie. Heb je een eigen twist die je wilt delen? Laat een reactie achter – happy coding!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [Automate Excel Conditional Formatting Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java&#58; A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}