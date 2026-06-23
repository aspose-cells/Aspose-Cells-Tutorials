---
category: general
date: 2026-05-04
description: Skapa Excel från mall och mappa JSON till Excel med dynamisk bladnamngivning.
  Lär dig hur du fyller i Excel från JSON och genererar Excel med JSON på några minuter.
draft: false
keywords:
- create excel from template
- map json to excel
- populate excel from json
- dynamic worksheet naming excel
- generate excel using json
language: sv
og_description: Skapa Excel från mall snabbt. Den här guiden visar hur du mappar JSON
  till Excel, fyller i Excel från JSON, använder dynamisk bladnamngivning och genererar
  Excel med JSON.
og_title: Skapa Excel från mall – Komplett .NET-handledning
tags:
- C#
- Aspose.Cells
- SmartMarker
- JSON
title: Skapa Excel från mall – Steg‑för‑steg‑guide för .NET‑utvecklare
url: /sv/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa Excel från mall – Komplett .NET‑handledning

Har du någonsin behövt **create Excel from template** men känt dig fast med JSON‑data och bladnamn? Du är inte ensam. I många rapporteringsprojekt innehåller mallen layouten medan JSON‑payloaden styr de faktiska värdena, och att få dem att samarbeta kan vara en huvudvärk.  

Den goda nyheten? Med några rader C# och Aspose Cells SmartMarker‑motor kan du **populate Excel from JSON**, byta namn på detaljbladen i farten och slutligen **generate Excel using JSON** utan att någonsin röra UI‑et.  

I den här handledningen går vi igenom hela kedjan: läsa in en mall, mappa JSON till Excel, konfigurera dynamisk bladnamngivning och spara den slutliga arbetsboken. I slutet har du ett återanvändbart kodsnutt som du kan klistra in i vilken .NET‑tjänst som helst. Inga externa verktyg, bara ren kod.

---

## Vad du behöver

- **Aspose.Cells for .NET** (v24.10 eller senare) – biblioteket som driver SmartMarker.
- En **template.xlsx**‑fil som innehåller SmartMarker‑taggar som `{Master:Name}` och `{Detail:Item}`.
- En **data.json**‑fil som matchar master‑detail‑strukturen.
- Visual Studio 2022 (eller någon annan IDE du föredrar) som riktar sig mot .NET 6 eller senare.

Det är allt. Om du redan har dessa delar är du redo att köra.

---

## Skapa Excel från mall – Översikt

Kärnidén är enkel: behandla Excel‑filen som en *mall* och låt SmartMarker ersätta platshållare med värden från din JSON. Biblioteket låter dig också byta namn på detaljbladet baserat på ett master‑fält, vilket är där **dynamic worksheet naming excel** glänser.

Nedan är den kompletta, körklara koden. Kopiera och klistra in i en konsolapp och peka sökvägarna till dina egna filer.

```csharp
// ------------------------------------------------------------
// Full example: create Excel from template using JSON data
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains SmartMarker tags
            //    (e.g., {Master:Name} in the master sheet and {Detail:Item} in the detail sheet)
            string templatePath = @"C:\MyProject\Templates\template.xlsx";
            Workbook wb = new Workbook(templatePath);

            // 2️⃣ Read the JSON data that will populate the markers
            //    The JSON should match the structure expected by the template.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // 3️⃣ Configure the SmartMarker processor to rename the detail sheet
            //    dynamically based on the master record’s Name field.
            //    This demonstrates dynamic worksheet naming excel.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // 4️⃣ Execute the SmartMarker processing using the JSON data.
            //    This step maps JSON to Excel and populates every marker.
            wb.SmartMarkerProcessor.Execute(json);

            // 5️⃣ Save the processed workbook – now it’s a brand‑new file.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Excel file generated successfully at: " + outputPath);
        }
    }
}
```

> **Förväntat resultat:**  
> - Master‑bladet visar namnet från `Master.Name`.  
> - Detaljbladet kommer att bytas namn till något i stil med `Detail_JohnDoe`.  
> - Alla `{Detail:Item}`‑rader fylls med items‑arrayen från JSON‑en.

---

## Mappa JSON till Excel – Ladda data

Innan SmartMarker‑motorn kan göra sin magi måste JSON‑en vara **well‑formed** och spegla den hierarki som används i mallen. En typisk master‑detail‑JSON ser ut så här:

```json
{
  "Master": {
    "Name": "John Doe",
    "Date": "2026-05-04"
  },
  "Detail": [
    { "Item": "Widget A", "Qty": 10, "Price": 2.5 },
    { "Item": "Widget B", "Qty": 5,  "Price": 5.0 }
  ]
}
```

**Varför detta är viktigt:**  
- Nycklarna `Master` och `Detail` motsvarar direkt `{Master:…}`‑ och `{Detail:…}`‑taggarna.  
- Om JSON‑strukturen avviker kommer SmartMarker inte hitta någon matchning, och cellerna förblir tomma.  

**Tips:** Validera din JSON med en snabb online‑validator eller `System.Text.Json.JsonDocument.Parse(json)` för att fånga syntaxfel tidigt.

---

## Fyll i Excel från JSON – SmartMarker‑inställning

SmartMarker fungerar genom att skanna arbetsboken efter taggar och sedan injicera data. Steget **populate excel from json** är i princip `Execute`‑anropet vi såg tidigare, men det finns några valfria inställningar som är värda att nämna:

| Inställning | Vad den gör | När den ska användas |
|------------|--------------|----------------------|
| `Options.CaseSensitive` | Behandlar taggnamn som skiftlägeskänsliga. | Om din mall blandar stora och små bokstäver och du behöver strikt matchning. |
| `Options.RemoveEmptyRows` | Tar bort rader som inte fick någon data. | För att hålla det slutliga bladet snyggt när vissa detaljposter är valfria. |
| `Options.EnableHyperlink` | Tillåter hyperlänkar i JSON att bli klickbara. | När du behöver klickbara URL:er i rapporten. |

Du kan kedja dem så här:

```csharp
wb.SmartMarkerProcessor.Options.CaseSensitive = true;
wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;
```

---

## Dynamisk bladnamngivning Excel – Konfigurera detaljbladets namn

Ett av de knepigare kraven som många projekt har är **dynamic worksheet naming excel**. Istället för ett statiskt “Detail”-blad kan du vilja att varje rapport bär kundens namn eller ett ordernummer.

Raden:

```csharp
wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";
```

gör exakt det. Platshållaren `{Master.Name}` ersätts *efter* att JSON har bearbetats, så det nya bladnamnet blir `Detail_JohnDoe`.  

**Edge case:** Om namnet innehåller tecken som är otillåtna i bladnamn (`:`, `\`, `/`, `?`, `*`, `[`, `]`), så sanerar Aspose dem automatiskt, men du kan för‑rensa strängen i JSON om du behöver ett specifikt format.

---

## Generera Excel med JSON – Execute och spara

De sista två raderna i koden (`Execute` och `Save`) är där magin **generate excel using json** sker. Under huven parsar Aspose JSON‑en till en datatabell, itererar över mallen och skriver utdatafilen.

Om du behöver generera flera arbetsböcker i en loop (t.ex. en per kund), flytta bara `Workbook`‑instansieringen in i loopen och ändra utdatafilens namn därefter:

```csharp
foreach (var customerJson in customers)
{
    Workbook wb = new Workbook(templatePath);
    wb.SmartMarkerProcessor.Options.DetailSheetNewName = $"Detail_{customerJson.Master.Name}";
    wb.SmartMarkerProcessor.Execute(customerJson);
    wb.Save($@"C:\Reports\Report_{customerJson.Master.Name}.xlsx");
}
```

Det mönstret är vanligt i batch‑rapporterings‑tjänster.

---

## Vanliga fallgropar & pro‑tips

- **Missing tags:** Om en cell fortfarande visar `{Master:Name}`, så har taggen inte identifierats. Dubbelkolla stavning och att taggen är i en cell, inte i en kommentar.
- **Large JSON payloads:** För enorma dataset, överväg att streama JSON eller använda `DataTable` istället för en rå sträng för att minska minnesbelastningen.
- **Thread safety:** `Workbook`‑instanser är inte trådsäkra. Skapa en ny instans per tråd om du kör parallella jobb.
- **File locks:** Se till att mallen inte är öppen i Excel medan din kod körs; annars får du ett `IOException`.

> **Pro tip:** Behåll en kopia av originalmallen i en skrivskyddad mapp. Detta förhindrar oavsiktliga överskrivningar under felsökning.

---

## Fullt fungerande exempel – Sammanfattning

Här är hela programmet igen, den här gången med inline‑kommentarer för varje icke‑uppenbar rad:

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTemplateDemo
{
    class Program
    {
        static void Main()
        {
            // Path to the Excel template that contains SmartMarker tags.
            string templatePath = @"C:\MyProject\Templates\template.xlsx";

            // Load the workbook – this is the "create excel from template" step.
            Workbook wb = new Workbook(templatePath);

            // Read JSON data that maps directly to the template's tags.
            string jsonPath = @"C:\MyProject\Data\data.json";
            string json = File.ReadAllText(jsonPath);

            // OPTIONAL: tweak SmartMarker behavior (case‑sensitivity, empty rows, etc.).
            wb.SmartMarkerProcessor.Options.CaseSensitive = false;
            wb.SmartMarkerProcessor.Options.RemoveEmptyRows = true;

            // Set up dynamic worksheet naming based on the master record's Name field.
            wb.SmartMarkerProcessor.Options.DetailSheetNewName = "Detail_{Master.Name}";

            // Run the SmartMarker engine – this is where we "populate excel from json".
            wb.SmartMarkerProcessor.Execute(json);

            // Save the newly generated workbook – the final "generate excel using json" step.
            string outputPath = @"C:\MyProject\Output\output.xlsx";
            wb.Save(outputPath);

            Console.WriteLine("✅ Workbook created at: " + outputPath);
        }
    }
}
```

Att köra den här konsolappen kommer att producera `output.xlsx` med ett omdöpt detaljblad och all data ifylld.

---

## Nästa steg & relaterade ämnen

- **Export to PDF:** Efter att ha genererat arbetsboken kan du anropa `wb.Save("report.pdf", SaveFormat.Pdf);` för att leverera en PDF‑version.
- **Chart population:** SmartMarker stödjer också diagramdatakällor; bind bara JSON‑arrayen till diagrammets serieräckvidd.
- **Conditional formatting:** Använd Excels inbyggda regler i mallen; de kvarstår efter SmartMarker‑ersättning.
- **Performance tuning:** För högvolyms‑scenarier, återanvänd en enda `Workbook`‑instans med `Clone` för att undvika upprepade fil‑I/O.

Känn dig fri att experimentera med olika JSON‑strukturer, namnbytesmönster, eller till och med kombinera flera mallar i ett körning. Flexibiliteten med **create excel from template** med Aspose.Cells betyder att du kan anpassa lösningen till fakturor, instrumentpaneler eller vilket rapporteringsbehov som helst.

---

## Visuell sammanfattning

![Create Excel from Template workflow showing JSON → SmartMarker → Dynamic Sheet Naming](/images/create-excel-from-template-workflow.png "Create Excel from Template workflow diagram")

*(Alt‑texten innehåller primär nyckelord för SEO)*

---

### Sammanfattning

Vi har gått igenom allt du behöver för att **create Excel from template**, **map JSON to Excel**, **populate Excel from JSON**, använda **dynamic worksheet naming excel**, och slutligen **generate Excel using JSON**. Koden är komplett, förklaringarna visar *varför* varje rad är viktig, och du har nu en solid grund för att bygga större rapporterings‑pipelines.

Har du en variant du försöker implementera? Lämna en kommentar nedan, så felsöker vi tillsammans. Lycka till med kodandet!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}