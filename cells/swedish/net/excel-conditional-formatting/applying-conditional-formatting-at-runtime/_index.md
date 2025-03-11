---
title: Tillämpa villkorlig formatering vid körning i Excel
linktitle: Tillämpa villkorlig formatering vid körning i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du använder villkorlig formatering vid körning i Excel med Aspose.Cells för .NET i den här omfattande, steg-för-steg-guiden.
weight: 11
url: /sv/net/excel-conditional-formatting/applying-conditional-formatting-at-runtime/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tillämpa villkorlig formatering vid körning i Excel

## Introduktion

de är kraftfulla verktyg för dataanalys och visualisering. En av de utmärkande funktionerna i Excel är villkorlig formatering, som tillåter användare att tillämpa specifika formateringsstilar på celler baserat på deras värden. Detta kan göra det lättare att identifiera trender, lyfta fram viktiga datapunkter eller helt enkelt göra data mer läsbara. Om du funderar på att implementera villkorlig formatering i dina Excel-filer programmatiskt, är du på rätt plats! I den här guiden går vi igenom hur man tillämpar villkorlig formatering under körning med Aspose.Cells för .NET.

## Förutsättningar
Innan vi dyker in i koden, låt oss se till att du har allt du behöver för att komma igång:

1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Du kan använda vilken version som helst som stöder .NET-utveckling.
2.  Aspose.Cells för .NET: Du måste ha Aspose.Cells för .NET installerat. Du kan ladda ner den från[Aspose hemsida](https://releases.aspose.com/cells/net/).
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
4. .NET Framework: Se till att ditt projekt är inriktat på en kompatibel version av .NET Framework.

Nu när vi har täckta förutsättningarna, låt oss hoppa in i den roliga delen!

## Importera paket
För att komma igång med Aspose.Cells måste du importera de nödvändiga namnrymden i ditt C#-projekt. Så här kan du göra det:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Dessa namnutrymmen ger dig tillgång till de klasser och metoder som krävs för att manipulera Excel-filer och tillämpa villkorlig formatering.

Låt oss nu dela upp processen med att tillämpa villkorlig formatering i hanterbara steg.

## Steg 1: Konfigurera ditt projekt
Först och främst måste du skapa ett nytt C#-projekt i Visual Studio. Så här gör du:

1. Öppna Visual Studio och välj Arkiv > Nytt > Projekt.
2. Välj Console App (.NET Framework) och ge ditt projekt ett namn.
3. Klicka på Skapa.

## Steg 2: Lägg till Aspose.Cells Reference
När ditt projekt är konfigurerat måste du lägga till en referens till Aspose.Cells-biblioteket:

1. Högerklicka på ditt projekt i Solution Explorer.
2. Välj Hantera NuGet-paket.
3. Sök efter Aspose.Cells och installera det.

Detta gör att du kan använda all funktionalitet som tillhandahålls av Aspose.Cells-biblioteket.

## Steg 3: Skapa ett arbetsboksobjekt
Låt oss sedan skapa en ny arbetsbok och ett kalkylblad. Det är här all magi händer:

```csharp
// Sökvägen till dokumentkatalogen.
string dataDir = "Your Document Directory";
string filePath = dataDir + "Book1.xlsx";

// Instantiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

I det här steget definierar vi katalogen där vår Excel-fil ska sparas, skapar en ny arbetsbok och kommer åt det första kalkylbladet.

## Steg 4: Lägg till villkorlig formatering
Låt oss nu lägga till lite villkorlig formatering. Vi börjar med att skapa ett tomt villkorligt formateringsobjekt:

```csharp
// Lägger till en tom villkorlig formatering
int index = sheet.ConditionalFormattings.Add();
FormatConditionCollection fcs = sheet.ConditionalFormattings[index];
```

Här lägger vi till en ny samling av villkorlig formatering till vårt kalkylblad, som kommer att innehålla våra formateringsregler.

## Steg 5: Definiera formatintervallet
Därefter måste vi specificera cellintervallet som den villkorliga formateringen ska gälla för. Låt oss säga att vi vill formatera den första raden och den andra kolumnen:

```csharp
// Ställer in det villkorliga formatintervallet.
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

I den här koden definierar vi två områden för villkorlig formatering. Det första området är för cellen vid (0,0) och det andra för (1,1). Justera gärna dessa intervall utifrån dina specifika behov!

## Steg 6: Lägg till villkorliga formateringsvillkor
Nu är det dags att definiera villkoren för vår formatering. Låt oss säga att vi vill markera celler baserat på deras värden:

```csharp
// Lägger till skick.
int conditionIndex = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "=A2", "100");

// Lägger till skick.
int conditionIndex2 = fcs.AddCondition(FormatConditionType.CellValue, OperatorType.Between, "50", "100");
```

 I det här steget lägger vi till två villkor: ett för värden mellan`A2` och`100` , och en annan för värden mellan`50` och`100`. Detta gör att du dynamiskt kan markera celler baserat på deras värden.

## Steg 7: Ställ in formateringsstilar
Med våra villkor på plats kan vi nu ställa in formateringsstilarna. Låt oss ändra bakgrundsfärgen för våra förhållanden:

```csharp
// Ställer in bakgrundsfärgen.
FormatCondition fc = fcs[conditionIndex];
fc.Style.BackgroundColor = Color.Red;
```

Här ställer vi in bakgrundsfärgen för det första villkoret till rött. Du kan anpassa detta ytterligare genom att ändra teckensnittsfärg, gränser och andra stilar efter behov!

## Steg 8: Spara Excel-filen
Äntligen är det dags att rädda vårt arbete! Vi sparar arbetsboken i den angivna katalogen:

```csharp
// Sparar Excel-filen
workbook.Save(dataDir + "output.xls");
```

Denna kodrad sparar Excel-filen med den villkorliga formateringen tillämpad. Se till att kontrollera den angivna katalogen för din utdatafil!

## Slutsats
Och där har du det! Du har framgångsrikt tillämpat villkorlig formatering vid körning i Excel med Aspose.Cells för .NET. Detta kraftfulla bibliotek gör det enkelt att manipulera Excel-filer programmatiskt, så att du kan automatisera tråkiga uppgifter och förbättra dina datapresentationer. Oavsett om du arbetar med ett litet projekt eller en storskalig applikation kan Aspose.Cells hjälpa dig att effektivisera ditt arbetsflöde och förbättra din produktivitet.

## FAQ's

### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer programmatiskt.

### Kan jag använda Aspose.Cells med andra programmeringsspråk?
Ja, Aspose.Cells är tillgängligt för flera programmeringsspråk, inklusive Java, Python och mer.

### Finns det en gratis testversion tillgänglig för Aspose.Cells?
 Ja, du kan ladda ner en gratis testversion från[Aspose hemsida](https://releases.aspose.com/).

### Hur kan jag få support för Aspose.Cells?
 Du kan få stöd genom att besöka[Aspose supportforum](https://forum.aspose.com/c/cells/9).

### Behöver jag en licens för att använda Aspose.Cells?
 Ja, en licens krävs för kommersiell användning, men du kan begära en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
