---
"description": "Lär dig hur du hämtar och ställer in temafärger i Excel med Aspose.Cells för .NET med den här lättförståeliga handledningen. Komplett steg-för-steg-guide och kodexempel ingår."
"linktitle": "Hämta och ställa in temafärger i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Hämta och ställa in temafärger i Excel"
"url": "/sv/net/excel-themes-and-formatting/getting-and-setting-theme-colors/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hämta och ställa in temafärger i Excel

## Introduktion
Att anpassa utseendet på en Excel-arbetsbok kan göra en enorm skillnad när man presenterar data. En viktig aspekt av anpassning är att kontrollera temafärgerna i dina Excel-filer. Om du arbetar med .NET är Aspose.Cells ett otroligt kraftfullt API som låter dig enkelt manipulera Excel-filer programmatiskt, och i den här handledningen ska vi dyka ner i hur man hämtar och ställr in temafärger i Excel med hjälp av Aspose.Cells för .NET.
Låter det komplicerat? Oroa dig inte, jag har åtgärdat allt! Vi går igenom det steg för steg så att du i slutet av den här guiden enkelt kan finjustera färgerna. Nu sätter vi igång!
## Förkunskapskrav
Innan vi går in i koden, låt oss ta en titt på vad du behöver för att få allt att fungera smidigt:
1. Aspose.Cells för .NET – Se till att du har den senaste versionen installerad. Om du inte redan har den kan du göra det. [ladda ner den här](https://releases.aspose.com/cells/net/).
2. .NET-utvecklingsmiljö – Du kan använda Visual Studio eller någon annan IDE som du väljer.
3. Grundläggande kunskaper i C# – Detta hjälper dig att följa kodningsexemplen.
4. Excel-fil – Ett exempel på en Excel-fil som du vill manipulera.
Du kan också få en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för att utforska Aspose.Cells fullständiga funktionalitet gratis innan du binder dig.
## Importera namnrymder
Till att börja med, låt oss se till att du importerar de nödvändiga namnrymderna till ditt projekt. Detta ger dig tillgång till alla klasser och metoder du behöver för att manipulera Excel-temafärger.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
Nu ska vi dyka in i själva processen för att hämta och ställa in temafärger i din Excel-arbetsbok. Jag ska dela upp koden i enkla steg för bättre förståelse.
## Steg 1: Ladda din Excel-fil
Först och främst måste du ladda Excel-filen som du ska ändra. Vi använder Workbook-klassen för att öppna en befintlig Excel-fil.
Du initierar ett nytt arbetsboksobjekt och laddar din Excel-fil i det. Detta gör att du kan göra ändringar i arbetsboken.
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
// Instansiera arbetsboksobjekt för att öppna en befintlig Excel-fil.
Workbook workbook = new Workbook(dataDir + "book1.xlsx");
```
Det är här magin börjar! Vi har nu öppnat filen och är redo att börja justera temafärgerna.
## Steg 2: Hämta de aktuella temafärgerna
Innan vi ändrar några färger, låt oss först kontrollera vilka temafärger som är aktuella. I det här exemplet fokuserar vi på Bakgrund1 och Accent2.
Du använder metoden GetThemeColor för att hämta den aktuella temafärgen för både Bakgrund1 och Accent2.
```csharp
// Hämta temafärgen Bakgrund1.
Color c = workbook.GetThemeColor(ThemeColorType.Background1);
// Skriv ut färgen.
Console.WriteLine("Theme color Background1: " + c);
// Hämta temafärgen Accent2.
c = workbook.GetThemeColor(ThemeColorType.Accent2);
// Skriv ut färgen.
Console.WriteLine("Theme color Accent2: " + c);
```
När du kör detta kommer det att skriva ut de aktuella färgerna som används i temat. Detta är användbart om du vill veta standardinställningarna innan du gör ändringar.
## Steg 3: Ställ in nya temafärger
Nu kommer det roliga! Vi ändrar färgerna för Bakgrund1 och Accent2. Nu ändrar vi Bakgrund1 till röd och Accent2 till blå. Detta ger arbetsboken ett nytt, djärvt utseende!
Du använder metoden SetThemeColor för att ändra temafärgerna för Background1 och Accent2.
```csharp
// Ändra temafärgen Bakgrund1 till röd.
workbook.SetThemeColor(ThemeColorType.Background1, Color.Red);
// Ändra Accent2-temafärgen till blå.
workbook.SetThemeColor(ThemeColorType.Accent2, Color.Blue);
```
Ser ni vad vi gjorde där? Vi skickade helt enkelt in den färg vi ville ha, och pang! Temafärgerna har nu ändrats. Men vänta, hur vet vi om det fungerade? Det är härnäst.
## Steg 4: Verifiera ändringarna
Vi vill inte bara anta att ändringarna har gjorts. Låt oss verifiera de nya färgerna genom att hämta dem igen och skriva ut dem.
Du hämtar de uppdaterade temafärgerna med hjälp av GetThemeColor-metoden igen för att bekräfta att ändringarna har tillämpats.
```csharp
// Hämta den uppdaterade temafärgen för Bakgrund1.
c = workbook.GetThemeColor(ThemeColorType.Background1);
// Skriv ut den uppdaterade färgen för bekräftelse.
Console.WriteLine("Theme color Background1 changed to: " + c);
// Hämta den uppdaterade temafärgen för Accent2.
c = workbook.GetThemeColor(ThemeColorType.Accent2);
// Skriv ut den uppdaterade färgen för bekräftelse.
Console.WriteLine("Theme color Accent2 changed to: " + c);
```
På så sätt kan du vara säker på att dina ändringar fungerar som förväntat. När du har bekräftat att allt är klart kan vi gå vidare till det sista steget.
## Steg 5: Spara den modifierade Excel-filen
Glöm inte att spara ditt arbete efter att du har gjort alla dessa spännande ändringar! Det här steget säkerställer att de uppdaterade temafärgerna tillämpas på din Excel-fil.
Du använder metoden Spara för att spara arbetsboken med de ändringar du har gjort.
```csharp
// Spara den uppdaterade filen.
workbook.Save(dataDir + "output.out.xlsx");
```
Och det var allt! Du har precis lyckats ändra temafärgerna i din Excel-fil med Aspose.Cells för .NET. High five!
## Slutsats
Att ändra temafärger i en Excel-fil med Aspose.Cells för .NET är enkelt när du väl fått kläm på det. Med bara några få rader kod kan du helt ändra utseendet och känslan i din arbetsbok och ge den ett anpassat och professionellt utseende. Oavsett om du vill matcha ditt företags varumärke eller helt enkelt vill få ditt kalkylblad att sticka ut, tillhandahåller Aspose.Cells verktygen för att få det gjort.
## Vanliga frågor
### Kan jag ställa in andra anpassade färger än de fördefinierade temafärgerna?
Ja, med Aspose.Cells kan du ange anpassade färger för vilken del som helst av din Excel-arbetsbok, inte bara de fördefinierade temafärgerna.
### Behöver jag en betald licens för att använda Aspose.Cells?
Du kan börja med en [gratis provperiod](https://releases.aspose.com/) eller få en [tillfällig licens](https://purchase.aspose.com/temporary-license/)För att låsa upp alla funktioner rekommenderas en betald licens.
### Kan jag använda olika temafärger på enskilda ark?
Ja, du kan manipulera temafärgerna för enskilda blad i arbetsboken genom att läsa in dem separat och använda önskade färger.
### Är det möjligt att återgå till de ursprungliga temafärgerna?
Ja, om du vill återgå till standardtemafärgerna kan du hämta och återställa dem med samma metoder som GetThemeColor och SetThemeColor.
### Kan jag automatisera den här processen för flera arbetsböcker?
Absolut! Med Aspose.Cells kan du programmatiskt tillämpa temaändringar i flera arbetsböcker i en batchprocess.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}