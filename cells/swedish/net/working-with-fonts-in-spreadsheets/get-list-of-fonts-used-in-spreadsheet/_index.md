---
"description": "Lär dig hur du hämtar och listar teckensnitt från Excel-kalkylblad med Aspose.Cells för .NET med den här lättförståeliga handledningen."
"linktitle": "Hämta lista över teckensnitt som används i kalkylblad"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Hämta lista över teckensnitt som används i kalkylblad"
"url": "/sv/net/working-with-fonts-in-spreadsheets/get-list-of-fonts-used-in-spreadsheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hämta lista över teckensnitt som används i kalkylblad

## Introduktion
Har du någonsin skrollat igenom ett Excel-kalkylblad och undrat över vilka typsnitt som används i dess olika celler? Kanske har du stött på ett gammalt dokument och vill veta vilka typografiska val som gjordes? Då har du tur! Med Aspose.Cells för .NET är det som att ha en verktygslåda som låter dig gå igenom och avslöja de där typsnittshemligheterna som är gömda i dina kalkylblad. I den här guiden tar vi dig igenom hur du enkelt hittar en lista över alla typsnitt som används i en Excel-fil. Spänn fast säkerhetsbältet och dyk ner i kalkylbladens värld!
## Förkunskapskrav
Innan vi börjar med kodning finns det några saker du behöver för att komma igång. Oroa dig inte, det är väldigt enkelt. Här är en checklista över vad du behöver:
1. Visual Studio: Se till att du har en version av Visual Studio installerad på din dator. Det är här vi skriver vår kod.
2. Aspose.Cells för .NET: Du behöver ha Aspose.Cells-biblioteket tillgängligt. Om du inte har laddat ner det än kan du hämta det från [plats](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: Lite förståelse för C#-programmering kommer definitivt att hjälpa dig att navigera genom koden enkelt.
4. En exempelfil i Excel: Du behöver en exempelfil i Excel, som "sampleGetFonts.xlsx", att arbeta med. Det är här vi ska utforska teckensnitt.
När du har fått allt på plats är du redo att börja programmera!
## Importera paket
För att komma igång, låt oss importera de nödvändiga namnrymderna. I .NET är import av paket ungefär som att bjuda in rätt gäster till din fest – utan dem kommer saker och ting helt enkelt inte att fungera smidigt.
Så här importerar du Aspose.Cells:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Med den här enkla raden bjuder vi in kärnfunktionerna i Aspose.Cells i vårt projekt. Nu går vi vidare till att läsa in arbetsboken.
## Steg 1: Ställ in dokumentkatalogen
Först och främst – innan vi går in på koden måste du ange sökvägen till din dokumentkatalog. Det är här din Excel-fil finns. 
```csharp
string dataDir = "Your Document Directory";
```
Du ersätter "Din dokumentkatalog" med den faktiska sökvägen där din Excel-fil finns. Tänk på detta som att du säger till programmet: "Här har jag gömt min Excel-fil; gå och kolla in den!"
## Steg 2: Läs in källarbetsboken
Det är dags att ladda upp Excel-filen. Vi skapar en ny instans av den `Workbook` klass och skicka i filens sökväg. 
```csharp
Workbook wb = new Workbook(dataDir + "sampleGetFonts.xlsx");
```
Vad händer här? Vi öppnar i princip dörren till vårt kalkylblad. `Workbook` klassen låter oss interagera med innehållet i Excel-filen. 
## Steg 3: Hämta alla teckensnitt
Nu kommer det magiska ögonblicket – låt oss faktiskt hämta typsnitten! `GetFonts()` Metoden är vår guldbiljett.
```csharp
Aspose.Cells.Font[] fnts = wb.GetFonts();
```
Här ber vi arbetsboken att avslöja alla teckensnitt som används i den. `fnts` uppställningen kommer att innehålla våra skatter.
## Steg 4: Skriv ut teckensnitten
Slutligen, låt oss ta de där typsnitten och skriva ut dem. Detta hjälper oss att verifiera vad vi har hittat.
```csharp
for (int i = 0; i < fnts.Length; i++)
{
	Console.WriteLine(fnts[i]);
}
```
Denna loop går genom varje typsnitt i vår `fnts` array och matar ut dem till konsolen en efter en. Det är som att visa upp alla coola typografiska alternativ du har i din Excel-fil!
## Slutsats
Och där har du det! Med bara några få rader kod har du lyckats hämta och skriva ut listan över teckensnitt som används i ditt Excel-kalkylblad med Aspose.Cells för .NET. Det här handlar inte bara om teckensnitt; det handlar om att förstå finesserna i dina dokument, förbättra dina presentationer och bemästra typografins konst i dina kalkylblad. Oavsett om du är en utvecklare eller någon som helt enkelt älskar att experimentera med Excel, kan det här lilla snippet vara revolutionerande. 
## Vanliga frågor
### Behöver jag installera Aspose.Cells separat?
Ja, du måste ladda ner och referera till biblioteket i ditt projekt. 
### Kan jag använda Aspose.Cells för andra format?
Absolut! Aspose.Cells fungerar med flera Excel-format, som XLSX, XLS och CSV.
### Finns det en gratis provperiod tillgänglig?
Ja, du kan få en gratis provperiod från [nedladdningslänk](https://releases.aspose.com/).
### Hur kan jag få teknisk support?
Om du behöver hjälp, [Aspose supportforum](https://forum.aspose.com/c/cells/9) är en utmärkt resurs.
### Är Aspose.Cells kompatibelt med .NET Core?
Ja, Aspose.Cells är även kompatibelt med .NET Core-projekt.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}