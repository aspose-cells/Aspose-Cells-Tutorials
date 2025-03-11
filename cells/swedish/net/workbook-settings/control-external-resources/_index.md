---
title: Styr externa resurser med arbetsboksinställning
linktitle: Styr externa resurser med arbetsboksinställning
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du kontrollerar externa resurser i Excel med Aspose.Cells för .NET med vår omfattande steg-för-steg-handledning.
weight: 10
url: /sv/net/workbook-settings/control-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Styr externa resurser med arbetsboksinställning

## Introduktion
När det gäller datamanipulation och presentation kan hantering av externa resurser effektivt vara en spelomvandlare. Om du arbetar med Excel-filer och vill hantera externa resurser sömlöst med Aspose.Cells för .NET, har du hamnat på rätt plats! I den här artikeln kommer vi att dyka djupt in i att kontrollera externa resurser när du arbetar med Excel-arbetsböcker. I slutet av den här guiden kommer du att kunna implementera en anpassad lösning för att ladda bilder och data från externa källor utan ansträngning.
## Förutsättningar
Innan vi hoppar in i det nitty-gritty med kodning, finns det några förutsättningar du måste ha på plats. Se till att du:
1. Har Visual Studio: Du behöver en IDE för att skriva och testa dina .NET-applikationer. Visual Studio är det mest rekommenderade alternativet på grund av dess omfattande stöd och användarvänlighet.
2.  Ladda ner Aspose.Cells för .NET: Om du inte redan har gjort det, hämta Aspose.Cells-biblioteket från[nedladdningslänk](https://releases.aspose.com/cells/net/). 
3. Grundläggande förståelse för C#: Bekantskap med C#- och .NET-ramverkskoncept kommer att göra processen smidigare för dig.
4. Ställ in din miljö: Se till att ditt projekt refererar till Aspose.Cells-biblioteket. Du kan göra detta via NuGet Package Manager i Visual Studio.
5. Exempelfiler: Ha ett exempel på en Excel-fil redo som innehåller en extern resurs, till exempel en länkad bild. Den här filen kommer att hjälpa till att demonstrera de funktioner vi diskuterar.
När du väl är konfigurerad med dessa är du redo att fördjupa dig i att kontrollera externa resurser med Aspose.Cells.
## Importera paket
För att börja koda måste du importera de nödvändiga paketen i din C#-fil. Här är vad du behöver:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
Dessa namnområden ger tillgång till de funktioner som krävs för att manipulera Excel-filer och hantera bilder.
 Låt oss dela upp det i hanterbara steg för att hjälpa dig kontrollera externa resurser med hjälp av`Workbook Settings`. Vi går igenom att skapa en anpassad strömleverantör, ladda en Excel-fil och rendera ett kalkylblad till en bild. Följ gärna med!
## Steg 1: Definiera käll- och utdatakataloger
Till att börja med måste vi ange katalogerna varifrån vi ska läsa våra filer och var vi ska spara våra utdata. Det är viktigt att ställa in rätt sökvägar för att undvika fel på filen som inte hittas.
```csharp
// Källkatalog
static string sourceDir = "Your Document Directory";
// Utdatakatalog
static string outputDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen där dina filer finns.
## Steg 2: Implementera IStreamProvider-gränssnittet
 Därefter skapar vi en anpassad klass som implementerar`IStreamProvider` gränssnitt. Den här klassen kommer att hantera hur externa resurser (som bilder) nås.
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // Rensa upp eventuella resurser om det behövs
    }
    public void InitStream(StreamProviderOptions options)
    {
        // Öppna filströmmen för den externa resursen
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
 I den`InitStream` metoden öppnar vi filen som fungerar som vår externa resurs och tilldelar den till`Stream`egendom. Detta tillåter arbetsboken att komma åt resursen vid rendering.
## Steg 3: Ladda Excel-filen
Nu när vi har vår strömleverantör redo, låt oss ladda Excel-arbetsboken som innehåller den externa resursen.
```csharp
public static void Run()
{
    // Ladda exempel på Excel-fil
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // Ge din implementering av IStreamProvider
    wb.Settings.StreamProvider = new SP();
```
 I det här utdraget laddar vi vår Excel-fil och tilldelar vår anpassade`StreamProvider` implementering för att hantera externa resurser.
## Steg 4: Öppna arbetsbladet
Efter att ha laddat arbetsboken kan vi enkelt komma åt önskat arbetsblad. Låt oss ta den första.
```csharp
    // Öppna första kalkylbladet
    Worksheet ws = wb.Worksheets[0];
```
Det är okomplicerat, eller hur? Du kan komma åt vilket kalkylblad som helst genom att ange dess index.
## Steg 5: Konfigurera bild- eller utskriftsalternativ
Nu ska vi definiera hur vi vill att utdatabilden ska se ut. Vi kommer att konfigurera alternativ som att se till att det finns en sida för varje ark och ange typen av utdatabild.
```csharp
    // Ange bild- eller utskriftsalternativ
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
Att välja PNG som utdataformat säkerställer att kvaliteten förblir skarp och tydlig!
## Steg 6: Gör arbetsbladet till en bild
Med allt inställt, låt oss göra vårt valda kalkylblad till en bildfil! Detta är den spännande delen; du kommer att se ditt Excel-ark förvandlas till en vacker bild.
```csharp
    // Skapa arkrendering genom att skicka nödvändiga parametrar
    SheetRender sr = new SheetRender(ws, opts);
    // Konvertera hela ditt kalkylblad till png-bild
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
 De`ToImage` funktionen gör allt det tunga arbetet och konverterar arket till en bild. När detta steg är klart hittar du bilden sparad i din utdatakatalog.
## Slutsats
Och där har du det! Du har nu kunskapen att kontrollera externa resurser när du arbetar med Excel-filer med Aspose.Cells i .NET. Detta förbättrar inte bara din applikations möjligheter utan gör också hantering av datauppsättningar och presentationer till en strandpromenad. Genom att följa de angivna stegen kan du enkelt replikera och anpassa denna funktion för att passa ditt projekts specifika behov.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek designat för C#- och .NET-utvecklare för att skapa, manipulera och hantera Excel-filer utan att behöva installera Microsoft Excel.
### Hur kan jag ladda ner Aspose.Cells för .NET?
 Du kan ladda ner den från[Aspose hemsida](https://releases.aspose.com/cells/net/).
### Finns det en gratis provperiod?
 Ja! Du kan få tillgång till en gratis provversion av Aspose.Cells från deras[släpp sida](https://releases.aspose.com/).
### Vilka typer av filer stöder Aspose.Cells?
Aspose.Cells stöder olika Excel-format, inklusive XLS, XLSX, CSV och mer.
### Var kan jag hitta support för Aspose.Cells?
 Du kan besöka Asposes supportforum på[Aspose Forum](https://forum.aspose.com/c/cells/9) för hjälp.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
