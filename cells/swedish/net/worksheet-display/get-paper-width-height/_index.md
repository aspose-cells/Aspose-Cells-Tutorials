---
title: Få papperets bredd och höjd för utskrift av arbetsblad
linktitle: Få papperets bredd och höjd för utskrift av arbetsblad
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du får papperets bredd och höjd för utskrift av kalkylblad i Aspose.Cells för .NET med denna steg-för-steg-guide.
weight: 16
url: /sv/net/worksheet-display/get-paper-width-height/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Få papperets bredd och höjd för utskrift av arbetsblad

## Introduktion
Att skriva ut dokument korrekt kräver kunskap om papperets mått. Om du är en utvecklare eller arbetar med ett program som hanterar Excel-filer kan du behöva veta hur du får fram pappersbredd och höjd när du skriver ut kalkylblad. Lyckligtvis erbjuder Aspose.Cells för .NET ett robust sätt att hantera Excel-dokument programmatiskt. I den här artikeln guidar vi dig genom processen att bestämma pappersstorleksspecifikationer, med enkla exempel för att illustrera grundläggande koncept. 
## Förutsättningar
Innan vi dyker in i de tekniska detaljerna, låt oss få lite grundarbete. För att framgångsrikt följa den här handledningen behöver du:
### 1. Grundläggande kunskaper i C#
Du bör ha ett bra grepp om C#-programmering, då vi kommer att arbeta i en .NET-miljö.
### 2. Aspose.Cells Library
Se till att du har Aspose.Cells-biblioteket installerat i ditt projekt. Om du inte har gjort det ännu kan du ladda ner den senaste versionen från[Aspose.Cells nedladdningssida](https://releases.aspose.com/cells/net/).
### 3. Visual Studio IDE
Det är fördelaktigt att ha Visual Studio för att köra och hantera dina C#-projekt. Alla versioner som stöder .NET borde fungera utmärkt.
### 4. En giltig Aspose-licens
 Även om Aspose.Cells kan testas, överväg att köpa en licens om du använder den för långsiktiga projekt. Du kan köpa den genom[denna länk](https://purchase.aspose.com/buy) eller utforska en[tillfällig licens](https://purchase.aspose.com/temporary-license/) för korta testfaser.
När du är klar, låt oss gå in i koden!
## Importera paket
Det första steget i vår resa innebär att importera viktiga namnområden. Detta är avgörande, eftersom det låter oss komma åt de klasser och metoder vi kommer att använda för att manipulera Excel-filer. Så här gör du:
```csharp
using System;
using System.IO;
using Aspose.Cells;
```
Se till att inkludera den här raden överst i din .cs-fil. Nu när vi har importen klar, låt oss fortsätta med att skapa vår arbetsbok och komma åt arbetsbladet.
## Steg 1: Skapa din arbetsbok
Vi börjar med att skapa en instans av`Workbook` klass. Detta utgör grunden för vår Excel-filmanipulation.
```csharp
Workbook wb = new Workbook();
```
Den här raden talar om för programmet att initiera en ny arbetsbok, vilket gör att vi kan dyka in i våra arbetsblad.
## Steg 2: Öppna det första arbetsbladet
Därefter kommer vi åt det första kalkylbladet i vår nyskapade arbetsbok. Det är ganska okomplicerat:
```csharp
Worksheet ws = wb.Worksheets[0];
```
Här kommer vi åt det första arket (indexerat till 0) i vår arbetsbok. Det är här vi kommer att ställa in pappersstorlekarna.
## Ställa in pappersstorlek och hämta mått
Nu går vi in i kärnan av operationen – ställer in pappersstorleken och hämtar dess dimensioner! Låt oss bryta ner detta steg för steg.
## Steg 3: Ställ in pappersstorlek till A2
Låt oss först ställa in vår pappersstorlek till A2 och skriva ut dess mått.
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
 Efter denna inställning använder vi`Console.WriteLine` för att visa måtten. När du kör detta kommer du att se bredden och höjden i tum för A2-pappersstorlek.
## Steg 4: Ställ in pappersstorlek till A3
Nu är det dags för A3! Vi upprepar helt enkelt processen:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Voila! Deklarationen kommer att skriva ut den specifika höjden och bredden för A3-papper.
## Steg 5: Ställ in pappersstorleken till A4
Följ samma mönster, låt oss kolla hur A4 mäter sig:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Detta ger oss måtten för A4—en av de vanligaste pappersstorlekarna.
## Steg 6: Ställ in pappersstorlek till Letter
För att avrunda vår utforskning av pappersstorlek, låt oss ställa in den på Letter-storlek:
```csharp
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```
Återigen kommer vi att se den specifika bredden och höjden för Letter-storlek.
## Slutsats
Och där har du det! Du har precis lärt dig hur du får papperets bredd och höjd för olika storlekar när du förbereder arbetsblad för utskrift med Aspose.Cells för .NET. Det här verktyget kan vara oerhört användbart, särskilt när du planerar dina utskriftslayouter eller hanterar utskriftsinställningar programmatiskt. Genom att veta de exakta måtten i tum kan du undvika vanliga fallgropar och se till att dina dokument skrivs ut som avsett.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som tillhandahåller en rad funktioner för att arbeta med Excel-filer programmatiskt.
### Hur kommer jag igång med Aspose.Cells?
Börja med att ladda ner biblioteket från[Aspose hemsida](https://releases.aspose.com/cells/net/) och följ dokumentationen för att ställa in det i ditt projekt.
### Kan jag använda Aspose.Cells gratis?
Aspose.Cells erbjuder en testversion, som du kan använda för att utforska dess funktioner. För långvarig användning måste du köpa en licens.
### Vilka pappersstorlekar stöds av Aspose.Cells?
Aspose.Cells stöder olika pappersstorlekar inklusive A2, A3, A4, Letter och många andra.
### Var kan jag hitta fler resurser eller support för Aspose.Cells?
 Du kan kontrollera[Aspose forum](https://forum.aspose.com/c/cells/9) för samhällshjälp och[dokumentation](https://reference.aspose.com/cells/net/) för handledning och referensmaterial.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
