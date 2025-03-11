---
title: Dela upp rader och kolumner i Excel med Aspose.Cells
linktitle: Dela upp rader och kolumner i Excel med Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du avgrupperar rader och kolumner i Excel med Aspose.Cells för .NET med den här omfattande guiden. Förenkla din Excel-datamanipulation.
weight: 15
url: /sv/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dela upp rader och kolumner i Excel med Aspose.Cells

## Introduktion
När det gäller hantering av Excel-filer kan du hamna i situationer där du behöver avgruppera rader och kolumner. Oavsett om du rensar upp ett kalkylblad eller formaterar om data för bättre presentation är Aspose.Cells för .NET ett fantastiskt verktyg som förenklar processen. I den här handledningen guidar jag dig genom stegen för att avgruppera rader och kolumner i Excel med Aspose.Cells. I slutet kommer du att ha en gedigen förståelse för hur du arbetar med Excel-filer programmatiskt.
## Förutsättningar
Innan vi dyker in i koden, låt oss se till att du har allt inställt. Här är vad du behöver:
1.  Visual Studio: Du bör ha en fungerande version av Visual Studio installerad på din dator. Om du inte har det ännu kan du ladda ner det från[Visual Studios webbplats](https://visualstudio.microsoft.com/).
2. Aspose.Cells för .NET: Du måste ladda ner Aspose.Cells-biblioteket. Du kan ta den från[Sidan Aspose Releases](https://releases.aspose.com/cells/net/) . Se till att du har de nödvändiga licenserna, som kan köpas eller erhållas via en[tillfällig licens](https://purchase.aspose.com/temporary-license/).
3. Grundläggande kunskaper om C#: En grundläggande förståelse för C#-programmering hjälper dig att följa med lättare.
När du har allt klart kan vi hoppa in i den roliga delen: koden!
## Importera paket
För att komma igång måste du importera nödvändiga paket i ditt C#-projekt. Så här gör du:
1. Öppna ditt projekt i Visual Studio.
2. Lägg till en referens till Aspose.Cells-biblioteket. Du kan göra detta genom att högerklicka på referenserna i ditt projekt och välja Lägg till referens. Bläddra till platsen där du sparade Aspose.Cells DLL.
3. Överst i din C#-fil lägger du till följande med hjälp av direktiv:
```csharp
using System.IO;
using Aspose.Cells;
```
Nu när allt är konfigurerat, låt oss gå igenom stegen för att avgruppera rader och kolumner i ditt Excel-ark. 
## Steg 1: Definiera dokumentkatalogen
Först måste du ange katalogen där din Excel-fil finns. Du kan ställa in detta på följande sätt:
```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen på din dator där Excel-filen sparas. 
## Steg 2: Skapa en filström
Därefter måste du skapa en filström för att öppna Excel-filen. Så här kan du göra det:
```csharp
// Skapa en filström som innehåller Excel-filen som ska öppnas
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 Här öppnar du filen med namnet`book1.xls`. Se till att den här filen finns i din angivna katalog, annars kommer du att stöta på ett felmeddelande om att filen inte hittades.
## Steg 3: Instantiera ett arbetsboksobjekt
Låt oss nu ladda Excel-filen till ett arbetsboksobjekt. Detta låter dig manipulera arbetsboken programmatiskt:
```csharp
// Instantiera ett arbetsboksobjekt
// Öppna Excel-filen genom filströmmen
Workbook workbook = new Workbook(fstream);
```
Med denna kodrad har du framgångsrikt laddat in Excel-filen i minnet och är redo att arbeta med den.
## Steg 4: Öppna arbetsbladet
När du har arbetsboken är nästa steg att komma åt det specifika kalkylbladet där du vill avgruppera rader och kolumner. Så här gör du det:
```csharp
// Åtkomst till det första kalkylbladet i Excel-filen
Worksheet worksheet = workbook.Worksheets[0];
```
I det här fallet kommer vi åt det första kalkylbladet. Om dina data finns på ett annat blad kan du ändra indexet i enlighet med detta.
## Steg 5: Dela upp rader
Nu kommer den spännande delen! Låt oss dela upp de första sex raderna (från rad 0 till rad 5). Använd följande kod:
```csharp
// Dela upp de första sex raderna (från 0 till 5)
worksheet.Cells.UngroupRows(0, 5);
```
Den här metoden tar bort alla grupperingar som har tillämpats på de angivna raderna. Så enkelt är det!
## Steg 6: Dela upp kolumner
Precis som rader kan du också avgruppera kolumner. Så här avgrupperar du de tre första kolumnerna (från kolumn 0 till kolumn 2):
```csharp
// Dela upp de tre första kolumnerna (från 0 till 2)
worksheet.Cells.UngroupColumns(0, 2);
```
## Steg 7: Spara den modifierade Excel-filen
 När du har delat upp raderna och kolumnerna är nästa steg att spara ändringarna tillbaka till en Excel-fil. Du kan göra detta genom att använda`Save` metod:
```csharp
// Sparar den ändrade Excel-filen
workbook.Save(dataDir + "output.xls");
```
 I det här exemplet sparar vi den modifierade filen som`output.xls`. Du kan ändra filnamnet till vad du föredrar.
## Steg 8: Stäng filströmmen
Slutligen, för att frigöra resurser, bör du stänga filströmmen:
```csharp
// Stänger filströmmen för att frigöra alla resurser
fstream.Close();
```
Detta är en bra praxis för att säkerställa att din ansökan inte håller kvar filhandtagen längre än nödvändigt.
## Slutsats
Och där har du det! Du har framgångsrikt lärt dig att dela upp rader och kolumner i en Excel-fil med Aspose.Cells för .NET. Med bara några rader kod kan du göra betydande ändringar i dina Excel-filer programmatiskt. Oavsett om du automatiserar rapporter eller förbereder data för analys, kan du spara massor av tid genom att behärska dessa tekniker.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för att arbeta med Excel-filer i .NET-applikationer, vilket möjliggör enkel manipulation, konvertering och skapande av kalkylblad.
### Kan jag dela upp rader och kolumner i Excel med andra bibliotek?
Ja, det finns andra bibliotek tillgängliga för Excel-manipulation i .NET, men Aspose.Cells erbjuder omfattande funktioner och användarvänlighet.
### Finns det något sätt att ångra ändringar efter att du har sparat?
När du väl har sparat en Excel-fil kan det tidigare tillståndet inte återställas om du inte har en säkerhetskopia av originalfilen.
### Hur får jag support för Aspose.Cells?
 Du kan hitta support genom att besöka[Aspose Supportforum](https://forum.aspose.com/c/cells/9), där du kan ställa frågor och hitta lösningar.
### Kan jag använda Aspose.Cells utan licens?
Ja, du kan använda Aspose.Cells gratis med vissa begränsningar, och du kan börja med en[tillfällig licens](https://purchase.aspose.com/temporary-license/) för full funktionalitet.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
