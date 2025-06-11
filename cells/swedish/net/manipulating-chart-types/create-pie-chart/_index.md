---
"description": "Lär dig hur du skapar ett cirkeldiagram i Excel med Aspose.Cells för .NET med den här steg-för-steg-guiden. Visualisera dina data enkelt."
"linktitle": "Skapa cirkeldiagram"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Skapa cirkeldiagram"
"url": "/sv/net/manipulating-chart-types/create-pie-chart/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa cirkeldiagram

## Introduktion

Att skapa diagram är viktigt för att visuellt representera data, och cirkeldiagram är ett av de mest populära sätten att illustrera hur delar utgör en helhet. Med Aspose.Cells för .NET kan du enkelt automatisera genereringen av cirkeldiagram i Excel-filer. I den här handledningen går vi in på hur man skapar ett cirkeldiagram från grunden med Aspose.Cells för .NET, med en steg-för-steg-guide för att göra processen smidig och okomplicerad. Oavsett om du är nybörjare på verktyget eller vill förbättra dina Excel-automatiseringsfärdigheter, har den här guiden det du behöver!

## Förkunskapskrav

Innan du går in i koden, se till att du har följande inställningar:

1. Aspose.Cells för .NET-biblioteket: Se till att du har Aspose.Cells installerat i ditt projekt. Om du inte har installerat det än kan du ladda ner det från [här](https://releases.aspose.com/cells/net/).
2. .NET-utvecklingsmiljö: Se till att ditt projekt är konfigurerat för att använda .NET Framework eller .NET Core.
3. Grundläggande kunskaper i C#: Du bör vara bekväm med C#-programmering, särskilt objektorienterad programmering (OOP).

För avancerade användare kan en tillfällig licens ansökas för att låsa upp alla funktioner i Aspose.Cells. Du kan begära en från [här](https://purchase.aspose.com/temporary-license/).

## Importera paket

För att börja, importera de namnrymder och paket som krävs för den här handledningen. Dessa inkluderar grundläggande I/O-operationer och Aspose.Cells-paketet.

```csharp
using System;
using System.IO;

using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

## Steg 1: Skapa en ny arbetsbok

Först måste vi skapa en instans av `Workbook` klass, som representerar Excel-filen. En arbetsbok innehåller flera ark, och i vårt exempel kommer vi att arbeta med två ark – ett för data och ett för cirkeldiagrammet.

```csharp
Workbook workbook = new Workbook();
```

Detta initierar en ny Excel-arbetsbok. Men vart tar informationen vägen? Låt oss ta hand om det i nästa steg.

## Steg 2: Lägg till data i kalkylbladet

När arbetsboken är skapad behöver vi komma åt det första arbetsbladet och ge det ett namn. Det är här vi matar in de data som krävs för cirkeldiagrammet.

```csharp
Worksheet sheet = workbook.Worksheets[0];
sheet.Name = "Data";
Cells cells = sheet.Cells;
```

Nu kan vi mata in lite dummyförsäljningsdata som representerar olika regioner:

```csharp
cells["A1"].PutValue("Region");
cells["A2"].PutValue("France");
cells["A3"].PutValue("Germany");
cells["A4"].PutValue("England");
cells["A5"].PutValue("Sweden");
cells["A6"].PutValue("Italy");
cells["A7"].PutValue("Spain");
cells["A8"].PutValue("Portugal");

cells["B1"].PutValue("Sales");
cells["B2"].PutValue(70000);
cells["B3"].PutValue(55000);
cells["B4"].PutValue(30000);
cells["B5"].PutValue(40000);
cells["B6"].PutValue(35000);
cells["B7"].PutValue(32000);
cells["B8"].PutValue(10000);
```

Här lägger vi till två kolumner: en för regioner och en annan för försäljningssiffror. Denna information kommer att representeras i cirkeldiagrammet.

## Steg 3: Lägg till ett diagramblad

Nästa steg är att lägga till ett separat arbetsblad för att innehålla cirkeldiagrammet.

```csharp
int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
Worksheet chartSheet = workbook.Worksheets[sheetIndex];
chartSheet.Name = "Chart";
```

Det här nya arket kommer att vara värd för cirkeldiagrammet. Genom att ge det ett namn som "Diagram" säkerställer du att användarna vet vad de kan förvänta sig när de öppnar filen.

## Steg 4: Skapa cirkeldiagrammet

Nu är det dags att skapa själva diagrammet. Vi anger att vi vill ha ett cirkeldiagram och definierar dess position på arket.

```csharp
int chartIndex = chartSheet.Charts.Add(Aspose.Cells.Charts.ChartType.Pie, 5, 0, 25, 10);
Aspose.Cells.Charts.Chart chart = chartSheet.Charts[chartIndex];
```

Metoden `Add()` accepterar parametrar för diagramtypen (i det här fallet, `ChartType.Pie`), och dess plats på kalkylbladet. Siffrorna representerar rad- och kolumnpositioner.

## Steg 5: Anpassa diagrammets utseende

Ett cirkeldiagram skulle inte vara komplett utan lite anpassning! Låt oss göra vårt diagram visuellt tilltalande genom att justera färgerna, etiketterna och titeln.

### Ange diagramtitel
```csharp
chart.Title.Text = "Sales By Region";
chart.Title.Font.Color = Color.Blue;
chart.Title.Font.IsBold = true;
chart.Title.Font.Size = 12;
```

### Anpassa ritningsområdet
```csharp
chart.PlotArea.Area.ForegroundColor = Color.Coral;
chart.PlotArea.Area.FillFormat.SetTwoColorGradient(Color.Yellow, Color.White, GradientStyleType.Vertical, 2);
chart.PlotArea.Border.IsVisible = false;
```

Vi ställer in gradientfyllningen för plottområdet och döljer kantlinjen för ett renare utseende.

## Steg 6: Definiera diagramdata

Det är dags att länka diagrammet till våra data. `NSeries` Egenskapen för diagrammet binder försäljningssiffrorna och regionerna till cirkeldiagrammet.

```csharp
chart.NSeries.Add("Data!B2:B8", true);
chart.NSeries.CategoryData = "Data!A2:A8";
chart.NSeries.IsColorVaried = true;
```

Den första raden anger att vi använder försäljningsdata från celler `B2:B8`Vi anger också att diagrammet ska använda regionnamnen från `A2:A8` som kategorietiketter.

## Steg 7: Lägg till dataetiketter

Att lägga till etiketter direkt i diagramsegmenten kan göra det lättare att förstå. Låt oss inkludera regionnamnen och försäljningsvärdena i cirkeldiagrammets utsnitt.

```csharp
for (int i = 0; i < chart.NSeries.Count; i++)
{
    DataLabels labels = chart.NSeries[i].DataLabels;
    labels.ShowCategoryName = true;
    labels.ShowValue = true;
    labels.Position = LabelPositionType.InsideBase;
}
```

## Steg 8: Anpassa diagramområde och förklaring

Slutligen, låt oss ge diagramområdet och förklaringen några sista finjusteringar. Detta förbättrar diagrammets övergripande presentation.

### Diagramområde
```csharp
ChartArea chartArea = chart.ChartArea;
chartArea.Area.Formatting = FormattingType.Custom;
chartArea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
```

### Legend
```csharp
Legend legend = chart.Legend;
legend.Position = LegendPositionType.Left;
legend.Font.IsBold = true;
legend.Border.Color = Color.Blue;
legend.Area.FillFormat.Texture = TextureType.Bouquet;
```

## Steg 9: Spara arbetsboken

Slutligen sparar vi arbetsboken till en Excel-fil. Du kan ange utdatakatalog och filnamn efter behov.

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## Slutsats

Att skapa ett cirkeldiagram med Aspose.Cells för .NET är en enkel och anpassningsbar process. Genom att följa den här guiden kan du generera ett professionellt diagram som förmedlar värdefulla insikter i bara några få steg. Oavsett om det är för affärsrapportering eller utbildningsändamål, kommer att bemästra diagramskapandet att höja dina kunskaper inom Excel-automation. Kom ihåg att Aspose.Cells ger den flexibilitet du behöver för att enkelt skapa fantastiska, datadrivna Excel-filer.

## Vanliga frågor

### Kan jag skapa andra typer av diagram med Aspose.Cells för .NET?
Ja! Aspose.Cells stöder olika diagramtyper, inklusive stapeldiagram, linjediagram och spridningsdiagram.

### Behöver jag en betald licens för att använda Aspose.Cells för .NET?
Du kan använda gratisversionen med vissa begränsningar. För att få tillgång till alla funktioner behöver du en licens som du kan köpa. [här](https://purchase.aspose.com/buy).

### Kan jag exportera diagrammet till format som PDF eller bilder?
Absolut! Aspose.Cells låter dig exportera diagram till olika format, inklusive PDF och PNG.

### Är det möjligt att utforma varje pajskiva med olika färger?
Ja, du kan använda olika färger på varje skiva genom att ställa in `IsColorVaried` egendom till `true`, som visas i handledningen.

### Kan jag automatisera genereringen av flera diagram i en enda arbetsbok?
Ja, du kan skapa och anpassa så många diagram som behövs i en enda Excel-fil.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}