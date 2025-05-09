---
"description": "Lär dig hur du använder villkorsstyrd formatering vid körning i Excel med Aspose.Cells för .NET i den här omfattande steg-för-steg-guiden."
"linktitle": "Använda villkorsstyrd formatering vid körning i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Använda villkorsstyrd formatering vid körning i Excel"
"url": "/sv/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Använda villkorsstyrd formatering vid körning i Excel

## Introduktion

De är kraftfulla verktyg för dataanalys och visualisering. En av de mest framstående funktionerna i Excel är villkorsstyrd formatering, som gör det möjligt för användare att tillämpa specifika formateringsstilar på celler baserat på deras värden. Detta kan göra det enklare att identifiera trender, markera viktiga datapunkter eller helt enkelt göra data mer läsbar. Om du vill implementera villkorsstyrd formatering i dina Excel-filer programmatiskt har du kommit rätt! I den här guiden går vi igenom hur du tillämpar villkorsstyrd formatering vid körning med Aspose.Cells för .NET.

## Förkunskapskrav
Innan vi går in i koden, låt oss se till att du har allt du behöver för att komma igång:

1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Du kan använda vilken version som helst som stöder .NET-utveckling.
2. Aspose.Cells för .NET: Du måste ha Aspose.Cells för .NET installerat. Du kan ladda ner det från [Aspose webbplats](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
4. .NET Framework: Se till att ditt projekt riktar sig mot en kompatibel version av .NET Framework.

Nu när vi har täckt förkunskaperna, låt oss hoppa in i det roliga!

## Importera paket
För att komma igång med Aspose.Cells måste du importera de nödvändiga namnrymderna i ditt C#-projekt. Så här gör du det:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Dessa namnrymder ger dig tillgång till de klasser och metoder som krävs för att manipulera Excel-filer och tillämpa villkorsstyrd formatering.

Nu ska vi dela upp processen för att tillämpa villkorsstyrd formatering i hanterbara steg.

## Steg 1: Konfigurera ditt projekt
Först och främst måste du skapa ett nytt C#-projekt i Visual Studio. Så här gör du:

1. Öppna Visual Studio och välj Arkiv > Nytt > Projekt.
2. Välj Konsolapp (.NET Framework) och ge ditt projekt ett namn.
3. Klicka på Skapa.

## Steg 2: Lägg till Aspose.Cells-referens
När ditt projekt är konfigurerat måste du lägga till en referens till Aspose.Cells-biblioteket:

1. Högerklicka på ditt projekt i lösningsutforskaren.
2. Välj Hantera NuGet-paket.
3. Sök efter Aspose.Cells och installera det.

Detta gör att du kan använda all funktionalitet som tillhandahålls av Aspose.Cells-biblioteket.

## Steg 3: Skapa ett arbetsboksobjekt
Nu ska vi skapa en ny arbetsbok och ett kalkylblad. Det är här all magi händer:

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Instansiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

I det här steget definierar vi katalogen där vår Excel-fil ska sparas, skapar en ny arbetsbok och öppnar det första kalkylbladet.

## Steg 4: Lägg till villkorsstyrd formatering
Nu ska vi lägga till lite villkorsstyrd formatering. Vi börjar med att skapa ett tomt objekt för villkorsstyrd formatering:

```csharp
// Lägger till en tom villkorsstyrd formatering
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Här lägger vi till en ny samling villkorsstyrd formatering i vårt kalkylblad, som kommer att innehålla våra formateringsregler.

## Steg 5: Definiera formatintervallet
Nästa steg är att ange cellområdet som den villkorliga formateringen ska tillämpas på. Låt oss säga att vi vill formatera den första raden och den andra kolumnen:

```csharp
// Anger intervallet för villkorsstyrd formatering.
CellArea ca = new CellArea();
ca.StartRow =0;
ca.EndRow =0;
ca.StartColumn =0;
ca.EndColumn =0;
fcs.AddArea(ca);

ca = new CellArea();
ca.StartRow =1;
ca.EndRow =1;
ca.StartColumn =1;
ca.EndColumn =1;
fcs.AddArea(ca);
```

I den här koden definierar vi två områden för villkorsstyrd formatering. Det första området är för cellen vid (0,0) och det andra för (1,1). Du kan gärna justera dessa områden baserat på dina specifika behov!

## Steg 6: Lägg till villkor för villkorsstyrd formatering
Nu är det dags att definiera villkoren för vår formatering. Låt oss säga att vi vill markera celler baserat på deras värden:

```csharp
// Lägger till villkor.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Lägger till villkor.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

I det här steget lägger vi till två villkor: ett för värden mellan `A2` och `100`, och en annan för värden mellan `50` och `100`Detta gör att du kan dynamiskt markera celler baserat på deras värden.

## Steg 7: Ställ in formateringsstilar
Med våra villkor på plats kan vi nu ställa in formateringsstilarna. Låt oss ändra bakgrundsfärgen för våra villkor:

```csharp
// Ställer in bakgrundsfärgen.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Här ställer vi in bakgrundsfärgen för det första villkoret till röd. Du kan anpassa detta ytterligare genom att ändra teckenfärg, ramar och andra stilar efter behov!

## Steg 8: Spara Excel-filen
Äntligen är det dags att spara vårt arbete! Vi sparar arbetsboken i den angivna katalogen:

```csharp
// Spara Excel-filen
workbook.Save(dataDir + "output.xls");
```

Den här kodraden sparar Excel-filen med villkorsstyrd formatering. Se till att kontrollera den angivna katalogen för din utdatafil!

## Slutsats
Och där har du det! Du har framgångsrikt tillämpat villkorsstyrd formatering vid körning i Excel med hjälp av Aspose.Cells för .NET. Detta kraftfulla bibliotek gör det enkelt att manipulera Excel-filer programmatiskt, vilket gör att du kan automatisera tråkiga uppgifter och förbättra dina datapresentationer. Oavsett om du arbetar med ett litet projekt eller en storskalig applikation kan Aspose.Cells hjälpa dig att effektivisera ditt arbetsflöde och förbättra din produktivitet.

## Vanliga frågor

### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer programmatiskt.

### Kan jag använda Aspose.Cells med andra programmeringsspråk?
Ja, Aspose.Cells är tillgängligt för flera programmeringsspråk, inklusive Java, Python med flera.

### Finns det en gratis provversion av Aspose.Cells?
Ja, du kan ladda ner en gratis provversion från [Aspose webbplats](https://releases.aspose.com/).

### Hur kan jag få support för Aspose.Cells?
Du kan få stöd genom att besöka [Aspose supportforum](https://forum.aspose.com/c/cells/9).

### Behöver jag en licens för att använda Aspose.Cells?
Ja, en licens krävs för kommersiellt bruk, men du kan begära en tillfällig licens [här](https://purchase.aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}