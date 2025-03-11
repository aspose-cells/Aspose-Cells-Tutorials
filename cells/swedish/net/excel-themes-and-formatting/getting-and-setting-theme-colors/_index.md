---
title: Få och ställ in temafärger i Excel
linktitle: Få och ställ in temafärger i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du skaffar och ställer in temafärger i Excel med Aspose.Cells för .NET med denna lättanvända handledning. Komplett steg-för-steg-guide och kodexempel ingår.
weight: 11
url: /sv/net/excel-themes-and-formatting/getting-and-setting-theme-colors/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Få och ställ in temafärger i Excel

## Introduktion
Att anpassa utseendet på en Excel-arbetsbok kan göra en värld av skillnad när du presenterar data. En viktig aspekt av anpassning är att kontrollera temafärgerna i dina Excel-filer. Om du arbetar med .NET är Aspose.Cells ett otroligt kraftfullt API som gör att du enkelt kan manipulera Excel-filer programmatiskt, och i den här handledningen kommer vi att dyka ner i att hämta och ställa in temafärger i Excel med Aspose.Cells för . NETTO.
Låter det komplicerat? Oroa dig inte, jag har dig täckt! Vi kommer att dela upp det steg för steg så att du i slutet av den här guiden kommer att kunna justera de färgerna med lätthet. Låt oss komma igång!
## Förutsättningar
Innan vi dyker in i koden, låt oss ta en titt på vad du behöver för att få allt att fungera smidigt:
1. Aspose.Cells för .NET – Se till att du har den senaste versionen installerad. Om du inte har det än så kan du[ladda ner den här](https://releases.aspose.com/cells/net/).
2. .NET-utvecklingsmiljö – Du kan använda Visual Studio eller vilken annan IDE du väljer.
3. Grundläggande kunskaper om C# – Detta hjälper dig att följa med i kodningsexemplen.
4. Excel-fil – Ett exempel på Excel-fil som du vill manipulera.
 Du kan också få en[tillfällig licens](https://purchase.aspose.com/temporary-license/) för att utforska alla funktioner i Aspose.Cells gratis innan du bestämmer dig.
## Importera namnområden
Till att börja med, låt oss se till att du importerar de nödvändiga namnrymden till ditt projekt. Detta ger dig tillgång till alla klasser och metoder du behöver för att manipulera Excel-temafärger.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Låt oss nu dyka in i själva processen att hämta och ställa in temafärger i din Excel-arbetsbok. Jag delar upp koden i enkla steg för bättre förståelse.
## Steg 1: Ladda din Excel-fil
Först och främst måste du ladda Excel-filen som du ska ändra. Vi använder klassen Workbook för att öppna en befintlig Excel-fil.
Du initierar ett nytt arbetsboksobjekt och laddar in din Excel-fil i den. Detta gör att du kan göra ändringar i arbetsboken.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instantiera arbetsboksobjekt för att öppna en befintlig Excel-fil.
Workbook workbook = new Workbook(dataDir + "book1.xlsx");
```
Det är här magin börjar! Vi har nu öppnat filen och vi är redo att börja justera temafärgerna.
## Steg 2: Skaffa de aktuella temafärgerna
Innan du ändrar några färger, låt oss först kontrollera vad de aktuella temafärgerna är. För det här exemplet kommer vi att fokusera på Bakgrund1 och Accent2.
Du använder metoden GetThemeColor för att hämta den aktuella temafärgen för både Bakgrund1 och Accent2.
```csharp
// Skaffa temafärgen Bakgrund1.
Color c = workbook.GetThemeColor(ThemeColorType.Background1);
// Skriv ut färgen.
Console.WriteLine("Theme color Background1: " + c);
// Skaffa temafärgen Accent2.
c = workbook.GetThemeColor(ThemeColorType.Accent2);
// Skriv ut färgen.
Console.WriteLine("Theme color Accent2: " + c);
```
När du kör detta kommer det att skriva ut de aktuella färgerna som används i temat. Detta är användbart om du vill veta standardinställningarna innan du gör ändringar.
## Steg 3: Ställ in nya temafärger
Nu kommer det roliga! Vi kommer att ändra färgerna för Bakgrund1 och Accent2. Låt oss ändra Bakgrund1 till röd och Accent2 till blå. Detta kommer att ge arbetsboken ett djärvt nytt utseende!
Du använder metoden SetThemeColor för att ändra temafärgerna för Bakgrund1 och Accent2.
```csharp
// Ändra temafärgen Bakgrund1 till röd.
workbook.SetThemeColor(ThemeColorType.Background1, Color.Red);
// Ändra temafärgen Accent2 till blå.
workbook.SetThemeColor(ThemeColorType.Accent2, Color.Blue);
```
Ser du vad vi gjorde där? Vi klarade helt enkelt den färg vi ville ha, och bam! Temafärgerna har nu ändrats. Men vänta, hur vet vi om det fungerade? Det kommer härnäst.
## Steg 4: Verifiera ändringarna
Vi vill inte bara anta att förändringarna har gjorts. Låt oss verifiera de nya färgerna genom att hämta dem igen och skriva ut dem.
Du hämtar de uppdaterade temafärgerna med GetThemeColor-metoden igen för att bekräfta att ändringarna har tillämpats.
```csharp
// Skaffa den uppdaterade temafärgen Bakgrund1.
c = workbook.GetThemeColor(ThemeColorType.Background1);
// Skriv ut den uppdaterade färgen för bekräftelse.
Console.WriteLine("Theme color Background1 changed to: " + c);
// Skaffa den uppdaterade temafärgen Accent2.
c = workbook.GetThemeColor(ThemeColorType.Accent2);
// Skriv ut den uppdaterade färgen för bekräftelse.
Console.WriteLine("Theme color Accent2 changed to: " + c);
```
På så sätt kan du vara säker på att dina ändringar fungerar som förväntat. När du har verifierat att allt är bra kan vi gå vidare till det sista steget.
## Steg 5: Spara den modifierade Excel-filen
Efter att ha gjort alla dessa spännande ändringar, glöm inte att spara ditt arbete! Detta steg säkerställer att de uppdaterade temafärgerna tillämpas på din Excel-fil.
Du använder metoden Spara för att spara arbetsboken med de ändringar du gjort.
```csharp
// Spara den uppdaterade filen.
workbook.Save(dataDir + "output.out.xlsx");
```
Och det är det! Du har just framgångsrikt modifierat temafärgerna i din Excel-fil med Aspose.Cells för .NET. High five!
## Slutsats
Att ändra temafärger i en Excel-fil med Aspose.Cells för .NET är enkelt när du väl har fått kläm på det. Med bara några rader kod kan du helt ändra utseendet och känslan på din arbetsbok, vilket ger den ett anpassat och professionellt utseende. Oavsett om du vill matcha ditt företags varumärke eller helt enkelt vill få ditt kalkylblad att poppa upp, tillhandahåller Aspose.Cells verktygen för att få det gjort.
## FAQ's
### Kan jag ställa in andra anpassade färger än de fördefinierade temafärgerna?
Ja, med Aspose.Cells kan du ställa in anpassade färger för vilken del av din Excel-arbetsbok som helst, inte bara de fördefinierade temafärgerna.
### Behöver jag en betald licens för att använda Aspose.Cells?
 Du kan börja med en[gratis provperiod](https://releases.aspose.com/)eller skaffa en[tillfällig licens](https://purchase.aspose.com/temporary-license/). För att låsa upp full funktionalitet rekommenderas en betald licens.
### Kan jag använda olika temafärger på enskilda ark?
Ja, du kan manipulera temafärgerna för enskilda ark i arbetsboken genom att ladda dem separat och använda önskade färger.
### Är det möjligt att återgå till de ursprungliga temafärgerna?
Ja, om du vill återgå till standardtemafärgerna kan du hämta och återställa dem med samma GetThemeColor- och SetThemeColor-metoder.
### Kan jag automatisera den här processen för flera arbetsböcker?
Absolut! Aspose.Cells låter dig programmässigt tillämpa temaändringar över flera arbetsböcker i en batchprocess.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
