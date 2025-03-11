---
title: Skapa diagram PDF med önskad sidstorlek
linktitle: Skapa diagram PDF med önskad sidstorlek
second_title: Aspose.Cells .NET Excel Processing API
description: Skapa en PDF med ditt Excel-diagram med Aspose.Cells för .NET. Lär dig hur med denna steg-för-steg-guide.
weight: 12
url: /sv/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa diagram PDF med önskad sidstorlek

## Introduktion

Att skapa visuellt tilltalande och informativa diagram är viktigt för datarepresentation inom olika områden. Oavsett om du har att göra med försäljningsdata, prestationsstatistik eller någon annan typ av information, ger möjligheten att producera diagram av hög kvalitet dina resultat djup och tydlighet. Om du arbetar med .NET-applikationer är Aspose.Cells ett kraftfullt bibliotek som gör det enkelt att hantera Excel-dokument och generera diagram. I den här handledningen guidar vi dig genom processen att skapa en PDF av ett diagram från en Excel-fil med önskad sidstorlek.

## Förutsättningar

Innan du dyker in i koden finns det några förutsättningar du måste uppfylla för att säkerställa en smidig upplevelse:

### Grundläggande kunskaper i C# och .NET

Du behöver en grundläggande förståelse för C#-programmering och .NET-ramverket. Detta hjälper dig att förstå strukturen för koden som du kommer att stöta på i den här guiden.

### Aspose.Cells för .NET

Se till att du har Aspose.Cells för .NET installerat. Du kan hitta alla detaljer på[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/). 

### Utvecklingsmiljö

 Ställ in din utvecklingsmiljö. Detta kan vara Visual Studio eller någon annan IDE som stöder C#. Ladda ner och installera Aspose.Cells-biblioteket från[nedladdningssida](https://releases.aspose.com/cells/net/).

### Exempel på Excel-fil

Du behöver ett exempel på en Excel-fil som innehåller minst ett diagram. Du kan skapa en exempelfil eller ladda ner en för att använda genom hela den här handledningen.

## Importera paket

För att börja arbeta med Aspose.Cells måste du importera de nödvändiga namnrymden i din C#-applikation. Så här gör du det:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Dessa namnrymder ger dig tillgång till de klasser och metoder som behövs för att manipulera Excel-arbetsböcker och deras innehåll.

Nu när vi har alla förutsättningar utredda, låt oss dela upp processen i detaljerade steg.

## Steg 1: Ställ in utdata- och källkataloger

Till att börja med måste du definiera var utdata-PDF-filen ska sparas och var ditt Excel-källdokument finns.

```csharp
//Utdatakatalog
string outputDir = "Your Output Directory";

//Källkatalog
string sourceDir = "Your Document Directory";
```

Se till att ersätta "Din utdatakatalog" och "Din dokumentkatalog" med de faktiska sökvägarna på ditt system. Detta dikterar var Aspose kommer att spara den genererade PDF-filen och var den hittar Excel-filen.

## Steg 2: Ladda Excel-exempelfilen

Därefter måste du ladda Excel-filen som innehåller diagrammet. Så här gör du:

```csharp
//Ladda exempel på Excel-fil som innehåller diagrammet.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

 De`Workbook` klass är central för att interagera med ditt Excel-dokument. Se till att sökvägen pekar korrekt till din Excel-fil – ett fel här kommer att förhindra att resten av koden körs.

## Steg 3: Öppna det första arbetsbladet

När arbetsboken har laddats är nästa steg att komma åt arbetsbladet som innehåller det önskade diagrammet.

```csharp
//Öppna första kalkylbladet.
Worksheet ws = wb.Worksheets[0];
```

 I Aspose.Cells indexeras kalkylblad från noll, alltså`Worksheets[0]` hänvisar till det första bladet.

## Steg 4: Öppna det första diagrammet

Låt oss nu komma åt diagrammet du vill exportera till en PDF. Det här steget förutsätter att ditt kalkylblad innehåller minst ett diagram.

```csharp
//Öppna första diagrammet i kalkylbladet.
Chart ch = ws.Charts[0];
```

Återigen, detta kommer åt det första diagrammet i kalkylbladet; se till att din kalkylbladsstruktur passar detta tillvägagångssätt.

## Steg 5: Skapa PDF med önskad sidstorlek

Slutligen är det dags att skapa PDF-filen från diagrammet med en angiven sidstorlek. Här är den magiska kodraden som gör allt:

```csharp
//Skapa diagram pdf med önskad sidstorlek.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

I denna kod:
- PDF-filen kommer att sparas i den utdatakatalog du angav tidigare.
-  Siffrorna`7, 7` representerar bredden och höjden på den önskade sidstorleken.
- PageLayoutAlignmentType.Center säkerställer att diagrammet är centrerat på sidan.

## Steg 6: Bekräftelsemeddelande

För att låta dig själv (och andra) veta att allt gick smidigt, inkludera ett bekräftelsemeddelande i slutet av koden:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Detta meddelande visas i konsolfönstret när processen är klar, vilket signalerar att din PDF har skapats utan problem.

## Slutsats

Grattis! Du har precis lärt dig hur du använder Aspose.Cells för .NET för att skapa en PDF från ett diagram som finns i en Excel-fil. Detta kraftfulla bibliotek effektiviserar processen med att manipulera Excel-dokument och generera visuella representationer av data, vilket sparar timmar av manuell formatering. Se till att utforska mängden av andra funktioner som Aspose.Cells erbjuder utöver bara PDF-generering – du vet aldrig vad som kan förbättra dina projekt ytterligare!

## FAQ's

### Vad används Aspose.Cells för .NET till?  
Aspose.Cells för .NET används för att skapa, redigera och konvertera Excel-dokument programmatiskt i .NET-applikationer.

### Kan jag använda Aspose.Cells gratis?  
 Ja, Aspose.Cells erbjuder en[gratis provperiod](https://releases.aspose.com/) i utvärderingssyfte.

### Finns det något sätt att förlänga min provperiod utöver den inledande perioden?  
 Du kan ansöka om en[tillfällig licens](https://purchase.aspose.com/temporary-license/) för utökade tester.

### Vad händer om jag stöter på problem eller har frågor?  
 Du kan söka hjälp från Aspose-gemenskapen på deras[supportforum](https://forum.aspose.com/c/cells/9).

### Hur kan jag köpa Aspose.Cells?  
 Du kan köpa Aspose.Cells från[köpsidan](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
