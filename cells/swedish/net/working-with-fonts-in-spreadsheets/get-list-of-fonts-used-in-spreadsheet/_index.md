---
title: Hämta lista över teckensnitt som används i kalkylblad
linktitle: Hämta lista över teckensnitt som används i kalkylblad
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du hämtar och listar teckensnitt från Excel-kalkylblad med Aspose.Cells för .NET med denna lättanvända handledning.
weight: 10
url: /sv/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hämta lista över teckensnitt som används i kalkylblad

## Introduktion
Har du någonsin hittat dig själv att bläddra igenom ett Excel-kalkylblad och undrat över de typsnitt som används i dess olika celler? Kanske har du stött på ett gammalt dokument och skulle älska att veta vilka typografival som gjordes? Tja, du har tur! Med Aspose.Cells för .NET är det som att ha en verktygslåda som låter dig sålla igenom och avslöja de teckensnittshemligheter som är gömda i dina kalkylblad. I den här guiden tar vi dig igenom hur du enkelt hämtar en lista över alla typsnitt som används i en Excel-fil. Spänn fast dig och låt oss dyka in i kalkylarksvärlden!
## Förutsättningar
Innan vi går in i kod finns det några saker du behöver för att komma igång. Oroa dig inte, det är väldigt enkelt. Här är en checklista över vad du behöver:
1. Visual Studio: Se till att du har en version av Visual Studio installerad på din dator. Det är här vi skriver vår kod.
2. Aspose.Cells för .NET: Du måste ha Aspose.Cells-biblioteket tillgängligt. Om du inte har laddat ner den än kan du hämta den från[plats](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om C#: En liten förståelse för C#-programmering kommer definitivt att hjälpa dig att enkelt navigera genom koden.
4. Ett exempel på en Excel-fil: Du behöver ett exempel på en Excel-fil, som "sampleGetFonts.xlsx," att arbeta med. Det är här vi kommer att tillämpa vår typsnittsutforskning.
När du har fått allt i rutten är du redo att hoppa in i kodning!
## Importera paket
För att sätta igång, låt oss importera de nödvändiga namnrymden. I .NET är import av paket som att bjuda in rätt gäster till din fest – utan dem fungerar det helt enkelt inte smidigt.
Så här importerar du Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Med denna enkla linje bjuder vi in Aspose.Cells kärnfunktionalitet i vårt projekt. Låt oss nu gå vidare till att ladda arbetsboken.
## Steg 1: Ställ in dokumentkatalogen
Först och främst – innan vi dyker in i koden måste du ange sökvägen till din dokumentkatalog. Det är här din Excel-fil sitter. 
```csharp
string dataDir = "Your Document Directory";
```
Du kommer att ersätta "Din dokumentkatalog" med den faktiska sökvägen där din Excel-fil finns. Se det här som att säga till programmet: "Hej, här har jag gömt min Excel-fil; gå och kolla!"
## Steg 2: Ladda källarbetsboken
 Det är dags att ladda upp Excel-filen. Vi kommer att skapa en ny instans av`Workbook` klass och passera i filens sökväg. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
 Vad händer här? Vi öppnar i princip dörren till vårt kalkylblad. De`Workbook` klass tillåter oss att interagera med innehållet i Excel-filen. 
## Steg 3: Hämta alla teckensnitt
 Nu kommer det magiska ögonblicket – låt oss faktiskt hämta typsnitten! De`GetFonts()` metoden är vår gyllene biljett.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
 Här ber vi arbetsboken att spilla bönor om alla typsnitt som används i den. De`fnts` array kommer att hålla våra skatter.
## Steg 4: Skriv ut teckensnitten
Slutligen, låt oss ta dessa typsnitt och skriva ut dem. Detta hjälper oss att verifiera vad vi har hittat.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
 Denna loop går igenom varje typsnitt i vår`fnts` array och matar ut dem till konsolen en efter en. Det är som att visa upp alla coola typografival du har i din Excel-fil!
## Slutsats
Och där har du det! Med bara några rader kod har du framgångsrikt hämtat och skrivit ut listan över teckensnitt som används i ditt Excel-kalkylblad med Aspose.Cells för .NET. Det här handlar inte bara om typsnitt; det handlar om att förstå finesserna i dina dokument, förbättra dina presentationer och behärska typografikonsten i dina kalkylblad. Oavsett om du är en utvecklare eller någon som helt enkelt älskar att mixtra med Excel, kan det här lilla utdraget vara en spelväxlare. 
## FAQ's
### Behöver jag installera Aspose.Cells separat?
Ja, du måste ladda ner och referera till biblioteket i ditt projekt. 
### Kan jag använda Aspose.Cells för andra format?
Absolut! Aspose.Cells fungerar med flera Excel-format, som XLSX, XLS och CSV.
### Finns det en gratis provperiod?
 Ja, du kan få en gratis provperiod från[nedladdningslänk](https://releases.aspose.com/).
### Hur kan jag få teknisk support?
 Om du behöver hjälp,[Aspose supportforum](https://forum.aspose.com/c/cells/9) är en stor resurs.
### Är Aspose.Cells kompatibel med .NET Core?
Ja, Aspose.Cells är också kompatibelt med .NET Core-projekt.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
