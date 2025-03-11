---
title: Styr externa resurser i Excel till PDF i Aspose.Cells
linktitle: Styr externa resurser i Excel till PDF i Aspose.Cells
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck hur du styr externa resurser i Excel till PDF-konvertering med Aspose.Cells för .NET med vår lättanvända guide.
weight: 12
url: /sv/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Styr externa resurser i Excel till PDF i Aspose.Cells

## Introduktion
I dagens digitala tidsålder är det en vanlig uppgift att konvertera Excel-kalkylblad till PDF-dokument. Oavsett om det handlar om att förbereda rapporter, finansiella data eller presentationsmaterial vill du se till att dina PDF-filer ser ut precis som du tänkt dig. Aspose.Cells för .NET är ett robust bibliotek som låter dig kontrollera denna konverteringsprocess in i minsta detalj, speciellt när du hanterar externa resurser som bilder som åtföljer dina Excel-filer. I den här guiden fördjupar vi oss i hur man kontrollerar externa resurser under konverteringsprocessen från Excel till PDF med Aspose.Cells. Så ta din favoritdryck och låt oss komma igång!
## Förutsättningar
Innan vi hoppar in i det roliga, låt oss se till att du har allt du behöver för att komma igång. Här är en snabb checklista:
1. Visual Studio eller någon .NET-kompatibel IDE: Du vill ha en miljö för att skriva och testa din kod.
2.  Aspose.Cells för .NET: Om du inte har installerat det ännu, gå över till[Aspose nedladdningar](https://releases.aspose.com/cells/net/) sida och hämta den senaste versionen.
3. Grundläggande kunskaper i C#: Bekantskap med programmeringsspråket C# kommer att vara till hjälp. Om du är osäker på några begrepp, tveka inte att slå upp dem.
4. Ett exempel på en Excel-fil: Förbered en Excel-fil med alla externa resurser som du vill konvertera. Du kan använda den medföljande exempelfilen "samplePdfSaveOptions_StreamProvider.xlsx".
5. En bildfil för testning: Denna kommer att användas som en extern resurs under konverteringen. Bildfilen "newPdfSaveOptions_StreamProvider.png" är en bra platshållare.
## Importera paket
För att komma igång måste du importera de nödvändiga namnrymden från Aspose.Cells-biblioteket. Detta är avgörande för att få tillgång till dess funktioner. Se till att lägga till följande med hjälp av direktiv överst i filen:
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
Dessa paket kommer att tillhandahålla alla viktiga klasser och metoder du behöver för att utföra dina uppgifter.
## Steg 1: Skapa din strömleverantörsklass
 Den första ordern är att skapa en strömleverantörsklass som implementerar`IStreamProvider` gränssnitt. Den här klassen låter dig kontrollera hur externa resurser laddas.
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        // Läs den nya bilden i en minnesström och tilldela den till Stream-egenskapen
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
I den här klassen:
- CloseStream: Denna metod kommer att anropas när strömmen stängs. För närvarande skriver vi bara ett felsökningsmeddelande för spårning.
-  InitStream: Det är här magin börjar. Här kommer du att läsa din externa bild som en byte-array, konvertera den till en minnesström och tilldela den till`options.Stream` egendom.
## Steg 2: Ställ in käll- och utdatakataloger
Nu när din streamleverantör är redo är det dags att fastställa var din Excel-fil finns och var du vill spara din PDF.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
 Byt bara ut`"Your Document Directory"` med den faktiska sökvägen på din dator där dina filer finns. Att hålla dina filer organiserade är nyckeln!
## Steg 3: Ladda din Excel-fil
Därefter laddar du Excel-filen från vilken du vill skapa PDF-filen.
```csharp
// Ladda källexcelfil som innehåller externa bilder
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
 Vi använder`Workbook` klass från Aspose.Cells, som representerar din Excel-fil. Filen kan innehålla olika externa resurser som bilder som du vill kontrollera under konverteringen.
## Steg 4: Ställ in PDF-sparalternativ
Innan du sparar arbetsboken som en PDF, låt oss ange hur du vill spara den. Du kan justera dessa alternativ enligt dina krav.
```csharp
// Ange Pdf-sparalternativ - Stream Provider
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Spara varje ark på en ny sida
```
 Här skapar vi en ny instans av`PdfSaveOptions` , som låter dig anpassa hur din PDF-fil ska formateras. De`OnePagePerSheet`alternativet är praktiskt för att säkerställa att varje Excel-ark får sin egen sida i den slutliga PDF-filen.
## Steg 5: Tilldela din strömleverantör
Med dina PDF-alternativ inställda måste du berätta för Aspose att använda din anpassade strömleverantör för externa resurser.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
 Denna linje ansluter din`Workbook` exempel med`MyStreamProvider` klass du skapade tidigare. Detta innebär att närhelst externa resurser påträffas under konverteringen kommer din leverantör att hantera dem enligt vad som anges.
## Steg 6: Spara arbetsboken som PDF
Med allt klart är det äntligen dags att spara din Excel-arbetsbok som en PDF.
```csharp
// Spara arbetsboken till pdf
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
 Genom att ringa till`Save` metod på arbetsboksobjektet och skickar in din utdatakatalog tillsammans med PDF-alternativen, konverterar du Excel-filen till en vackert formaterad PDF.
## Steg 7: Bekräfta framgångsrik exekvering
För att avsluta saken är det alltid trevligt att bekräfta att din process har varit framgångsrik!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Att skriva ut ett framgångsmeddelande till konsolen hjälper dig att hålla dig informerad om statusen för din operation. Det är en god vana att inkludera dessa små bekräftelser i din kod.
## Slutsats
Där har du det! Genom att följa dessa enkla steg kan du sakkunnigt kontrollera hur externa resurser hanteras under Excel till PDF-konverteringar med Aspose.Cells. Detta innebär att dina dokument nu kan innehålla bilder och andra externa element exakt, vilket säkerställer en polerad slutprodukt varje gång.
## FAQ's
### Vad är Aspose.Cells?  
Aspose.Cells är ett kraftfullt bibliotek för .NET-utvecklare som låter dig skapa, manipulera, konvertera och rendera Excel-filer i olika format.
### Hur laddar jag ner Aspose.Cells?  
 Du kan ladda ner den senaste versionen av Aspose.Cells från[Ladda ner länk](https://releases.aspose.com/cells/net/).
### Kan jag prova Aspose.Cells gratis?  
 Ja! Du kan få en gratis provperiod genom att besöka[Gratis provsida](https://releases.aspose.com/).
### Var kan jag hitta support för Aspose.Cells?  
 För alla supportrelaterade frågor kan du besöka[Aspose Supportforum](https://forum.aspose.com/c/cells/9).
### Hur kan jag få en tillfällig licens för Aspose.Cells?  
 Du kan ansöka om en tillfällig licens[här](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
