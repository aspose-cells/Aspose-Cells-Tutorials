---
title: Implementera sidhuvud och sidfot i kalkylblad
linktitle: Implementera sidhuvud och sidfot i kalkylblad
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du ställer in sidhuvuden och sidfötter i Excel-kalkylblad med Aspose.Cells för .NET med en steg-för-steg handledning, praktiska exempel och användbara tips.
weight: 22
url: /sv/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Implementera sidhuvud och sidfot i kalkylblad

## Introduktion

När du arbetar med Excel-kalkylblad spelar sidhuvuden och sidfötter en nyckelroll för att leverera viktig kontextuell information, som filnamn, datum eller sidnummer, till din publik. Oavsett om du automatiserar rapporter eller genererar dynamiska filer, gör Aspose.Cells för .NET det enkelt att anpassa sidhuvuden och sidfötter i kalkylblad programmatiskt. Den här guiden dyker ner i en omfattande, steg-för-steg-metod för att lägga till sidhuvuden och sidfötter med Aspose.Cells för .NET, vilket ger dina Excel-filer en extra snygg och professionalism.

## Förutsättningar

Innan du börjar, se till att du har följande på plats:

1.  Aspose.Cells för .NET: Du behöver Aspose.Cells för .NET installerat.[Ladda ner den här](https://releases.aspose.com/cells/net/).
2. IDE-installation: Visual Studio (eller din föredragna IDE) med .NET framework installerat.
3.  Licens: Även om du kan komma igång med den kostnadsfria provperioden, kommer en fullständig eller tillfällig licens att låsa upp Aspose.Cells fulla potential.[Skaffa en tillfällig licens](https://purchase.aspose.com/temporary-license/).

Dokumentationen för Aspose.Cells är en praktisk resurs för referens under hela denna process. Du kan hitta den[här](https://reference.aspose.com/cells/net/).

## Importera paket

Importera de nödvändiga namnrymden i ditt projekt:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Genom att importera det här paketet får du tillgång till de klasser och metoder som behövs för att arbeta med sidhuvuden, sidfötter och andra Excel-funktioner inom Aspose.Cells.

I den här guiden kommer vi att dela upp varje steg så att du enkelt kan följa med, även om du är ny på Aspose.Cells eller .NET.

## Steg 1: Konfigurera din arbetsbok och sidinställningar

Först till kvarn: skapa en ny arbetsbok och få tillgång till kalkylbladets sidinställningar. Detta ger dig de verktyg du behöver för att ändra sidhuvudet och sidfoten för kalkylbladet.

```csharp
// Definiera sökvägen för att spara ditt dokument
string dataDir = "Your Document Directory";

// Instantiera ett arbetsboksobjekt
Workbook excel = new Workbook();
```

 Här har vi skapat en`Workbook` objekt, som representerar vår Excel-fil. De`PageSetup` i kalkylbladet är där vi kan ändra sidhuvud och sidfotsalternativ.


## Steg 2: Öppna kalkylbladet och egenskaperna för sidinställningar

 I Aspose.Cells har varje kalkylblad en`PageSetup`egenskap som styr layoutfunktioner, inklusive sidhuvuden och sidfötter. Låt oss ta`PageSetup` objekt för vårt arbetsblad.

```csharp
// Skaffa referensen till PageSetup för det första kalkylbladet
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Med detta,`pageSetup` innehåller nu alla inställningar som behövs för att anpassa sidhuvuden och sidfötter.


## Steg 3: Ställ in den vänstra delen av rubriken

Rubriker i Excel är indelade i tre sektioner: vänster, mitten och höger. Låt oss börja med att ställa in den vänstra delen för att visa kalkylbladets namn.

```csharp
// Ange kalkylbladsnamn till vänster i rubriken
pageSetup.SetHeader(0, "&A");
```

 Använder`&A` låter dig visa kalkylbladets namn dynamiskt. Detta är särskilt användbart om du har flera ark i en arbetsbok och vill att varje rubrik ska återspegla dess arktitel.


## Steg 4: Lägg till datum och tid i mitten av rubriken

Låt oss sedan lägga till aktuellt datum och tid i mitten av rubriken. Dessutom kommer vi att använda ett anpassat teckensnitt för styling.

```csharp
// Ställ in datum och tid i mitten av rubriken med fet stil
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

I denna kod:
- `&D`infogar aktuellt datum.
- `&T` infogar aktuell tid.
- `"Times New Roman,Bold"` tillämpar Times New Roman i fetstil på dessa element.


## Steg 5: Visa filnamnet i den högra delen av rubriken

För att slutföra rubriken, låt oss visa filnamnet på höger sida, tillsammans med en teckensnittsjustering.

```csharp
// Visa filnamnet i den högra delen av rubriken med anpassad teckenstorlek
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` representerar filnamnet, vilket gör det tydligt vilken fil de utskrivna sidorna tillhör.
- `&12` ändrar teckenstorleken till 12 för det här avsnittet.


## Steg 6: Lägg till text med anpassat teckensnitt i den vänstra sidfotssektionen

Går vidare till sidfötter! Vi börjar med att ställa in den vänstra sidfotssektionen med anpassad text och en specificerad typsnittsstil.

```csharp
// Lägg till anpassad text med typsnittsstil till den vänstra delen av sidfoten
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

 De`&\"Courier New\"&14` inställningen i ovanstående kod tillämpar typsnittet "Courier New" med storlek 14 på den angivna texten (`123`). Resten av texten finns kvar i standardfonten för sidfot.


## Steg 7: Infoga sidnummer i mitten av sidfoten

Att inkludera sidnummer i sidfoten är ett utmärkt sätt att hjälpa läsarna att hålla reda på flersidiga dokument.

```csharp
// Infoga sidnummer i mitten av sidfoten
pageSetup.SetFooter(1, "&P");
```

 Här,`&P` lägger till det aktuella sidnumret i sidfotens mittsektion. Det är en liten detalj, men avgörande för professionella dokument.


## Steg 8: Visa totalt antal sidor i höger sidfotssektion

Slutligen, låt oss slutföra sidfoten genom att visa det totala antalet sidor i det högra avsnittet.

```csharp
// Visa det totala antalet sidor i den högra delen av sidfoten
pageSetup.SetFooter(2, "&N");
```

- `&N` ger det totala antalet sidor och låter läsarna veta hur långt dokumentet är.


## Steg 9: Spara arbetsboken

När du har ställt in dina sidhuvuden och sidfötter är det dags att spara arbetsboken. Detta är det sista steget för att skapa en Excel-fil med helt anpassade sidhuvuden och sidfötter.

```csharp
// Spara arbetsboken
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Den här raden sparar filen i din angivna katalog med anpassade sidhuvuden och sidfötter på plats.


## Slutsats

Att lägga till sidhuvuden och sidfötter i Excel-kalkylblad är en värdefull färdighet för att skapa organiserade, professionella dokument. Med Aspose.Cells för .NET har du fullständig kontroll över dina Excel-filers sidhuvuden och sidfötter, från att visa kalkylbladets namn till att infoga anpassad text, datum, tid och till och med dynamiska sidnummer. Nu när du har sett varje steg i aktion kan du ta din Excel-automatisering till nästa nivå.

## FAQ's

### Kan jag använda olika typsnitt för olika sektioner av sidhuvuden och sidfötter?  
Ja, Aspose.Cells för .NET låter dig ange teckensnitt för varje sektion av sidhuvudet och sidfoten med hjälp av specifika teckensnittstaggar.

### Hur tar jag bort sidhuvuden och sidfötter?  
 Du kan rensa sidhuvuden och sidfötter genom att ställa in sidhuvudet eller sidfoten till en tom sträng med`SetHeader` eller`SetFooter`.

### Kan jag infoga bilder i sidhuvuden eller sidfötter med Aspose.Cells för .NET?  
För närvarande stöder Aspose.Cells främst text i sidhuvuden och sidfötter. Bilder kan kräva en lösning, som att infoga bilder i själva kalkylbladet.

### Stöder Aspose.Cells dynamisk data i sidhuvuden och sidfötter?  
 Ja, du kan använda olika dynamiska koder (som`&D` för datum eller`&P` för sidnummer) för att lägga till dynamiskt innehåll.

### Hur kan jag justera sidhuvudet eller sidfotens höjd?  
 Aspose.Cells tillhandahåller alternativ inom`PageSetup` klass för att justera sidhuvuds- och sidfotsmarginaler, vilket ger dig kontroll över avståndet.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
