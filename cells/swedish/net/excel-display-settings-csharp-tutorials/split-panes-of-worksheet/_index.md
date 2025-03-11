---
title: Delade rutor av arbetsblad
linktitle: Delade rutor av arbetsblad
second_title: Aspose.Cells för .NET API-referens
description: Lär dig hur du delar upp kalkylbladsrutor i Aspose.Cells för .NET med vår steg-för-steg-guide. Förbättra Excel-filnavigering med denna enkla handledning.
weight: 130
url: /sv/net/excel-display-settings-csharp-tutorials/split-panes-of-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Delade rutor av arbetsblad

## Introduktion

Är du redo att dela upp rutor i ett Excel-kalkylblad med Aspose.Cells för .NET? Föreställ dig detta: du har ett gigantiskt Excel-ark och du är trött på att ständigt rulla tillbaka till rubrikerna bara för att komma ihåg vilken kolumn du arbetar med. Ange "Delade fönster". Denna praktiska funktion låter dig frysa en del av ditt kalkylblad, vilket gör det mycket lättare att navigera. Oavsett om du arbetar med finansiell data, lagerhantering eller massiva datauppsättningar, kan delade rutor förbättra din produktivitet tiofaldigt. 

## Förutsättningar

Innan vi börjar dela upp rutor som en kalkylbladsguide, låt oss göra rätt inställningar. Här är vad du behöver:

-  Aspose.Cells för .NET: Se till att du har laddat ner och installerat det. Om du inte har gjort det ännu, ta den[här](https://releases.aspose.com/cells/net/).
- .NET Framework: Den här guiden förutsätter att du arbetar i en .NET-miljö.
- En Excel-arbetsbok: Vi använder ett exempel på en Excel-fil för att visa hur den här funktionen fungerar.
-  En tillfällig eller fullständig licens: Aspose.Cells kräver en licens. Om du bara provar det, skaffa en[gratis tillfällig licens](https://purchase.aspose.com/temporary-license/) för att undvika utvärderingsbegränsningar.

## Importera paket

Innan vi dyker in i kod, låt oss först importera de nödvändiga namnrymden. Du kan egentligen inte göra någonting i Aspose.Cells utan att inkludera dessa.

```csharp
using System.IO;
using Aspose.Cells;
```

Nu när vi har täckt det väsentliga, låt oss gå vidare till den spännande delen – dela rutorna!

## Steg 1: Instantiera en arbetsbok

 Det första steget i denna process är att skapa en`Workbook` objekt, som kommer att representera Excel-filen du vill ändra. I det här fallet kommer vi att ladda en fil från en katalog. Det här är din duk, Excel-arket som du ska arbeta med din magi på.

Innan vi kan dela upp rutor behöver vi en arbetsbok att arbeta med! Detta steg är lika viktigt som att öppna en bok innan du börjar läsa den.

```csharp
// Sökvägen till dokumentkatalogen
string dataDir = "YOUR DOCUMENT DIRECTORY";

// Instantiera en ny arbetsbok och öppna en mallfil
Workbook book = new Workbook(dataDir + "Book1.xls");
```

 I koden ovan, ersätt`"YOUR DOCUMENT DIRECTORY"` med den faktiska sökvägen där din Excel-fil finns. De`Workbook`klass laddar Excel-filen i minnet.

## Steg 2: Ställ in den aktiva cellen

 Efter att ha laddat arbetsboken är det dags att ställa in den aktiva cellen. I Excel-termer är den aktiva cellen den som för närvarande är vald eller i fokus. I den här handledningen väljer vi cell`A20` i det första arbetsbladet.

Att ställa in den aktiva cellen är avgörande eftersom rutuppdelningen börjar från denna aktiva cell. Det är som att välja var du ska göra det första snittet i en pizza – välj din skiva!

```csharp
// Ställ in den aktiva cellen
book.Worksheets[0].ActiveCell = "A20";
```

 Denna kodbit gör`A20` den aktiva cellen. Det är viktigt eftersom delning sker runt denna punkt, precis som hur din navigering i Excel ofta centreras kring en specifik cell.

## Steg 3: Dela upp arbetsbladet

Nu när den aktiva cellen är inställd, låt oss gå till den roliga delen – dela upp kalkylbladet! Det här steget är där magin händer. Du kommer att kunna dela upp kalkylbladet i flera rutor för enklare visning och navigering.

Detta är kärnan i hela handledningen. Genom att dela upp kalkylbladet skapar du separata rutor som låter dig bläddra igenom olika delar av ditt Excel-ark utan att tappa rubriker eller andra viktiga områden ur sikte.

```csharp
// Dela upp kalkylbladets fönster
book.Worksheets[0].Split();
```

 Med`Split()` metod, säger du till Aspose.Cells att dela upp kalkylbladet i den aktiva cellen (`A20` i detta fall). Från denna punkt skapar Excel en division i arket som separerar rutor så att du kan navigera självständigt.

## Steg 4: Spara arbetsboken

Efter att ha delat upp rutorna är allt som återstår att spara ditt arbete. Detta sista steg kommer att säkerställa att dina ändringar sparas i den angivna utdatafilen.

Vad hjälper allt ditt hårda arbete om du inte sparar det? Spara säkerställer att dina vackert delade rutor hålls intakta för framtida användning.

```csharp
// Spara Excel-filen
book.Save(dataDir + "output.xls");
```

 Här, den`Save()` metod sparar arbetsboken med dina nyligen delade rutor till en utdata Excel-fil. Ändringarna du gjort är nu redo för dig – eller någon annan – att använda.

## Slutsats

Och där har du det! Du har precis lärt dig hur du delar upp rutor i ett Excel-kalkylblad med Aspose.Cells för .NET. Inget mer oändligt rullande eller tappa reda på dina data. Denna metod gör hanteringen av stora Excel-filer mycket mindre överväldigande och mycket effektivare. Med möjligheten att dela rutor kan du nu hålla reda på viktiga datapunkter medan du arbetar med komplexa kalkylblad.

## FAQ's

### Kan jag dela upp fler än två rutor?  
 Ja, du kan dela upp kalkylbladet i flera rutor genom att ange olika aktiva celler och anropa`Split()` metod.

### Vad är skillnaden mellan att dela rutor och frysa rutor?  
Med delade rutor kan du rulla i båda rutor oberoende av varandra. Frysande rutor låser rubrikerna eller specifika rader/kolumner så att de förblir synliga när du rullar.

### Kan jag ta bort splitten efter att ha applicerat den?  
Ja, du kan ta bort uppdelningen genom att antingen stänga och öppna arbetsboken igen eller genom att programmera återställa den.

### Fungerar delningsrutor på samma sätt för olika Excel-filformat (XLS, XLSX)?  
 Ja, den`Split()` Metoden fungerar för både XLS- och XLSX-format.

### Kan jag använda Aspose.Cells utan licens?  
 Ja, men det kommer med begränsningar. För en fullständig upplevelse är det bäst att använda en[tillfällig](https://purchase.aspose.com/temporary-license/) eller[betald licens](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
