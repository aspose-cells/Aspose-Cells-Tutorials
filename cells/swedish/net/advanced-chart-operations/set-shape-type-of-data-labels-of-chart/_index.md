---
title: Ställ in formtyp för dataetiketter för diagram
linktitle: Ställ in formtyp för dataetiketter för diagram
second_title: Aspose.Cells .NET Excel Processing API
description: Förbättra dina Excel-diagram med anpassade dataetikettformer med Aspose.Cells för .NET. Följ den här steg-för-steg-guiden för att lyfta din datapresentation.
weight: 14
url: /sv/net/advanced-chart-operations/set-shape-type-of-data-labels-of-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in formtyp för dataetiketter för diagram

## Introduktion

en värld av datavisualisering är diagram en god metod för att presentera komplex information på ett tillgängligt sätt. Men alla dataetiketter är inte skapade lika! Ibland måste du få dessa etiketter att poppa, och att använda olika former kan göra en betydande skillnad. Om du vill förbättra dataetiketterna i dina Excel-diagram med anpassade former, har du hamnat på rätt plats. Den här guiden går igenom hur du ställer in formtypen för dataetiketter i ett diagram med Aspose.Cells för .NET. Låt oss dyka in i det!

## Förutsättningar

Innan vi går in i kodning, låt oss se till att du har allt korrekt inställt. Här är vad du behöver:

1.  Aspose.Cells för .NET: Om du inte redan har gjort det, ladda ner det från[Aspose hemsida](https://releases.aspose.com/cells/net/). Detta bibliotek tillåter alla typer av manipulationer med Excel-dokument.
2. Visual Studio: Du bör ha detta installerat på ditt system för att skriva och köra .NET-applikationer. Se till att det är versionen som stöder .NET Framework eller .NET Core enligt dina projektbehov.
3. En grundläggande förståelse för C#: Bekantskap med grundläggande programmeringskoncept och C#-syntax kommer definitivt att hjälpa dig att förstå kodavsnitten bättre.
4. En Excel-fil: Du behöver också ett exempel på en Excel-arbetsbok att arbeta med. Du kan skapa din egen eller använda någon befintlig.

Nu när vi har förutsättningarna, låt oss hoppa direkt in i det!

## Importera paket

Innan du kan börja koda måste du importera relevanta Aspose.Cells-namnområden. Detta ger dig tillgång till den rika funktionalitet som biblioteket erbjuder. Så här gör du:

### Importera Aspose.Cells

Öppna ditt Visual Studio-projekt och lägg till följande med hjälp av direktivet överst i din C#-fil:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
```

Dessa namnutrymmen låter dig skapa och manipulera arbetsböcker, kalkylblad och diagram enkelt.

Nu när vi alla är klara, låt oss dyka in i kodningsdelen! Vi kommer att dela upp det steg för steg för tydlighetens skull.

## Steg 1: Definiera dina kataloger

Först och främst, låt oss definiera var dina filer finns – både källfilen och målmappen där du vill spara den ändrade filen.

```csharp
// Källkatalog
string sourceDir = "Your Document Directory";

// Utdatakatalog
string outputDir = "Your Output Directory";
```

 Ersätta`"Your Document Directory"` och`"Your Output Directory"` med de faktiska sökvägarna på din maskin.

## Steg 2: Ladda källfilen för Excel

Därefter måste du ladda Excel-filen du vill arbeta med. Det är här magin börjar!

```csharp
// Ladda källfilen i Excel
Workbook wb = new Workbook(sourceDir + "sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```

 Denna rad skapar en ny`Workbook` objekt och pekar det till din befintliga fil. Se till att filsökvägen är korrekt!

## Steg 3: Öppna det första arbetsbladet

Nu när vi har vår arbetsbok behöver vi få tillgång till kalkylbladet som innehåller diagrammet du vill anpassa.

```csharp
// Öppna första kalkylbladet
Worksheet ws = wb.Worksheets[0];
```

 Här kommer vi åt det första kalkylbladet (index`0`). Justera indexet om ditt diagram finns på ett annat ark.

## Steg 4: Öppna det första diagrammet

När du har fått ditt kalkylblad är det dags att komma åt diagrammet. Varje kalkylblad kan innehålla flera diagram, men för enkelhetens skull håller vi oss till det första här.

```csharp
// Få tillgång till första diagrammet
Chart ch = ws.Charts[0];
```

Återigen, om ditt önskade diagram inte är det första, ändra bara indexet därefter.

## Steg 5: Öppna sjökortsserien

Med diagrammet nu tillgängligt måste du dyka djupare för att ändra dataetiketterna. Serien representerar datapunkterna i ditt diagram.

```csharp
// Få tillgång till första serien
Series srs = ch.NSeries[0];
```

Vi riktar in oss på den första serien här, som vanligtvis innehåller de etiketter du kanske vill ändra.

## Steg 6: Ställ in formtypen för dataetiketter

Nu till den avgörande delen! Låt oss ställa in formtypen för dataetiketterna. Aspose.Cells stöder olika former, och för det här exemplet väljer vi en pratbubbla oval för en rolig touch.

```csharp
// Ställ in formtypen för dataetiketter, dvs Speech Bubble Oval
srs.DataLabels.ShapeType = DataLabelShapeType.WedgeEllipseCallout;
```

 Experimentera gärna med olika formtyper genom att byta`DataLabelShapeType.WedgeEllipseCallout` till andra tillgängliga alternativ!

## Steg 7: Spara Excel-filen

Du har gjort det tunga arbetet, och nu är det dags att spara ditt arbete. Låt oss sätta tillbaka den modifierade dataetikettformen till en Excel-fil.

```csharp
// Spara den utgående Excel-filen
wb.Save(outputDir + "outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

Detta kommer att spara den ändrade arbetsboken i din angivna utdatakatalog.

## Steg 8: Kör och bekräfta

Äntligen är det dags att köra ditt program. Efter exekvering bör du se meddelandet som bekräftar att allt gick smidigt!

```csharp
Console.WriteLine("SetShapeTypeOfDataLabelsOfChart executed successfully.");
```

När du ser det meddelandet, gå till din utdatakatalog för att kontrollera den nya Excel-filen. Öppna den och släpp lös din kreativitet med de nyformade dataetiketterna!

## Slutsats

Och där har du det - en enkel guide för att förbättra dataetiketter i Excel-diagram med Aspose.Cells för .NET! Att anpassa formtyperna gör inte bara dina diagram mer visuellt tilltalande utan hjälper också till att förmedla din databerättelse mer effektivt. Kom ihåg att datavisualisering handlar om tydlighet och engagemang. Så tveka inte att leka med olika former och stilar – trots allt förtjänar din data den bästa presentationen.

## FAQ's

### Vad är Aspose.Cells?  
Aspose.Cells är ett kraftfullt .NET-bibliotek som tillåter utvecklare att manipulera Excel-filer programmatiskt.

### Kan jag ändra olika aspekter av ett Excel-diagram med Aspose?  
Absolut! Aspose.Cells erbjuder omfattande funktioner för att ändra diagram, inklusive dataserier, etiketter, stilar och mer.

### Vilka programmeringsspråk kan jag använda med Aspose.Cells?  
Även om den här artikeln fokuserar på .NET, stöder Aspose.Cells även Java, PHP, Python och mer via REST API:er.

### Behöver jag betala för Aspose.Cells?  
Aspose.Cells är en kommersiell produkt, men de erbjuder en gratis provperiod, som du kan hitta[här](https://releases.aspose.com/).

### Var kan jag få hjälp om jag får problem med Aspose.Cells?  
 Om du stöter på några problem, deras[supportforum](https://forum.aspose.com/c/cells/9) är en stor resurs för att få hjälp av experter.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
