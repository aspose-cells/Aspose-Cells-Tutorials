---
"description": "Upptäck hur du styr externa resurser i Excel till PDF-konvertering med Aspose.Cells för .NET med vår lättförståeliga guide."
"linktitle": "Kontrollera externa resurser i Excel till PDF i Aspose.Cells"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Kontrollera externa resurser i Excel till PDF i Aspose.Cells"
"url": "/sv/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kontrollera externa resurser i Excel till PDF i Aspose.Cells

## Introduktion
I dagens digitala tidsålder är det en vanlig uppgift att konvertera Excel-kalkylblad till PDF-dokument. Oavsett om det gäller att förbereda rapporter, finansiell data eller presentationsmaterial vill du se till att dina PDF-filer ser ut exakt som du avser. Aspose.Cells för .NET är ett robust bibliotek som låter dig kontrollera denna konverteringsprocess in i minsta detalj, särskilt när du hanterar externa resurser som bilder som medföljer dina Excel-filer. I den här guiden går vi in på hur man kontrollerar externa resurser under konverteringsprocessen från Excel till PDF med Aspose.Cells. Så ta din favoritdryck och låt oss sätta igång!
## Förkunskapskrav
Innan vi går in på detaljerna, låt oss se till att du har allt du behöver för att komma igång. Här är en snabb checklista:
1. Visual Studio eller någon .NET-kompatibel IDE: Du behöver en miljö för att skriva och testa din kod.
2. Aspose.Cells för .NET: Om du inte har installerat det än, gå till [Aspose-nedladdningar](https://releases.aspose.com/cells/net/) sidan och hämta den senaste versionen.
3. Grundläggande kunskaper i C#: Bekantskap med programmeringsspråket C# är bra. Om du är osäker på några begrepp, tveka inte att slå upp dem.
4. En exempelfil i Excel: Förbered en Excel-fil med eventuella externa resurser som du vill konvertera. Du kan använda den medföljande exempelfilen "samplePdfSaveOptions_StreamProvider.xlsx".
5. En bildfil för testning: Denna kommer att användas som en extern resurs under konverteringen. Bildfilen "newPdfSaveOptions_StreamProvider.png" är en bra platshållare.
## Importera paket
För att komma igång måste du importera nödvändiga namnrymder från Aspose.Cells-biblioteket. Detta är avgörande för att komma åt dess funktioner. Se till att lägga till följande using-direktiv högst upp i din fil:
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
Den första uppgiften är att skapa en strömleverantörsklass som implementerar `IStreamProvider` gränssnitt. Den här klassen låter dig styra hur externa resurser laddas.
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
- CloseStream: Den här metoden anropas när strömmen stängs. För tillfället skriver vi bara ett felsökningsmeddelande för spårning.
- InitStream: Det är här magin börjar. Här läser du din externa bild som en byte-array, konverterar den till en minnesström och tilldelar den till `options.Stream` egendom.
## Steg 2: Konfigurera käll- och utdatakataloger
Nu när din strömningsleverantör är klar är det dags att fastställa var din Excel-fil finns och var du vill spara din PDF.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
Byt bara ut `"Your Document Directory"` med den faktiska sökvägen på din dator där dina filer finns. Att hålla dina filer organiserade är nyckeln!
## Steg 3: Ladda din Excel-fil
Sedan laddar du Excel-filen som du vill skapa PDF-filen från.
```csharp
// Ladda källfilen i Excel som innehåller externa bilder
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
Vi använder `Workbook` klassen från Aspose.Cells, som representerar din Excel-fil. Filen kan innehålla olika externa resurser som bilder som du vill kontrollera under konverteringen.
## Steg 4: Ställ in alternativ för att spara PDF
Innan du sparar arbetsboken som en PDF, låt oss ange hur du vill att den ska sparas. Du kan justera dessa alternativ efter dina behov.
```csharp
// Ange alternativ för att spara PDF - Stream Provider
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // Spara varje ark på en ny sida
```
Här skapar vi en ny instans av `PdfSaveOptions`vilket låter dig anpassa hur din PDF ska formateras. `OnePagePerSheet` Alternativet är praktiskt för att säkerställa att varje Excel-ark får sin egen sida i den slutliga PDF-filen.
## Steg 5: Tilldela din streamingleverantör
Med dina PDF-alternativ inställda måste du ange att Aspose ska använda din anpassade strömleverantör för externa resurser.
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
Den här linjen förbinder din `Workbook` exempel med `MyStreamProvider` klass som du skapade tidigare. Det betyder att närhelst externa resurser påträffas under konverteringen kommer din leverantör att hantera dem enligt specifikationerna.
## Steg 6: Spara arbetsboken som PDF
Med allt klart är det äntligen dags att spara din Excel-arbetsbok som en PDF.
```csharp
// Spara arbetsboken till PDF
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
Genom att ringa `Save` metod på arbetsboksobjektet och skickar in din utdatakatalog tillsammans med PDF-alternativen, konverterar du Excel-filen till en vackert formaterad PDF.
## Steg 7: Bekräfta lyckad körning
För att sammanfatta är det alltid trevligt att få bekräftat att processen har varit framgångsrik!
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
Att skriva ut ett lyckat meddelande till konsolen hjälper dig att hålla dig informerad om statusen för din operation. Det är en god vana att inkludera dessa små bekräftelser i din kod.
## Slutsats
Där har du det! Genom att följa dessa enkla steg kan du professionellt kontrollera hur externa resurser hanteras under konverteringar från Excel till PDF med hjälp av Aspose.Cells. Det betyder att dina dokument nu kan inkludera bilder och andra externa element korrekt, vilket garanterar en polerad slutprodukt varje gång.
## Vanliga frågor
### Vad är Aspose.Cells?  
Aspose.Cells är ett kraftfullt bibliotek för .NET-utvecklare som låter dig skapa, manipulera, konvertera och rendera Excel-filer i olika format.
### Hur laddar jag ner Aspose.Cells?  
Du kan ladda ner den senaste versionen av Aspose.Cells från [Nedladdningslänk](https://releases.aspose.com/cells/net/).
### Kan jag prova Aspose.Cells gratis?  
Ja! Du kan få en gratis provperiod genom att besöka [Gratis provsida](https://releases.aspose.com/).
### Var kan jag hitta support för Aspose.Cells?  
För supportrelaterade frågor kan du besöka [Aspose supportforum](https://forum.aspose.com/c/cells/9).
### Hur kan jag få en tillfällig licens för Aspose.Cells?  
Du kan ansöka om ett tillfälligt körkort [här](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}