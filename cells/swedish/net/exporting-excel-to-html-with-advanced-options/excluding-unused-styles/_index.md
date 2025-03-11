---
title: Exkludera oanvända formatmallar vid export av Excel till HTML
linktitle: Exkludera oanvända formatmallar vid export av Excel till HTML
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du utesluter oanvända stilar när du exporterar Excel till HTML med Aspose.Cells för .NET i den här detaljerade steg-för-steg-guiden.
weight: 10
url: /sv/net/exporting-excel-to-html-with-advanced-options/excluding-unused-styles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exkludera oanvända formatmallar vid export av Excel till HTML

## Introduktion
Excel-filer finns överallt i affärsvärlden, ofta fyllda med intrikata stilar och format. Men har du någonsin ställts inför en situation där din Excel-fil, när den exporteras till HTML, bär med sig alla dessa oanvända stilar? Det kan få dina webbsidor att se röriga och oprofessionella ut. Var inte rädd! I den här guiden går vi igenom processen att exkludera oanvända stilar medan du exporterar en Excel-fil till HTML med Aspose.Cells för .NET. I slutet av den här handledningen kommer du att navigera i den här processen som ett proffs.
## Förutsättningar
För att effektivt följa med i den här handledningen behöver du några saker konfigurerade i förväg:
### 1. Visual Studio
Se till att du har Visual Studio installerat på din dator. Det är här du kommer att skriva och köra din .NET-kod.
### 2. Aspose.Cells för .NET
Ladda ner Aspose.Cells-biblioteket. Det är ett kraftfullt verktyg för att hantera Excel-filer programmatiskt. Du kan få tag i det[här](https://releases.aspose.com/cells/net/).
### 3. Grundläggande kunskaper i C#
Bekantskap med programmeringsspråket C# hjälper dig att lättare förstå begreppen.
### 4. Microsoft Excel
Även om vi inte nödvändigtvis behöver Microsoft Excel för kodning, kan det hjälpa dig att ha den till hands för testning och validering.
Med dessa objekt överstrukna från din lista är du redo att dyka in i Aspose.Cells värld!
## Importera paket
Innan vi skriver vår kod, låt oss ta en stund att importera de nödvändiga paketen. Se till att du inkluderar Aspose.Cells-namnrymden i ditt Visual Studio-projekt överst i din C#-fil:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Den här raden ger dig tillgång till alla funktioner som tillhandahålls av Aspose.Cells-biblioteket, så att du enkelt kan skapa och manipulera Excel-filer.
Nu när vi har allt klart kan vi hoppa direkt in i handledningen. Nedan finns en steg-för-steg-guide som bryter ner koden för att utesluta oanvända stilar när du exporterar Excel-filer till HTML.
## Steg 1: Ställ in utdatakatalogen
För att komma igång måste vi definiera var vi vill att vår exporterade HTML-fil ska sparas. Det här steget är enkelt, och så här gör du:
```csharp
// Utdatakatalog
string outputDir = "Your Document Directory";
```
 Byt ut i raden ovan`"Your Document Directory"` med den faktiska sökvägen där du vill spara HTML-filen. Det kan till exempel vara något liknande`C:\\Users\\YourName\\Documents\\`.
## Steg 2: Skapa en arbetsboksinstans
Därefter skapar vi en ny arbetsbok. Se arbetsboken som en tom duk där vi kan måla våra data och stilar:
```csharp
// Skapa arbetsbok
Workbook wb = new Workbook();
```
 Den här raden initierar en ny instans av`Workbook` klass. Det är din utgångspunkt för allt som har med Excel att göra.
## Steg 3: Skapa en oanvänd namngiven stil
Även om vi försöker utesluta oanvända stilar, låt oss skapa en för att illustrera processen bättre:
```csharp
// Skapa en oanvänd namngiven stil
wb.CreateStyle().Name = "UnusedStyle_XXXXXXXXXXXXXX";
```
I det här steget skapar vi en ny stil men tillämpar den inte på några celler. Därför förblir den oanvänd – perfekt för våra behov.
## Steg 4: Öppna det första arbetsbladet
Låt oss nu komma åt det första kalkylbladet i vår arbetsbok. Kalkylbladet är där datamagin händer:
```csharp
// Öppna första kalkylbladet
Worksheet ws = wb.Worksheets[0];
```
Precis som det, nollar du in på det första arket i din arbetsbok, redo att lägga till lite innehåll!
## Steg 5: Lägg till exempeldata till en cell
Låt oss lägga in lite text i en cell – det här steget känns lite som att fylla i detaljerna på din duk:
```csharp
// Sätt ett värde i cell C7
ws.Cells["C7"].PutValue("This is sample text.");
```
Här placerar vi texten "Detta är exempeltext." i cell C7 i det aktiva kalkylbladet. Ändra gärna texten till det som passar ditt projekt!
## Steg 6: Ange HTML-sparalternativ
Därefter kommer vi att definiera hur vi vill spara vår arbetsbok. Det här steget är avgörande om du vill kontrollera om oanvända stilar ska inkluderas i exporten:
```csharp
// Ange html-sparalternativ, vi vill utesluta oanvända stilar
HtmlSaveOptions opts = new HtmlSaveOptions();
// Kommentera den här raden för att inkludera oanvända stilar
opts.ExcludeUnusedStyles = true;
```
 I koden ovan skapar vi en ny instans av`HtmlSaveOptions` och ställ in`ExcludeUnusedStyles` till`true`Detta säger till Aspose.Cells att ta bort alla stilar som inte används i den slutliga HTML-utdata.
## Steg 7: Spara arbetsboken i HTML-format
Äntligen är det dags att spara din arbetsbok som en HTML-fil. Det här är den givande delen där allt ditt tidigare arbete lönar sig:
```csharp
// Spara arbetsboken i html-format
wb.Save(outputDir + "outputExcludeUnusedStylesInExcelToHTML.html", opts);
```
Här kombinerar du din angivna utdatakatalog med ditt önskade filnamn för att spara arbetsboken. Voilà! Din HTML-fil är klar.
## Steg 8: Bekräfta framgång med konsolutgång
Sist men inte minst, låt oss ge lite feedback om att vår kod kördes framgångsrikt:
```csharp
Console.WriteLine("ExcludeUnusedStylesInExcelToHTML executed successfully.");
```
Den här raden skickar helt enkelt ett framgångsmeddelande i konsolen, så att du kan bekräfta att hela processen gick utan problem.
## Slutsats
Och det är en wrap! Du har framgångsrikt lärt dig hur du utesluter oanvända stilar när du exporterar en Excel-fil till HTML med Aspose.Cells för .NET. Den här tekniken hjälper dig inte bara att upprätthålla ett rent och professionellt utseende i ditt webbinnehåll utan optimerar också laddningstider genom att förhindra onödig uppblåsthet. 
Experimentera gärna med fler anpassade stilar eller andra funktioner som erbjuds av Aspose.Cells och ta dina Excel-filmanipulationer till nya höjder!
## FAQ's
### Vad används Aspose.Cells till?  
Aspose.Cells är ett .NET-bibliotek som låter utvecklare skapa, manipulera och konvertera Excel-filer programmatiskt.
### Behöver jag en licens för att använda Aspose.Cells?  
Även om det finns en gratis testversion, krävs en tillfällig eller fullständig licens för fortsatt användning av dess avancerade funktioner.
### Kan jag konvertera Excel till andra format än HTML?  
Ja! Aspose.Cells stöder konvertering av Excel-filer till olika format, inklusive PDF, CSV och mer.
### Hur kan jag få support för Aspose.Cells?  
 Du kan få hjälp från Aspose.Cells community och supportforum[här](https://forum.aspose.com/c/cells/9).
### Är det möjligt att inkludera oanvända stilar om jag behöver dem?  
 Absolut! Enkelt inställt`opts.ExcludeUnusedStyles` till`false` att inkludera alla stilar, oavsett om de används eller oanvända.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
