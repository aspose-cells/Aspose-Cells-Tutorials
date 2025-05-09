---
"description": "Lär dig hur du ställer in tiden för PDF-skapande i .NET med Aspose.Cells. Följ vår steg-för-steg-guide för sömlös konvertering från Excel till PDF."
"linktitle": "Ställa in PDF-skapningstid i .NET"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ställa in PDF-skapningstid i .NET"
"url": "/sv/net/xps-and-pdf-operations/setting-pdf-creation-time/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ställa in PDF-skapningstid i .NET

## Introduktion
dagens digitala tidsålder är möjligheten att konvertera dokument till olika format avgörande för många applikationer. Ett vanligt behov är att konvertera Excel-kalkylblad till PDF-filer. Detta bevarar inte bara formateringen, utan gör det också mycket enklare att dela och skriva ut. Om du är en utvecklare som arbetar med .NET är Aspose.Cells ett fantastiskt bibliotek som förenklar denna process. I den här handledningen går vi in på hur man ställer in PDF-skapningstiden när man konverterar en Excel-fil till PDF med Aspose.Cells för .NET.
## Förkunskapskrav
Innan vi går in på kodens detaljer, låt oss se till att du har allt du behöver för att komma igång.
### Vad du behöver
1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Detta kommer att vara din utvecklingsmiljö.
2. Aspose.Cells för .NET: Ladda ner Aspose.Cells-biblioteket från [webbplats](https://releases.aspose.com/cells/net/)Du kan också börja med en gratis provperiod för att testa dess funktioner.
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
4. Excel-fil: Ha en Excel-fil redo för konvertering. I det här exemplet använder vi en fil med namnet `Book1.xlsx`.
Nu när du har sorterat förutsättningarna, låt oss gå vidare till den roliga delen – att importera de nödvändiga paketen och skriva koden!
## Importera paket
För att börja måste du importera de namnrymder som krävs till din C#-fil. Detta är avgörande eftersom det ger dig åtkomst till de klasser och metoder som tillhandahålls av Aspose.Cells-biblioteket.
### Öppna ditt C#-projekt
Öppna Visual Studio och skapa antingen ett nytt projekt eller öppna ett befintligt där du vill implementera PDF-konverteringsfunktionen.
### Lägg till Aspose.Cells-referens
Du kan lägga till Aspose.Cells-biblioteket i ditt projekt genom att högerklicka på projektet i Solution Explorer, välja "Hantera NuGet-paket" och söka efter "Aspose.Cells". Installera paketet.
### Importera namnrymder
Överst i din C#-fil, inkludera följande namnrymder:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Dessa namnrymder ger dig tillgång till Workbook-klassen och andra viktiga funktioner.

Nu när vi har importerat våra paket, låt oss gå igenom processen för att konvertera en Excel-fil till en PDF samtidigt som vi ställer in skapandetiden.
## Steg 1: Definiera dokumentkatalogen
Först måste du ange katalogen där dina dokument lagras. Det är här din Excel-fil finns och där den utgående PDF-filen kommer att sparas.
```csharp
string dataDir = "Your Document Directory"; // Ange din dokumentkatalog
```
Ersätta `"Your Document Directory"` med den faktiska vägen dit din `Book1.xlsx` filen finns. Den här sökvägen hjälper programmet att hitta filen för bearbetning.
## Steg 2: Ladda Excel-filen
Sedan laddar du Excel-filen till en `Workbook` objekt. Det är här Aspose.Cells glänser, eftersom det låter dig arbeta med Excel-filer utan ansträngning.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Sökväg till din Excel-fil
Workbook workbook = new Workbook(inputPath); // Ladda Excel-filen
```
De `Workbook` Klassen används för att ladda och manipulera Excel-filer. Genom att skicka inmatningssökvägen anger du vilken fil programmet ska arbeta med.
## Steg 3: Skapa PDFSaveOptions
Nu är det dags att skapa en instans av `PdfSaveOptions`Den här klassen låter dig ange olika alternativ för att spara din arbetsbok som en PDF, inklusive skapandetid.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Skapa PdfSaveOptions-instans
options.CreatedTime = DateTime.Now; // Ställ in skapandetiden till nu
```
Genom att ställa in `options.CreatedTime` till `DateTime.Now`, ser du till att PDF-filen återspeglar aktuellt datum och tid då den skapades.
## Steg 4: Spara arbetsboken som PDF
Slutligen sparar du arbetsboken som en PDF-fil med de alternativ du just definierade.
```csharp
workbook.Save(dataDir + "output.pdf", options); // Spara som PDF
```
Den här kodraden tar arbetsboken och sparar den i PDF-format på den angivna platsen. `options` parametern skickas för att inkludera skapandetiden i PDF-metadata.

## Slutsats
Och där har du det! Du har framgångsrikt konverterat en Excel-fil till en PDF med Aspose.Cells för .NET, komplett med en tidsstämpel för skapande. Den här funktionen kan vara otroligt användbar när du behöver hålla reda på dokumentversioner eller när du vill ge mottagarna information om när dokumentet skapades.
Om du vill utforska fler funktioner i Aspose.Cells, tveka inte att kolla in [dokumentation](https://reference.aspose.com/cells/net/).
## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för .NET som låter utvecklare skapa, manipulera och konvertera Excel-filer.
### Kan jag använda Aspose.Cells gratis?
Ja, du kan börja med en gratis provperiod som är tillgänglig på [Aspose webbplats](https://releases.aspose.com/).
### Hur ställer jag in andra PDF-egenskaper?
Du kan ange olika PDF-egenskaper med hjälp av `PdfSaveOptions` klass, såsom sidstorlek, komprimering med mera.
### Är det möjligt att konvertera flera Excel-filer samtidigt?
Ja, du kan gå igenom en lista med filer och tillämpa samma konverteringsprocess på var och en.
### Var kan jag få support för Aspose.Cells?
Du kan få stöd från Aspose-communityn på deras [supportforum](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}