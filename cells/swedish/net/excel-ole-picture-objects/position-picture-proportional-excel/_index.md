---
"description": "Lär dig hur du placerar bilder proportionellt i Excel med Aspose.Cells för .NET. Gör dina kalkylblad mer visuellt tilltalande."
"linktitle": "Positionera bilden (proportionell) i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Positionera bilden (proportionell) i Excel"
"url": "/sv/net/excel-ole-picture-objects/position-picture-proportional-excel/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Positionera bilden (proportionell) i Excel

## Introduktion
Är du trött på de där pixelerade bilderna som aldrig verkar få plats precis i dina Excel-ark? Tänk dig detta: du har en vacker logotyp som behöver visas tydligt i ditt Excel-ark, men den blir klämd, uttänjd eller felplacerad. Ingen vill ha det! Håll i er, för idag ska du lära dig hur du placerar bilder proportionellt i Excel med hjälp av Aspose.Cells-biblioteket för .NET. Det här kraftfulla biblioteket gör det enkelt att manipulera Excel-filer, vare sig det är för rapportering, dataanalys eller bara för att snygga till dina presentationer. Låt oss dyka in i detaljerna kring att justera dina bilder perfekt!
## Förkunskapskrav
Innan vi går in i själva kodningen finns det några saker du behöver ha konfigurerat på din maskin:
1. Visual Studio: Se till att du har Visual Studio installerat, eftersom det ger en praktisk miljö för ditt .NET-projekt.
2. Aspose.Cells-biblioteket: Du behöver Aspose.Cells-biblioteket. Du kan hämta en gratis provversion eller köpa det från [Aspose webbplats](https://purchase.aspose.com/buy).
3. Grundläggande kunskaper i C#: Lite förtrogenhet med C#-programmering kommer att vara till stor hjälp för att förstå exemplen vi kommer att diskutera.
4. En bildfil: Ha en bild redo (som din logotyp) som du vill infoga i Excel-arket.
Nu när du har allt på plats, låt oss börja med kodningen!
## Importera paket
För att börja använda Aspose.Cells i ditt projekt måste du importera de specifika namnrymderna. Så här gör du:
### Skapa ett nytt projekt
Skapa ett nytt projekt i Visual Studio:
- Öppna Visual Studio.
- Klicka på "Skapa ett nytt projekt".
- Välj "Klassbibliotek (.NET Framework)" eller "Konsolprogram", beroende på vad du föredrar.
### Installera Aspose.Cells
Du kan lägga till Aspose.Cells-paketet till ditt projekt via NuGet. Så här gör du:
- Högerklicka på ditt projekt i lösningsutforskaren.
- Välj "Hantera NuGet-paket".
- Sök efter "Aspose.Cells" och klicka på "Installera".
### Lägg till med hjälp av direktiv
Högst upp i din kodfil, inkludera följande direktiv:
```csharp
using System.IO;
using Aspose.Cells;
```
Dessa direktiv ger dig tillgång till de klasser du behöver för att manipulera dina Excel-filer.
Nu ska vi dela upp detta i detaljerade steg för att framgångsrikt placera en bild proportionellt i Excel.
## Steg 1: Konfigurera din katalog
Först och främst, se till att du har en särskild mapp för dina dokument. Så här skapar du en katalog om den inte finns:
```csharp
string dataDir = "Your Document Directory";
// Skapa katalog om den inte redan finns.
bool isExists = System.IO.Directory.Exists(dataDir);
if (!isExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Det här kodavsnittet skapar en ny katalog (om den inte finns) för att lagra dina Excel-filer. Ersätt bara `"Your Document Directory"` med den faktiska sökvägen dit du vill spara dina filer.
## Steg 2: Instansiera en arbetsbok
Nu skapar vi en ny arbetsbok:
```csharp
Workbook workbook = new Workbook();
```
Den här raden initierar ett nytt arbetsboksobjekt, vilket ger dig en tom arbetsyta att arbeta på.
## Steg 3: Lägg till ett nytt arbetsblad
Nu när vi har konfigurerat vår arbetsbok, låt oss lägga till ett nytt arbetsblad i den:
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
Detta lägger till ett nytt kalkylblad och returnerar indexet för det arket, vilket vi kan använda för att manipulera det senare.
## Steg 4: Öppna det nya arbetsbladet
För att manipulera det nyligen tillagda kalkylbladet behöver du komma åt det:
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
Nu, `worksheet` kommer att låta oss lägga till innehåll och bilder till det specifika arket.
## Steg 5: Infoga bilden
Nu kommer den spännande delen! Nu lägger vi till din vackra bild. Ersätt `"logo.jpg"` med namnet på din bildfil:
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
Den här raden lägger till bilden i cell F6 (eftersom rader och kolumner är nollindexerade, `5` hänvisar till den sjätte cellen).
## Steg 6: Få åtkomst till den tillagda bilden
När bilden är infogad kan du komma åt den så här:
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
Detta gör att du kan manipulera bildens egenskaper.
## Steg 7: Placera bilden proportionellt
Nu ska vi placera bilden proportionellt:
```csharp
picture.UpperDeltaX = 200;
picture.UpperDeltaY = 200;
```
Här, `UpperDeltaX` och `UpperDeltaY` justera bildens position i förhållande till cellens dimensioner. Du kan justera dessa värden för att få bilden precis rätt.
## Steg 8: Spara dina ändringar
Spara slutligen din arbetsbok för att behålla alla ändringar:
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
Den här raden sparar din arbetsbok som `book1.out.xls` i den angivna katalogen.
## Slutsats
Och där har du det! Du har precis lärt dig hur man placerar bilder proportionellt i Excel med hjälp av Aspose.Cells för .NET. Det handlar inte bara om att infoga bilder; det handlar om att få dem att se perfekta ut i dina kalkylblad. Kom bara ihåg: en välplacerad bild kan höja din datapresentation avsevärt.
Ha kul när du experimenterar med olika bilder och placeringar, och tveka inte att fördjupa dig i de rika funktionerna som Aspose.Cells erbjuder. Dina Excel-ark kommer snart att få en rejäl makeover!
## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för .NET som gör det möjligt för användare att skapa, manipulera och konvertera Excel-filer utan att behöva installera Microsoft Excel.
### Kan jag använda Aspose.Cells gratis?
Ja, Aspose.Cells erbjuder en gratis provperiod som du kan ladda ner [här](https://releases.aspose.com/).
### Var kan jag hitta dokumentationen?
Du kan få tillgång till den omfattande [dokumentation](https://reference.aspose.com/cells/net/) för Aspose.Cells.
### Stöder Aspose.Cells alla bildformat?
Aspose.Cells stöder olika format inklusive JPEG, PNG, BMP, GIF och TIFF.
### Hur kan jag få support för Aspose.Cells?
För eventuella frågor, besök gärna [supportforum](https://forum.aspose.com/c/cells/9) där du kan ställa dina frågor.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}