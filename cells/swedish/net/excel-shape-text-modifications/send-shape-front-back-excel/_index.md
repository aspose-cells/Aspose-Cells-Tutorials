---
"description": "Upptäck hur du skickar former till framsidan eller baksidan i Excel med Aspose.Cells för .NET. Den här guiden ger en steg-för-steg-handledning med tips."
"linktitle": "Skicka form fram eller bak i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Skicka form fram eller bak i Excel"
"url": "/sv/net/excel-shape-text-modifications/send-shape-front-back-excel/"
"weight": 16
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skicka form fram eller bak i Excel

## Introduktion
När du arbetar med Excel-filer kan du behöva mer kontroll över de visuella elementen i ditt kalkylblad. Former, som bilder och grafik, kan förbättra presentationen av dina data. Men vad händer när dessa former överlappar varandra eller behöver ändras ordning? Det är här Aspose.Cells för .NET glänser. I den här handledningen guidar vi dig genom stegen för att manipulera former i ett Excel-kalkylblad, specifikt genom att skicka former till fram- eller baksidan av andra former. Om du är redo att förbättra ditt Excel-spel, låt oss dyka in direkt!
## Förkunskapskrav
Innan vi börjar behöver du ha några saker på plats:
1. Installation av Aspose.Cells-biblioteket: Se till att du har Aspose.Cells-biblioteket installerat för .NET. Du hittar det [här](https://releases.aspose.com/cells/net/).
2. Utvecklingsmiljö: Se till att du har en utvecklingsmiljö konfigurerad med .NET-stöd, till exempel Visual Studio.
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
Okej, har du kryssat i alla rutor på listan över förkunskapskrav? Toppen! Nu går vi vidare till det roliga – att skriva lite kod!
## Importera paket
Innan vi dyker in i själva kodningen, låt oss importera de nödvändiga paketen. Lägg bara till följande using-direktiv högst upp i din C#-fil:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Dessa namnrymder är avgörande eftersom de innehåller de klasser och metoder vi kommer att använda för att manipulera Excel-filer och former.
## Steg 1: Definiera dina filsökvägar
det här första steget behöver vi etablera käll- och utdatakatalogerna. Det är här din Excel-fil finns och där du vill spara den modifierade filen.
```csharp
//Källkatalog
string sourceDir = "Your Document Directory";
//Utdatakatalog
string outputDir = "Your Document Directory";
```
Ersätta `"Your Document Directory"` med den faktiska sökvägen där dina Excel-filer lagras.
## Steg 2: Läs in arbetsboken
Nu när vi har konfigurerat våra kataloger, låt oss ladda arbetsboken (Excel-filen) som innehåller de former vi vill manipulera.
```csharp
//Ladda källfilen i Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
Den här kodraden initierar en ny `Workbook` objektet och laddar den angivna Excel-filen till minnet så att vi kan arbeta med den.
## Steg 3: Öppna arbetsbladet 
Nästa steg är att komma åt det specifika arbetsbladet där våra former finns. I det här exemplet använder vi det första arbetsbladet.
```csharp
//Åtkomst till första kalkylbladet
Worksheet ws = wb.Worksheets[0];
```
Genom att referera `Worksheets[0]`, vi riktar in oss på det första arket i vår arbetsbok. Om dina former finns på ett annat ark, justera indexet därefter.
## Steg 4: Komma åt formerna
Med tillgång till arbetsbladet klart, låt oss hämta de former vi är intresserade av. I det här exemplet kommer vi att använda den första och fjärde formen.
```csharp
//Åtkomst till första och fjärde formen
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Dessa linjer hämtar de specifika formerna från kalkylbladet baserat på deras index.
## Steg 5: Skriv ut Z-ordningens position för former
Innan vi flyttar några former, låt oss skriva ut deras nuvarande position i Z-ordning. Detta hjälper oss att spåra deras positionering innan vi gör ändringar.
```csharp
//Skriv ut formens Z-ordningsposition
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
Genom att ringa `ZOrderPosition`, kan vi se var varje form sitter i ritordningen.
## Steg 6: Skicka den första formen framåt
Nu är det dags för handling! Nu skickar vi den första formen till Z-ordningens framsida.
```csharp
//Skicka den här formen till framsidan
sh1.ToFrontOrBack(2);
```
Genom att passera `2` till `ToFrontOrBack`, instruerar vi Aspose.Cells att föra den här formen framåt. 
## Steg 7: Skriv ut den andra formens Z-ordningsposition
Innan vi skickar den andra formen till baksidan, låt oss kontrollera var den är placerad.
```csharp
//Skriv ut formens Z-ordningsposition
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Detta ger oss insikt i den fjärde formens position innan vi gör några ändringar.
## Steg 8: Flytta den fjärde formen längst bak
Slutligen ska vi skicka den fjärde formen till baksidan av Z-ordningsstacken.
```csharp
//Skicka den här formen till baksidan
sh4.ToFrontOrBack(-2);
```
Användning `-2` eftersom parametern skickar formen mot baksidan av stacken, vilket säkerställer att den inte skymmer andra former eller text.
## Steg 9: Spara arbetsboken 
Det sista steget är att spara din arbetsbok med de nyligen placerade formerna.
```csharp
//Spara utdatafilen i Excel
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Det här kommandot sparar den ändrade arbetsboken i den angivna utdatakatalogen.
## Steg 10: Bekräftelsemeddelande
Slutligen, låt oss ge en enkel bekräftelse för att informera oss om att vår uppgift har slutförts.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Och det avslutar koden för vår handledning!
## Slutsats
Att manipulera former i Excel med Aspose.Cells för .NET är inte bara enkelt utan också kraftfullt. Genom att följa den här guiden bör du nu enkelt kunna skicka former till framsidan eller baksidan, vilket ger bättre kontroll över dina Excel-presentationer. Med dessa verktyg till ditt förfogande är du redo att förbättra dina kalkylblads visuella attraktionskraft.
## Vanliga frågor
### Vilket programmeringsspråk behöver jag för Aspose.Cells?  
Du behöver använda C# eller något annat språk som stöds av .NET för att arbeta med Aspose.Cells.
### Kan jag prova Aspose.Cells gratis?  
Ja, du kan börja med en gratis provperiod av Aspose.Cells [här](https://releases.aspose.com/).
### Vilka typer av former kan jag manipulera i Excel?  
Du kan manipulera olika former som rektanglar, cirklar, linjer och bilder.
### Hur kan jag få support för Aspose.Cells?  
Du kan besöka deras communityforum för support eller frågor [här](https://forum.aspose.com/c/cells/9).
### Finns det en tillfällig licens tillgänglig för Aspose.Cells?  
Ja, du kan ansöka om en tillfällig licens [här](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}