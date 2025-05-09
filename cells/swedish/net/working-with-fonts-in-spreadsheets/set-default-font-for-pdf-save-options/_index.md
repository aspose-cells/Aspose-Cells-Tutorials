---
"description": "Lär dig hur du ställer in standardteckensnitt för PDF-sparalternativ med Aspose.Cells för .NET, så att dina dokument ser perfekta ut varje gång."
"linktitle": "Ange standardteckensnitt för PDF-sparalternativ"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ange standardteckensnitt för PDF-sparalternativ"
"url": "/sv/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange standardteckensnitt för PDF-sparalternativ

## Introduktion
När det gäller att generera rapporter, fakturor eller andra dokument i PDF-format är det av största vikt att se till att ditt innehåll ser perfekt ut. Typsnitt spelar en viktig roll för att bibehålla det visuella intrycket och läsbarheten hos dina dokument. Men vad händer när typsnittet du använde i din Excel-fil inte är tillgängligt på systemet där du genererar din PDF? Det är där Aspose.Cells för .NET kommer väl till pass. Detta kraftfulla bibliotek låter dig ställa in standardtypsnitt för dina PDF-sparalternativ, vilket säkerställer att dina dokument ser professionella och konsekventa ut, oavsett var de öppnas.
## Förkunskapskrav
Innan vi börjar, se till att du har följande:
1. Visual Studio: Du behöver en utvecklingsmiljö som Visual Studio för att skriva och exekvera din kod.
2. Aspose.Cells för .NET: Du kan ladda ner den senaste versionen från [den här länken](https://releases.aspose.com/cells/net/)Alternativt kan du installera det via NuGet Package Manager i Visual Studio.
3. Grundläggande kunskaper i C#: Att förstå grunderna i C# hjälper dig att följa kodexemplen.
4. Exempel på Excel-fil: Ha en exempelfil i Excel redo för testning. Du kan skapa en med olika teckensnitt och stilar för att se hur Aspose.Cells hanterar saknade teckensnitt.
## Importera paket
Innan du kan använda Aspose.Cells i ditt projekt måste du importera de nödvändiga paketen. Så här gör du:
1. Öppna ditt projekt: Starta Visual Studio och öppna ditt befintliga projekt eller skapa ett nytt.
2. Lägg till referenser: Högerklicka på ditt projekt i lösningsutforskaren och välj "Hantera NuGet-paket".
3. Installera Aspose.Cells: Sök efter "Aspose.Cells" och klicka på knappen "Installera".
4. Lägg till Använda direktiv: Överst i din C#-fil, inkludera följande namnrymder:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## Steg 1: Konfigurera dina kataloger
Innan du arbetar med filer är det viktigt att definiera käll- och utdatakatalogerna. Detta gör det enklare att hitta din Excel-indatafil och spara de genererade utdatafilerna.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
Ersätta `"Your Document Directory"` med den faktiska sökvägen till dina kataloger.
## Steg 2: Öppna Excel-filen
Nu när vi har konfigurerat våra kataloger, låt oss öppna Excel-filen som du vill arbeta med. `Workbook` Klassen i Aspose.Cells används för att läsa in Excel-dokumentet.
```csharp
// Öppna en Excel-fil
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
Se till att ersätta filnamnet med ditt faktiska filnamn.
## Steg 3: Konfigurera alternativ för bildrendering
Nästa steg är att konfigurera renderingsalternativen för att konvertera vårt Excel-ark till ett bildformat. Vi skapar en instans av `ImageOrPrintOptions`, anger bildtyp och standardteckensnitt.
```csharp
// Rendering till PNG-filformat
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
I det här kodavsnittet ställer vi in `CheckWorkbookDefaultFont` egendom till `false`vilket innebär att om några teckensnitt saknas, kommer det angivna standardteckensnittet ("Times New Roman") att användas istället.
## Steg 4: Rendera arket som en bild
Nu ska vi rendera det första bladet i arbetsboken som en PNG-bild. Vi använder `SheetRender` klass för att åstadkomma detta.
```csharp
// Rendera det första kalkylbladet till en bild
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## Steg 5: Ändra bildtyp och rendera till TIFF
Om du vill rendera samma ark till ett annat bildformat, som TIFF, kan du helt enkelt ändra `ImageType` egenskapen och upprepa renderingsprocessen.
```csharp
// Ställ in på TIFF-format
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## Steg 6: Konfigurera PDF-sparalternativ
Nu ska vi konfigurera alternativen för att spara PDF:en. Vi skapar en instans av `PdfSaveOptions`, ange standardteckensnittet och ange att vi vill kontrollera om det finns saknade teckensnitt.
```csharp
// Konfigurera alternativ för att spara PDF
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## Steg 7: Spara arbetsboken som en PDF
Med konfigurerade sparalternativ är det dags att spara vår Excel-arbetsbok som en PDF-fil. 
```csharp
// Spara arbetsboken till PDF
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## Steg 8: Bekräfta körning
Slutligen är det en bra idé att låta användaren veta att processen har slutförts. Du kan uppnå detta med hjälp av ett enkelt konsolmeddelande.
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## Slutsats
Aspose.Cells erbjuder ett flexibelt och robust sätt att hantera manipulationer av Excel-filer, vilket gör det enklare för utvecklare att skapa visuellt tilltalande dokument som bibehåller sin formatering. Oavsett om du arbetar med rapporter, ekonomiska dokument eller någon annan form av datapresentation, kan kontroll över teckensnittsrendering avsevärt förbättra din utskriftskvalitet.
## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt .NET-bibliotek som låter utvecklare manipulera Excel-filer utan att behöva installera Microsoft Excel. Det stöder olika filformat och erbjuder omfattande funktioner för att arbeta med kalkylblad.
### Hur kan jag ställa in ett standardteckensnitt för mina Excel-filer?
Du kan ange ett standardteckensnitt med hjälp av `PdfSaveOptions` klassen och ange önskat teckensnittsnamn. Detta säkerställer att även om ett teckensnitt saknas kommer ditt dokument att använda standardteckensnittet du har angett.
### Kan jag konvertera Excel-filer till andra format än PDF?
Absolut! Aspose.Cells låter dig konvertera Excel-filer till olika format, inklusive bilder (PNG, TIFF), HTML, CSV med mera.
### Är Aspose.Cells gratis att använda?
Aspose.Cells är en kommersiell produkt, men du kan prova den gratis med en begränsad testversion. För full funktionalitet måste du köpa en licens.
### Var kan jag hitta support för Aspose.Cells?
Du kan hitta support för Aspose.Cells genom att besöka [Aspose-forumet](https://forum.aspose.com/c/cells/9), där du kan ställa frågor och dela insikter med andra användare och utvecklare.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}