---
"description": "Lär dig hur du konfigurerar sidhuvuden och sidfot i Excel-kalkylblad med Aspose.Cells för .NET med en steg-för-steg-handledning, praktiska exempel och användbara tips."
"linktitle": "Implementera sidhuvud och sidfot i kalkylblad"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Implementera sidhuvud och sidfot i kalkylblad"
"url": "/sv/net/worksheet-page-setup-features/implement-header-and-footer/"
"weight": 22
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Implementera sidhuvud och sidfot i kalkylblad

## Introduktion

När du arbetar med Excel-kalkylblad spelar sidhuvuden och sidfot en nyckelroll för att leverera viktig kontextuell information, som filnamn, datum eller sidnummer, till din publik. Oavsett om du automatiserar rapporter eller genererar dynamiska filer gör Aspose.Cells för .NET det enkelt att anpassa sidhuvuden och sidfot i kalkylblad programmatiskt. Den här guiden går in på en omfattande steg-för-steg-metod för att lägga till sidhuvuden och sidfot med Aspose.Cells för .NET, vilket ger dina Excel-filer extra glans och professionalism.

## Förkunskapskrav

Innan du börjar, se till att du har följande på plats:

1. Aspose.Cells för .NET: Du behöver Aspose.Cells för .NET installerat. [Ladda ner den här](https://releases.aspose.com/cells/net/).
2. IDE-installation: Visual Studio (eller din föredragna IDE) med .NET framework installerat.
3. Licens: Även om du kan komma igång med den kostnadsfria provperioden, kommer en fullständig eller tillfällig licens att frigöra Aspose.Cells fulla potential. [Få en tillfällig licens](https://purchase.aspose.com/temporary-license/).

Dokumentationen för Aspose.Cells är en praktisk resurs att använda under hela processen. Du hittar den [här](https://reference.aspose.com/cells/net/).

## Importera paket

Importera de namnrymder som krävs i ditt projekt:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Genom att importera det här paketet får du tillgång till de klasser och metoder som behövs för att arbeta med sidhuvuden, sidfötter och andra Excel-funktioner i Aspose.Cells.

I den här guiden kommer vi att gå igenom varje steg så att du enkelt kan följa med, även om du är nybörjare på Aspose.Cells eller .NET.

## Steg 1: Konfigurera din arbetsbok och sidinställningar

Först och främst: skapa en ny arbetsbok och öppna arbetsbladets sidinställningar. Detta ger dig de verktyg du behöver för att ändra sidhuvudet och sidfoten för arbetsbladet.

```csharp
// Definiera sökvägen för att spara dokumentet
string dataDir = "Your Document Directory";

// Instansiera ett arbetsboksobjekt
Workbook excel = new Workbook();
```

Här har vi skapat en `Workbook` objektet, vilket representerar vår Excel-fil. `PageSetup` i kalkylbladet är där vi kan ändra alternativ för sidhuvud och sidfot.


## Steg 2: Åtkomst till egenskaperna för kalkylblad och sidinställningar

I Aspose.Cells har varje kalkylblad en `PageSetup` egenskap som styr layoutfunktioner, inklusive sidhuvuden och sidfot. Låt oss ta reda på `PageSetup` objekt för vårt arbetsblad.

```csharp
// Hämta referensen till sidinställningarna för det första kalkylbladet
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

Med detta, `pageSetup` innehåller nu alla inställningar som behövs för att anpassa sidhuvuden och sidfot.


## Steg 3: Ställ in den vänstra delen av rubriken

Rubriker i Excel är indelade i tre sektioner: vänster, centrerad och höger. Låt oss börja med att ställa in den vänstra sektionen för att visa kalkylbladets namn.

```csharp
// Ange kalkylbladets namn i vänster del av rubriken
pageSetup.SetHeader(0, "&A");
```

Användning `&A` låter dig visa kalkylbladets namn dynamiskt. Detta är särskilt användbart om du har flera blad i en arbetsbok och vill att varje rubrik ska återspegla dess bladtitel.


## Steg 4: Lägg till datum och tid i mitten av rubriken

Nu lägger vi till aktuellt datum och tid i mitten av rubriken. Dessutom använder vi ett anpassat teckensnitt för stilen.

```csharp
// Ange datum och tid i mitten av rubriken med fetstil
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

I den här koden:
- `&D` infogar aktuellt datum.
- `&T` infogar aktuell tid.
- `"Times New Roman,Bold"` tillämpar Times New Roman i fetstil på dessa element.


## Steg 5: Visa filnamnet i den högra delen av rubriken

För att komplettera rubriken visar vi filnamnet på höger sida, tillsammans med en justering av teckensnittet.

```csharp
// Visa filnamnet i högra delen av rubriken med anpassad teckenstorlek
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F` representerar filnamnet, vilket tydligt visar vilken fil de utskrivna sidorna tillhör.
- `&12` ändrar teckenstorleken till 12 för det här avsnittet.


## Steg 6: Lägg till text med anpassat teckensnitt i vänster sidfot

Vi går vidare till sidfot! Vi börjar med att konfigurera den vänstra sidfotssektionen med anpassad text och ett specificerat teckensnitt.

```csharp
// Lägg till anpassad text med teckensnittsstil i vänster del av sidfoten
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

De `&\"Courier New\"&14` Inställningen i koden ovan tillämpar teckensnittet "Courier New" med storlek 14 på den angivna texten (`123`Resten av texten bibehålls med standardteckensnittet för sidfoten.


## Steg 7: Infoga sidnummer i mitten av sidfoten

Att inkludera sidnummer i sidfoten är ett bra sätt att hjälpa läsare att hålla koll på dokument med flera sidor.

```csharp
// Infoga sidnummer i mitten av sidfoten
pageSetup.SetFooter(1, "&P");
```

Här, `&P` lägger till det aktuella sidnumret i sidfotens mittsektion. Det är en liten detalj, men avgörande för professionellt utseende dokument.


## Steg 8: Visa totalt antal sidor i högersidfoten

Slutligen, låt oss komplettera sidfoten genom att visa det totala antalet sidor i den högra sektionen.

```csharp
// Visa totalt antal sidor i högra delen av sidfoten
pageSetup.SetFooter(2, "&N");
```

- `&N` anger det totala sidantalet och låter läsarna veta hur långt dokumentet är.


## Steg 9: Spara arbetsboken

När du har konfigurerat dina sidhuvuden och sidfot är det dags att spara arbetsboken. Detta är det sista steget för att generera en Excel-fil med helt anpassade sidhuvuden och sidfot.

```csharp
// Spara arbetsboken
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Den här raden sparar filen i din angivna katalog med de anpassade sidhuvuden och sidfoten på plats.


## Slutsats

Att lägga till sidhuvuden och sidfot i Excel-kalkylblad är en värdefull färdighet för att skapa organiserade, professionella dokument. Med Aspose.Cells för .NET har du fullständig kontroll över dina Excel-filers sidhuvuden och sidfot, från att visa kalkylbladets namn till att infoga anpassad text, datum, tid och till och med dynamiska sidnummer. Nu när du har sett varje steg i praktiken kan du ta din Excel-automatisering till nästa nivå.

## Vanliga frågor

### Kan jag använda olika teckensnitt för olika delar av sidhuvuden och sidfoten?  
Ja, Aspose.Cells för .NET låter dig ange teckensnitt för varje sektion av sidhuvudet och sidfoten med hjälp av specifika teckensnittstaggar.

### Hur tar jag bort sidhuvuden och sidfot?  
Du kan rensa sidhuvuden och sidfoten genom att ange en tom sträng för sidhuvudet eller sidfoten med `SetHeader` eller `SetFooter`.

### Kan jag infoga bilder i sidhuvuden eller sidfoten med Aspose.Cells för .NET?  
För närvarande stöder Aspose.Cells främst text i sidhuvuden och sidfot. Bilder kan kräva en lösning, till exempel att infoga bilder i själva kalkylbladet.

### Stöder Aspose.Cells dynamisk data i sidhuvuden och sidfot?  
Ja, du kan använda olika dynamiska koder (som `&D` för datum eller `&P` för sidnummer) för att lägga till dynamiskt innehåll.

### Hur kan jag justera höjden på sidhuvudet eller sidfoten?  
Aspose.Cells erbjuder alternativ inom `PageSetup` klass för att justera marginalerna för sidhuvud och sidfot, vilket ger dig kontroll över avståndet.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}