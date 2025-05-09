---
"description": "Lär dig hur du dela upp rader och kolumner i Excel med hjälp av Aspose.Cells för .NET med den här omfattande guiden. Förenkla din Excel-datahantering."
"linktitle": "Dela upp rader och kolumner i Excel med Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Dela upp rader och kolumner i Excel med Aspose.Cells"
"url": "/sv/net/row-and-column-management/ungrouping-rows-and-columns/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dela upp rader och kolumner i Excel med Aspose.Cells

## Introduktion
När det gäller att hantera Excel-filer kan du hamna i situationer där du behöver dela upp rader och kolumner. Oavsett om du rensar upp ett kalkylblad eller formaterar om data för bättre presentation är Aspose.Cells för .NET ett fantastiskt verktyg som förenklar processen. I den här handledningen guidar jag dig genom stegen för att dela upp rader och kolumner i Excel med hjälp av Aspose.Cells. I slutet kommer du att ha en gedigen förståelse för hur man arbetar med Excel-filer programmatiskt.
## Förkunskapskrav
Innan vi går in i koden, låt oss se till att du har allt konfigurerat. Här är vad du behöver:
1. Visual Studio: Du bör ha en fungerande version av Visual Studio installerad på din dator. Om du inte redan har den kan du ladda ner den från [Visual Studios webbplats](https://visualstudio.microsoft.com/).
2. Aspose.Cells för .NET: Du behöver ladda ner Aspose.Cells-biblioteket. Du kan hämta det från [Aspose-utgåvorsida](https://releases.aspose.com/cells/net/)Se till att du har nödvändiga licenser, vilka kan köpas eller erhållas via en [tillfällig licens](https://purchase.aspose.com/temporary-license/).
3. Grundläggande kunskaper i C#: En grundläggande förståelse för C#-programmering hjälper dig att följa med lättare.
När du har allt klart kan vi hoppa in i den roliga delen: koden!
## Importera paket
För att komma igång behöver du importera de nödvändiga paketen i ditt C#-projekt. Så här gör du:
1. Öppna ditt projekt i Visual Studio.
2. Lägg till en referens i Aspose.Cells-biblioteket. Du kan göra detta genom att högerklicka på referenserna i ditt projekt och välja Lägg till referens. Bläddra till den plats där du sparade Aspose.Cells DLL.
3. Överst i din C#-fil lägger du till följande med hjälp av direktiv:
```csharp
using System.IO;
using Aspose.Cells;
```
Nu när allt är konfigurerat, låt oss gå igenom stegen för att dela upp rader och kolumner i ditt Excel-ark. 
## Steg 1: Definiera dokumentkatalogen
Först måste du ange katalogen där din Excel-fil finns. Du kan ställa in detta så här:
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
Ersätta `"Your Document Directory"` med den faktiska sökvägen på din dator där Excel-filen är sparad. 
## Steg 2: Skapa en filström
Nästa steg är att skapa en filström för att öppna Excel-filen. Så här gör du det:
```csharp
// Skapa en filström som innehåller Excel-filen som ska öppnas
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Här öppnar du filen med namnet `book1.xls`Se till att den här filen finns i den angivna katalogen, annars får du ett felmeddelande om att filen inte hittades.
## Steg 3: Instansiera ett arbetsboksobjekt
Nu ska vi ladda Excel-filen till ett arbetsboksobjekt. Detta gör att du kan manipulera arbetsboken programmatiskt:
```csharp
// Instansiera ett arbetsboksobjekt
// Öppna Excel-filen via filströmmen
Workbook workbook = new Workbook(fstream);
```
Med den här kodraden har du laddat Excel-filen till minnet och är redo att arbeta med den.
## Steg 4: Öppna arbetsbladet
När du har arbetsboken är nästa steg att komma åt det specifika kalkylbladet där du vill dela upp rader och kolumner. Så här gör du:
```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Worksheet worksheet = workbook.Worksheets[0];
```
I det här fallet använder vi det första kalkylbladet. Om dina data finns på ett annat kalkylblad kan du ändra indexet därefter.
## Steg 5: Dela upp rader
Nu kommer den spännande delen! Låt oss dela upp de första sex raderna (från rad 0 till rad 5). Använd följande kod:
```csharp
// Avgruppera de första sex raderna (från 0 till 5)
worksheet.Cells.UngroupRows(0, 5);
```
Den här metoden tar bort alla grupperingar som har tillämpats på de angivna raderna. Så enkelt är det!
## Steg 6: Dela upp kolumner
Precis som med rader kan du även avgruppera kolumner. Så här avgrupperar du de tre första kolumnerna (från kolumn 0 till kolumn 2):
```csharp
// Avgrupperar de tre första kolumnerna (från 0 till 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Steg 7: Spara den modifierade Excel-filen
När du har avgrupperat raderna och kolumnerna är nästa steg att spara ändringarna tillbaka till en Excel-fil. Du kan göra detta genom att använda `Save` metod:
```csharp
// Spara den modifierade Excel-filen
workbook.Save(dataDir + "output.xls");
```
I det här exemplet sparar vi den modifierade filen som `output.xls`Du kan ändra filnamnet till vad du vill.
## Steg 8: Stäng filströmmen
Slutligen, för att frigöra resurser, bör du stänga filströmmen:
```csharp
// Stänger filströmmen för att frigöra alla resurser
fstream.Close();
```
Detta är en bra vana för att säkerställa att din applikation inte lagrar filreferenser längre än nödvändigt.
## Slutsats
Och där har du det! Du har framgångsrikt lärt dig hur man dela upp rader och kolumner i en Excel-fil med hjälp av Aspose.Cells för .NET. Med bara några få rader kod kan du göra betydande ändringar i dina Excel-filer programmatiskt. Oavsett om du automatiserar rapporter eller förbereder data för analys kan det spara dig massor av tid att bemästra dessa tekniker.
## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för att arbeta med Excel-filer i .NET-applikationer, vilket möjliggör enkel manipulation, konvertering och skapande av kalkylblad.
### Kan jag dela upp rader och kolumner i Excel med hjälp av andra bibliotek?
Ja, det finns andra bibliotek tillgängliga för Excel-manipulation i .NET, men Aspose.Cells erbjuder omfattande funktioner och är enkelt att använda.
### Finns det något sätt att ångra ändringar efter att man har sparat?
När du har sparat en Excel-fil kan det inte återställas till det tidigare tillståndet om du inte har en säkerhetskopia av originalfilen.
### Hur får jag support för Aspose.Cells?
Du kan hitta stöd genom att besöka [Aspose supportforum](https://forum.aspose.com/c/cells/9), där du kan ställa frågor och hitta lösningar.
### Kan jag använda Aspose.Cells utan licens?
Ja, du kan använda Aspose.Cells gratis med vissa begränsningar, och du kan börja med en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för full funktionalitet.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}