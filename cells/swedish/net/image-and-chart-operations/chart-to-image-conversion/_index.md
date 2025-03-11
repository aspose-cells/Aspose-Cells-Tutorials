---
title: Diagram till bildkonvertering i .NET
linktitle: Diagram till bildkonvertering i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du konverterar diagram till bilder i .NET med Aspose.Cells med denna steg-för-steg-guide. Konvertera enkelt Excel-diagram till bilder av hög kvalitet.
weight: 10
url: /sv/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Diagram till bildkonvertering i .NET

## Introduktion
Att konvertera ett diagram från Excel till en bild kan vara ett avgörande krav när man bygger rapporteringssystem eller delar visuella datarepresentationer. Som tur är, med Aspose.Cells för .NET, är denna process lätt som en plätt! Oavsett om du genererar rapporter eller bara konverterar Excel-diagram till bilder för bättre visning, kommer den här guiden att leda dig genom processen steg för steg.
## Förutsättningar
Innan vi börjar, låt oss se till att du har allt på plats att följa tillsammans med den här handledningen.
### Aspose.Cells för .NET Library
Först måste du ladda ner och referera till Aspose.Cells for .NET-biblioteket i ditt projekt. Du kan hämta den senaste versionen här:
- [Ladda ner Aspose.Cells för .NET](https://releases.aspose.com/cells/net/)
### .NET-miljö
Se till att du har .NET-ramverket installerat på ditt system. Du kan använda Visual Studio eller någon annan .NET-utvecklingsmiljö för att köra det här exemplet.
### Licensinställningar (valfritt)
 Även om du kan använda Aspose.Cells med en gratis provperiod, för fullständig funktionalitet utan begränsningar, överväg att ansöka om en[tillfällig licens](https://purchase.aspose.com/temporary-license/) eller köp en från[här](https://purchase.aspose.com/buy).

## Importera paket
För att sätta igång, låt oss importera de nödvändiga namnrymden för att fungera med Aspose.Cells-biblioteket. Detta gör att vi kan manipulera Excel-filer och generera bilder.
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
Se till att du har dessa paket redo innan du startar kodningsdelen.

Låt oss nu dela upp processen att konvertera ett diagram till en bild i enkla steg.
## Steg 1: Konfigurera din projektkatalog
Du behöver en plats att spara dina genererade bilder, eller hur? Låt oss först skapa en katalog där utdatabilderna kommer att sparas.

Vi börjar med att definiera sökvägen för vår dokumentkatalog och se till att mappen finns. Om det inte gör det skapar vi en.
```csharp
// Definiera katalogen för att spara bilder
string dataDir = "Your Document Directory";
//Kontrollera om katalogen finns
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Med det här steget är du redo att generera och spara dina diagrambilder i den här katalogen.
## Steg 2: Skapa en ny arbetsbok
Här kommer vi att instansiera ett Workbook-objekt. Detta kommer att representera vår Excel-fil där diagrammet kommer att bäddas in.

En arbetsbok är som en Excel-fil som innehåller ark. Genom att skapa en ny arbetsbok börjar vi på nytt med en tom Excel-fil.
```csharp
// Skapa ett nytt arbetsboksobjekt
Workbook workbook = new Workbook();
```
## Steg 3: Lägg till ett nytt arbetsblad
Varje Excel-fil har kalkylblad (eller flikar). Låt oss lägga till en i vår arbetsbok.

Det är viktigt att lägga till ett nytt kalkylblad eftersom vi infogar våra data och diagram i det här bladet. När arket har lagts till hämtar vi dess referens.
```csharp
// Lägg till ett nytt kalkylblad i arbetsboken
int sheetIndex = workbook.Worksheets.Add();
// Hämta det nyligen tillagda kalkylbladet
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## Steg 4: Fyll kalkylbladet med data
För att skapa ett meningsfullt diagram behöver vi lite data, eller hur? Låt oss fylla i några celler med exempelvärden.

Vi kommer att lägga till data till specifika celler på kalkylbladet. Dessa data kommer att användas för att generera vårt diagram senare.
```csharp
// Lägg till exempeldata i celler
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## Steg 5: Lägg till ett diagram i arbetsbladet
Låt oss nu skapa ett kolumndiagram som visualiserar data vi just har lagt till.

Vi anger typen av diagram (kolumndiagram) och definierar dess storlek och position i kalkylbladet.
```csharp
// Lägg till ett kolumndiagram i kalkylbladet
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## Steg 6: Definiera diagramdatakällan
Här är där magin händer: länka diagrammet till data i kalkylbladet!

Vi länkar diagrammet till data i kolumn A1 till B3. Detta talar om för diagrammet varifrån data ska hämtas.
```csharp
// Länka diagrammet till data i intervallet A1 till B3
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## Steg 7: Konvertera diagrammet till en bild
Sanningens ögonblick: vi ska konvertera det här diagrammet till en bildfil!

 Här använder vi`ToImage` metod för att konvertera diagrammet till ett valfritt bildformat. I det här fallet konverterar vi det till ett EMF-format (Enhanced Metafile).
```csharp
// Konvertera diagrammet till en bild och spara det i katalogen
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
Och det är det! Ditt diagram har nu sparats som en bild. Dags att klappa dig själv på axeln.
## Steg 8: Visa framgångsmeddelande
För att avsluta saker och ting, låt oss visa ett meddelande som bekräftar bildgenereringen.
```csharp
// Visa ett meddelande för att indikera framgång
System.Console.WriteLine("Image generated successfully.");
```
## Slutsats
Bom! Så enkelt är det att konvertera ett diagram från Excel till en bild med Aspose.Cells för .NET. Denna process förenklar inte bara presentationen av data utan förbättrar också flexibiliteten i rapporter eller instrumentpaneler där bilder föredras framför inbäddade diagram.
Genom att följa stegen som beskrivs i den här guiden kan du nu konvertera alla Excel-diagram till en bild, så att du kan integrera visuell data i olika applikationer sömlöst.
## FAQ's
### Kan jag konvertera olika typer av diagram med den här metoden?
Ja, du kan konvertera alla diagramtyper som stöds av Aspose.Cells inklusive cirkeldiagram, stapeldiagram, linjediagram och mer!
### Är det möjligt att ändra bildformatet?
 Absolut! Medan vi använde EMF i det här exemplet kan du ändra bildformatet till PNG, JPEG, BMP och andra genom att helt enkelt ändra`ImageFormat` parameter.
### Stöder Aspose.Cells högupplösta bilder?
Ja, Aspose.Cells låter dig kontrollera bildupplösning och kvalitetsinställningar när du exporterar diagram till bilder.
### Kan jag konvertera flera diagram till bilder på en gång?
Ja, du kan gå igenom flera diagram i en arbetsbok och konvertera dem alla till bilder på bara några rader kod.
### Finns det en gräns för antalet diagram jag kan konvertera?
Det finns ingen inneboende begränsning av Aspose.Cells, men bearbetning av stora mängder data kan bero på ditt systems minne och prestanda.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
