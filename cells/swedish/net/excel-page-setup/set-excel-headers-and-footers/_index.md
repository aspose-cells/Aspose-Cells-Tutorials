---
title: Ställ in sidhuvuden och sidfötter i Excel
linktitle: Ställ in sidhuvuden och sidfötter i Excel
second_title: Aspose.Cells för .NET API-referens
description: Lär dig hur du enkelt ställer in sidhuvuden och sidfötter i Excel med Aspose.Cells för .NET med vår steg-för-steg-guide. Perfekt för professionella dokument.
weight: 100
url: /sv/net/excel-page-setup/set-excel-headers-and-footers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in sidhuvuden och sidfötter i Excel

## Introduktion

När det gäller att hantera kalkylarksdokument spelar sidhuvuden och sidfötter en avgörande roll för att ge sammanhang. Föreställ dig att öppna en Excel-fil, och högst upp ser du namnet på kalkylbladet, datumet och kanske till och med filnamnet. Det ger ditt dokument en professionell touch och hjälper till att kommunicera viktiga detaljer med ett ögonkast. Om du vill förbättra professionaliteten hos dina Excel-ark med Aspose.Cells för .NET, har du hamnat på rätt plats! I den här guiden går vi igenom stegen för att enkelt ställa in sidhuvuden och sidfötter i dina Excel-kalkylblad. 

## Förutsättningar

Innan vi dyker in i det nitty-gritty, låt oss se till att du har allt du behöver för att komma igång. Först och främst behöver du:

1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Det är här du kommer att skriva och köra din C#-kod.
2.  Aspose.Cells för .NET Library: Du måste ha Aspose.Cells-biblioteket. Om du inte redan har gjort det kan du ladda ner det från[här](https://releases.aspose.com/cells/net/).
3. En grundläggande förståelse för C#: Bekantskap med C#-programmering är avgörande, eftersom alla kodexempel kommer att vara på detta språk.
4. En projektinställning: Skapa ett nytt C#-projekt i Visual Studio där vi kommer att implementera vår Excel sidhuvud/sidfotslogik.

När du har bekräftat att du har ovanstående förutsättningar är det dags att göra oss smutsiga!

## Importera paket

För att börja arbeta med Aspose.Cells måste du importera lämpliga namnområden i din C#-kod.

### Öppna ditt C#-projekt

Öppna ditt projekt i Visual Studio där du vill implementera inställningarna för sidhuvud och sidfot. Se till att du har en tydlig struktur som kan rymma din kod.

### Lägg till referens till Aspose.Cells

När du har skapat eller öppnat ditt projekt måste du lägga till en referens till Aspose.Cells-biblioteket. Högerklicka på ditt projekt i Solution Explorer, välj "Manage NuGet Packages" och sök efter 'Aspose.Cells'. Installera det till ditt projekt.

### Importera namnområdet

Överst i din C#-fil lägger du till följande rad för att importera Aspose.Cells-namnrymden:

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Genom att importera detta namnutrymme kan du använda funktionerna som tillhandahålls av Aspose.Cells-biblioteket utan några hinder.

Stor! Nu när din miljö är konfigurerad och dina paket är importerade, låt oss bryta ner processen för att ställa in sidhuvuden och sidfötter i Excel steg för steg.

## Steg 1: Initiera arbetsboken

Först måste vi instansiera ett arbetsboksobjekt, som representerar vår Excel-fil i minnet.

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY";
Workbook excel = new Workbook();
```

 Förklaring: Här, byt ut`YOUR DOCUMENT DIRECTORY` med den faktiska sökvägen där du vill spara din Excel-fil. De`Workbook` objekt är din huvudsakliga startpunkt för att skapa och manipulera Excel-filer.

## Steg 2: Skaffa referens för PageSetup

 Därefter måste vi komma åt`PageSetup` egenskapen för kalkylbladet där vi vill ställa in sidhuvuden och sidfötter.

```csharp
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

 Förklaring: Vi kommer åt det första kalkylbladet (index`0` ) i vår arbetsbok. De`PageSetup` klass tillhandahåller egenskaper och metoder för att anpassa hur sidan ser ut när den skrivs ut, inklusive sidhuvuden och sidfötter.

## Steg 3: Ställ in rubriken

Låt oss nu börja ställa in rubriken. Vi börjar med det vänstra avsnittet:

```csharp
pageSetup.SetHeader(0, "&A");
```

 Förklaring: The`SetHeader` metoden tillåter oss att definiera innehållet i rubriken. Här,`&A` anger namnet på kalkylbladet, som kommer att visas på vänster sida av rubriken.

## Steg 4: Anpassa den centrala rubriken

Därefter kommer vi att anpassa den centrala rubriken för att visa aktuellt datum och tid i ett specifikt teckensnitt.

```csharp
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

 Förklaring: The`&D` och`&T` koder kommer automatiskt att ersätta sig själva med aktuellt datum respektive tid. Vi anger också att teckensnittet för den här rubriken ska vara "Times New Roman" och fetstil.

## Steg 5: Ställ in rätt rubrik

Låt oss nu ställa in den högra delen av rubriken för att visa namnet på filen.

```csharp
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

 Förklaring: Här,`&F` kommer att ersättas av filnamnet. Vi använder samma typsnitt som vi gjorde för den centrala rubriken för att bibehålla ett konsekvent utseende.

## Steg 6: Konfigurera sidfoten

Nu när våra sidhuvuden ser snygga ut, låt oss rikta vår uppmärksamhet mot sidfötterna. Vi börjar med den vänstra sidfoten:

```csharp
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

Förklaring: Vi infogar ett anpassat meddelande i den vänstra sidfoten, "Hello World!" tillsammans med texten`123` i en annan typsnittsstil—Courier New.

## Steg 7: Centersidfotskonfiguration

Därefter ställer vi in mittsidfoten för att visa det aktuella sidnumret:

```csharp
pageSetup.SetFooter(1, "&P");
```

 Förklaring: The`&P` kod infogar automatiskt sidnumret i mitten av sidfoten – ett praktiskt sätt att hålla reda på sidor.

## Steg 8: Konfiguration av höger sidfot

För att avsluta våra sidfotsinställningar, låt oss ställa in den högra sidfoten så att den visar det totala antalet sidor i dokumentet.

```csharp
pageSetup.SetFooter(2, "&N");
```

 Förklaring: Här,`&N` kommer att ersättas av det totala antalet sidor. Det ger en professionell touch, särskilt för längre dokument.

## Steg 9: Spara arbetsboken

Med allt nu inställt behöver du bara spara arbetsboken för att se frukterna av ditt arbete.

```csharp
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

 Förklaring: Byt ut`"SetHeadersAndFooters_out.xls"` med önskat filnamn. Spara din arbetsbok och du är klar!

## Slutsats

Och där har du det! Att ställa in sidhuvuden och sidfötter i Excel med Aspose.Cells för .NET är enkelt om du följer dessa steg. Du har inte bara förbättrat ditt dokuments utseende utan också förbättrat dess funktionalitet genom att tillhandahålla viktiga sammanhang. Oavsett om du förbereder rapporter, delar mallar eller bara organiserar dina data, tillför sidhuvuden och sidfötter en professionell stil som är svår att slå. Så ge det ett försök och se hur enkelt det är att hantera dina Excel-dokument med detta kraftfulla bibliotek!

## FAQ's

### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som används för att skapa, manipulera och rendera Excel-filer programmatiskt.

### Kan jag prova Aspose.Cells gratis?
 Ja! Du kan ladda ner en gratis testversion från[här](https://releases.aspose.com/).

### Är Aspose.Cells kompatibel med äldre Excel-format?
Absolut! Aspose.Cells stöder både gamla och nya Excel-filformat.

### Var kan jag hitta mer dokumentation?
 Du kan kontrollera den detaljerade dokumentationen på[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/).

### Hur får jag support för Aspose.Cells?
 För support, besök[Aspose Support Forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
