---
category: general
date: 2026-06-30
description: Skapa villkorsstyrd formatering i en Excel-arbetsbok med Aspose.Cells.
  Lär dig hur du ställer in cellbakgrund, rankar celler och bygger filen programmässigt.
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: sv
og_description: Skapa villkorsstyrd formatering i en Excel-arbetsbok med Aspose.Cells.
  Följ den här kompletta handledningen för att sätta cellbakgrund, rangordna celler
  och automatisera Excel.
og_title: Skapa villkorsstyrd formatering i Excel med Aspose.Cells
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
title: Skapa villkorsstyrd formatering i Excel med Aspose.Cells – Steg‑för‑steg‑guide
url: /sv/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa villkorsstyrd formatering i Excel med Aspose.Cells – Steg‑för‑steg‑guide

Har du någonsin undrat hur man **create conditional formatting** i en Excel‑fil utan att öppna UI‑gränssnittet? Du är inte ensam. Många utvecklare behöver **create excel workbook**‑filer i farten, och att göra det programatiskt sparar timmar av manuellt arbete. I den här handledningen visar vi exakt hur du **create conditional formatting**, formaterar celler och till och med rankar de högsta värdena—allt med det kraftfulla Aspose.Cells‑biblioteket för .NET.

Vi går igenom ett verkligt exempel: generera ett poängblad, markera höga poäng i ljusgrönt och ge en guldbakgrund till de tre bästa. I slutet kommer du att veta **how to set cell background**, **how to rank cells** och **how to use Aspose** för sofistikerad Excel‑automation. Inga onödiga utsvävningar, bara en komplett, körbar lösning som du kan slänga in i vilket C#‑projekt som helst.

## Vad du kommer att lära dig

- Hur man **create excel workbook** med Aspose.Cells  
- Hur man fyller ett område med slumpmässiga data (poäng)  
- Hur man **set cell background** med solida färger  
- Hur man tillämpar en formelbaserad regel för att **rank cells** och markera de tre bästa  
- Hur man sparar resultatet som en .xlsx‑fil  

Förutsättningar: .NET 6+ (eller .NET Framework 4.6+), Visual Studio (eller någon C#‑IDE), och en referens till Aspose.Cells‑NuGet‑paketet. Om du aldrig har använt Aspose tidigare, oroa dig inte—vi täcker **how to use Aspose** från grunden.

---

![Exempel på villkorsstyrd formatering](https://example.com/images/create-conditional-formatting.png "Skärmbild som visar villkorsstyrd formatering i den genererade Excel‑filen")

*Image alt text: exempel på villkorsstyrd formatering i en Excel‑arbetsbok genererad med Aspose.Cells.*

## Så skapar du ett Excel‑arbetsbok med Aspose.Cells

Först och främst: du behöver ett workbook‑objekt att arbeta med. Aspose.Cells gör detta till en endaste rad.

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

Varför byter vi namn på bladet? Ett tydligt namn (som **Scores**) gör det enklare att referera till senare, särskilt när du delar filen med icke‑tekniska användare.  

Nu när arbetsboken finns, låt oss fylla kolumn A med slumpmässiga poäng.

## Så fyller du data – Skapar slumpmässiga poäng

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

En snabb notering: `PutValue` upptäcker automatiskt datatypen, så du behöver inte kasta till `int`. Loopen startar vid `i = 0` men skriver till rad `i + 1` eftersom Excel‑rader är 1‑baserade medan `Cells`‑samlingen är 0‑baserad.

## Så sätter du cellbakgrund för höga poäng

Nu ska vi **create conditional formatting** som färgar alla poäng ≥ 80 i en ljusgrön nyans.

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

`ForegroundColor`‑egenskapen styr fyllningsfärgen, medan `Pattern = BackgroundType.Solid` talar om för Excel att använda en solid fyllning istället för en gradient eller ett mönster. Detta är kärnan i **how to set cell background** baserat på ett numeriskt tröskelvärde.

## Så rankar du celler och markerar topp‑3

Rankning är lite knepigare eftersom vi behöver en formel som utvärderar varje cell mot hela området. Aspose.Cells låter dig använda samma Excel‑formelsyntax som du skulle skriva i UI‑gränssnittet.

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

Varför `A2` i formeln? Aspose utvärderar formeln relativt varje cell i området, så `A2` automatiskt skiftar till `A3`, `A4` osv. när regeln appliceras rad för rad. `RANK`‑funktionen returnerar positionen för ett värde inom det angivna området, och delen `<=3` säkerställer att endast de tre högsta poängen får den gula fyllningen.

## Så sparar du arbetsboken

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

Byt ut `YOUR_DIRECTORY` mot en absolut eller relativ sökväg som din applikation kan skriva till. Efter att metoden har körts, öppna filen i Excel och du kommer att se:

- Ljusgröna celler för alla poäng ≥ 80  
- Guldceller för de tre högsta poängen, oavsett om de också är ≥ 80  

Det är hela **create conditional formatting**‑pipeline.

---

## Fullt, körbart exempel

Här är hela metoden igen, redo att kopieras och klistras in i en konsolapp eller någon C#‑klass:

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

### Förväntat resultat

När du öppnar `Scores_ConditionalFormatting.xlsx`:

- Celler med värden **80** eller högre lyser i ljusgrönt.  
- De tre högsta siffrorna (även om de är under 80) visas med en **gold**‑bakgrund.  
- Alla andra celler behåller den standardvita bakgrunden.

Denna visuella ledtråd visar omedelbart en chef vilka toppresterande som är, utan någon manuell sortering.

---

## Vanliga frågor & specialfall

**Vad händer om jag behöver fler än tre topppoäng?**  
Byt bara ut delen `<=3` i formeln till `<=5` (eller vilket antal du önskar). Regeln anpassas automatiskt.

**Kan jag tillämpa flera formateringsområden?**  
Absolut. Anropa `sheet.ConditionalFormattings.Add` igen med ett annat område, och lägg sedan till villkor på det nya `ConditionalFormatting`‑objektet.

**Vad händer med äldre Excel‑versioner?**  
Aspose.Cells sparar som standard i det moderna `.xlsx`‑formatet, vilket är kompatibelt med Excel 2007 och senare. Om du behöver `.xls`, skicka `SaveFormat.Excel97To2003` till `Save`‑metoden.

**Finns det prestandapåverkan för stora blad?**  
Villkorsstyrd formatering lagras som metadata, så den påverkar inte filstorleken nämnvärt. Däremot kan generering av hundratusentals rader öka minnesanvändningen—överväg att bearbeta i batcher.

---

## Nästa steg

Nu när du har bemästrat **how to create conditional formatting**, kanske du vill utforska:

- **How to create Excel charts** programmatically (another Aspose.Cells gem)  
- **How to set cell background** based on text values (e.g., “Pass/Fail”)  
- **How to use Aspose.Cells for data validation** and drop‑down lists  

Varje ämne bygger på samma grunder du just lärt dig, så du kommer snabbt känna dig hemma.

---

## Sammanfattning

Vi har just gått igenom ett komplett, end‑to‑end‑exempel på hur man **create conditional formatting** i en Excel‑arbetsbok med Aspose.Cells. Från initiering av arbetsboken, fyllning av data, **setting cell background**, rankning av toppresterande, till slutlig sparning av filen, varje steg täcktes med både **how to rank cells** och **how to use Aspose** i åtanke.  

Kör koden, justera tröskelvärdena, och se hur snabbt du kan generera polerade rapporter för vilket affärsscenario som helst. Har du ett eget twist du vill dela? Lägg en kommentar nedan—lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstrerats i denna guide. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Automatisera Excel villkorsstyrd formatering med Aspose.Cells för Java: En komplett guide](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Hur man skapar och formaterar Excel‑celler med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Skapa en Excel‑arbetsbok med Aspose.Cells i Java: En steg‑för‑steg‑guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}