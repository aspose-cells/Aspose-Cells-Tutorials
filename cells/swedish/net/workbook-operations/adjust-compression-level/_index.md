---
title: Justera komprimeringsnivån i arbetsboken
linktitle: Justera komprimeringsnivån i arbetsboken
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du justerar komprimeringsnivån för Excel-arbetsböcker med Aspose.Cells för .NET med denna steg-för-steg-guide. Optimera din filhantering.
weight: 14
url: /sv/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Justera komprimeringsnivån i arbetsboken

## Introduktion
När det gäller att hantera stora Excel-filer är komprimering en spelförändring. Det sparar inte bara lagringsutrymme, det gör också filöverföringar snabbare och effektivare. Om du arbetar med Aspose.Cells för .NET kan du enkelt justera komprimeringsnivån för dina arbetsböcker. I den här guiden går vi igenom processen steg-för-steg, och säkerställer att du förstår varje del av koden och hur den fungerar.
## Förutsättningar
Innan du dyker in i koden finns det några förutsättningar du måste ha på plats:
1. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
2.  Aspose.Cells Library: Du måste ha Aspose.Cells-biblioteket installerat. Du kan ladda ner den från[här](https://releases.aspose.com/cells/net/).
3. Visual Studio: En utvecklingsmiljö som Visual Studio kommer att vara nödvändig för att köra koden.
4. .NET Framework: Se till att ditt projekt är konfigurerat med en kompatibel version av .NET Framework.
## Importera paket
För att komma igång måste du importera nödvändiga paket i ditt C#-projekt. Så här kan du göra det:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
 Dessa paket är viktiga för att arbeta med Excel-filer med Aspose.Cells-biblioteket. De`Aspose.Cells` namnområdet innehåller alla klasser du behöver för att manipulera Excel-filer, medan`Aspose.Cells.Xlsb` ger alternativen för att spara filer i XLSB-formatet.
Låt oss nu dela upp processen att justera komprimeringsnivån i en arbetsbok i hanterbara steg.
## Steg 1: Definiera käll- och utdatakataloger
Först måste du ange var dina källfiler finns och var du vill spara utdatafilerna. Detta är avgörande för att säkerställa att ditt program vet var det ska hitta filerna som det behöver arbeta med.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen till dina kataloger. Detta hjälper programmet att hitta de filer du vill komprimera.
## Steg 2: Ladda arbetsboken
Därefter ska du ladda arbetsboken som du vill komprimera. Det är här magin börjar!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
På den här raden skapar vi en ny instans av`Workbook` klass och ladda en befintlig Excel-fil. Se till att filnamnet matchar det du har i din källkatalog.
## Steg 3: Ställ in sparalternativ
Nu är det dags att konfigurera sparalternativen. Vi kommer att ställa in komprimeringstypen för utdatafilen. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
 De`XlsbSaveOptions` class låter dig ange olika alternativ när du sparar din arbetsbok i XLSB-formatet, inklusive komprimeringsnivåer.
## Steg 4: Mät kompressionstid för nivå 1
Låt oss börja med den första kompressionsnivån. Vi kommer att mäta hur lång tid det tar att spara arbetsboken med denna komprimeringsnivå.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Här ställer vi in komprimeringstypen till nivå 1, sparar arbetsboken och mäter sedan den förflutna tiden. Detta ger oss en uppfattning om hur lång tid processen tar.
## Steg 5: Mät kompressionstid för nivå 6
Låt oss sedan se hur nivå 6-komprimering fungerar.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
Det här steget liknar det föregående, men vi ändrar komprimeringsnivån till nivå 6. Du kommer att märka att tiden det tar kan variera beroende på hur komplex arbetsboken är.
## Steg 6: Mät kompressionstid för nivå 9
Slutligen, låt oss kolla in prestandan med den högsta komprimeringsnivån.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
I det här steget ställer vi in komprimeringsnivån till nivå 9. Det är här du vanligtvis ser den mest betydande minskningen av filstorleken, men det kan ta längre tid att bearbeta.
## Steg 7: Slutlig utdata
Efter att ha kört alla komprimeringsnivåer kan du mata ut ett meddelande som indikerar att processen har slutförts framgångsrikt.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
Denna enkla kodrad bekräftar att ditt program har avslutats utan några problem.
## Slutsats
Att justera komprimeringsnivån för dina arbetsböcker med Aspose.Cells för .NET är en enkel process som kan leda till betydande fördelar när det gäller filstorlek och prestanda. Genom att följa stegen som beskrivs i den här guiden kan du enkelt implementera komprimering i dina applikationer och förbättra effektiviteten i din Excel-filhantering.
## FAQ's
### Vad är Aspose.Cells?  
Aspose.Cells är ett kraftfullt bibliotek för .NET som låter utvecklare skapa, manipulera och konvertera Excel-filer utan att behöva Microsoft Excel.
### Hur installerar jag Aspose.Cells?  
 Du kan ladda ner och installera Aspose.Cells från[Aspose hemsida](https://releases.aspose.com/cells/net/).
### Vilka kompressionsnivåer finns tillgängliga?  
Aspose.Cells stöder flera komprimeringsnivåer från nivå 1 (lägsta komprimering) till nivå 9 (högsta komprimering).
### Kan jag testa Aspose.Cells gratis?  
 Ja! Du kan få en gratis provversion av Aspose.Cells[här](https://releases.aspose.com/).
### Var kan jag hitta support för Aspose.Cells?  
 För frågor eller support kan du besöka Asposes supportforum[här](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
