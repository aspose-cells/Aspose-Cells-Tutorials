---
title: Ställa in PDF Creation Time i .NET
linktitle: Ställa in PDF Creation Time i .NET
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du ställer in PDF-genereringstiden i .NET med Aspose.Cells. Följ vår steg-för-steg-guide för sömlös konvertering av Excel till PDF.
weight: 11
url: /sv/net/xps-and-pdf-operations/setting-pdf-creation-time/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Ställa in PDF Creation Time i .NET

## Introduktion
dagens digitala tidsålder är förmågan att konvertera dokument till olika format avgörande för många applikationer. Ett vanligt behov är att konvertera Excel-kalkylblad till PDF-filer. Detta bevarar inte bara formateringen, utan det gör också delning och utskrift mycket enklare. Om du är en utvecklare som arbetar med .NET är Aspose.Cells ett fantastiskt bibliotek som förenklar denna process. I den här handledningen kommer vi att dyka in i hur du ställer in PDF-genereringstiden när du konverterar en Excel-fil till PDF med Aspose.Cells för .NET.
## Förutsättningar
Innan vi går in i kodens snålhet, låt oss se till att du har allt du behöver för att komma igång.
### Vad du behöver
1. Visual Studio: Se till att du har Visual Studio installerat på din dator. Detta kommer att vara din utvecklingsmiljö.
2.  Aspose.Cells för .NET: Ladda ner Aspose.Cells-biblioteket från[webbplats](https://releases.aspose.com/cells/net/). Du kan också börja med en gratis provperiod för att testa dess funktioner.
3. Grundläggande kunskaper i C#: Bekantskap med C#-programmering hjälper dig att förstå kodavsnitten bättre.
4.  Excel-fil: Ha en Excel-fil redo för konvertering. För det här exemplet använder vi en fil med namnet`Book1.xlsx`.
Nu när du har ordning på förutsättningarna, låt oss gå in på den roliga delen – importera de nödvändiga paketen och skriva koden!
## Importera paket
Till att börja med måste du importera de nödvändiga namnområdena i din C#-fil. Detta är avgörande eftersom det ger dig tillgång till klasserna och metoderna som tillhandahålls av Aspose.Cells-biblioteket.
### Öppna ditt C#-projekt
Öppna Visual Studio och antingen skapa ett nytt projekt eller öppna ett befintligt där du vill implementera PDF-konverteringsfunktionen.
### Lägg till Aspose.Cells Reference
Du kan lägga till Aspose.Cells-biblioteket till ditt projekt genom att högerklicka på ditt projekt i Solution Explorer, välja "Hantera NuGet-paket" och söka efter "Aspose.Cells." Installera paketet.
### Importera namnområden
Inkludera följande namnrymder högst upp i din C#-fil:
```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Charts;
```
Dessa namnrymder ger dig tillgång till Workbook-klassen och andra viktiga funktioner.

Nu när vi har importerat våra paket, låt oss bryta ner processen för att konvertera en Excel-fil till en PDF medan vi ställer in skapelsetiden.
## Steg 1: Definiera dokumentkatalogen
Först måste du ange katalogen där dina dokument lagras. Det är här din Excel-fil finns och där den utgående PDF-filen kommer att sparas.
```csharp
string dataDir = "Your Document Directory"; // Ange din dokumentkatalog
```
 Ersätta`"Your Document Directory"` med den faktiska vägen där din`Book1.xlsx` filen finns. Den här sökvägen hjälper applikationen att hitta filen för bearbetning.
## Steg 2: Ladda Excel-filen
 Därefter ska du ladda Excel-filen i en`Workbook` objekt. Det är här Aspose.Cells lyser, eftersom det låter dig arbeta med Excel-filer utan ansträngning.
```csharp
string inputPath = dataDir + "Book1.xlsx"; // Sökväg till din Excel-fil
Workbook workbook = new Workbook(inputPath); // Ladda Excel-filen
```
 De`Workbook` klass används för att ladda och manipulera Excel-filer. Genom att skicka indatasökvägen talar du om för programmet vilken fil den ska arbeta med.
## Steg 3: Skapa PdfSaveOptions
 Nu är det dags att skapa en instans av`PdfSaveOptions`. Den här klassen låter dig ange olika alternativ för att spara din arbetsbok som en PDF, inklusive skapelsetiden.
```csharp
PdfSaveOptions options = new PdfSaveOptions(); // Skapa PdfSaveOptions-instans
options.CreatedTime = DateTime.Now; // Ställ in skapelsetiden till nu
```
 Genom att ställa in`options.CreatedTime` till`DateTime.Now`, säkerställer du att PDF-filen återspeglar det aktuella datumet och tiden när den skapades.
## Steg 4: Spara arbetsboken som PDF
Slutligen kommer du att spara arbetsboken som en PDF-fil med de alternativ du just definierade.
```csharp
workbook.Save(dataDir + "output.pdf", options); //Spara som PDF
```
 Denna kodrad tar arbetsboken och sparar den i PDF-format på den angivna platsen. De`options` parametern skickas för att inkludera skapelsetiden i PDF-metadata.

## Slutsats
Och där har du det! Du har framgångsrikt konverterat en Excel-fil till en PDF med Aspose.Cells för .NET, komplett med en tidsstämpel för skapande. Den här funktionen kan vara otroligt användbar när du behöver hålla reda på dokumentversioner eller när du vill förse mottagarna med information om när dokumentet skapades.
 Om du vill utforska fler funktioner i Aspose.Cells, tveka inte att kolla in[dokumentation](https://reference.aspose.com/cells/net/).
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett kraftfullt bibliotek för .NET som låter utvecklare skapa, manipulera och konvertera Excel-filer.
### Kan jag använda Aspose.Cells gratis?
 Ja, du kan börja med en gratis provperiod tillgänglig på[Aspose hemsida](https://releases.aspose.com/).
### Hur ställer jag in andra PDF-egenskaper?
 Du kan ställa in olika PDF-egenskaper med hjälp av`PdfSaveOptions` klass, som sidstorlek, komprimering och mer.
### Är det möjligt att konvertera flera Excel-filer samtidigt?
Ja, du kan gå igenom en lista med filer och tillämpa samma konverteringsprocess på var och en.
### Var kan jag få support för Aspose.Cells?
 Du kan få stöd från Aspose-communityt på deras[supportforum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
