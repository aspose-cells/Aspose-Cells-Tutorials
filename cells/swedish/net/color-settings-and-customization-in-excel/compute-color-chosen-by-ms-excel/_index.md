---
"description": "Lär dig hur du beräknar färgen som valts av MS Excel med hjälp av Aspose.Cells för .NET. Följ den här steg-för-steg-guiden för att få åtkomst till Excels villkorsstyrda formateringsfärg programmatiskt."
"linktitle": "Beräkna färg vald av MS Excel programmatiskt"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Beräkna färg vald av MS Excel programmatiskt"
"url": "/sv/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Beräkna färg vald av MS Excel programmatiskt

## Introduktion
Har du någonsin arbetat med Excel-filer och undrat hur vissa färger automatiskt väljs för formatering? Du är inte ensam. Excels villkorsstyrda formatering kan vara lite av ett mysterium, särskilt när man försöker extrahera exakt den färg som Excel tilldelar. Men oroa dig inte, vi har det du behöver! I den här handledningen går vi djupare in på hur man programmatiskt beräknar färgen som väljs av MS Excel med hjälp av Aspose.Cells för .NET. Vi går igenom det steg för steg, så att du enkelt kan följa med och tillämpa det i dina egna projekt. Nu sätter vi igång!
## Förkunskapskrav
Innan vi går in i koden, låt oss gå igenom vad du behöver för att följa den här handledningen:
- Aspose.Cells för .NET installerat. Om du inte redan har det kan du göra det. [ladda ner den här](https://releases.aspose.com/cells/net/).
- Goda kunskaper i C# och .NET framework.
- Ett exempel på en Excel-fil (Book1.xlsx) med villkorsstyrd formatering.
Du kan också prova den kostnadsfria testversionen av Aspose.Cells för .NET om du inte redan har en licens. Hämta testversionen. [här](https://releases.aspose.com/).
## Importera paket
Innan vi börjar koda behöver vi importera de nödvändiga paketen för att säkerställa att allt går smidigt. Se till att du inkluderar följande namnrymder i ditt projekt:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Dessa importer ger åtkomst till de huvudsakliga Aspose.Cells-klasserna och .NET:s inbyggda systemritbibliotek för hantering av färger.

Nu när vi har allt på plats, låt oss dela upp uppgiften i lättsmälta steg:
## Steg 1: Konfigurera arbetsboksobjektet
Det första vi behöver göra är att instansiera en `Workbook` objektet och ladda Excel-filen vi vill arbeta med. Det är här resan börjar!
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instansiera ett arbetsboksobjekt och öppna mallfilen
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
I det här steget skapar vi en ny instans av `Workbook` klassen från Aspose.Cells. Den `Workbook` klassen representerar en Excel-fil, och genom att ange sökvägen till vår fil kan vi enkelt ladda den för vidare manipulation.
## Steg 2: Öppna det första arbetsbladet
När arbetsboken är laddad behöver vi komma åt det specifika arbetsbladet där vi vill extrahera färgen. I det här exemplet arbetar vi med det första arket.
```csharp
// Hämta det första arbetsbladet
Worksheet worksheet = workbook.Worksheets[0];
```
Här hämtar vi det första arbetsbladet i arbetsboken med hjälp av `Worksheets[0]` Med Aspose.Cells kan du komma åt vilket kalkylblad som helst i Excel-filen via dess index eller namn.
## Steg 3: Markera den aktuella cellen
Härnäst ska vi välja en specifik cell i kalkylbladet. I den här handledningen fokuserar vi på cell "A1", men du kan välja vilken cell som helst med villkorsstyrd formatering.
```csharp
// Hämta A1-cellen
Cell a1 = worksheet.Cells["A1"];
```
Vi använder `Cells` egenskapen för att referera till en specifik cell med dess adress. I det här fallet markerar vi cell "A1" eftersom vi vill extrahera resultaten av villkorsstyrd formatering som tillämpats på den här cellen.
## Steg 4: Hämta resultatet av villkorlig formatering
Nu händer magin! Vi använder Aspose.Cells för att hämta resultatet av villkorsstyrd formatering för den markerade cellen. Så här beräknar Excel formateringen dynamiskt, inklusive färger.
```csharp
// Hämta det resulterande objektet för villkorlig formatering
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
De `GetConditionalFormattingResult()` Metoden är avgörande i det här steget. Den returnerar ett objekt som innehåller resultaten av all villkorsstyrd formatering som tillämpats på cellen. Det är här vi börjar utnyttja färginformationen som Excel använder.
## Steg 5: Få åtkomst till ColorScaleResult
När vi har resultatet av villkorsstyrd formatering kan vi gräva djupare och komma åt färgskalan som Excel använde för just den här cellen.
```csharp
// Hämta det resulterande färgobjektet i ColorScale
Color c = cfr1.ColorScaleResult;
```
Villkorsstyrd formatering i Excel använder ofta färgskalor. Den här raden låter oss extrahera den resulterande färgen som tillämpades baserat på reglerna för villkorsstyrd formatering.
## Steg 6: Mata ut färginformationen
Slutligen vill vi se vilken färg som används i Excel. Låt oss skriva ut färginformationen i ett format som är lätt att förstå, inklusive både ARGB-värdet och namnet.
```csharp
// Läs färgen
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
De `ToArgb()` metoden ger oss färgen i ARGB-format (Alfa, Röd, Grön, Blå), medan `Name` egenskapen ger färgnamnet i ett mer lättläst format. Du kan använda dessa färgdetaljer för att matcha dem i andra program eller modifiera dina Excel-filer programmatiskt.

## Slutsats
Och där har du det! Genom att följa dessa steg har du precis lärt dig hur du programmatiskt beräknar färgen som valts av MS Excel med hjälp av Aspose.Cells för .NET. Denna metod kan vara otroligt användbar för att automatisera Excel-baserade uppgifter, särskilt när du arbetar med komplex villkorsstyrd formatering. Nu, nästa gång du stöter på en mystisk färg i Excel, vet du exakt hur du avslöjar dess hemligheter.
## Vanliga frågor
### Kan jag tillämpa villkorsstyrd formatering programmatiskt med Aspose.Cells?
Ja, Aspose.Cells låter dig tillämpa, ändra och till och med ta bort villkorsstyrd formatering i Excel-filer programmatiskt.
### Stöder Aspose.Cells alla versioner av Excel?
Absolut! Aspose.Cells stöder Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) och fler format, inklusive PDF, HTML och CSV.
### Är Aspose.Cells tillgängligt för andra plattformar än .NET?
Ja, Aspose.Cells är tillgängligt för olika plattformar, inklusive Java, C++ och Android via Java.
### Hur kan jag få en gratis provversion av Aspose.Cells?
Du kan ladda ner en gratis testversion av Aspose.Cells för .NET från [här](https://releases.aspose.com/).
### Hur hanterar jag stora Excel-filer med Aspose.Cells?
Aspose.Cells är optimerad för prestanda, även vid hantering av stora filer. Du kan använda streaming-API:er för att hantera stora datamängder effektivt.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}