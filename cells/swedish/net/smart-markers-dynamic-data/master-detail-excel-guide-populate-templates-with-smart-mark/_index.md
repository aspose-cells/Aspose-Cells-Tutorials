---
category: general
date: 2026-07-03
description: Master‑detail‑Excel‑handledning visar hur man fyller i en Excel‑mall
  och genererar Excel från mallen med Smart Markers – en snabb, kod‑först‑guide.
draft: false
keywords:
- master detail excel
- populate excel template
- generate excel from template
- use smart markers
- how to create master‑detail report
language: sv
og_description: Master‑detail‑excel‑handledning lär dig hur du fyller i en Excel‑mall
  och genererar Excel från mallen med Smart Markers i C#.
og_title: master‑detail Excel – Fyll i mallar med smarta markörer
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: master detail excel tutorial shows how to populate excel template and
    generate excel from template using Smart Markers – quick, code‑first guide.
  headline: master detail excel guide – populate templates with Smart Markers
  type: TechArticle
- description: master detail excel tutorial shows how to populate excel template and
    generate excel from template using Smart Markers – quick, code‑first guide.
  name: master detail excel guide – populate templates with Smart Markers
  steps:
  - name: '**Loading the template** – By keeping the template separate, you preserve
      formatting, formulas, and any static content. The `Workbook` constructor reads
      the file into memory without locking it, which is essential for web‑service
      scenarios.'
    text: '**Loading the template** – By keeping the template separate, you preserve
      formatting, formulas, and any static content. The `Workbook` constructor reads
      the file into memory without locking it, which is essential for web‑service
      scenarios.'
  - name: '**Hierarchical data model** – Smart Markers rely on *named* collections
      (`Master`, `Detail`). The anonymous type we create mirrors the relational structure:
      each master row can have multiple detail rows sharing the same `Id`. This is
      the same pattern you’d use with a DataSet or Entity Framework quer'
    text: '**Hierarchical data model** – Smart Markers rely on *named* collections
      (`Master`, `Detail`). The anonymous type we create mirrors the relational structure:
      each master row can have multiple detail rows sharing the same `Id`. This is
      the same pattern you’d use with a DataSet or Entity Framework quer'
  - name: '**SmartMarkerProcessor** – This class is the heart of the **use smart markers**
      feature. It parses the worksheet, builds an internal map of markers, and then
      iterates over the data model. You don’t need to manually loop through rows;
      the processor does it for you, guaranteeing correct cell merging a'
    text: '**SmartMarkerProcessor** – This class is the heart of the **use smart markers**
      feature. It parses the worksheet, builds an internal map of markers, and then
      iterates over the data model. You don’t need to manually loop through rows;
      the processor does it for you, guaranteeing correct cell merging a'
  - name: '**Process call** – The single `processor.Process(workbook, dataModel)`
      line triggers the expansion of both master and detail ranges. If your template
      includes grouping, totals, or conditional formatting, the processor respects
      those as well.'
    text: '**Process call** – The single `processor.Process(workbook, dataModel)`
      line triggers the expansion of both master and detail ranges. If your template
      includes grouping, totals, or conditional formatting, the processor respects
      those as well.'
  - name: '**Saving the result** – The final `Save` call writes a brand‑new file (`MasterDetail.xlsx`).
      Because the original template remains untouched, you can reuse it for subsequent
      runs—perfect for batch jobs.'
    text: '**Saving the result** – The final `Save` call writes a brand‑new file (`MasterDetail.xlsx`).
      Because the original template remains untouched, you can reuse it for subsequent
      runs—perfect for batch jobs.'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: Master‑detail Excel‑guide – fyll i mallar med Smart Markers
url: /sv/net/smart-markers-dynamic-data/master-detail-excel-guide-populate-templates-with-smart-mark/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# master detail excel – Fyll i en Excel‑mall med Smart Markers

Har du någonsin undrat hur du kan **master detail excel**‑rapportering utan att drunkna i manuellt copy‑paste? Du är inte ensam. I många företag är behovet av att producera en master‑detail‑rapport—tänk fakturor med radposter eller en produktkatalog med specifikationer—en daglig rutin. De goda nyheterna? Med några rader C# kan du automatiskt **populate excel template**‑filer, låta Smart Markers göra det tunga arbetet.

I den här handledningen går vi igenom ett komplett, körbart exempel som visar exakt **how to create master‑detail report** med Aspose.Cells Smart Marker‑motor. I slutet kommer du kunna **generate excel from template**‑filer på sekunder, och du kommer förstå varför varje steg görs så att du kan anpassa mönstret till dina egna datakällor.

## Vad du behöver

- .NET 6.0 eller senare (koden fungerar även med .NET Framework 4.6+)  
- Aspose.Cells för .NET NuGet‑paket (`Install-Package Aspose.Cells`)  
- En enkel Excel‑fil (`template.xlsx`) som innehåller Smart Markers som `{Master}` och `{Detail}`  
- En IDE efter eget val (Visual Studio, Rider, VS Code…)

> **Pro tip:** Behåll din mall i samma mapp som projektet för enkel sökvägshantering, eller använd en konfigurerbar inställning om du paketerar appen.

## master detail excel: Förbereda Smart Marker‑mallen

Smart Markers är platshållare som Aspose.Cells ersätter med data vid körning. För ett master‑detail‑scenario behöver du vanligtvis två markörer:

| Markör   | Syfte                              |
|----------|-----------------------------------|
| `{Master}` | Expanderar en rad för varje master‑post |
| `{Detail}` | Expanderar ett nästlat område för relaterade detaljer |

Öppna Excel, skriv in några statiska rubriker, och i raden där du vill ha master‑data skriver du `{Master.Id}` och `{Master.Name}`. Nedanför skapar du en sub‑tabell och placerar `{Detail.Id}` och `{Detail.Item}` i lämpliga celler. Spara filen som `template.xlsx`.

![exempel på master detail excel‑rapport](https://example.com/placeholder.png "exempel på master detail excel‑rapport")

*Bildtext: exempel på master detail excel‑rapport som visar Smart Marker‑platshållare.*

## Steg‑för‑steg kodgenomgång

Nedan är det fullständiga, fristående programmet. Vi delar upp det i logiska delar, förklarar resonemanget och pekar på vanliga fallgropar.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // Step 1: Load the Excel template that contains Smart Markers {Master}
        //         and {Detail}
        // -----------------------------------------------------------------
        var templatePath = @"YOUR_DIRECTORY/template.xlsx";
        Workbook workbook = new Workbook(templatePath);

        // -----------------------------------------------------------------
        // Step 2: Build a hierarchical data model (master collection + detail)
        // -----------------------------------------------------------------
        var dataModel = new
        {
            Master = new[]
            {
                new { Id = 1, Name = "Alpha" },
                new { Id = 2, Name = "Beta" }
            },
            Detail = new[]
            {
                new { Id = 1, Item = "Item X" },
                new { Id = 1, Item = "Item Y" },
                new { Id = 2, Item = "Item Z" }
            }
        };

        // -----------------------------------------------------------------
        // Step 3: Create a SmartMarkerProcessor – this is the engine that
        //         scans the workbook, finds markers, and injects data.
        // -----------------------------------------------------------------
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // -----------------------------------------------------------------
        // Step 4: Apply the data model to the workbook. The processor will
        //         automatically expand master‑detail ranges based on the
        //         relationships defined in the model.
        // -----------------------------------------------------------------
        processor.Process(workbook, dataModel);

        // -----------------------------------------------------------------
        // Step 5: Save the populated workbook – now you have a ready‑to‑use
        //         master‑detail Excel file.
        // -----------------------------------------------------------------
        var outputPath = @"YOUR_DIRECTORY/MasterDetail.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine("Excel file generated successfully at: " + outputPath);
    }
}
```

### Varför den här strukturen fungerar

1. **Loading the template** – Genom att hålla mallen separat bevaras formatering, formler och allt statiskt innehåll. `Workbook`‑konstruktorn läser in filen i minnet utan att låsa den, vilket är viktigt för webb‑tjänst‑scenarier.

2. **Hierarchical data model** – Smart Markers förlitar sig på *namngivna* samlingar (`Master`, `Detail`). Den anonyma typen vi skapar speglar den relationella strukturen: varje master‑rad kan ha flera detail‑rader som delar samma `Id`. Detta är samma mönster som du skulle använda med ett DataSet eller Entity Framework‑frågeresultat.

3. **SmartMarkerProcessor** – Denna klass är kärnan i **use smart markers**‑funktionen. Den analyserar kalkylbladet, bygger en intern karta över markörer och itererar sedan över datamodellen. Du behöver inte loopa manuellt genom rader; processorn gör det åt dig och garanterar korrekt cellsammanfogning och stilbevarande.

4. **Process call** – Den enda raden `processor.Process(workbook, dataModel)` triggar expansionen av både master‑ och detail‑områden. Om din mall innehåller gruppering, totaler eller villkorsstyrd formatering respekterar processorn dem också.

5. **Saving the result** – Det sista `Save`‑anropet skriver en helt ny fil (`MasterDetail.xlsx`). Eftersom den ursprungliga mallen förblir orörd kan du återanvända den för efterföljande körningar—perfekt för batch‑jobb.

### Särskilda fall & hur du hanterar dem

| Situation                               | Vad att hålla utkik efter                              | Föreslagen lösning |
|----------------------------------------|--------------------------------------------------------|--------------------|
| Ingen matchande detaljrader för en master | Detaljblocket blir tomt, men master‑raden visas fortfarande. | Se till att ditt LINQ‑ eller datakälla returnerar en tom samling istället för `null`. |
| Stora datamängder (10 000+ rader)      | Minnesanvändningen kan öka kraftigt under bearbetning. | Använd `SmartMarkerProcessor` med `SmartMarkerOptions` för att aktivera streaming (`processor.Options = new SmartMarkerOptions { UseFastProcessing = true };`). |
| Anpassad formatering på detaljrader    | Formatering kan gå förlorad om mallraden inte är formaterad. | Applicera önskad stil på den *första* detalj‑raden i mallen; processorn klonar den för varje ny rad. |
| Behöver infoga en totalsumma‑rad        | Smart Markers beräknar inte totaler automatiskt. | Lägg till en vanlig Excel‑formel i mallen som refererar till det expanderade området (t.ex. `=SUM(C2:C{Detail.RowCount})`). |

## populate excel template: Testa resultatet

Kör programmet. Öppna `MasterDetail.xlsx` och du bör se något liknande:

| Id | Namn | Id (Detalj) | Artikel |
|----|------|-------------|---------|
| 1  | Alpha | 1           | Item X |
|    |       | 1           | Item Y |
| 2  | Beta  | 2           | Item Z |

Observera hur master‑raderna (`Alpha`, `Beta`) förblir sammanslagna över detaljkollumnerna, vilket ger en ren master‑detail‑visualisering. Alla formler, villkorsformat och kolumnbredder från den ursprungliga mallen bevaras.

Om du inte ser de förväntade raderna, dubbelkolla:

- Att markörnamnen matchar egenskapsnamnen i datamodellen (skiftlägeskänsligt).  
- Att mallens markörceller är *inom* en tabell eller ett namngivet område; annars kan processorn behandla dem som isolerade celler.  

## generate excel from template: Utöka mönstret

När du har bemästrat grunderna kan du enkelt anpassa koden för mer komplexa scenarier:

- **Multiple master tables** – Lägg till en annan samling (t.ex. `Orders`) och motsvarande markörer (`{Orders}`) i ett separat kalkylblad.  
- **Dynamic worksheets** – Skapa ett nytt `Worksheet` vid körning, kopiera mallbladet och kör sedan `processor.Process` på det nya bladet.  
- **Web API endpoint** – Returnera den genererade arbetsboken som ett `FileResult` (`return File(workbook.SaveToStream(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");`).  

Alla dessa följer samma **populate excel template**‑princip: ladda, binda, bearbeta, spara.

## Hur man skapar master‑detail‑rapport: Vanliga frågor

**Q: Behöver jag installera Microsoft Office på servern?**  
Nej. Aspose.Cells är ett rent .NET‑bibliotek; det fungerar utan Office, vilket är idealiskt för CI/CD‑pipelines.

**Q: Kan jag använda en DataTable istället för en anonym typ?**  
Absolut. Processorn accepterar vilken `IEnumerable` eller `DataTable` som helst så länge egenskaps‑/kolumnnamnen matchar markörerna.

**Q: Vad händer om mina detaljrader behöver ett löpnummer?**  
Infoga en Smart Marker som `{Detail.RowNumber}`; motorn levererar automatiskt ett sekventiellt index för varje expanderad rad.

**Q: Är det möjligt att lokalisera den genererade Excel‑filen?**  
Ja. Placera din statiska text (rubriker, titlar) i mallen på målspråket och låt sedan Smart Markers fylla i de dynamiska delarna. Ingen extra kod behövs.

## Slutsats

Vi har just byggt en **master detail excel**‑lösning som **populate excel template**‑filer, **generate excel from template**, och fullt **use smart markers** för **how to create master‑detail report** på ett rent, underhållbart sätt. Metoden eliminerar repetitiv Excel‑automatiseringskod, garanterar stilkonsekvens och skalar från ett fåtal rader till tiotusentals.

Nästa steg, prova att lägga till diagram som refererar till de nyss skapade tabellerna, eller anslut en riktig databasfråga till konstruktionen av `dataModel`. Samma mönster gäller oavsett om du skapar fakturor, lagerlistor eller analytiska instrumentpaneler.

Har du en variant du vill dela? Lägg en kommentar, och lycka till med kodandet!

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Generera dynamiska Excel‑rapporter med Aspose.Cells .NET Smart Markers](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Behärska dynamisk Excel‑rapportering: Smart Markers & diagram med Aspose.Cells för .NET](/cells/english/net/templates-reporting/dynamic-excel-reports-aspose-cells-net/)
- [Behärska Aspose.Cells .NET Smart Markers för dataintegration i Excel](/cells/english/net/import-export/mastering-data-integration-aspose-cells-smart-markers/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}