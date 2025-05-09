---
"description": "Lär dig hur du skapar anpassade diagram i Excel med Aspose.Cells för .NET. Steg-för-steg-guide för att förbättra dina datavisualiseringsfärdigheter."
"linktitle": "Skapa anpassat diagram"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Skapa anpassat diagram"
"url": "/sv/net/manipulating-chart-types/create-custom-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa anpassat diagram

## Introduktion

Att skapa anpassade diagram i Excel med hjälp av Aspose.Cells-biblioteket för .NET är inte bara enkelt, utan det är också ett fantastiskt sätt att visualisera dina data effektivt. Diagram kan omvandla vardaglig data till fängslande berättelser, vilket gör det enklare för analytiker och beslutsfattare att få insikter. I den här handledningen går vi djupare in på hur du kan skapa anpassade diagram i dina applikationer. Så om du vill förbättra dina rapporter eller helt enkelt ge din datapresentation en touch av stil, har du kommit rätt!

## Förkunskapskrav

Innan vi går in på detaljerna kring att skapa diagram, låt oss se till att du har allt på plats. Här är vad du behöver:

1. Visual Studio eller någon .NET-kompatibel IDE: Detta blir din lekplats för att skriva och testa din kod.
2. Aspose.Cells för .NET-biblioteket: Se till att du har det här biblioteket installerat. Du kan ladda ner det. [här](https://releases.aspose.com/cells/net/).
3. Grundläggande förståelse för C#: Det vore fördelaktigt om du behärskade grundläggande C#-koncept, eftersom vi kommer att använda dem i våra kodexempel.
4. Ett exempel på en datauppsättning: För att skapa diagram är det viktigt att ha lite data. Vi använder en enkel datauppsättning i vårt exempel, men du kan anpassa den efter dina behov.

## Importera paket

För att komma igång måste du importera det nödvändiga Aspose.Cells-namnutrymmet i ditt C#-program. Så här gör du:

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Nu när grundstrukturen är klar, låt oss gå vidare till steg-för-steg-guiden för att skapa ett anpassat diagram.

## Steg 1: Konfigurera din utdatakatalog

Först och främst måste du skapa en katalog där din Excel-fil ska sparas. Detta steg är avgörande för att säkerställa att din applikation vet var den ska placera sin slutprodukt.

```csharp
// Utdatakatalog
string outputDir = "Your Output Directory"; // Ändra detta till önskad sökväg
```

Istället för "Din utdatakatalog" kan du ange en faktisk sökväg där du vill att Excel-filen ska sparas. Se till att den här katalogen finns på ditt system, annars kommer du att stöta på fel senare.

## Steg 2: Instansiera ett arbetsboksobjekt

Nu vill du sätta igång genom att skapa en ny instans av `Workbook` klass. Detta är den grundläggande byggstenen för alla Excel-operationer som använder Aspose.Cells.

```csharp
// Instansiera ett arbetsboksobjekt
Workbook workbook = new Workbook();
```

Den här kodraden initierar en ny arbetsbok, och du är redo att börja lägga till data och diagram!

## Steg 3: Åtkomst till arbetsbladet

Nästa steg är att hämta en referens till kalkylbladet där dina data kommer att finnas. I det här fallet arbetar vi med det första kalkylbladet i arbetsboken.

```csharp
// Hämta referensen till det nyligen tillagda kalkylbladet
Worksheet worksheet = workbook.Worksheets[0];
```

Den här raden öppnar det första kalkylbladet (index 0). Aspose.Cells låter dig ha flera kalkylblad, så du kan välja därefter.

## Steg 4: Lägga till exempeldata i arbetsbladet


När kalkylbladet är klart är det dags att lägga till exempeldata i dina celler. En enkel datauppsättning hjälper oss att visualisera diagram mer effektivt.

```csharp
// Lägga till exempelvärden i celler
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["A4"].PutValue(110);
worksheet.Cells["B1"].PutValue(260);
worksheet.Cells["B2"].PutValue(12);
worksheet.Cells["B3"].PutValue(50);
worksheet.Cells["B4"].PutValue(100);
```

Här anger vi värden i intervallet A1 till B4. Du kan gärna ändra dessa värden för att testa olika datascenarier.

## Steg 5: Lägga till ett diagram i arbetsbladet

Nu kommer vi till den spännande delen – att lägga till ett diagram som visuellt representerar de data vi just har angett. Du kan välja mellan olika diagramtyper som finns tillgängliga i Aspose.Cells.

```csharp
// Lägga till ett diagram i kalkylbladet
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 25, 10);
```

På den här raden lägger vi till ett stapeldiagram. Du kan också använda andra typer som linje-, cirkel- eller stapeldiagram beroende på dina behov.

## Steg 6: Åtkomst till diagraminstansen

När vi har lagt till diagrammet behöver vi referera till det så att vi kan manipulera det ytterligare. Så här gör du:

```csharp
// Åtkomst till instansen av det nyligen tillagda diagrammet
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Vid det här laget har du en `chart` objekt som låter dig ändra dess egenskaper efter behov.

## Steg 7: Lägga till dataserier i diagrammet

Nu behöver du ange varifrån diagrammet ska hämta sina data. Detta görs genom att lägga till en dataserie i Aspose.Cells.

```csharp
// Lägga till NSeries (diagramdatakälla) i diagrammet
chart.NSeries.Add("A1:B4", true);
```

Den här linjen kopplar effektivt ditt diagram till de datapunkter du har placerat i cellerna, vilket gör att diagrammet kan visa dessa värden.

## Steg 8: Anpassa serietypen

Du kan ytterligare anpassa ditt diagram genom att ändra typen av valfri serie. Låt oss till exempel ändra den andra serien till ett linjediagram för bättre visuell tydlighet.

```csharp
// Ställa in diagramtypen för den andra N-serien att visas som linjediagram
chart.NSeries[1].Type = Aspose.Cells.Charts.ChartType.Line;
```

Detta möjliggör diagram av blandade typer, vilket erbjuder unika visualiseringsmöjligheter.

## Steg 9: Spara arbetsboken

Efter alla dessa konfigurationer är det dags att spara din Excel-fil. Så här gör du:

```csharp
// Spara Excel-filen
workbook.Save(outputDir + "outputHowToCreateCustomChart.xlsx");
```

Se till att du lägger till filnamnet med `.xlsx` tillägget för att säkerställa att arbetsboken sparas korrekt.

## Slutsats

Och där har du det! Du har precis skapat ett anpassat diagram med Aspose.Cells för .NET. Med bara några få rader kod kan du nu visualisera dina data effektivt, vilket gör rapporter och presentationer mycket mer engagerande. 

Kom ihåg att diagrammens kraft ligger i deras förmåga att berätta en historia, att göra komplex data begriplig med en snabb blick. Så experimentera med olika datamängder och diagramtyper och låt dina data tala!

## Vanliga frågor

### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för att arbeta med Excel-filer i .NET-applikationer, vilket möjliggör manipulation, skapande och konvertering av Excel-dokument.

### Hur installerar jag Aspose.Cells för .NET?
Du kan installera det via NuGet i Visual Studio eller ladda ner biblioteket direkt från [här](https://releases.aspose.com/cells/net/).

### Kan jag skapa olika typer av diagram?
Absolut! Aspose.Cells stöder olika diagramtyper, inklusive kolumn-, linje-, cirkel- och stapeldiagram.

### Finns det något sätt att få en tillfällig licens för Aspose.Cells?
Ja, du kan få ett tillfälligt körkort från [den här länken](https://purchase.aspose.com/temporary-license/).

### Var kan jag hitta mer dokumentation om Aspose.Cells?
Du kan utforska hela dokumentationen [här](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}