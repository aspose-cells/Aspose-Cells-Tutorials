---
title: Ställ in standardteckensnitt för PDF-sparalternativ
linktitle: Ställ in standardteckensnitt för PDF-sparalternativ
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du ställer in standardteckensnitt för PDF-sparalternativ med Aspose.Cells för .NET, vilket säkerställer att dina dokument ser perfekta ut varje gång.
weight: 11
url: /sv/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställ in standardteckensnitt för PDF-sparalternativ

## Introduktion
När det kommer till att generera rapporter, fakturor eller andra dokument i PDF-format är det viktigt att se till att ditt innehåll ser helt rätt ut. Teckensnitt spelar en viktig roll för att upprätthålla det visuella tilltalande och läsbarheten hos dina dokument. Men vad händer när typsnittet du använde i din Excel-fil inte är tillgängligt på systemet där du genererar din PDF? Det är där Aspose.Cells för .NET kommer väl till pass. Detta kraftfulla bibliotek låter dig ställa in standardteckensnitt för dina PDF-sparalternativ, vilket säkerställer att dina dokument ser professionella och konsekventa ut, oavsett var de öppnas.
## Förutsättningar
Innan vi börjar, se till att du har följande:
1. Visual Studio: Du behöver en utvecklingsmiljö som Visual Studio för att skriva och köra din kod.
2.  Aspose.Cells för .NET: Du kan ladda ner den senaste versionen från[denna länk](https://releases.aspose.com/cells/net/). Alternativt kan du installera den via NuGet Package Manager i Visual Studio.
3. Grundläggande kunskaper om C#: Att förstå grunderna i C# hjälper dig att följa med i kodexemplen.
4. Exempel på Excel-fil: Ha ett exempel på en Excel-fil redo för testning. Du kan skapa en med olika typsnitt och stilar för att se hur Aspose.Cells hanterar saknade teckensnitt.
## Importera paket
Innan du kan använda Aspose.Cells i ditt projekt måste du importera de nödvändiga paketen. Så här gör du:
1. Öppna ditt projekt: Starta Visual Studio och öppna ditt befintliga projekt eller skapa ett nytt.
2. Lägg till referenser: Högerklicka på ditt projekt i Solution Explorer och välj "Hantera NuGet-paket."
3. Installera Aspose.Cells: Sök efter "Aspose.Cells" och klicka på knappen "Installera".
4. Lägg till med hjälp av direktiv: Överst i din C#-fil, inkludera följande namnområden:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Steg 1: Konfigurera dina kataloger
Innan du arbetar med filer är det viktigt att definiera käll- och utdatakatalogerna. Detta kommer att göra det lättare att hitta din indata Excel-fil och spara de genererade utdatafilerna.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
 Ersätta`"Your Document Directory"` med den faktiska sökvägen till dina kataloger.
## Steg 2: Öppna Excel-filen
 Nu när vi har ställt in våra kataloger, låt oss öppna Excel-filen som du vill arbeta med. De`Workbook` klass i Aspose.Cells används för att ladda Excel-dokumentet.
```csharp
// Öppna en Excel-fil
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Se till att ersätta filnamnet med ditt faktiska filnamn.
## Steg 3: Ställ in alternativ för bildrendering
Därefter måste vi konfigurera renderingsalternativen för att konvertera vårt Excel-ark till ett bildformat. Vi skapar en instans av`ImageOrPrintOptions`, som anger bildtyp och standardteckensnitt.
```csharp
// Rendering till PNG-filformat
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
 I det här kodavsnittet ställer vi in`CheckWorkbookDefaultFont` egendom till`false`, vilket innebär att om några teckensnitt saknas kommer det angivna standardteckensnittet (“Times New Roman”) att användas istället.
## Steg 4: Gör arket som en bild
 Låt oss nu återge det första arket i arbetsboken som en PNG-bild. Vi kommer att använda`SheetRender` klass för att åstadkomma detta.
```csharp
// Gör det första kalkylbladet till en bild
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Steg 5: Ändra bildtyp och rendera till TIFF
 Om du vill rendera samma ark till ett annat bildformat, som TIFF, kan du helt enkelt ändra`ImageType` egenskap och upprepa renderingsprocessen.
```csharp
// Ställ in på TIFF-format
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Steg 6: Konfigurera PDF-sparalternativ
 Nästa upp, låt oss ställa in PDF-sparalternativen. Vi kommer att skapa en instans av`PdfSaveOptions`ställ in standardteckensnittet och ange att vi vill kontrollera om teckensnitt saknas.
```csharp
// Konfigurera PDF-sparalternativ
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Steg 7: Spara arbetsboken som en PDF
Med sparalternativen konfigurerade är det dags att spara vår Excel-arbetsbok som en PDF-fil. 
```csharp
// Spara arbetsboken till PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Steg 8: Bekräfta exekvering
Slutligen är det en bra praxis att låta användaren veta att processen har slutförts framgångsrikt. Du kan uppnå detta genom att använda ett enkelt konsolmeddelande.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Slutsats
Aspose.Cells tillhandahåller ett flexibelt och robust sätt att hantera Excel-filmanipulationer, vilket gör det lättare för utvecklare att skapa visuellt tilltalande dokument som bibehåller sin formatering. Oavsett om du arbetar med rapporter, finansiella dokument eller någon annan form av datapresentation, kan kontroll över teckensnittsrendering förbättra din utskriftskvalitet avsevärt.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt .NET-bibliotek som tillåter utvecklare att manipulera Excel-filer utan att behöva installera Microsoft Excel. Den stöder olika filformat och erbjuder rika funktioner för att arbeta med kalkylblad.
### Hur kan jag ställa in ett standardteckensnitt för mina Excel-filer?
 Du kan ställa in ett standardteckensnitt med hjälp av`PdfSaveOptions` klass och ange önskat teckensnittsnamn. Detta säkerställer att även om ett teckensnitt saknas kommer ditt dokument att använda standardteckensnittet du har angett.
### Kan jag konvertera Excel-filer till andra format än PDF?
Absolut! Aspose.Cells låter dig konvertera Excel-filer till olika format, inklusive bilder (PNG, TIFF), HTML, CSV och mer.
### Är Aspose.Cells gratis att använda?
Aspose.Cells är en kommersiell produkt, men du kan prova den gratis med en begränsad testversion. För full funktionalitet måste du köpa en licens.
### Var kan jag hitta support för Aspose.Cells?
 Du kan hitta support för Aspose.Cells genom att besöka[Aspose forum](https://forum.aspose.com/c/cells/9), där du kan ställa frågor och dela insikter med andra användare och utvecklare.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
