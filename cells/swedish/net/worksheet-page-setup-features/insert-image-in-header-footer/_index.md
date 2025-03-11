---
title: Infoga bild i sidhuvudet på arbetsbladet
linktitle: Infoga bild i sidhuvudet på arbetsbladet
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du enkelt infogar en bild i sidhuvud/sidfot med Aspose.Cells för .NET i den här omfattande guiden.
weight: 15
url: /sv/net/worksheet-page-setup-features/insert-image-in-header-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Infoga bild i sidhuvudet på arbetsbladet

## Introduktion
När det gäller att skapa professionella Excel-kalkylblad kan små detaljer göra en enorm skillnad. En sådan detalj är att lägga till bilder i sidhuvudet eller sidfoten på dina kalkylblad. Det är ett säkert sätt att skapa ett varumärke för dina dokument och genomsyra dem med en touch av professionalism. Även om det här kan låta komplicerat, särskilt om du inte är en tekniker, förenklar processen avsevärt med Aspose.Cells för .NET. Så låt oss dyka in och lära oss hur du gör detta steg för steg!
## Förutsättningar
Innan du börjar din resa med att infoga bilder i sidhuvuds- och sidfotsavsnitt, se till att du har några saker på plats:
1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Denna IDE är ett kraftpaket för .NET-utveckling.
2.  Aspose.Cells för .NET: Du kan få en gratis provperiod eller köpa den om du menar allvar med att maximera dina Excel-funktioner. Ladda ner den[här](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper om C#: En grundläggande förståelse för C# och hur man kör en .NET-applikation kommer att vara fördelaktigt.
4. Bildfil: Förbered en bildfil som en företagslogotyp. I det här exemplet kommer vi att hänvisa till det som`aspose-logo.jpg`.
## Importera paket
För att få igång vår kodningsresa, se till att du har de nödvändiga paketen importerade i ditt C#-projekt. Du behöver namnutrymmet Aspose.Cells som innehåller alla klasser och metoder du kommer att arbeta med.
Så här inkluderar du det i din kod:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Nu när vi har ställt in allt, låt oss gå igenom processen med lätta att följa steg.
## Steg 1: Konfigurera din katalog
Definiera var dina filer ska lagras.
 Först och främst måste vi ange sökvägen till vår dokumentkatalog där Excel-filen och bilden finns. Du kan ställa in vilken väg som helst; bara ersätta`"Your Document Directory"` med din faktiska katalogsökväg.
```csharp
string dataDir = "Your Document Directory";
```
## Steg 2: Skapa ett arbetsboksobjekt
Skapa en instans av din Excel-arbetsbok.
Med sökvägen måste vi nu skapa en ny instans av ett kalkylblad där vi kommer att infoga vår bild. 
```csharp
Workbook workbook = new Workbook();
```
## Steg 3: Ladda din bild
Öppna och läs bildfilen och konvertera den till en byte-array för bearbetning.
Därefter kommer vi att ställa in sökvägen för vår bild (logotypen, i det här fallet) och initiera en`FileStream` objekt för att läsa bilden. Så här gör du:
```csharp
string logo_url = dataDir + "aspose-logo.jpg";
// Deklarera ett FileStream-objekt
FileStream inFile;
byte[] binaryData;
// Skapar instansen av FileStream-objektet
inFile = new FileStream(logo_url, FileMode.Open, FileAccess.Read);
```
## Steg 4: Läs in bilden i en bytearray
Konvertera bildfilens data till en byte-array.
För att arbeta med bilden måste vi läsa in den i en byte-array. Detta är viktigt eftersom det tillåter oss att manipulera bilden i applikationen.
```csharp
// Instantiera byte-arrayen för FileStream-objektets storlek
binaryData = new byte[inFile.Length];
// Läser ett block av byte från strömmen och skriver data i en given buffert av byte array.
long bytesRead = inFile.Read(binaryData, 0, (int)inFile.Length);
```
## Steg 5: Konfigurera sidinställningar för sidhuvud/sidfot
Gå till PageSetup-objektet för att manipulera sidhuvuds- och sidfotssektionerna.
För att infoga vår bild måste vi konfigurera sidinställningarna. Detta gör att vi kan anpassa rubriken på vårt kalkylblad:
```csharp
PageSetup pageSetup = workbook.Worksheets[0].PageSetup;
```
## Steg 6: Infoga logotypen i rubriken
Bädda in bilden i kalkylbladets rubriksektion.
Detta är det magiska ögonblicket! Vi kommer att infoga vår logotyp i den centrala delen av rubriken:
```csharp
// Ställ in logotypen/bilden i mitten av sidhuvudet.
pageSetup.SetHeaderPicture(1, binaryData);
// Ställ in manuset för logotypen/bilden
pageSetup.SetHeader(1, "&G");
// Ställ in arkets namn i den högra delen av sidhuvudet med skriptet
pageSetup.SetHeader(2, "&A");
```
## Steg 7: Spara din arbetsbok
Spara dina ändringar i en ny Excel-fil.
Efter att ha konfigurerat allt är det dags att spara vår arbetsbok. Se till att ange ett nytt namn för din utdatafil:
```csharp
workbook.Save(dataDir + "InsertImageInHeaderFooter_out.xls");
```
## Steg 8: Rensa upp resurser
Stäng FileStream för att frigöra resurser.
 Slutligen, efter all manipulation, glöm inte att städa genom att stänga din`FileStream`!
```csharp
inFile.Close();
```
## Slutsats
Och där har du det! Du har framgångsrikt infogat en bild i sidhuvudet/sidfoten i ett Excel-kalkylblad med Aspose.Cells för .NET. Det är enkelt, eller hur? När du förstår stegen kan du anpassa den ytterligare för att passa dina specifika behov. Oavsett om du letar efter varumärkesrapporter för ditt företag eller bara lägger till en personlig touch, är den här tekniken otroligt användbar. 
## FAQ's
### Kan jag använda vilket bildformat som helst?
Ja, Aspose.Cells stöder olika bildformat inklusive JPEG, PNG och BMP för sidhuvud och sidfotsbilder.
### Är Aspose.Cells gratis att använda?
 Aspose.Cells erbjuder en gratis provperiod, men för fortsatt användning måste du köpa en licens. Läs mer om prissättning[här](https://purchase.aspose.com/buy).
### Hur kommer jag åt Aspose.Cells dokumentation?
 Du kan dyka djupt in i funktionerna och funktionerna i Aspose.Cells genom att besöka[dokumentation](https://reference.aspose.com/cells/net/).
### Kan jag använda Aspose.Cells utan Visual Studio?
Ja, så länge du har .NET runtime-miljön kan du använda Aspose.Cells i vilken .NET-kompatibel utvecklingsmiljö som helst.
### Vad ska jag göra om jag stöter på problem?
 Om du stöter på några problem eller behöver support, kontrollera[Aspose supportforum](https://forum.aspose.com/c/cells/9) för hjälp från samhället och utvecklare.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
