---
"description": "Lär dig hur du enkelt infogar en bild i sidhuvud/sidfot med Aspose.Cells för .NET i den här omfattande guiden."
"linktitle": "Infoga bild i sidfoten på arbetsbladet"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Infoga bild i sidfoten på arbetsbladet"
"url": "/sv/net/worksheet-page-setup-features/insert-image-in-header-footer/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Infoga bild i sidfoten på arbetsbladet

## Introduktion
När det gäller att skapa professionellt utseende Excel-kalkylblad kan små detaljer göra en enorm skillnad. En sådan detalj är att lägga till bilder i sidhuvudet eller sidfoten på dina kalkylblad. Det är ett säkert sätt att varumärkeskännedom och ge dem en touch av professionalism. Även om detta kan låta komplicerat, särskilt om du inte är ett teknikexpert, förenklar Aspose.Cells för .NET processen avsevärt. Så låt oss dyka in och lära oss hur du gör detta steg för steg!
## Förkunskapskrav
Innan du börjar infoga bilder i sidhuvud och sidfot, se till att du har några saker på plats:
1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Denna IDE är ett kraftpaket för .NET-utveckling.
2. Aspose.Cells för .NET: Du kan få en gratis provversion eller köpa den om du menar allvar med att maximera dina Excel-funktioner. Ladda ner den. [här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: En grundläggande förståelse för C# och hur man kör en .NET-applikation är meriterande.
4. Bildfil: Förbered en bildfil, till exempel en företagslogotyp. I det här exemplet refererar vi till den som `aspose-logo.jpg`.
## Importera paket
För att komma igång med vår kodningsresa, se till att du har importerat de nödvändiga paketen i ditt C#-projekt. Du behöver namnrymden Aspose.Cells som innehåller alla klasser och metoder du kommer att arbeta med.
Så här inkluderar du det i din kod:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nu när vi har allt klart, låt oss gå igenom processen med enkla steg.
## Steg 1: Konfigurera din katalog
Definiera var dina filer ska lagras.
Först måste vi ange sökvägen till vår dokumentkatalog där Excel-filen och bilden finns. Du kan ange vilken sökväg som helst; ersätt bara `"Your Document Directory"` med din faktiska katalogsökväg.
```csharp
string dataDir = "Your Document Directory";
```
## Steg 2: Skapa ett arbetsboksobjekt
Skapa en instans av din Excel-arbetsbok.
Med sökvägen inställd behöver vi nu skapa en ny instans av ett kalkylblad där vi ska infoga vår bild. 
```csharp
Workbook workbook = new Workbook();
```
## Steg 3: Ladda din bild
Öppna och läs bildfilen och konvertera den till en byte-array för bearbetning.
Nästa steg är att ange sökvägen för vår bild (logotypen i det här fallet) och initiera en `FileStream` objekt för att läsa bilden. Så här gör du:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Deklarera ett FileStream-objekt
FileStream inFile;
byte[] binaryData;
// Skapa instansen av FileStream-objektet
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Steg 4: Läs bilden in i en byte-array
Konvertera bildfildata till en byte-array.
För att arbeta med bilden behöver vi läsa in den i en byte-array. Detta är viktigt eftersom det låter oss manipulera bilden i applikationen.
```csharp
// Instansiera byte-arrayen för FileStream-objektets storlek
binaryData = new byte[inFile.Length];
// Läser ett block med byte från strömmen och skriver data i en given buffert med en byte-array.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Steg 5: Konfigurera sidinställningar för sidhuvud/sidfot
Använd PageSetup-objektet för att manipulera sidhuvud- och sidfotssektionerna.
För att infoga vår bild måste vi konfigurera sidinställningar-objektet. Detta gör att vi kan anpassa rubriken på vårt kalkylblad:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Steg 6: Infoga logotypen i sidhuvudet
Bädda in bilden i sidhuvudet i kalkylbladet.
Detta är det magiska ögonblicket! Vi infogar vår logotyp i den centrala delen av rubriken:
```csharp
// Placera logotypen/bilden i den mittersta delen av sidhuvudet.
pageSetup.SetHeaderPicture(1, binaryData);
// Ställ in skriptet för logotypen/bilden
pageSetup.SetHeader(1, "&G");
// Ange arkets namn i den högra delen av sidhuvudet med skriptet
pageSetup.SetHeader(2, "&A");
```
## Steg 7: Spara din arbetsbok
Spara dina ändringar i en ny Excel-fil.
Efter att allt har konfigurerats är det dags att spara vår arbetsbok. Se till att ange ett nytt namn för din utdatafil:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Steg 8: Rensa upp resurser
Stäng FileStream för att frigöra resurser.
Slutligen, efter all manipulation, glöm inte att städa upp genom att stänga din `FileStream`!
```csharp
inFile.Close();
```
## Slutsats
Och där har du det! Du har lyckats infoga en bild i sidhuvudet/sidfoten i ett Excel-ark med Aspose.Cells för .NET. Det är enkelt, eller hur? När du väl förstår stegen kan du anpassa det ytterligare för att passa dina specifika behov. Oavsett om du vill varumärkesbygga rapporter för ditt företag eller helt enkelt lägga till en personlig touch, är den här tekniken otroligt användbar. 
## Vanliga frågor
### Kan jag använda vilket bildformat som helst?
Ja, Aspose.Cells stöder olika bildformat inklusive JPEG, PNG och BMP för sidhuvud- och sidfotsbilder.
### Är Aspose.Cells gratis att använda?
Aspose.Cells erbjuder en gratis provperiod, men för fortsatt användning måste du köpa en licens. Läs mer om priser [här](https://purchase.aspose.com/buy).
### Hur får jag tillgång till Aspose.Cells-dokumentationen?
Du kan fördjupa dig i funktionerna och funktionerna i Aspose.Cells genom att besöka [dokumentation](https://reference.aspose.com/cells/net/).
### Kan jag använda Aspose.Cells utan Visual Studio?
Ja, så länge du har .NET runtime-miljön kan du använda Aspose.Cells i vilken .NET-kompatibel utvecklingsmiljö som helst.
### Vad ska jag göra om jag stöter på problem?
Om du stöter på problem eller behöver support, kolla [Aspose supportforum](https://forum.aspose.com/c/cells/9) för hjälp från communityn och utvecklare.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}