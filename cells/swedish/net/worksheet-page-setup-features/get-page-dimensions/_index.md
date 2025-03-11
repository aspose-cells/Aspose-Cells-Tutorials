---
title: Hämta sidmått för arbetsblad
linktitle: Hämta sidmått för arbetsblad
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du får siddimensioner i ett Excel-kalkylblad med Aspose.Cells för .NET. En steg-för-steg-guide för att anpassa pappersstorlekarna A2, A3, A4 och Letter.
weight: 13
url: /sv/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta sidmått för arbetsblad

## Introduktion
Om du arbetar med Excel-filer programmatiskt med Aspose.Cells för .NET, kan det finnas tillfällen du behöver komma åt och ställa in siddimensioner för ett kalkylblad. Att känna till måtten kan hjälpa till med layouter, utskrift och anpassning av Excel-ark för specifika ändamål. I den här artikeln kommer vi att utforska hur du hämtar och visar olika siddimensioner i Excel med Aspose.Cells för .NET. Vi kommer att gå igenom en steg-för-steg handledning för att se till att du har alla detaljer för att komma igång med säkerhet.
## Förutsättningar
Innan du dyker in, låt oss se till att du har allt du behöver följa tillsammans med den här handledningen.
1.  Aspose.Cells for .NET: Se till att du har Aspose.Cells for .NET installerat. Du kan[ladda ner biblioteket här](https://releases.aspose.com/cells/net/) eller installera det via NuGet i ditt .NET-projekt.
2. .NET-miljö: En kompatibel .NET-utvecklingsmiljö (t.ex. Visual Studio).
3.  Licensinställningar: För full funktionalitet av Aspose.Cells, tillämpa en licens. Du kan[begära en gratis tillfällig licens](https://purchase.aspose.com/temporary-license/) i utvärderingssyfte.
Börja med den kostnadsfria testversionen av Aspose.Cells om du utvärderar den för första gången.
## Importera paket
Innan vi hoppar in i koden måste du importera Aspose.Cells-namnrymden till ditt projekt för att komma åt alla nödvändiga klasser och metoder.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Låt oss dela upp processen i enkla steg. Här kommer vi åt olika pappersstorlekar, applicerar dem på ett kalkylblad och skriver ut måtten för varje.
## Steg 1: Skapa en arbetsboksinstans
 Det första steget är att skapa en instans av`Workbook` klass. Detta objekt kommer att fungera som vår huvudarbetsbok som innehåller kalkylblad som vi kan manipulera.
```csharp
Workbook book = new Workbook();
```
 Tänka på`Workbook` som huvudbehållare för din Excel-fil. Vi behöver det för att komma åt och kontrollera enskilda arbetsblad.
## Steg 2: Öppna det första arbetsbladet
 Låt oss sedan komma åt det första kalkylbladet i arbetsboken. Som standard kommer en ny arbetsbok med ett ark, så vi kan direkt referera till den med hjälp av ett index av`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
 De`Worksheets` samling i`Workbook` tillåter oss att komma åt varje kalkylblad per index. Här tar vi tag i det första arket för att börja ställa in sidmått.
## Steg 3: Ställ in pappersstorlek till A2 och skärmmått
Nu när vi har tillgång till vårt kalkylblad, låt oss ställa in dess pappersstorlek till A2. Att ställa in pappersstorleken är användbart för att formatera sidan innan du skriver ut eller exporterar den. När vi har ställt in pappersstorleken skriver vi ut sidmåtten i tum.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
 Här ändrar vi`PaperSize` egendom till`PaperA2` . Efter att ha ställt in storleken,`PageSetup.PaperWidth` och`PageSetup.PaperHeight` hämta arkets bredd och höjd i tum. Detta ger oss en snabb överblick över siddimensionerna.
## Steg 4: Ställ in pappersstorlek till A3 och skärmmått
Genom att följa samma steg som ovan, låt oss justera sidmåtten till A3-storlek. Denna ändring är användbar för lite större utskrifter eller för att passa in mer innehåll på en sida.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3-storleken är dubbelt så stor som A4, vilket gör den till ett bra val för stora bord eller detaljerade diagram. Genom att ändra pappersstorleken kan du anpassa kalkylbladets layout därefter.
## Steg 5: Ställ in pappersstorlek till A4 och skärmmått
Låt oss nu ställa in pappersstorleken till A4. Detta är den vanligaste sidstorleken för utskrift av dokument. Vi visar de uppdaterade måtten efteråt.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Om ditt mål är ett standarddokumentformat är A4 vanligtvis den lämpligaste storleken. Att känna till måtten kan hjälpa till att justera innehållslayouten för att undvika utskriftsproblem.
## Steg 6: Ställ in pappersstorlek till Letter och skärmmått
Slutligen ställer vi in pappersstorleken till Letter-formatet, som vanligtvis används i Nordamerika. Låt oss skriva ut måtten en sista gång.
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
Letter-storleken används ofta för dokument i Nordamerika, så att ställa in den här storleken hjälper när du samarbetar med team eller kunder som är baserade där.
## Slutsats
den här handledningen gick vi igenom hur man ställer in och hämtar sidmått för olika pappersstorlekar med Aspose.Cells för .NET. Genom att konfigurera sidstorlekar som A2, A3, A4 och Letter kan du formatera Excel-kalkylblad för att passa specifika utskrifts- och layoutbehov. Denna kontroll över siddimensioner är särskilt värdefull för professionell rapportering och presentation, eftersom den säkerställer att ditt innehåll passar perfekt på varje sidstorlek.
## FAQ's
### Hur kan jag ändra orienteringen på sidan i Aspose.Cells?  
 Du kan ändra orienteringen med hjälp av`PageSetup.Orientation` egenskap och ställer in den på antingen`PageOrientationType.Portrait` eller`PageOrientationType.Landscape`.
### Kan jag ställa in anpassade siddimensioner i Aspose.Cells?  
 Ja, du kan ställa in anpassade siddimensioner genom att justera marginalerna och skalningsalternativen under`PageSetup` för mer kontroll.
### Vilken är standardpappersstorleken i Aspose.Cells?  
Standardpappersstorleken är vanligtvis A4. Detta kan dock bero på regionala inställningar och kan justeras efter behov.
### Är det möjligt att förhandsgranska sidlayouter i Aspose.Cells?  
Även om Aspose.Cells inte erbjuder en grafisk förhandsgranskning, kan du programmerat ställa in layouter och använda förhandsvisningar i Excel.
### Hur installerar jag Aspose.Cells för .NET?  
 Du kan installera Aspose.Cells med NuGet Package Manager i Visual Studio eller ladda ner DLL från[Aspose.Cells nedladdningssida](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
