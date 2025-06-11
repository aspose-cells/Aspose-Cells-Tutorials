---
"description": "Upptäck det maximala antalet rader och kolumner som stöds av XLS- och XLSX-format med Aspose.Cells för .NET. Maximera din Excel-datahantering med den här omfattande handledningen."
"linktitle": "Hitta max antal rader och kolumner som stöds av XLS- och XLSX-format"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Hitta max antal rader och kolumner som stöds av XLS- och XLSX-format"
"url": "/sv/net/workbook-settings/find-maximum-supported-rows-columns/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Hitta max antal rader och kolumner som stöds av XLS- och XLSX-format

## Introduktion
I Excels värld kan det vara en svår uppgift att hantera stora datamängder, särskilt när det gäller att hantera det maximala antalet rader och kolumner som stöds av olika filformat. Den här handledningen guidar dig genom processen att hitta det maximala antalet rader och kolumner som stöds av XLS- och XLSX-formaten med hjälp av Aspose.Cells för .NET-biblioteket. I slutet av den här artikeln har du en omfattande förståelse för hur du använder detta kraftfulla verktyg för att hantera dina Excel-relaterade uppgifter effektivt.
## Förkunskapskrav
Innan vi går in i handledningen, se till att du har följande förutsättningar på plats:
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) eller [.NET-kärna](https://dotnet.microsoft.com/en-us/download) installerat på ditt system.
2. [Aspose.Cells för .NET](https://releases.aspose.com/cells/net/) biblioteket som laddats ner och refererats till i ditt projekt.
Om du inte redan har gjort det kan du ladda ner Aspose.Cells för .NET-biblioteket från [webbplats](https://releases.aspose.com/cells/net/) eller installera den via [NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Importera paket
För att komma igång måste du importera de nödvändiga paketen från Aspose.Cells för .NET-biblioteket. Lägg till följande using-satser högst upp i din C#-fil:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Steg 1: Hitta det maximala antalet rader och kolumner som stöds av XLS-formatet
Låt oss börja med att utforska det maximala antalet rader och kolumner som stöds av XLS-formatet (Excel 97-2003).
```csharp
// Skriv ut meddelande om XLS-format.
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// Skapa arbetsbok i XLS-format.
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// Skriv ut det maximala antalet rader och kolumner som stöds av XLS-formatet.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
I det här steget gör vi följande:
1. Skriv ut ett meddelande som anger att vi arbetar med XLS-formatet.
2. Skapa en ny `Workbook` exempel med hjälp av `FileFormatType.Excel97To2003` enum, vilket representerar XLS-formatet.
3. Hämta det maximala antalet rader och kolumner som stöds av XLS-formatet med hjälp av `Workbook.Settings.MaxRow` och `Workbook.Settings.MaxColumn` egenskaper, respektive. Vi lägger till 1 till dessa värden för att få det faktiska maximala antalet rader och kolumner (eftersom de är nollbaserade).
4. Skriv ut det maximala antalet rader och kolumner till konsolen.
## Steg 2: Hitta det maximala antalet rader och kolumner som stöds av XLSX-formatet
Nu ska vi utforska det maximala antalet rader och kolumner som stöds av XLSX-formatet (Excel 2007 och senare).
```csharp
// Skriv ut meddelande om XLSX-format.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Skapa arbetsboken i XLSX-format.
wb = new Workbook(FileFormatType.Xlsx);
// Skriv ut det maximala antalet rader och kolumner som stöds av XLSX-formatet.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
I det här steget gör vi följande:
1. Skriv ut ett meddelande som anger att vi arbetar med XLSX-formatet.
2. Skapa en ny `Workbook` exempel med hjälp av `FileFormatType.Xlsx` enum, vilket representerar XLSX-formatet.
3. Hämta det maximala antalet rader och kolumner som stöds av XLSX-formatet med hjälp av `Workbook.Settings.MaxRow` och `Workbook.Settings.MaxColumn` egenskaper, respektive. Vi lägger till 1 till dessa värden för att få det faktiska maximala antalet rader och kolumner (eftersom de är nollbaserade).
4. Skriv ut det maximala antalet rader och kolumner till konsolen.
## Steg 3: Visa ett meddelande om att det lyckades
Slutligen visar vi ett meddelande som indikerar att exemplet "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats" har körts.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Det här steget skriver helt enkelt ut ett meddelande om framgång till konsolen.
## Slutsats
I den här handledningen har du lärt dig hur du använder Aspose.Cells för .NET-biblioteket för att hitta det maximala antalet rader och kolumner som stöds av XLS- och XLSX-filformaten. Genom att förstå begränsningarna med dessa format kan du bättre planera och hantera dina Excel-baserade projekt och säkerställa att dina data ryms inom de intervall som stöds.
## Vanliga frågor
### Vilket är det maximala antalet rader som stöds av XLS-formatet?
Det maximala antalet rader som stöds av XLS-formatet (Excel 97-2003) är 65 536.
### Vilket är det maximala antalet kolumner som stöds av XLS-formatet?
Det maximala antalet kolumner som stöds av XLS-formatet (Excel 97-2003) är 256.
### Vilket är det maximala antalet rader som stöds av XLSX-formatet?
Det maximala antalet rader som stöds av XLSX-formatet (Excel 2007 och senare) är 1 048 576.
### Vilket är det maximala antalet kolumner som stöds av XLSX-formatet?
Det maximala antalet kolumner som stöds av XLSX-formatet (Excel 2007 och senare) är 16 384.
### Kan jag använda Aspose.Cells för .NET-biblioteket för att arbeta med andra Excel-filformat?
Ja, Aspose.Cells för .NET-biblioteket stöder ett brett utbud av Excel-filformat, inklusive XLS, XLSX, ODS och fler. Du kan utforska [dokumentation](https://reference.aspose.com/cells/net/) för att lära dig om tillgängliga funktioner och funktionaliteter.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}