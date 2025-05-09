---
"description": "Skapa en PDF med ditt Excel-diagram med Aspose.Cells för .NET. Lär dig hur med den här steg-för-steg-guiden."
"linktitle": "Skapa diagram i PDF-format med önskad sidstorlek"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Skapa diagram i PDF-format med önskad sidstorlek"
"url": "/sv/net/chart-rendering-and-conversion/create-chart-pdf-with-desired-page-size/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa diagram i PDF-format med önskad sidstorlek

## Introduktion

Att skapa visuellt tilltalande och informativa diagram är avgörande för datarepresentation inom olika områden. Oavsett om du arbetar med försäljningsdata, prestationsmått eller någon annan typ av information, ger möjligheten att producera högkvalitativa diagram dina resultat djup och tydlighet. Om du arbetar med .NET-applikationer är Aspose.Cells ett kraftfullt bibliotek som gör det enkelt att hantera Excel-dokument och generera diagram. I den här handledningen guidar vi dig genom processen att skapa en PDF av ett diagram från en Excel-fil med önskad sidstorlek.

## Förkunskapskrav

Innan du går in i koden finns det några förutsättningar du måste uppfylla för att säkerställa en smidig upplevelse:

### Grundläggande kunskaper i C# och .NET

Du behöver grundläggande förståelse för C#-programmering och .NET-ramverket. Detta hjälper dig att förstå strukturen i den kod du kommer att stöta på i den här guiden.

### Aspose.Cells för .NET

Se till att du har Aspose.Cells för .NET installerat. Du hittar all information på [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/). 

### Utvecklingsmiljö

Konfigurera din utvecklingsmiljö. Detta kan vara Visual Studio eller någon annan IDE som stöder C#. Ladda ner och installera Aspose.Cells-biblioteket från [nedladdningssida](https://releases.aspose.com/cells/net/).

### Exempel på Excel-fil

Du behöver en exempelfil i Excel som innehåller minst ett diagram. Du kan skapa en exempelfil eller ladda ner en som du kan använda i den här handledningen.

## Importera paket

För att börja arbeta med Aspose.Cells behöver du importera de nödvändiga namnrymderna i ditt C#-program. Så här gör du det:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using Aspose.Cells.Charts;
```

Dessa namnrymder ger dig åtkomst till de klasser och metoder som behövs för att manipulera Excel-arbetsböcker och deras innehåll.

Nu när vi har alla förutsättningar klara, låt oss dela upp processen i detaljerade steg.

## Steg 1: Konfigurera utdata- och källkataloger

Till att börja med måste du definiera var den utgående PDF-filen ska sparas och var ditt källdokument i Excel finns.

```csharp
//Utdatakatalog
string outputDir = "Your Output Directory";

//Källkatalog
string sourceDir = "Your Document Directory";
```

Se till att ersätta "Your Output Directory" och "Your Document Directory" med de faktiska sökvägarna på ditt system. Detta avgör var Aspose sparar den genererade PDF-filen och var Excel-filen hittar den.

## Steg 2: Ladda exempelfilen i Excel

Nästa steg är att ladda Excel-filen som innehåller diagrammet. Så här gör du:

```csharp
//Ladda exempel-Excel-filen som innehåller diagrammet.
Workbook wb = new Workbook(sourceDir + "sampleCreateChartPDFWithDesiredPageSize.xlsx");
```

De `Workbook` Klassen är central för att interagera med ditt Excel-dokument. Se till att sökvägen pekar korrekt till din Excel-fil – ett fel här förhindrar att resten av koden körs.

## Steg 3: Öppna det första arbetsbladet

När arbetsboken har laddats är nästa steg att komma åt kalkylbladet som innehåller önskat diagram.

```csharp
//Åtkomst till första arbetsbladet.
Worksheet ws = wb.Worksheets[0];
```

I Aspose.Cells indexeras kalkylblad från noll, så `Worksheets[0]` hänvisar till det första arket.

## Steg 4: Få åtkomst till det första diagrammet

Nu ska vi komma åt diagrammet du vill exportera till en PDF. Det här steget förutsätter att ditt kalkylblad innehåller minst ett diagram.

```csharp
//Få åtkomst till det första diagrammet i kalkylbladet.
Chart ch = ws.Charts[0];
```

Återigen, detta öppnar det första diagrammet i kalkylbladet; se till att din kalkylbladsstruktur passar denna metod.

## Steg 5: Skapa PDF med önskad sidstorlek

Slutligen är det dags att skapa PDF-filen från diagrammet med en specificerad sidstorlek. Här är den magiska kodraden som gör allt:

```csharp
//Skapa ett diagram i pdf-format med önskad sidstorlek.
ch.ToPdf(outputDir + "outputCreateChartPDFWithDesiredPageSize.pdf", 7, 7, PageLayoutAlignmentType.Center, PageLayoutAlignmentType.Center);
```

I den här koden:
- PDF-filen sparas i den utdatakatalog du angav tidigare.
- Siffrorna `7, 7` representerar bredden respektive höjden på den önskade sidstorleken.
- PageLayoutAlignmentType.Center säkerställer att diagrammet är centrerat på sidan.

## Steg 6: Bekräftelsemeddelande

För att informera dig själv (och andra) om att allt gick smidigt, inkludera ett bekräftelsemeddelande i slutet av din kod:

```csharp
Console.WriteLine("CreateChartPDFWithDesiredPageSize executed successfully.");
```

Det här meddelandet visas i konsolfönstret när processen är klar, vilket signalerar att din PDF har skapats utan problem.

## Slutsats

Grattis! Du har precis lärt dig hur du använder Aspose.Cells för .NET för att skapa en PDF från ett diagram som finns i en Excel-fil. Detta kraftfulla bibliotek effektiviserar processen att manipulera Excel-dokument och generera visuella representationer av data, vilket sparar dig timmar av manuell formatering. Se till att utforska de många andra funktioner som Aspose.Cells erbjuder utöver bara PDF-generering – du vet aldrig vad som kan förbättra dina projekt ytterligare!

## Vanliga frågor

### Vad används Aspose.Cells för .NET till?  
Aspose.Cells för .NET används för att skapa, redigera och konvertera Excel-dokument programmatiskt i .NET-applikationer.

### Kan jag använda Aspose.Cells gratis?  
Ja, Aspose.Cells erbjuder en [gratis provperiod](https://releases.aspose.com/) för utvärderingsändamål.

### Finns det något sätt att förlänga min provperiod utöver den initiala perioden?  
Du kan ansöka om en [tillfällig licens](https://purchase.aspose.com/temporary-license/) för utökad testning.

### Vad händer om jag stöter på problem eller har frågor?  
Du kan söka hjälp från Aspose-communityn på deras [supportforum](https://forum.aspose.com/c/cells/9).

### Hur kan jag köpa Aspose.Cells?  
Du kan köpa Aspose.Cells från [köpsida](https://purchase.aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}