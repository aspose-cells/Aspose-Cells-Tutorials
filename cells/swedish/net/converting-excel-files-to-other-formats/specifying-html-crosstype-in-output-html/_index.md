---
"description": "Lär dig hur du anger HTML CrossType i Aspose.Cells för .NET. Följ vår steg-för-steg-handledning för att konvertera Excel-filer till HTML med precision."
"linktitle": "Ange HTML CrossType i utdata-HTML programmatiskt i .NET"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Ange HTML CrossType i utdata-HTML programmatiskt i .NET"
"url": "/sv/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ange HTML CrossType i utdata-HTML programmatiskt i .NET

## Introduktion
När det gäller att konvertera Excel-filer till HTML i .NET-applikationer kan du behöva ange hur korsreferenser hanteras i utdata. Klassen HtmlSaveOptions i Aspose.Cells för .NET tillhandahåller olika inställningar för att styra konverteringsprocessen, och ett av dessa alternativ är HtmlCrossType. I den här handledningen går vi igenom hur man programmatiskt anger HTML-korstypen när man exporterar Excel-filer till HTML-format. 
## Förkunskapskrav
Innan du går in i koden, se till att du har följande:
- Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket installerat i ditt projekt. Du kan ladda ner det från [Aspose webbplats](https://releases.aspose.com/cells/net/).
- Visual Studio: En fungerande installation av Visual Studio eller någon annan .NET-utvecklingsmiljö.
- Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå exemplen bättre.
- Exempel på Excel-fil: Ha en exempelfil i Excel redo att arbeta med. I det här exemplet använder vi `sampleHtmlCrossStringType.xlsx`.
## Importera paket
För att komma igång måste du importera de nödvändiga Aspose.Cells-namnrymderna. Så här gör du:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Låt oss gå igenom detta steg för steg, så att det blir enkelt för dig att följa med och implementera funktionen i dina egna projekt.
## Steg 1: Definiera dina käll- och utdatakataloger
Först måste du ange katalogerna för din källfil i Excel och var du vill spara HTML-utdatafilen.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
## Steg 2: Ladda exempelfilen i Excel
Ladda sedan in din exempelfil i Excel till en `Workbook` objekt. Det är här all magi börjar.
```csharp
// Ladda exempelfilen i Excel
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
Här, ersätt `"Your Document Directory"` med den faktiska sökvägen dit din Excel-fil finns. Den här raden läser in Excel-filen i minnet så att du kan manipulera den.
## Steg 3: Ange HTML-sparalternativ
Nu ska vi skapa en instans av `HtmlSaveOptions`, vilket låter dig konfigurera hur Excel-filen ska konverteras till HTML.
```csharp
// Ange HTML-korstyp
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
I det här steget har vi ställt in `HtmlCrossStringType` till `HtmlCrossType.Default`, vilket är ett av de tillgängliga alternativen för att hantera korsreferenser i utdata-HTML:n.
## Steg 4: Ändra korstypen efter behov
Du kan ange olika typer för `HtmlCrossStringType` baserat på dina krav. Här är de olika alternativen du kan använda:
- `HtmlCrossType.Default`Standardkorstypen.
- `HtmlCrossType.MSExport`Exporterar HTML-koden med ett beteende som liknar MS Excel.
- `HtmlCrossType.Cross`Skapar korsreferenser.
- `HtmlCrossType.FitToCell`Anpassar korsreferenserna till celldimensionerna.
Du kan ändra `HtmlCrossStringType` så här:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExpellert;
// eller 
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// or
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Steg 5: Spara HTML-utdatafilen
När du har konfigurerat dina alternativ är det dags att spara den konverterade HTML-filen. Använd `Save` metod på din `Workbook` objekt:
```csharp
// Utdata i HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
Här namnger vi utdatafilen baserat på `HtmlCrossStringType` vi har ställt in. På så sätt kan du enkelt identifiera vilken korstyp som användes i konverteringen.
## Steg 6: Bekräfta lyckad körning
Slutligen är det alltid en bra idé att bekräfta att din operation lyckades. Du kan skriva ut ett meddelande till konsolen:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Detta kommer att informera dig om att processen har slutförts utan några fel.
## Slutsats
Och där har du det! Du har framgångsrikt angett HTML-korstypen för din Excel-export i .NET med hjälp av Aspose.Cells. Den här funktionen är särskilt användbar när du behöver behålla specifik formatering eller referenser i din HTML-utdata, vilket säkerställer att dina konverterade dokument uppfyller dina krav.
## Vanliga frågor
### Vad är HtmlCrossType i Aspose.Cells?  
HtmlCrossType definierar hur korsreferenser i Excel-filen hanteras under HTML-konvertering. Du kan välja alternativ som Standard, MSExport, Kors och AnpassaTillCell.
### Kan jag använda Aspose.Cells gratis?  
Aspose.Cells erbjuder en gratis testversion. Du kan ladda ner den från deras [webbplats](https://releases.aspose.com/).
### Hur installerar jag Aspose.Cells i mitt .NET-projekt?  
Du kan installera Aspose.Cells via NuGet Package Manager i Visual Studio genom att köra kommandot: `Install-Package Aspose.Cells`.
### Var kan jag hitta dokumentationen för Aspose.Cells?  
Du hittar omfattande dokumentation om Aspose.Cells [här](https://reference.aspose.com/cells/net/).
### Vad ska jag göra om jag stöter på ett fel när jag sparar HTML-filen?  
Se till att sökvägarna till katalogen är korrekta och att du har skrivbehörighet för utdatakatalogen. Om problemet kvarstår kan du söka i Asposes supportforum för hjälp.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}