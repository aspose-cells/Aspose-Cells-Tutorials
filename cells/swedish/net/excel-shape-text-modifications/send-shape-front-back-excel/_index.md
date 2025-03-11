---
title: Skicka form fram eller bak i Excel
linktitle: Skicka form fram eller bak i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck hur du skickar former till fram- eller baksidan i Excel med Aspose.Cells för .NET. Den här guiden ger en steg-för-steg handledning med tips.
weight: 16
url: /sv/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skicka form fram eller bak i Excel

## Introduktion
När du arbetar med Excel-filer kan du behöva mer kontroll över de visuella elementen i ditt kalkylblad. Former, som bilder och grafik, kan förbättra presentationen av din data. Men vad händer när dessa former överlappar varandra eller behöver ordnas om? Det är här Aspose.Cells för .NET lyser. I den här självstudien går vi igenom stegen för att manipulera former i ett Excel-kalkylblad, särskilt att skicka former till fram- eller baksidan av andra former. Om du är redo att förstärka ditt Excel-spel, låt oss dyka in direkt!
## Förutsättningar
Innan vi börjar måste du ha några saker på plats:
1.  Installation av Aspose.Cells Library: Se till att du har Aspose.Cells-biblioteket installerat för .NET. Du kan hitta den[här](https://releases.aspose.com/cells/net/).
2. Utvecklingsmiljö: Se till att du har en utvecklingsmiljö inställd med .NET-stöd, som Visual Studio.
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
Okej, du har markerat alla rutor på förkunskapslistan? Stor! Låt oss gå vidare till den roliga delen – att skriva lite kod!
## Importera paket
Innan vi dyker in i själva kodningen, låt oss importera de nödvändiga paketen. Lägg bara till följande med hjälp av direktivet överst i din C#-fil:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
Dessa namnutrymmen är avgörande eftersom de innehåller de klasser och metoder vi kommer att använda för att manipulera Excel-filer och former.
## Steg 1: Definiera dina filsökvägar
I detta första steg måste vi upprätta käll- och utdatakataloger. Det är här din Excel-fil finns och där du vill spara den ändrade filen.
```csharp
//Källkatalog
string sourceDir = "Your Document Directory";
//Utdatakatalog
string outputDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen där dina Excel-filer lagras.
## Steg 2: Ladda arbetsboken
Nu när vi har våra kataloger inställda, låt oss ladda arbetsboken (Excel-filen) som innehåller formerna vi vill manipulera.
```csharp
//Ladda källfilen i Excel
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 Denna kodrad initierar en ny`Workbook` objekt, laddar den angivna Excel-filen i minnet så att vi kan arbeta med den.
## Steg 3: Öppna arbetsbladet 
Därefter måste vi komma åt det specifika kalkylbladet där våra former finns. För det här exemplet använder vi det första kalkylbladet.
```csharp
//Öppna första kalkylbladet
Worksheet ws = wb.Worksheets[0];
```
 Genom att referera`Worksheets[0]`, riktar vi oss mot det första arket i vår arbetsbok. Om dina former finns på ett annat ark, justera indexet därefter.
## Steg 4: Få åtkomst till formerna
Med tillgång till kalkylbladet redo, låt oss ta formerna vi är intresserade av. I det här exemplet kommer vi åt den första och fjärde formen.
```csharp
//Få tillgång till första och fjärde formen
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
Dessa linjer får de specifika formerna från kalkylbladet baserat på deras index.
## Steg 5: Skriv ut Z-ordningspositionen för former
Innan vi flyttar några former, låt oss skriva ut deras nuvarande Z-Order-position. Detta hjälper oss att spåra deras positionering innan vi gör ändringar.
```csharp
//Skriv ut Z-Order-positionen för formen
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 Genom att ringa`ZOrderPosition`, kan vi se var varje form sitter i ritordningen.
## Steg 6: Skicka den första formen till fronten
Nu är det dags för action! Låt oss skicka den första formen till framsidan av Z-Ordern.
```csharp
//Skicka den här formen till fronten
sh1.ToFrontOrBack(2);
```
 Genom att passera`2` till`ToFrontOrBack`, instruerar vi Aspose.Cells att föra fram den här formen. 
## Steg 7: Skriv ut Z-Order-positionen för den andra formen
Innan vi skickar den andra formen till baksidan, låt oss kontrollera var den är placerad.
```csharp
//Skriv ut Z-Order-positionen för formen
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
Detta ger oss insikt i positionen för den fjärde formen innan vi gör några ändringar.
## Steg 8: Skicka den fjärde formen på baksidan
Slutligen kommer vi att skicka den fjärde formen till baksidan av Z-Order-stacken.
```csharp
//Skicka denna form på baksidan
sh4.ToFrontOrBack(-2);
```
 Använder`-2` eftersom parametern skickar formen mot baksidan av stapeln, vilket säkerställer att den inte hindrar andra former eller text.
## Steg 9: Spara arbetsboken 
Det sista steget är att spara din arbetsbok med de nyligen placerade formerna.
```csharp
//Spara den utgående Excel-filen
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
Detta kommando sparar den modifierade arbetsboken i den angivna utdatakatalogen.
## Steg 10: Bekräftelsemeddelande
Låt oss slutligen ge en enkel bekräftelse för att låta oss veta att vår uppgift slutförts framgångsrikt.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
Och det avslutar koden för vår handledning!
## Slutsats
Att manipulera former i Excel med Aspose.Cells för .NET är inte bara enkelt utan också kraftfullt. Genom att följa den här guiden bör du nu enkelt kunna skicka former fram eller bak, vilket ger bättre kontroll över dina Excel-presentationer. Med dessa verktyg till ditt förfogande är du redo att förbättra det visuella tilltalande av dina kalkylblad.
## FAQ's
### Vilket programmeringsspråk behöver jag för Aspose.Cells?  
Du måste använda C# eller något annat .NET-stödt språk för att arbeta med Aspose.Cells.
### Kan jag prova Aspose.Cells gratis?  
 Ja, du kan börja med en gratis provperiod av Aspose.Cells[här](https://releases.aspose.com/).
### Vilken typ av former kan jag manipulera i Excel?  
Du kan manipulera olika former som rektanglar, cirklar, linjer och bilder.
### Hur kan jag få support för Aspose.Cells?  
 Du kan besöka deras communityforum för all support eller frågor[här](https://forum.aspose.com/c/cells/9).
### Finns det en tillfällig licens tillgänglig för Aspose.Cells?  
 Ja, du kan begära en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
