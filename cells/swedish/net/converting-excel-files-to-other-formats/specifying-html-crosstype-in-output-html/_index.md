---
title: Ange HTML CrossType i Output HTML Programmatically i .NET
linktitle: Ange HTML CrossType i Output HTML Programmatically i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du anger HTML CrossType i Aspose.Cells för .NET. Följ vår steg-för-steg handledning för att konvertera Excel-filer till HTML med precision.
weight: 17
url: /sv/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ange HTML CrossType i Output HTML Programmatically i .NET

## Introduktion
När det gäller att konvertera Excel-filer till HTML i .NET-applikationer kan du behöva specificera hur korsreferenser hanteras i utdata. Klassen HtmlSaveOptions i Aspose.Cells för .NET tillhandahåller olika inställningar för att styra konverteringsprocessen, och ett av dessa alternativ är HtmlCrossType. I den här självstudien går vi igenom hur du programmatiskt anger HTML-korstypen när du exporterar Excel-filer till HTML-format. 
## Förutsättningar
Innan du dyker in i koden, se till att du har följande:
-  Aspose.Cells för .NET: Se till att du har Aspose.Cells-biblioteket installerat i ditt projekt. Du kan ladda ner den från[Aspose hemsida](https://releases.aspose.com/cells/net/).
- Visual Studio: En fungerande installation av Visual Studio eller någon annan .NET-utvecklingsmiljö.
- Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå exemplen bättre.
-  Exempel på Excel-fil: Ha ett exempel på en Excel-fil redo att arbeta med. För det här exemplet kommer vi att använda`sampleHtmlCrossStringType.xlsx`.
## Importera paket
För att komma igång måste du importera de nödvändiga Aspose.Cells-namnrymden. Så här kan du göra det:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Låt oss dela upp detta steg för steg, vilket gör det enkelt för dig att följa med och implementera denna funktionalitet i dina egna projekt.
## Steg 1: Definiera dina käll- och utdatakataloger
Först måste du ställa in katalogerna för din Excel-källfil och var du vill spara HTML-utdatafilen.
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
// Utdatakatalog
string outputDir = "Your Document Directory";
```
## Steg 2: Ladda Excel-exempelfilen
 Ladda sedan in exemplet på Excel-filen i en`Workbook` objekt. Det är här all magi börjar.
```csharp
// Ladda exemplet på Excel-filen
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
 Här, byt ut`"Your Document Directory"` med den faktiska sökvägen där din Excel-fil finns. Den här raden läser in Excel-filen i minnet så att du kan manipulera den.
## Steg 3: Ange HTML-sparalternativ
 Nu ska vi skapa en instans av`HtmlSaveOptions`, som låter dig konfigurera hur Excel-filen ska konverteras till HTML.
```csharp
// Ange HTML Cross Type
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
 I det här steget har vi ställt in`HtmlCrossStringType` till`HtmlCrossType.Default`, vilket är ett av de tillgängliga alternativen för att hantera korsreferenser i utdata-HTML.
## Steg 4: Ändra korstypen efter behov
 Du kan ange olika typer för`HtmlCrossStringType` baserat på dina krav. Här är de olika alternativen du kan använda:
- `HtmlCrossType.Default`: Standardkrysstypen.
- `HtmlCrossType.MSExport`: Exporterar HTML med MS Excel-liknande beteende.
- `HtmlCrossType.Cross`: Skapar korsreferenser.
- `HtmlCrossType.FitToCell`: Passar korsreferenserna till celldimensionerna.
 Du kan ändra`HtmlCrossStringType` så här:
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
// eller
opts.HtmlCrossStringType = HtmlCrossType.Cross;
// eller
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## Steg 5: Spara HTML-filen för utdata
 När du har konfigurerat dina alternativ är det dags att spara den konverterade HTML-filen. Använd`Save` metod på din`Workbook` objekt:
```csharp
// Utdata HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
 Här namnger vi utdatafilen baserat på`HtmlCrossStringType` vi har satt. På så sätt kan du enkelt identifiera vilken korstyp som användes i konverteringen.
## Steg 6: Bekräfta framgångsrik exekvering
Slutligen är det alltid bra att bekräfta att din operation var framgångsrik. Du kan skriva ut ett meddelande till konsolen:
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
Detta kommer att låta dig veta att processen har slutförts utan några fel.
## Slutsats
Och där har du det! Du har angett HTML-korstypen för din Excel-export i .NET med Aspose.Cells. Den här funktionen är särskilt användbar när du behöver behålla specifik formatering eller referenser i din HTML-utdata, för att säkerställa att dina konverterade dokument uppfyller dina krav.
## FAQ's
### Vad är HtmlCrossType i Aspose.Cells?  
HtmlCrossType definierar hur korsreferenser i Excel-filen hanteras under HTML-konvertering. Du kan välja alternativ som Default, MSExport, Cross och FitToCell.
### Kan jag använda Aspose.Cells gratis?  
 Aspose.Cells erbjuder en gratis testversion. Du kan ladda ner den från deras[webbplats](https://releases.aspose.com/).
### Hur installerar jag Aspose.Cells i mitt .NET-projekt?  
 Du kan installera Aspose.Cells via NuGet Package Manager i Visual Studio genom att köra kommandot:`Install-Package Aspose.Cells`.
### Var kan jag hitta dokumentationen för Aspose.Cells?  
 Du kan hitta omfattande dokumentation på Aspose.Cells[här](https://reference.aspose.com/cells/net/).
### Vad ska jag göra om jag stöter på ett fel när jag sparar HTML-filen?  
Se till att katalogsökvägarna är korrekta och att du har skrivbehörighet för utdatakatalogen. Om problemet kvarstår, kolla Asposes supportforum för hjälp.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
