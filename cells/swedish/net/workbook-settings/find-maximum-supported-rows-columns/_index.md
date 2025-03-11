---
title: Hitta Max rader och kolumner som stöds av XLS- och XLSX-format
linktitle: Hitta Max rader och kolumner som stöds av XLS- och XLSX-format
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck det maximala antalet rader och kolumner som stöds av XLS- och XLSX-format med Aspose.Cells för .NET. Maximera din Excel-datahantering med denna omfattande handledning.
weight: 11
url: /sv/net/workbook-settings/find-maximum-supported-rows-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hitta Max rader och kolumner som stöds av XLS- och XLSX-format

## Introduktion
I Excel-världen kan det vara en skrämmande uppgift att hantera stora datamängder, särskilt när det gäller att hantera det maximala antalet rader och kolumner som stöds av olika filformat. Denna handledning guidar dig genom processen att hitta det maximala antalet rader och kolumner som stöds av XLS- och XLSX-formaten med hjälp av Aspose.Cells for .NET-biblioteket. I slutet av den här artikeln har du en omfattande förståelse för hur du använder detta kraftfulla verktyg för att hantera dina Excel-relaterade uppgifter effektivt.
## Förutsättningar
Innan vi dyker in i handledningen, se till att du har följande förutsättningar på plats:
1. [.NET Framework](https://dotnet.microsoft.com/en-us/download) eller[.NET Core](https://dotnet.microsoft.com/en-us/download) installerat på ditt system.
2. [Aspose.Cells för .NET](https://releases.aspose.com/cells/net/) bibliotek som laddas ner och refereras till i ditt projekt.
 Om du inte redan har gjort det kan du ladda ner Aspose.Cells for .NET-biblioteket från[webbplats](https://releases.aspose.com/cells/net/) eller installera den via[NuGet](https://www.nuget.org/packages/Aspose.Cells/).
## Importera paket
För att komma igång måste du importera de nödvändiga paketen från Aspose.Cells for .NET-biblioteket. Lägg till följande med hjälp av uttalanden överst i din C#-fil:
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
// Skriv ut maximalt antal rader och kolumner som stöds av XLS-format.
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
I det här steget:
1. Skriv ut ett meddelande för att indikera att vi arbetar med XLS-formatet.
2.  Skapa en ny`Workbook` instans med hjälp av`FileFormatType.Excel97To2003` enum, som representerar XLS-formatet.
3.  Hämta det maximala antalet rader och kolumner som stöds av XLS-formatet med hjälp av`Workbook.Settings.MaxRow` och`Workbook.Settings.MaxColumn`respektive fastigheter. Vi lägger till 1 till dessa värden för att få de faktiska maximala rad- och kolumnnumren (eftersom de är nollbaserade).
4. Skriv ut det maximala antalet rader och kolumner till konsolen.
## Steg 2: Hitta det maximala antalet rader och kolumner som stöds av XLSX-formatet
Låt oss sedan utforska det maximala antalet rader och kolumner som stöds av XLSX-formatet (Excel 2007 och senare).
```csharp
// Skriv ut meddelande om XLSX-format.
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// Skapa arbetsbok i XLSX-format.
wb = new Workbook(FileFormatType.Xlsx);
// Skriv ut maximalt antal rader och kolumner som stöds av XLSX-format.
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
I det här steget:
1. Skriv ut ett meddelande för att indikera att vi arbetar med XLSX-formatet.
2.  Skapa en ny`Workbook` instans med hjälp av`FileFormatType.Xlsx` enum, som representerar XLSX-formatet.
3.  Hämta det maximala antalet rader och kolumner som stöds av XLSX-formatet med hjälp av`Workbook.Settings.MaxRow` och`Workbook.Settings.MaxColumn`respektive fastigheter. Vi lägger till 1 till dessa värden för att få de faktiska maximala rad- och kolumnnumren (eftersom de är nollbaserade).
4. Skriv ut det maximala antalet rader och kolumner till konsolen.
## Steg 3: Visa ett framgångsmeddelande
Slutligen, låt oss visa ett framgångsmeddelande för att indikera att "FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats"-exemplet har körts framgångsrikt.
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
Detta steg skriver helt enkelt ut ett framgångsmeddelande till konsolen.
## Slutsats
den här handledningen har du lärt dig hur du använder Aspose.Cells för .NET-biblioteket för att hitta det maximala antalet rader och kolumner som stöds av filformaten XLS och XLSX. Genom att förstå begränsningarna för dessa format kan du bättre planera och hantera dina Excel-baserade projekt, och se till att dina data passar inom de intervall som stöds.
## FAQ's
### Vad är det maximala antalet rader som stöds av XLS-formatet?
Det maximala antalet rader som stöds av XLS-formatet (Excel 97-2003) är 65 536.
### Vad är det maximala antalet kolumner som stöds av XLS-formatet?
Det maximala antalet kolumner som stöds av XLS-formatet (Excel 97-2003) är 256.
### Vad är det maximala antalet rader som stöds av XLSX-formatet?
Det maximala antalet rader som stöds av XLSX-formatet (Excel 2007 och senare) är 1 048 576.
### Vad är det maximala antalet kolumner som stöds av XLSX-formatet?
Det maximala antalet kolumner som stöds av XLSX-formatet (Excel 2007 och senare) är 16 384.
### Kan jag använda Aspose.Cells for .NET-biblioteket för att arbeta med andra Excel-filformat?
 Ja, Aspose.Cells for .NET-biblioteket stöder ett brett utbud av Excel-filformat, inklusive XLS, XLSX, ODS och mer. Du kan utforska[dokumentation](https://reference.aspose.com/cells/net/) för att lära dig om tillgängliga funktioner och funktioner.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
