---
title: Uppdatera Power Query formelobjekt i arbetsbok
linktitle: Uppdatera Power Query formelobjekt i arbetsbok
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du uppdaterar Power Query-formler i Excel med Aspose.Cells för .NET i den här omfattande steg-för-steg-guiden.
weight: 27
url: /sv/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Uppdatera Power Query formelobjekt i arbetsbok

## Introduktion
Att förstå hur man hanterar data effektivt med Power Query i Excel är avgörande för alla dataanalytiker eller Excel-entusiaster. Om du någonsin har behövt uppdatera formelobjekten i din Power Query-arbetsbok är du på rätt plats. Den här guiden är skräddarsydd för att hjälpa dig lära dig hur du använder Aspose.Cells för .NET för att sömlöst uppdatera Power Query-formler i en Excel-arbetsbok. Med några enkla steg kommer du att kunna manipulera och effektivisera dina data och se till att dina arbetsböcker förblir dynamiska och centraliserade.
## Förutsättningar
Innan du börjar dyka in i exempelkoden och stegen, låt oss gå igenom vad du behöver:
1. Grundläggande förståelse för C# och .NET: Bekantskap med programmeringskoncept i C# kommer att vara fördelaktigt eftersom vi kommer att skriva lite kod.
2.  Installera Aspose.Cells för .NET: Du måste ha Aspose.Cells-biblioteket integrerat i ditt .NET-projekt. Du kan ladda ner den[här](https://releases.aspose.com/cells/net/).
3. En Excel-fil redo för ändring: Se till att du har en Excel-fil som innehåller en Power Query som du vill uppdatera. Du måste ha ett exempel på arbetsboken`SamplePowerQueryFormula.xlsx` till ditt förfogande.
## Importera paket
För att komma igång, se till att du har följande namnrymder inkluderade i din C#-fil:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Detta ger dig tillgång till funktionerna som tillhandahålls av Aspose.Cells-biblioteket, särskilt för att arbeta med arbetsböcker och Power Query-data.
## Steg 1: Konfigurera dina arbetskataloger
Först och främst måste du definiera var dina käll- och utdatafiler finns. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
 I det här steget anger du katalogsökvägarna. Ersätta`"Your Document Directory"` med den faktiska sökvägen där dina Excel-filer sparas. Detta talar om för programmet var det ska leta efter din källfil och var den uppdaterade filen ska sparas.
## Steg 2: Ladda arbetsboken
Nu när du har dina arbetskataloger inställda är nästa steg att ladda din Excel-fil i programmet.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Här skapar du en`Workbook` objekt som laddar den angivna Excel-filen. De`Workbook`klass är en del av Aspose.Cells-biblioteket och är avgörande för alla operationer du ska utföra på den Excel-filen.
## Steg 3: Få åtkomst till Power Query-data
När arbetsboken har laddats är det dags att komma åt Power Query-formlerna som finns lagrade i.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 I den här raden`DataMashup` egenskapen hjälper till att komma åt Power Query-datastrukturerna i arbetsboken. Den här egenskapen ger dig möjlighet att interagera med olika aspekter av Power Query-data som finns i din Excel-fil.
## Steg 4: Loop Through Power Query-formler
Med Power Query-data tillgänglig är nästa steg att iterera genom var och en av de närvarande formlerna.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
 Det är här magin händer. Vi går igenom var och en`PowerQueryFormula` och sedan genom varje`PowerQueryFormulaItem` . De`if` satsen letar efter formelobjektet med namnet "Source" och uppdaterar dess värde till att vara sökvägen till källfilen som du vill att Power Query ska referera till. Detta gör att du dynamiskt kan ändra vilken fil Power Query hämtar data från.
## Steg 5: Spara den uppdaterade arbetsboken
Efter att ha uppdaterat de nödvändiga formelobjekten är ditt sista steg att spara arbetsboken.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Den här raden sparar den ändrade arbetsboken till en ny fil, och bevarar därmed originalet samtidigt som du kan arbeta med den uppdaterade versionen.
## Steg 6: Bekräftelsemeddelande
Slutligen är det bra att kontrollera om din kod har körts korrekt.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Detta enkla meddelande kommer att bekräfta för dig i konsolen att din operation lyckades, vilket ger ett lugnande slut på processen.
## Slutsats
Och där har du det! Att uppdatera Power Query-formelobjekt i Excel med Aspose.Cells för .NET kan göras med bara några enkla steg. Genom att följa den här guiden kan du effektivt hantera dina Excel-dataanslutningar och hålla dina arbetsböcker igång smidigt. Oavsett om du är ett erfaret proffs eller precis har börjat med datamanipulation, erbjuder Aspose.Cells ett kraftfullt sätt att automatisera och förbättra Excel-arbetsflöden. 
## FAQ's
### Kan jag använda Aspose.Cells med någon version av .NET?
Aspose.Cells är kompatibel med flera versioner av .NET, inklusive .NET Framework och .NET Core.
### Är Aspose.Cells gratis att använda?
 Aspose.Cells erbjuder en gratis provperiod, men för kontinuerlig användning krävs en licens. Du kan få en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).
### Vad händer om min befintliga Excel-fil inte har Power Query?
Processen som beskrivs fokuserar på att uppdatera Power Query-objekt, så om din fil saknar dem måste du först inkorporera Power Queries.
### Var kan jag hitta mer information om Aspose.Cells?
 Kontrollera dokumentationen för omfattande vägledning och exempel. Besök[dokumentation](https://reference.aspose.com/cells/net/).
### Hur rapporterar jag buggar eller problem med Aspose.Cells?
Du kan kontakta deras stödda forum för att få hjälp angående eventuella problem du stöter på.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
