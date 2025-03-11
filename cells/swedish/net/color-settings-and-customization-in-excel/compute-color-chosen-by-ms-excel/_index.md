---
title: Beräkna färg vald av MS Excel Programmatiskt
linktitle: Beräkna färg vald av MS Excel Programmatiskt
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du beräknar färgen vald av MS Excel med Aspose.Cells för .NET. Följ den här steg-för-steg-guiden för att komma åt Excels villkorliga formateringsfärg programmatiskt.
weight: 10
url: /sv/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Beräkna färg vald av MS Excel Programmatiskt

## Introduktion
Har du någonsin arbetat med Excel-filer och undrat hur vissa färger automatiskt väljs för formatering? Du är inte ensam. Excels villkorliga formatering kan vara lite av ett mysterium, särskilt när man försöker extrahera den exakta färgen som Excel tilldelar. Men oroa dig inte, vi har dig täckt! I den här handledningen kommer vi att dyka djupt in i hur man programmässigt beräknar färgen som valts av MS Excel med Aspose.Cells för .NET. Vi delar upp det steg för steg, så att du enkelt kan följa med och tillämpa det på dina egna projekt. Låt oss komma igång!
## Förutsättningar
Innan vi dyker in i koden, låt oss täcka vad du behöver för att följa denna handledning:
-  Aspose.Cells för .NET installerat. Om du inte har det än så kan du[ladda ner den här](https://releases.aspose.com/cells/net/).
- En praktisk kunskap om C# och .NET framework.
- Ett exempel på Excel-fil (Book1.xlsx) med viss villkorlig formatering tillämpad.
Du kan också prova den kostnadsfria testversionen av Aspose.Cells för .NET om du inte redan har en licens. Ta provversionen[här](https://releases.aspose.com/).
## Importera paket
Innan vi börjar koda måste vi importera de nödvändiga paketen för att säkerställa att allt fungerar smidigt. Se till att du inkluderar följande namnrymder i ditt projekt:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Dessa importer ger tillgång till de viktigaste Aspose.Cells-klasserna och .NET:s inbyggda systemritningsbibliotek för hantering av färger.

Nu när vi har allt på plats, låt oss dela upp den här uppgiften i lättsmälta steg:
## Steg 1: Ställ in arbetsboksobjektet
 Det första vi behöver göra är att instansiera en`Workbook` objekt och ladda Excel-filen vi vill arbeta med. Det är här resan börjar!
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instantiera ett arbetsboksobjekt och öppna mallfilen
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
 I det här steget skapar vi en ny instans av`Workbook` klass från Aspose.Cells. De`Workbook`klass representerar en Excel-fil, och genom att tillhandahålla sökvägen till vår fil kan vi enkelt ladda den för vidare manipulation.
## Steg 2: Öppna det första arbetsbladet
När arbetsboken har laddats måste vi komma åt det specifika kalkylbladet där vi vill extrahera färgen. I det här exemplet kommer vi att arbeta med det första arket.
```csharp
// Skaffa det första arbetsbladet
Worksheet worksheet = workbook.Worksheets[0];
```
 Här hämtar vi det första kalkylbladet i arbetsboken med hjälp av`Worksheets[0]` index. Aspose.Cells låter dig komma åt alla kalkylblad i Excel-filen genom dess index eller namn.
## Steg 3: Välj cellen av intresse
Därefter väljer vi en specifik cell i kalkylbladet. För den här handledningen kommer vi att fokusera på cell "A1", men du kan välja vilken cell som helst med villkorlig formatering.
```csharp
// Skaffa A1-cellen
Cell a1 = worksheet.Cells["A1"];
```
 Vi använder`Cells` egenskap för att referera till en specifik cell genom dess adress. I det här fallet väljer vi cell "A1" eftersom vi vill extrahera de villkorliga formateringsresultaten som tillämpas på den här cellen.
## Steg 4: Hämta resultatet för villkorlig formatering
Nu, här är där magin händer! Vi använder Aspose.Cells för att ta tag i resultatet av villkorlig formatering för den valda cellen. Så här beräknar Excel formateringen dynamiskt, inklusive färger.
```csharp
// Hämta det resulterande objektet för villkorlig formatering
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
 De`GetConditionalFormattingResult()` Metoden är avgörande i detta steg. Den returnerar ett objekt som innehåller resultaten av eventuell villkorlig formatering som tillämpas på cellen. Det är här vi börjar ta del av färginformationen som Excel använder.
## Steg 5: Öppna ColorScaleResult
När vi har det villkorliga formateringsresultatet kan vi gräva djupare och komma åt färgskalan som Excel använde för just den här cellen.
```csharp
// Hämta det resulterande färgobjektet i ColorScale
Color c = cfr1.ColorScaleResult;
```
Villkorlig formatering i Excel bygger ofta på färgskalor. Den här raden låter oss extrahera den resulterande färgen som tillämpades baserat på reglerna för villkorlig formatering.
## Steg 6: Mata ut färginformationen
Slutligen vill vi se färgen Excel tillämpas. Låt oss skriva ut färgdetaljerna i ett format som är lätt att förstå, inklusive både dess ARGB-värde och dess namn.
```csharp
// Läs färgen
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
 De`ToArgb()` metoden ger oss färgen i ARGB-format (alfa, röd, grön, blå), medan`Name` egenskapen tillhandahåller färgnamnet i ett mer läsbart format. Du kan använda dessa färgdetaljer för att matcha dem i andra applikationer eller modifiera dina Excel-filer programmatiskt.

## Slutsats
Och där har du det! Genom att följa dessa steg har du precis lärt dig hur du programmatiskt beräknar färgen som valts av MS Excel med Aspose.Cells för .NET. Detta tillvägagångssätt kan vara oerhört användbart för att automatisera Excel-baserade uppgifter, särskilt när man hanterar komplex villkorlig formatering. Nu, nästa gång du stöter på en mystisk färg i Excel, vet du exakt hur du ska avslöja dess hemligheter.
## FAQ's
### Kan jag tillämpa villkorlig formatering programmatiskt med Aspose.Cells?
Ja, Aspose.Cells låter dig tillämpa, ändra och till och med ta bort villkorlig formatering i Excel-filer programmatiskt.
### Stöder Aspose.Cells alla versioner av Excel?
Absolut! Aspose.Cells stöder Excel 97-2003 (XLS), Excel 2007-2019/365 (XLSX) och fler format, inklusive PDF, HTML och CSV.
### Är Aspose.Cells tillgängligt för andra plattformar än .NET?
Ja, Aspose.Cells är tillgängligt för olika plattformar, inklusive Java, C++, och Android via Java.
### Hur kan jag få en gratis provperiod på Aspose.Cells?
 Du kan ladda ner en gratis testversion av Aspose.Cells för .NET från[här](https://releases.aspose.com/).
### Hur hanterar jag stora Excel-filer med Aspose.Cells?
Aspose.Cells är optimerad för prestanda, även när man hanterar stora filer. Du kan använda strömmande API:er för att hantera stora data effektivt.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
