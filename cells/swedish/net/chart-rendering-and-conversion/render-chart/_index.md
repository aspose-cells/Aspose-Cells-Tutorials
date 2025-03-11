---
title: Gör diagram
linktitle: Gör diagram
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck hur du renderar diagram i .NET med Aspose.Cells. Följ vår steg-för-steg handledning för att skapa fantastiska bilder utan ansträngning.
weight: 10
url: /sv/net/chart-rendering-and-conversion/render-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gör diagram

## Introduktion

Diagram är ett viktigt inslag i datapresentation och analys, vilket gör komplex information lättsmält. Om du arbetar med .NET och behöver generera diagram programmatiskt är Aspose.Cells ett kraftfullt bibliotek som ger intuitiva och avancerade funktioner för att hantera Excel-filer och diagram. I den här guiden går vi igenom processen att rendera ett diagram med Aspose.Cells för .NET. Gör dig redo att dyka in i denna detaljerade handledning, som är designad för att vara engagerande och lätt att följa!

## Förutsättningar

Innan vi hoppar in i koden, låt oss se till att du har allt klart. Här är vad du behöver:

1. .NET-miljö: Se till att du har en .NET-utvecklingsmiljö inställd. Du kan använda Visual Studio eller någon annan IDE som stöder .NET.
2.  Aspose.Cells för .NET: Du måste ha Aspose.Cells-biblioteket installerat. Du kan ladda ner den från[Asposes releasesida](https://releases.aspose.com/cells/net/).
3. Grundläggande C#-kunskaper: Bekantskap med C#-programmering hjälper dig att förstå exemplen bättre, men oroa dig inte om du är ny – den här guiden kommer att förklara allt steg för steg!

## Importera paket

Det första steget i din kodningsresa är att importera de nödvändiga paketen. Öppna ditt projekt i din IDE och lägg till följande namnområde:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
```

Dessa namnrymder ger dig tillgång till funktionaliteten som erbjuds av Aspose.Cells-biblioteket, så att du kan skapa och manipulera dina diagram sömlöst.


Nu när vi har täckt förutsättningarna och importen, låt oss dyka in i det snåriga med att rendera ett diagram! Vi delar upp det i tydliga, hanterbara steg.

## Steg 1: Konfigurera din utdatakatalog

Innan vi skapar vår arbetsbok och diagram måste vi fastställa var våra utdata kommer att sparas. På så sätt, när vårt diagram genereras, vet du exakt var du kan hitta det.

```csharp
string outputDir = "Your Output Directory"; // Ange utdatakatalogen här.
```

Se till att ersätta "Your Output Directory" med sökvägen där du vill spara dina diagrambilder.

## Steg 2: Skapa en arbetsbok

Därefter kommer vi att skapa en ny arbetsbok. Det är här all magi händer!

```csharp
Workbook workbook = new Workbook();
```

 Den här raden skapar en ny instans av`Workbook` klass, vilket gör att vi kan arbeta med ark och diagram.

## Steg 3: Lägg till ett nytt arbetsblad

Nu när vi har vår arbetsbok är det dags att lägga till ett nytt arbetsblad. Se kalkylblad som olika sidor i en anteckningsbok, där du kan hålla din data organiserad.

```csharp
int sheetIndex = workbook.Worksheets.Add();
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```

Här lägger vi till ett nytt arbetsblad och får en referens till det. Du kommer att arbeta med detta kalkylblad för att mata in dina data och diagram.

## Steg 4: Mata in exempelvärden

Med vårt kalkylblad skapat, låt oss lägga till några exempeldata till cellerna. Dessa data är vad ditt diagram kommer att baseras på, så välj värden som passar din diagramtyp!

```csharp
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```

det här utdraget fyller vi cellerna "A1" till "A3" med några numeriska värden och cellerna "B1" till "B3" med en annan uppsättning värden. Känn dig fri att anpassa dessa siffror för att passa dina behov!

## Steg 5: Skapa ett diagram

Nu är det dags att skapa ditt diagram. Vi kommer att lägga till en kolumndiagramtyp, vilket är bra för att jämföra värden.

```csharp
int chartIndex = worksheet.Charts.Add(ChartType.Column, 5, 0, 15, 5);
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
```

Här lägger vi till ett diagram på den angivna platsen genom att definiera dess layout: den första uppsättningen siffror representerar diagrammets position på rutnätet.

## Steg 6: Lägga till dataserier i diagrammet

Med diagrammet skapat måste vi nu binda det till de data vi angav i de föregående stegen.

```csharp
chart.NSeries.Add("A1:B3", true);
```

Denna linje ansluter diagrammets dataserie till värdena i cellerna "A1" till "B3". Detta innebär att ditt diagram visuellt kommer att representera data som avsett.

## Steg 7: Spara diagrammet som en bild

Låt oss nu konvertera vårt diagram till ett bildformat så att det enkelt kan delas och visas.

```csharp
chart.ToImage(outputDir + "outputChartRendering.emf", System.Drawing.Imaging.ImageFormat.Emf);
```

det här steget sparar vi diagrammet som en EMF-bild (Enhanced Metafile) i den angivna utdatakatalogen. Du kan också spara den i olika format som BMP eller PNG.

## Steg 8: Konvertera diagram till bitmapp

Om du föredrar att arbeta med bitmappar, så här konverterar du ditt diagram till ett bitmappsformat.

```csharp
System.Drawing.Bitmap bitmap = chart.ToImage();
bitmap.Save(outputDir + "outputChartRendering.bmp", System.Drawing.Imaging.ImageFormat.Bmp);
```

Detta kommer att spara ditt diagram som en BMP-bild. Kom ihåg att BMP-filer tenderar att vara större men är otroligt hög kvalitet!

## Steg 9: Rendering med avancerade alternativ

Vi kan också återge diagrammet med några avancerade bildalternativ för bättre kvalitet och upplösning. Låt oss ställa in några alternativ:

```csharp
ImageOrPrintOptions options = new ImageOrPrintOptions()
{
    VerticalResolution = 300,
    HorizontalResolution = 300,
    SmoothingMode = System.Drawing.Drawing2D.SmoothingMode.AntiAlias
};
```

Dessa alternativ hjälper till att förbättra den visuella kvaliteten på bilden du genererar, särskilt användbara för presentationer eller publikationer.

## Steg 10: Konvertera diagram till bild med avancerade alternativ

Låt oss nu faktiskt konvertera diagrammet med de avancerade alternativen vi just ställt in.

```csharp
chart.ToImage(outputDir + "outputChartRendering.png", options);
```

Detta sparar ditt diagram som en PNG-fil med förbättrade kvalitetsinställningar.

## Steg 11: Exportera diagrammet till PDF

Slutligen, om du vill ha ett polerat, lätt delbart dokument, kan du exportera ditt diagram direkt till ett PDF-format.

```csharp
chart.ToPdf(outputDir + "outputChartRendering.pdf");
```

Detta steg kommer att skapa en PDF som innehåller ditt diagram, vilket gör det perfekt för digitala rapporter eller delning med kollegor.

## Slutsats 

Grattis! Du har framgångsrikt renderat ett diagram med Aspose.Cells för .NET. Detta kraftfulla bibliotek förenklar skapandet och manipuleringen av Excel-filer och diagram, vilket gör dina data mycket mer tillgängliga och visuellt tilltalande. Oavsett om du förbereder rapporter, analyser eller presentationer, har diagram en betydande inverkan, och med Aspose kan du enkelt skapa dem programmatiskt.

## FAQ's

### Vilka typer av diagram kan jag skapa med Aspose.Cells för .NET?
Du kan skapa en mängd olika diagram, inklusive kolumn-, linje-, cirkel- och stapeldiagram, bland annat.

### Kan jag anpassa diagrammets utseende?
Ja, Aspose.Cells möjliggör omfattande anpassning, inklusive färger, stilar och diagramelement.

### Finns det en gratis provperiod?
Absolut! Du kan ladda ner en gratis testversion från[här](https://releases.aspose.com/).

### Var kan jag få support för Aspose.Cells?
 Du kan hitta gemenskapsstöd och resurser på[Aspose Support Forum](https://forum.aspose.com/c/cells/9).

### Behöver jag en licens för att använda Aspose.Cells?
 Ja, en licens krävs för fortsatt användning efter provperioden, men du kan ansöka om en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
