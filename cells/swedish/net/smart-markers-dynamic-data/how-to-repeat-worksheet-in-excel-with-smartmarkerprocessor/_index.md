---
category: general
date: 2026-11-19
description: Hur man upprepar kalkylblad när man fyller i Excel med arraydata. Lär
  dig att generera flera kalkylblad och fylla ett kalkylblad från en lista på några
  få steg.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: sv
lastmod: 2026-11-19
og_description: Hur man upprepar arbetsblad med SmartMarkerProcessor. Följ den här
  guiden för att fylla i Excel med arraydata, skapa flera arbetsblad och fylla i arbetsblad
  från en lista.
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Hur man upprepar ett kalkylblad i Excel – steg‑för‑steg‑guide
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: Hur man upprepar kalkylblad i Excel med SmartMarkerProcessor
url: /sv/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Så här upprepar du arbetsblad i Excel med SmartMarkerProcessor

Om du behöver **how to repeat worksheet** när du genererar Excel‑rapporter, visar den här guiden en komplett, körbar lösning. I slutet av tutorialen kommer du att kunna **populate Excel with array**‑data, **generate multiple worksheets** och **populate worksheet from list** med hjälp av SmartMarkerProcessor‑biblioteket.

Att upprepa ett arbetsblad är ett vanligt krav när varje avdelning, region eller tidsperiod behöver sin egen flik. Exemplet nedan visar de exakta stegen, förklarar varför varje inställning är viktig och täcker kantfall som tomma listor eller anpassade namn.

## Förutsättningar

- .NET 6.0 eller senare installerat
- En referens till **GroupDocs.Viewer** (eller motsvarande) NuGet‑paket som innehåller `SmartMarkerProcessor`
- En Excel‑mallarbetsbok (`.xlsx`) med en markör som `${repeat:Dept}` placerad i en rad du vill upprepa
- Grundläggande kunskap om C# och LINQ (valfritt men hjälpsamt)

Inga ytterligare tredjepartsbibliotek krävs.

## Steg 1: Skapa SmartMarkerProcessor‑instansen

Processorn orkestrerar markörersättning och duplicering av arbetsblad. Att instansiera den utan argument använder standardalternativen.

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

Att skapa processorn tidigt låter dig konfigurera globala alternativ innan någon data appliceras. Detta är grunden för att **how to repeat worksheet** korrekt.

## Steg 2: Aktivera arbetsbladsupprepning

Som standard ersätter processorn markörer endast på det aktuella bladet. Att sätta `RepeatWorksheet` till `true` instruerar motorn att klona hela arbetsbladet för varje objekt i datainsamlingen.

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

Att aktivera detta alternativ är nyckeln till **generate multiple worksheets** — processorn kommer att skapa en ny flik för varje element i `Dept`‑arrayen och behålla den ursprungliga formateringen.

## Steg 3: Förbered datakällan som en array eller lista

SmartMarkerProcessor fungerar med alla enumerable‑objekt, men att använda en array gör avsikten tydlig när du vill **populate worksheet from list**. Här skapar vi ett anonymt objekt som innehåller en `Dept`‑egenskap som håller en strängarray.

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

Om du redan har en `List<string>` kan du skicka den direkt; processorn kommer att behandla den på samma sätt. Det viktiga är att egenskapsnamnet (`Dept`) matchar markören `${repeat:Dept}` i mallen.

## Steg 4: Ladda mall‑arbetsbladet

Förutsatt att du har ett `ExcelPackage` (från EPPlus) eller ett `Workbook`‑objekt, hämta arbetsbladet du vill upprepa. Variabeln `ws` representerar det bladet.

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

Om du föredrar ett annat bibliotek (t.ex. ClosedXML) gäller samma princip: hämta ett arbetsbladsobjekt som implementerar det erforderliga gränssnittet.

## Steg 5: Bearbeta arbetsbladet med data

Applicera nu data på mallen. Processorn klonar arbetsbladet för varje avdelning, ersätter markören `${repeat:Dept}` med det faktiska avdelningsnamnet och lämnar resten av bladet orört.

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

När `Process` är klar blir `ws` det första av flera arbetsblad — ett per avdelning. Det ursprungliga bladets namn bevaras, medan duplikaten får inkrementella suffix (t.ex. “Sheet1 (1)”, “Sheet1 (2)”). Du kan byta namn på dem efteråt om du behöver ett eget namnschema.

### Förväntat resultat

När du öppnar den resulterande arbetsboken bör du se:

- **Sheet1** – den ursprungliga mallen (ofta tom eller använd som master)
- **Sheet1 (1)** – fylld med “HR”
- **Sheet1 (2)** – fylld med “IT”
- **Sheet1 (3)** – fylld med “Finance**”

Varje blad innehåller samma layout men med avdelningsnamnet ersatt där `${repeat:Dept}` förekom.

## Hantera kantfall

### Tomma eller null‑arrayer

Om `Dept` är null eller tom, kommer processorn inte att skapa några extra arbetsblad. För att undvika en helt tom arbetsbok kan du lägga till ett skydd:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Anpassade arbetsbladsnamn

Standardnamnschemat kanske inte passar alla rapporteringskrav. Efter bearbetning, byt namn på varje blad med en loop:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Fyll i ytterligare kolumner

Om du behöver **populate excel with array**‑värden utöver en enda markör, utöka dataobjektet:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

Justera sedan mallmarkörerna till `${repeat:Dept.Name}` och `${repeat:Dept.Headcount}`. Processorn kommer att upprepa raden för varje avdelning och fylla i båda kolumnerna.

## Fullt fungerande exempel

Nedan är en fristående konsolapplikation som demonstrerar hela flödet från mallinläsning till sparande av den slutliga arbetsboken.

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Förklaring av nyckelsektioner**

- **Processor creation** – etablerar motorn som kommer att tolka markörer.
- **RepeatWorksheet option** – aktiverar kärnfunktionen som svarar på *how to repeat worksheet*.
- **Data source** – använder en array (`new[]`) för att uppfylla **populate excel with array**.
- **Template loading** – demonstrerar ett vanligt sätt att få ett arbetsbladsobjekt.
- **Processing** – utför dupliceringen och datainmatningen i ett anrop.
- **Renaming** – visar hur man omvandlar de generiska namnen “(1)”, “(2)” till meningsfulla titlar, ett typiskt krav efter **generate multiple worksheets**.

Att köra detta program skapar `Result.xlsx` med tre avdelningsspecifika flikar, var och en fylld från arrayen.

## Vanliga fallgropar och pro‑tips

- **Marker spelling** – markören måste matcha egenskapsnamnet exakt (`${repeat:Dept}`). Ett stavfel förhindrar upprepning.
- **Worksheet index** – efter bearbetning förblir det ursprungliga bladet på index 0; genererade blad följer sekventiellt. Felaktig indexering kan leda till att fel flik byts namn.
- **Large data sets** – att generera hundratals arbetsblad kan öka filstorleken dramatiskt. Överväg att dela upp rapporter eller använda ett enda blad med grupperade sektioner om prestanda blir ett problem.
- **Thread safety** – `SmartMarkerProcessor` är inte trådsäker. Skapa en separat instans per tråd om du bearbetar flera arbetsböcker parallellt.

## Slutsats

Du vet nu **how to repeat worksheet** i Excel med SmartMarkerProcessor, hur du **populate excel with array**‑data, hur du **generate multiple worksheets**, och hur du **populate worksheet from list** effektivt. Det kompletta exemplet binder ihop alla koncept, och det valfria steget för namnbyte låter dig skapa rena, användarvänliga fliknamn.

Nästa steg kan vara att utforska:

- Att använda **populate worksheet from list** med komplexa objekt (nästlade samlingar)
- Applicera villkorsstyrd formatering efter arbetsbladsduplication
- Exportera den genererade arbetsboken till PDF eller CSV för vidare konsumtion

Känn dig fri att anpassa koden till dina egna rapporteringsscenarier, och njut av att automatisera Excel‑arbetsböcker med självförtroende!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man upprepar arbetsblad – Komplett guide för Excel‑automatisering](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Skapa arbetsblad per objekt – Hur man upprepar arbetsblad i C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [Hur man expanderar en array i Excel och fyller i en mall](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}