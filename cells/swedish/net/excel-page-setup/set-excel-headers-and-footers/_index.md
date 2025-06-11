---
"description": "Lär dig hur du enkelt ställer in sidhuvuden och sidfot i Excel med Aspose.Cells för .NET med vår steg-för-steg-guide. Perfekt för professionella dokument."
"linktitle": "Ställ in sidhuvuden och sidfot i Excel"
"second_title": "Aspose.Cells för .NET API-referens"
"title": "Ställ in sidhuvuden och sidfot i Excel"
"url": "/sv/net/excel-page-setup/set-excel-headers-and-footers/"
"weight": 100
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in sidhuvuden och sidfot i Excel

## Introduktion

När det gäller att hantera kalkylbladsdokument spelar sidhuvuden och sidfot en avgörande roll för att ge sammanhang. Tänk dig att du öppnar en Excel-fil och högst upp ser du namnet på kalkylbladet, datumet och kanske till och med filnamnet. Det ger ditt dokument en professionell touch och hjälper till att kommunicera viktiga detaljer med en snabb blick. Om du vill förbättra professionalismen i dina Excel-ark med Aspose.Cells för .NET har du kommit rätt! I den här guiden guidar vi dig genom stegen för att enkelt ställa in sidhuvuden och sidfot i dina Excel-kalkylblad. 

## Förkunskapskrav

Innan vi går in på detaljerna, låt oss se till att du har allt du behöver för att komma igång. Först behöver du:

1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Det är här du kommer att skriva och exekvera din C#-kod.
2. Aspose.Cells för .NET-biblioteket: Du behöver ha Aspose.Cells-biblioteket. Om du inte redan har gjort det kan du ladda ner det från [här](https://releases.aspose.com/cells/net/).
3. Grundläggande förståelse för C#: Bekantskap med C#-programmering är avgörande, eftersom alla kodexempel kommer att vara i detta språk.
4. En projektuppsättning: Skapa ett nytt C#-projekt i Visual Studio där vi ska implementera vår Excel-sidhuvud-/sidfotslogik.

När du väl har bekräftat att du uppfyller ovanstående förutsättningar är det dags att sätta igång!

## Importera paket

För att börja arbeta med Aspose.Cells måste du importera lämpliga namnrymder i din C#-kod.

### Öppna ditt C#-projekt

Öppna ditt projekt i Visual Studio där du vill implementera inställningarna för sidhuvud och sidfot. Se till att du har en tydlig struktur som kan hantera din kod.

### Lägg till referens till Aspose.Cells

Efter att du har skapat eller öppnat ditt projekt måste du lägga till en referens till Aspose.Cells-biblioteket. Högerklicka på ditt projekt i Solution Explorer, välj "Hantera NuGet-paket" och sök efter 'Aspose.Cells'. Installera det i ditt projekt.

### Importera namnrymden

Lägg till följande rad högst upp i din C#-fil för att importera namnrymden Aspose.Cells:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Genom att importera detta namnutrymme kan du använda funktionerna som tillhandahålls av Aspose.Cells-biblioteket utan hinder.

Toppen! Nu när din miljö är konfigurerad och dina paket har importerats, låt oss gå igenom processen för att ställa in sidhuvuden och sidfot i Excel steg för steg.

## Steg 1: Initiera arbetsboken

Först måste vi instansiera ett arbetsboksobjekt, som representerar vår Excel-fil i minnet.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Workbook excel = new Workbook();
```

Förklaring: Ersätt här `YOUR DOCUMENT DIRECTORY` med den faktiska sökvägen dit du vill spara din Excel-fil. Den `Workbook` objektet är din huvudsakliga ingångspunkt för att skapa och manipulera Excel-filer.

## Steg 2: Hämta referens för PageSetup

Nästa steg är att vi behöver komma åt `PageSetup` egenskapen för kalkylbladet där vi vill ange sidhuvuden och sidfoten.

```csharp
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

Förklaring: Vi öppnar det första arbetsbladet (index `0`) i vår arbetsbok. Den `PageSetup` Klassen tillhandahåller egenskaper och metoder för att anpassa hur sidan ser ut när den skrivs ut, inklusive sidhuvud och sidfot.

## Steg 3: Ställ in rubriken

Nu ska vi börja konfigurera rubriken. Vi börjar med den vänstra delen:

```csharp
pageSetup.SetHeader(0, "&A");
```

Förklaring: Den `SetHeader` Metoden låter oss definiera innehållet i rubriken. Här, `&A` anger namnet på kalkylbladet, vilket kommer att visas till vänster om sidhuvudet.

## Steg 4: Anpassa den centrala rubriken

Nästa steg är att anpassa den centrala rubriken för att visa aktuellt datum och tid med ett specifikt teckensnitt.

```csharp
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

Förklaring: Den `&D` och `&T` Koder kommer automatiskt att ersätta sig själva med aktuellt datum respektive tid. Vi anger också att teckensnittet för denna rubrik ska vara "Times New Roman" och fetstil.

## Steg 5: Ställ in rätt rubrik

Låt oss nu ställa in den högra delen av rubriken för att visa filnamnet.

```csharp
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

Förklaring: Här, `&F` kommer att ersättas av filnamnet. Vi använder samma teckensnitt som vi gjorde för den centrala rubriken för att bibehålla ett enhetligt utseende.

## Steg 6: Konfigurera sidfoten

Nu när våra sidhuvuden ser snygga ut, låt oss rikta vår uppmärksamhet mot sidfoten. Vi börjar med den vänstra sidfoten:

```csharp
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

Förklaring: Vi infogar ett anpassat meddelande i vänster sidfot, "Hej världen!" tillsammans med texten `123` i ett annat typsnitt – Courier New.

## Steg 7: Konfiguration av mittfot

Sedan ställer vi in mittfoten för att visa aktuellt sidnummer:

```csharp
pageSetup.SetFooter(1, "&P");
```

Förklaring: Den `&P` Koden infogar automatiskt sidnumret i mitten av sidfoten – ett praktiskt sätt att hålla reda på sidor.

## Steg 8: Konfiguration av höger sidfot

För att avsluta våra sidfotsinställningar, låt oss ställa in den högra sidfoten så att den visar det totala antalet sidor i dokumentet.

```csharp
pageSetup.SetFooter(2, "&N");
```

Förklaring: Här, `&N` kommer att ersättas av det totala antalet sidor. Det ger en professionell touch, särskilt för längre dokument.

## Steg 9: Spara arbetsboken

När allt är klart behöver du bara spara arbetsboken för att se frukterna av ditt arbete.

```csharp
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

Förklaring: Ersätt `"SetHeadersAndFooters_out.xls"` med önskat filnamn. Spara din arbetsbok, så är du klar!

## Slutsats

Och där har du det! Att ställa in sidhuvuden och sidfot i Excel med Aspose.Cells för .NET är enkelt om du följer dessa steg. Du har inte bara förbättrat ditt dokuments utseende utan också dess funktionalitet genom att ge viktig kontext. Oavsett om du förbereder rapporter, delar mallar eller bara organiserar dina data, ger sidhuvuden och sidfot en professionell känsla som är svår att slå. Så prova och se hur enkelt det är att hantera dina Excel-dokument med detta kraftfulla bibliotek!

## Vanliga frågor

### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som används för att skapa, manipulera och rendera Excel-filer programmatiskt.

### Kan jag prova Aspose.Cells gratis?
Ja! Du kan ladda ner en gratis provversion från [här](https://releases.aspose.com/).

### Är Aspose.Cells kompatibelt med äldre Excel-format?
Absolut! Aspose.Cells stöder både gamla och nya Excel-filformat.

### Var kan jag hitta mer dokumentation?
Du kan kontrollera den detaljerade dokumentationen på [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/).

### Hur får jag support för Aspose.Cells?
För support, besök [Aspose Supportforum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}