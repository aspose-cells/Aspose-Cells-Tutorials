---
title: Positionsbild (Proportionell) i Excel
linktitle: Positionsbild (Proportionell) i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du placerar bilder proportionellt i Excel med Aspose.Cells för .NET. Gör dina kalkylblad mer visuellt tilltalande.
weight: 14
url: /sv/net/excel-ole-picture-objects/position-picture-proportional-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Positionsbild (Proportionell) i Excel

## Introduktion
Är du trött på de där pixlade bilderna som aldrig verkar passa precis rätt i dina Excel-kalkylblad? Föreställ dig det här: du har en vacker logotyp som måste visas tydligt i ditt Excel-ark, men det slutar med att den kläms ihop, sträcks ut eller är dåligt placerad. Ingen vill det! Tja, håll fast vid dina platser för idag ska du lära dig hur du placerar bilder proportionellt i Excel med Aspose.Cells-biblioteket för .NET. Detta kraftfulla bibliotek gör det enkelt att manipulera Excel-filer, vare sig det är för rapportering, dataanalys eller bara piffa upp dina presentationer. Låt oss dyka in i det finurliga med att justera dina bilder perfekt!
## Förutsättningar
Innan vi dyker in i själva kodningen finns det några saker du måste ha ställt in på din maskin:
1. Visual Studio: Se till att du har Visual Studio installerat, eftersom det kommer att ge en bekväm miljö för ditt .NET-projekt.
2.  Aspose.Cells Library: Du behöver Aspose.Cells-biblioteket. Du kan ta en gratis provperiod eller köpa den från[Aspose hemsida](https://purchase.aspose.com/buy).
3. Grundläggande kunskaper om C#: En liten förtrogenhet med C#-programmering kommer att räcka långt för att förstå de exempel vi kommer att diskutera.
4. En bildfil: Ha en bild redo (som din logotyp) som du vill infoga i Excel-arket.
Nu när du har allt på plats, låt oss gå in på kodningen!
## Importera paket
För att börja använda Aspose.Cells i ditt projekt måste du importera de specifika namnrymden. Så här gör du det:
### Skapa ett nytt projekt
Skapa ett nytt projekt i Visual Studio:
- Öppna Visual Studio.
- Klicka på "Skapa ett nytt projekt."
- Välj "Klassbibliotek (.NET Framework)" eller "Konsolprogram", beroende på vad du föredrar.
### Installera Aspose.Cells
Du kan lägga till Aspose.Cells-paketet till ditt projekt via NuGet. Så här gör du:
- Högerklicka på ditt projekt i Solution Explorer.
- Välj "Hantera NuGet-paket."
- Sök efter "Aspose.Cells" och klicka på "Installera".
### Lägg till med hjälp av direktiv
Överst i din kodfil, inkludera följande direktiv:
```csharp
using System.IO;
using Aspose.Cells;
```
Dessa direktiv ger dig tillgång till de klasser du behöver för att manipulera dina Excel-filer.
Låt oss nu dela upp detta i detaljerade steg för att framgångsrikt placera en bild proportionellt i Excel.
## Steg 1: Konfigurera din katalog
Först och främst, se till att du har en avsedd mapp för dina dokument. Så här skapar du en katalog om den inte finns:
```csharp
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
 Det här utdraget skapar en ny katalog (om den inte finns) för att lagra dina Excel-filer. Byt bara ut`"Your Document Directory"` med den faktiska sökvägen där du vill att dina filer ska sparas.
## Steg 2: Instantiera en arbetsbok
Låt oss sedan skapa en ny arbetsbok:
```csharp
Workbook workbook = new Workbook();
```
Den här raden initierar ett nytt arbetsboksobjekt, vilket ger dig en tom arbetsyta att arbeta på.
## Steg 3: Lägg till ett nytt arbetsblad
Nu när vi har ställt in vår arbetsbok, låt oss lägga till ett nytt kalkylblad till den:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Detta kommer att lägga till ett nytt kalkylblad och returnera indexet för det arket, som vi kan använda för att manipulera det senare.
## Steg 4: Öppna det nya arbetsbladet
För att manipulera det nyligen tillagda kalkylbladet måste du komma åt det:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
 Nu,`worksheet` kommer att tillåta oss att lägga till innehåll och bilder till det specifika arket.
## Steg 5: Infoga bilden
Nu kommer den spännande delen! Låt oss lägga till din vackra bild. Ersätta`"logo.jpg"` med namnet på din bildfil:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
 Den här raden lägger till bilden i cell F6 (eftersom rader och kolumner är nollindexerade,`5` hänvisar till den sjätte cellen).
## Steg 6: Öppna den tillagda bilden
När bilden har infogats kan du komma åt den så här:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Detta gör att du kan manipulera bildens egenskaper.
## Steg 7: Placera bilden proportionellt
Låt oss nu placera bilden proportionellt:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
 Här,`UpperDeltaX` och`UpperDeltaY` justera bildens position i förhållande till cellens dimensioner. Du kan justera dessa värden för att få din bild helt rätt.
## Steg 8: Spara dina ändringar
Slutligen, spara din arbetsbok för att bevara alla ändringar:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
 Denna rad sparar din arbetsbok som`book1.out.xls` i den angivna katalogen.
## Slutsats
Och där har du det! Du har precis lärt dig hur du placerar bilder proportionellt i Excel med Aspose.Cells för .NET. Det handlar inte bara om att infoga bilder; det handlar om att få dem att se perfekta ut i dina kalkylblad. Kom bara ihåg: en välplacerad bild kan höja din datapresentation avsevärt.
Ha kul med att experimentera med olika bilder och placeringar, och tveka inte att dyka djupare in i de rika funktionerna som Aspose.Cells erbjuder. Dina Excel-ark är på väg att få en rejäl makeover!
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för .NET som gör det möjligt för användare att skapa, manipulera och konvertera Excel-filer utan att behöva installera Microsoft Excel.
### Kan jag använda Aspose.Cells gratis?
 Ja, Aspose.Cells erbjuder en gratis testversion som du kan ladda ner[här](https://releases.aspose.com/).
### Var kan jag hitta dokumentationen?
 Du kan komma åt den omfattande[dokumentation](https://reference.aspose.com/cells/net/) för Aspose.Cells.
### Stöder Aspose.Cells alla bildformat?
Aspose.Cells stöder olika format inklusive JPEG, PNG, BMP, GIF och TIFF.
### Hur kan jag få support för Aspose.Cells?
 För eventuella frågor, besök gärna[supportforum](https://forum.aspose.com/c/cells/9)där du kan ställa dina frågor.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
