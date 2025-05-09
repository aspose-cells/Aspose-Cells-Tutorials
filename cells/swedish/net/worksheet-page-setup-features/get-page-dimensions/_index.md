---
"description": "Lär dig hur du får sidmått i ett Excel-ark med Aspose.Cells för .NET. En steg-för-steg-guide för att anpassa pappersstorlekarna A2, A3, A4 och Letter."
"linktitle": "Hämta siddimensioner för arbetsblad"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Hämta siddimensioner för arbetsblad"
"url": "/sv/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hämta siddimensioner för arbetsblad

## Introduktion
Om du arbetar med Excel-filer programmatiskt med Aspose.Cells för .NET kan det finnas tillfällen då du behöver komma åt och ställa in siddimensioner för ett kalkylblad. Att känna till dimensionerna kan hjälpa till med layouter, utskrift och anpassning av Excel-ark för specifika ändamål. I den här artikeln utforskar vi hur man hämtar och visar olika siddimensioner i Excel med Aspose.Cells för .NET. Vi går igenom en steg-för-steg-handledning för att se till att du har alla detaljer för att komma igång med säkerhet.
## Förkunskapskrav
Innan vi börjar, låt oss se till att du har allt du behöver för att följa den här handledningen.
1. Aspose.Cells för .NET: Se till att du har Aspose.Cells för .NET installerat. Du kan [ladda ner biblioteket här](https://releases.aspose.com/cells/net/) eller installera den via NuGet i ditt .NET-projekt.
2. .NET-miljö: En kompatibel .NET-utvecklingsmiljö (t.ex. Visual Studio).
3. Licensinställningar: För att få full funktionalitet i Aspose.Cells, tillämpa en licens. Du kan [begär en kostnadsfri tillfällig licens](https://purchase.aspose.com/temporary-license/) för utvärderingsändamål.
Börja med den kostnadsfria testversionen av Aspose.Cells om du utvärderar det för första gången.
## Importera paket
Innan vi går in i koden måste du importera namnrymden Aspose.Cells till ditt projekt för att komma åt alla nödvändiga klasser och metoder.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Låt oss dela upp processen i enkla steg. Här kommer vi att få tillgång till olika pappersstorlekar, tillämpa dem på ett arbetsblad och skriva ut måtten för varje.
## Steg 1: Skapa en arbetsboksinstans
Det första steget är att skapa en instans av `Workbook` klass. Det här objektet kommer att fungera som vår huvudsakliga arbetsbok som innehåller arbetsblad som vi kan manipulera.
```csharp
Workbook book = new Workbook();
```
Tänka på `Workbook` som huvudbehållare för din Excel-fil. Vi behöver den för att komma åt och kontrollera enskilda kalkylblad.
## Steg 2: Öppna det första arbetsbladet
Nu ska vi öppna det första kalkylbladet i arbetsboken. Som standard kommer en ny arbetsbok med ett enda ark, så vi kan referera direkt till det med hjälp av ett index över `0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
De `Worksheets` samling i `Workbook` låter oss komma åt varje kalkylblad via index. Här hämtar vi det första arket för att börja ställa in sidmått.
## Steg 3: Ställ in pappersstorlek till A2 och visa mått
Nu när vi har tillgång till vårt kalkylblad ställer vi in dess pappersstorlek till A2. Att ställa in pappersstorleken är användbart för att formatera sidan innan du skriver ut eller exporterar den. När vi har ställt in pappersstorleken skriver vi ut sidans mått i tum.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Här ändrar vi `PaperSize` egendom till `PaperA2`Efter att du har ställt in storleken, `PageSetup.PaperWidth` och `PageSetup.PaperHeight` hämta bredden och höjden på arket i tum. Detta ger oss en snabb överblick över sidans dimensioner.
## Steg 4: Ställ in pappersstorlek till A3 och visa mått
Genom att följa samma steg som ovan justerar vi sidmåtten till A3-storlek. Denna ändring är användbar för något större utskrifter eller för att få plats med mer innehåll på en sida.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3-formatet är dubbelt så stort som A4, vilket gör det till ett bra val för stora tabeller eller detaljerade diagram. Att ändra pappersstorleken hjälper till att anpassa kalkylbladets layout därefter.
## Steg 5: Ställ in pappersstorlek till A4 och visningsmått
Nu ställer vi in pappersstorleken på A4. Detta är den vanligaste sidstorleken för utskrift av dokument. Vi visar de uppdaterade måtten senare.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Om ditt mål är ett standarddokumentformat är A4 vanligtvis den lämpligaste storleken. Att känna till måtten kan hjälpa till att justera innehållslayouten för att undvika utskriftsproblem.
## Steg 6: Ställ in pappersstorlek till Letter och visa mått
Slutligen ställer vi in pappersstorleken till Letter-formatet, vilket är vanligt förekommande i Nordamerika. Låt oss skriva ut måtten en sista gång.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Letter-storleken används ofta för dokument i Nordamerika, så det är bra att ställa in den här storleken när man samarbetar med team eller kunder där.
## Slutsats
den här handledningen gick vi igenom hur man ställer in och hämtar sidmått för olika pappersstorlekar med hjälp av Aspose.Cells för .NET. Genom att konfigurera sidstorlekar som A2, A3, A4 och Letter kan du formatera Excel-kalkylblad för att passa specifika utskrifts- och layoutbehov. Denna kontroll över sidmåtten är särskilt värdefull för professionell rapportering och presentation, eftersom den säkerställer att ditt innehåll passar perfekt på varje sidstorlek.
## Vanliga frågor
### Hur kan jag ändra sidans orientering i Aspose.Cells?  
Du kan ändra orienteringen med hjälp av `PageSetup.Orientation` egenskapen, och ställ in den på antingen `PageOrientationType.Pellertrait` or `PageOrientationType.Landscape`.
### Kan jag ange anpassade siddimensioner i Aspose.Cells?  
Ja, du kan ange anpassade sidmått genom att justera marginalerna och skalningsalternativen under `PageSetup` för mer kontroll.
### Vilken är standardpappersstorleken i Aspose.Cells?  
Standardpappersstorleken är vanligtvis A4. Detta kan dock bero på regionala inställningar och kan justeras efter behov.
### Är det möjligt att förhandsgranska sidlayouter i Aspose.Cells?  
Även om Aspose.Cells inte erbjuder en grafisk förhandsgranskning, kan du programmatiskt konfigurera layouter och använda förhandsgranskningar i Excel.
### Hur installerar jag Aspose.Cells för .NET?  
Du kan installera Aspose.Cells med hjälp av NuGet Package Manager i Visual Studio eller ladda ner DLL-filen från [Aspose.Cells nedladdningssida](https://releases.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}