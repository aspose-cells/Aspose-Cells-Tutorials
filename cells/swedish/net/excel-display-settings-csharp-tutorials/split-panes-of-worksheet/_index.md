---
"description": "Lär dig hur du delar upp kalkylbladsrutor i Aspose.Cells för .NET med vår steg-för-steg-guide. Förbättra navigeringen i Excel-filer med den här enkla handledningen."
"linktitle": "Dela upp paneler i arbetsblad"
"second_title": "Aspose.Cells för .NET API-referens"
"title": "Dela upp paneler i arbetsblad"
"url": "/sv/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dela upp paneler i arbetsblad

## Introduktion

Är du redo att dela upp rutorna i ett Excel-kalkylblad med Aspose.Cells för .NET? Tänk dig detta: du har ett gigantiskt Excel-ark och är trött på att ständigt skrolla tillbaka till rubrikerna bara för att komma ihåg vilken kolumn du arbetar med. Skriv in "Dela rutor". Den här praktiska funktionen låter dig frysa en del av ditt kalkylblad, vilket gör det mycket enklare att navigera. Oavsett om du arbetar med finansiell data, lagerhantering eller massiva datamängder kan delning av rutor öka din produktivitet tiofalt. 

## Förkunskapskrav

Innan vi börjar dela upp rutor som en kalkylbladsguide, låt oss få inställningarna rätt. Här är vad du behöver:

- Aspose.Cells för .NET: Se till att du har laddat ner och installerat det. Om du inte redan har gjort det, ladda ner det. [här](https://releases.aspose.com/cells/net/).
- .NET Framework: Den här guiden förutsätter att du arbetar i en .NET-miljö.
- En Excel-arbetsbok: Vi använder en exempelfil i Excel för att visa hur den här funktionen fungerar.
- En tillfällig eller fullständig licens: Aspose.Cells kräver en licens. Om du bara testar det, skaffa en [gratis tillfällig licens](https://purchase.aspose.com/temporary-license/) för att undvika utvärderingsbegränsningar.

## Importera paket

Innan vi går in i koden, låt oss först importera de nödvändiga namnrymderna. Du kan egentligen inte göra någonting i Aspose.Cells utan att inkludera dessa.

```csharp
using System.IO;
using Aspose.Cells;
```

Nu när vi har täckt det viktigaste, låt oss gå vidare till den spännande delen – att dela upp rutor!

## Steg 1: Instansiera en arbetsbok

Det första steget i denna process är att skapa en `Workbook` objekt, vilket representerar den Excel-fil du vill ändra. I det här fallet laddar vi en fil från en katalog. Detta är din arbetsyta, Excel-arket som du kommer att arbeta med din magi på.

Innan vi kan dela upp rutor behöver vi en arbetsbok att arbeta med! Det här steget är lika viktigt som att öppna en bok innan du börjar läsa den.

```csharp
// Sökvägen till dokumentkatalogen
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Instantiera en ny arbetsbok och öppna en mallfil
Workbook book = new Workbook(dataDir + "Book1.xls");
```

I koden ovan, ersätt `"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen dit din Excel-fil finns. `Workbook` klassen laddar Excel-filen till minnet.

## Steg 2: Ställ in den aktiva cellen

Efter att arbetsboken har laddats är det dags att ange den aktiva cellen. I Excel-termer är den aktiva cellen den som för närvarande är markerad eller i fokus. I den här handledningen kommer vi att markera celler. `A20` i det första arbetsbladet.

Att ställa in den aktiva cellen är avgörande eftersom paneldelningen börjar från denna aktiva cell. Det är som att välja var du ska göra det första snittet i en pizza – välj din bit!

```csharp
// Ställ in den aktiva cellen
book.Worksheets[0].ActiveCell = "A20";
```

Den här kodbiten gör `A20` den aktiva cellen. Det är viktigt eftersom delningen sker runt den här punkten, precis som hur din navigering i Excel ofta centreras kring en specifik cell.

## Steg 3: Dela upp arbetsbladet

Nu när den aktiva cellen är inställd, låt oss gå vidare till den roliga delen – att dela upp kalkylbladet! Det är i det här steget som magin händer. Du kommer att kunna dela upp kalkylbladet i flera rutor för enklare visning och navigering.

Detta är kärnan i hela handledningen. Genom att dela upp kalkylbladet skapar du separata rutor som låter dig bläddra igenom olika avsnitt i ditt Excel-ark utan att tappa rubriker eller andra viktiga områden ur sikte.

```csharp
// Dela kalkylbladsfönstret
book.Worksheets[0].Split();
```

Med den `Split()` metod, du säger till Aspose.Cells att dela kalkylbladet vid den aktiva cellen (`A20` (i det här fallet). Från och med nu skapar Excel en indelning i arket som separerar rutor så att du kan navigera oberoende av varandra.

## Steg 4: Spara arbetsboken

Efter att du har delat upp rutorna är allt som återstår att spara ditt arbete. Detta sista steg säkerställer att dina ändringar sparas i den angivna utdatafilen.

Vad är poängen med allt ditt hårda arbete om du inte sparar det? Att spara säkerställer att dina vackert delade rutor bevaras intakta för framtida bruk.

```csharp
// Spara Excel-filen
book.Save(dataDir + "output.xls");
```

Här, den `Save()` Metoden sparar arbetsboken med dina nyligen delade rutor till en Excel-fil. Ändringarna du gjort är nu redo för dig – eller någon annan – att använda.

## Slutsats

Och där har du det! Du har precis lärt dig hur man delar upp rutor i ett Excel-kalkylblad med Aspose.Cells för .NET. Inget mer oändligt skrollande eller att tappa bort dina data. Den här metoden gör hanteringen av stora Excel-filer mycket mindre överväldigande och mycket effektivare. Med möjligheten att dela upp rutor kan du nu hålla reda på viktiga datapunkter medan du arbetar med komplexa kalkylblad.

## Vanliga frågor

### Kan jag dela fler än två rutor?  
Ja, du kan dela upp kalkylbladet i flera rutor genom att ange olika aktiva celler och anropa `Split()` metod.

### Vad är skillnaden mellan att dela rutor och att frysa rutor?  
Genom att dela rutor kan du rulla i båda rutorna oberoende av varandra. Att frysa rutor låser rubrikerna eller specifika rader/kolumner så att de förblir synliga när du rullar.

### Kan jag ta bort splitten efter att jag har applicerat den?  
Ja, du kan ta bort delningen genom att antingen stänga och öppna arbetsboken igen eller genom att återställa den programmatiskt.

### Fungerar dela rutor på samma sätt för olika Excel-filformat (XLS, XLSX)?  
Ja, den `Split()` Metoden fungerar för både XLS- och XLSX-format.

### Kan jag använda Aspose.Cells utan licens?  
Ja, men det har sina begränsningar. För en fullständig upplevelse är det bäst att använda en [tillfällig](https://purchase.aspose.com/tempellerary-license/) or [betald licens](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}