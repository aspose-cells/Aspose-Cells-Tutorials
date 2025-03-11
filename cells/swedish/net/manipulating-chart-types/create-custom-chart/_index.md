---
title: Skapa anpassat diagram
linktitle: Skapa anpassat diagram
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du skapar anpassade diagram i Excel med Aspose.Cells för .NET. Steg-för-steg-guide för att förbättra dina färdigheter i datavisualisering.
weight: 10
url: /sv/net/manipulating-chart-types/create-custom-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa anpassat diagram

## Introduktion

Att skapa anpassade diagram i Excel med Aspose.Cells-biblioteket för .NET är inte bara enkelt, utan det är ett fantastiskt sätt att visualisera dina data effektivt. Diagram kan omvandla alldaglig data till fängslande berättelser, vilket gör det lättare för analytiker och beslutsfattare att skaffa sig insikter. I den här självstudien går vi djupt in i hur du kan skapa anpassade diagram i dina applikationer. Så om du vill lyfta dina rapporter eller helt enkelt lägga till stil till din datapresentation, är du på rätt plats!

## Förutsättningar

Innan vi fördjupar oss i det nättiga med att skapa diagram, låt oss se till att du har allt på plats. Här är vad du behöver:

1. Visual Studio eller någon .NET-kompatibel IDE: Detta kommer att vara din lekplats för att skriva och testa din kod.
2.  Aspose.Cells för .NET Library: Se till att du har det här biblioteket installerat. Du kan ladda ner den[här](https://releases.aspose.com/cells/net/).
3. Grundläggande förståelse för C#: Det skulle vara fördelaktigt för dig att förstå grundläggande C#-koncept, eftersom vi kommer att använda det i våra kodexempel.
4. Ett exempel på datauppsättning: För att skapa diagram är det viktigt att ha vissa data. Vi kommer att använda en enkel datauppsättning i vårt exempel, men du kan anpassa den efter dina behov.

## Importera paket

För att komma igång måste du importera den nödvändiga Aspose.Cells-namnrymden i din C#-applikation. Så här kan du göra detta:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Nu när den grundläggande strukturen är utlagd, låt oss gå in i steg-för-steg-guiden för att skapa ett anpassat diagram.

## Steg 1: Konfigurera din utdatakatalog

Först och främst måste du skapa en katalog där din Excel-fil kommer att sparas. Detta steg är avgörande för att säkerställa att din applikation vet var den ska placera sin slutprodukt.

```csharp
// Utdatakatalog
string outputDir = "Your Output Directory"; // Ändra detta till din önskade väg
```

I stället för "Din utdatakatalog" kan du ange en faktisk sökväg där du vill att Excel-filen ska sparas. Se till att den här katalogen finns på ditt system; annars kommer du att stöta på fel senare.

## Steg 2: Instantiera ett arbetsboksobjekt

 Nu vill du börja med att skapa en ny instans av`Workbook`klass. Detta är den grundläggande byggstenen för alla Excel-operationer som använder Aspose.Cells.

```csharp
// Instantiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
```

Denna kodrad initierar en ny arbetsbok, och du är redo att börja lägga till data och diagram!

## Steg 3: Få åtkomst till arbetsbladet

Därefter måste du skaffa en referens till arbetsbladet där dina data kommer att finnas. I det här fallet kommer vi att arbeta med det första kalkylbladet i arbetsboken.

```csharp
// Få referensen till det nyligen tillagda kalkylbladet
Worksheet worksheet = workbook.Worksheets[0];
```

Den här raden kommer åt det första kalkylbladet (index 0). Aspose.Cells låter dig ha flera kalkylblad, så att du kan välja därefter.

## Steg 4: Lägga till exempeldata till arbetsbladet


Med kalkylbladet klart är det nu dags att lägga till några exempeldata i dina celler. En enkel datauppsättning hjälper oss att visualisera genom diagram mer effektivt.

```csharp
// Lägga till exempelvärden till celler
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["A4"].PutValue(110);
worksheet.Cells["B1"].PutValue(260);
worksheet.Cells["B2"].PutValue(12);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(100);
```

Här sätter vi värden i intervallen A1 till B4. Ändra gärna dessa värden för att testa olika datascenarier.

## Steg 5: Lägga till ett diagram i arbetsbladet

Nu kommer vi till den spännande delen – att lägga till ett diagram som visuellt representerar de data vi just har angett. Du kan välja mellan olika diagramtyper tillgängliga i Aspose.Cells.

```csharp
// Lägga till ett diagram i arbetsbladet
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 25, 10);
```

På den här raden lägger vi till ett kolumndiagram. Du kan också använda andra typer som linje-, cirkel- eller stapeldiagram baserat på dina behov.

## Steg 6: Åtkomst till diagraminstansen

När vi har lagt till diagrammet måste vi referera till det så att vi kan manipulera det ytterligare. Så här gör du:

```csharp
// Åtkomst till instansen av det nyligen tillagda diagrammet
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

 Vid det här laget har du en`chart` objekt som låter dig ändra dess egenskaper efter behov.

## Steg 7: Lägga till dataserier i diagrammet

Nu måste du informera diagrammet var du kan hämta dess data från. Detta görs genom att lägga till en dataserie i Aspose.Cells.

```csharp
// Lägger till NSeries (diagramdatakälla) till diagrammet
chart.NSeries.Add("A1:B4", true);
```

Denna linje kopplar effektivt ditt diagram till datapunkterna du har placerat i cellerna, vilket gör att diagrammet kan visa dessa värden.

## Steg 8: Anpassa serietypen

Du kan anpassa ditt diagram ytterligare genom att ändra typen av en serie. Låt oss till exempel ändra den andra serien till ett linjediagram för bättre visuell klarhet.

```csharp
// Ställa in diagramtypen för 2nd NSeries att visa som linjediagram
chart.NSeries[1].Type = Aspose.Cells.Charts.ChartType.Line;
```

Detta möjliggör diagram av blandad typ, vilket ger unika visualiseringsmöjligheter.

## Steg 9: Spara arbetsboken

Efter alla dessa konfigurationer är det dags att spara din Excel-fil. Så här kan du göra det:

```csharp
// Sparar Excel-filen
workbook.Save(outputDir + "outputHowToCreateCustomChart.xlsx");
```

 Se till att du lägger till filnamnet med`.xlsx` tillägg för att säkerställa att arbetsboken sparas korrekt.

## Slutsats

Och där har du det! Du har precis skapat ett anpassat diagram med Aspose.Cells för .NET. Med bara några rader kod kan du nu visualisera dina data effektivt, vilket gör rapporter och presentationer mycket mer engagerande. 

Kom ihåg att kraften med diagram ligger i deras förmåga att berätta en historia, att göra komplexa data begripliga på ett ögonblick. Så fortsätt, experimentera med olika datauppsättningar och diagramtyper och låt din data tala!

## FAQ's

### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för att arbeta med Excel-filer i .NET-applikationer, vilket möjliggör manipulering, skapande och konvertering av Excel-dokument.

### Hur installerar jag Aspose.Cells för .NET?
 Du kan installera det via NuGet i Visual Studio eller ladda ner biblioteket direkt från[här](https://releases.aspose.com/cells/net/).

### Kan jag skapa olika typer av diagram?
Absolut! Aspose.Cells stöder olika diagramtyper, inklusive kolumn-, linje-, cirkel- och stapeldiagram.

### Finns det något sätt att få en tillfällig licens för Aspose.Cells?
 Ja, du kan få en tillfällig licens från[denna länk](https://purchase.aspose.com/temporary-license/).

### Var kan jag hitta mer dokumentation om Aspose.Cells?
 Du kan utforska hela dokumentationen[här](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
