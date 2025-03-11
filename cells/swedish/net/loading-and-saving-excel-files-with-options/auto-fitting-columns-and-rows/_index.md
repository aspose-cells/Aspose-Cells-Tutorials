---
title: Anpassa kolumner och rader automatiskt när HTML läses in i arbetsboken
linktitle: Anpassa kolumner och rader automatiskt när HTML läses in i arbetsboken
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du automatiskt anpassar kolumner och rader medan du laddar HTML till Excel med Aspose.Cells för .NET. Steg-för-steg-guide ingår.
weight: 10
url: /sv/net/loading-and-saving-excel-files-with-options/auto-fitting-columns-and-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Anpassa kolumner och rader automatiskt när HTML läses in i arbetsboken

## Introduktion
Har du någonsin undrat hur man automatiskt justerar kolumn- och radstorlekarna när du laddar HTML-innehåll i en Excel-arbetsbok med Aspose.Cells för .NET? Tja, du är på rätt plats! I den här självstudien kommer vi att fördjupa oss i hur du kan ladda en HTML-tabell i en arbetsbok och se till att kolumnerna och raderna automatiskt anpassas för att matcha innehållet. Om du arbetar med dynamiska data som ändras ofta, kommer den här guiden att vara din favorit för att skapa välformaterade Excel-ark från HTML.
### Förutsättningar
Innan du hoppar in i koden finns det några saker du måste ha konfigurerat på ditt system. Oroa dig inte, det är enkelt och okomplicerat!
1. Visual Studio installerad: Du behöver Visual Studio eller någon annan .NET-utvecklingsmiljö.
2.  Aspose.Cells för .NET: Du kan[ladda ner den senaste versionen](https://releases.aspose.com/cells/net/) eller använd NuGet-pakethanteraren för att installera den.
3. .NET Framework: Se till att du har .NET Framework 4.0 eller senare installerat.
4. Grundläggande förståelse för C#: Att ha lite kunskap om C# kommer att göra denna handledning smidigare för dig.
5. HTML-tabelldata: Förbered lite HTML-innehåll (även en grundläggande tabell) som du vill ladda in i Excel.
## Importera paket
Det första är först – låt oss importera de nödvändiga namnområdena för att komma igång. Här är en enkel lista över vad du behöver importera:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
```
Dessa paket låter dig hantera arbetsboken, manipulera HTML-data och ladda den sömlöst i Excel.
Låt oss dela upp den här processen i hanterbara bitar så att du enkelt kan följa med. I slutet av detta har du ett fungerande exempel på hur du automatiskt anpassar kolumner och rader medan du laddar HTML i en arbetsbok med Aspose.Cells för .NET.
## Steg 1: Konfigurera dokumentkatalogen
För att enkelt spara och hämta filer anger vi sökvägen där dina dokument ska lagras. Du kan ersätta katalogsökvägen med din egen mappplats.
```csharp
string dataDir = "Your Document Directory";
```
Den här raden anger katalogen där dina Excel-filer ska sparas. Det är viktigt att organisera dina filer ordentligt när du arbetar med flera projekt. Föreställ dig detta som ditt projekts arkivskåp!
## Steg 2: Skapa HTML-data som en sträng
Därefter kommer vi att definiera lite grundläggande HTML-innehåll. För det här exemplets skull kommer vi att använda en enkel HTML-tabell. Du kan anpassa den efter ditt projekts behov.
```csharp
string sampleHtml = "<html><body><table><tr><td>This is sample text.</td><td>Some text.</td></tr><tr><td>This is another sample text.</td><td>Some text.</td></tr></table></body></html>";
```
Vi definierar en mycket grundläggande HTML-sträng här. Den innehåller en tabell med ett par rader och kolumner. Du kan lägga till fler rader eller kolumner enligt dina krav. Se det som att förbereda ingredienserna innan du lagar en måltid!
## Steg 3: Ladda HTML-sträng i MemoryStream
 Nu när vi har vårt HTML-innehåll klart är nästa steg att ladda det i minnet med hjälp av`MemoryStream`. Detta gör att vi kan manipulera HTML-innehållet i minnet utan att först spara det på disken.
```csharp
MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(sampleHtml));
```
 Genom att konvertera HTML-strängen till en byte-array och mata in den till en`MemoryStream`, kan vi arbeta med HTML-data i minnet. Föreställ dig det här steget som att förbereda rätten i en kastrull innan du sätter in den i ugnen!
## Steg 4: Ladda MemoryStream i en arbetsbok (utan automatisk anpassning)
 När vi väl har HTML-innehållet i minnet laddar vi in det i en Aspose`Workbook`Vid det här laget anpassar vi inte kolumnerna och raderna automatiskt ännu. Detta är vårt "före"-scenario, för att jämföra med den automatiskt anpassade versionen senare.
```csharp
Workbook wb = new Workbook(ms);
wb.Save(dataDir + "outputWithout_AutoFitColsAndRows.xlsx");
```
Arbetsboken är laddad med HTML-innehåll, men kolumnerna och raderna är ännu inte automatiskt anpassade till texten. Se det här som att baka en tårta men glömma att kontrollera temperaturen – det fungerar, men det kanske inte är perfekt!
## Steg 5: Ange HTML-laddningsalternativ med Auto-Fit aktiverat
 Nu, här är magin! Vi skapar en instans av`HtmlLoadOptions` och aktivera`AutoFitColsAndRows` egendom. Detta säkerställer att när HTML-innehållet laddas justeras kolumnerna och raderna för att passa innehållet i dem.
```csharp
HtmlLoadOptions opts = new HtmlLoadOptions();
opts.AutoFitColsAndRows = true;
```
Genom att ställa in det här alternativet säger vi till Aspose.Cells att automatiskt ändra storlek på rader och kolumner. Föreställ dig att det här är att ställa in ugnen på perfekt temperatur så att kakan höjer sig lagom!
## Steg 6: Ladda HTML i arbetsboken med automatisk anpassning aktiverad
 Nu laddar vi HTML-innehållet igen, men den här gången med`AutoFitColsAndRows`alternativet aktiverat. Detta kommer att justera kolumnbredderna och radhöjderna baserat på innehållet i dem.
```csharp
wb = new Workbook(ms, opts);
wb.Save(dataDir + "outputWith_AutoFitColsAndRows.xlsx");
```
Detta steg laddar HTML-innehållet i en ny arbetsbok och sparar det som en Excel-fil, men nu är kolumnerna och raderna automatiskt anpassade! Tänk på det här som den perfekt bakade kakan, där allt har precis rätt storlek.
## Slutsats
Genom att följa dessa enkla steg har du lärt dig hur du laddar HTML-innehåll i en arbetsbok med Aspose.Cells för .NET och automatiskt anpassa kolumner och rader. Detta säkerställer att dina Excel-ark alltid ser snygga ut, oavsett hur dynamiskt innehållet är. Det är en enkel men kraftfull funktion som kan spara massor av tid för att formatera och organisera dina Excel-data.
Nu när du är utrustad med denna kunskap kan du experimentera med mer komplext HTML-innehåll, lägga till stil och till och med skapa hela Excel-arbetsböcker från webbsidor!
## FAQ's
### Kan jag använda den här metoden för att ladda stora HTML-tabeller?
Ja, Aspose.Cells hanterar stora HTML-tabeller effektivt, men för optimal prestanda är det lämpligt att testa med dina datastorlekar.
### Kan jag använda specifika kolumnbredder och radhöjder manuellt efter automatisk anpassning?
Absolut! Du kan fortfarande anpassa enskilda kolumner och rader även efter att du har använt den automatiska anpassningsfunktionen.
### Hur kan jag utforma tabellen efter att ha läst in HTML?
Du kan tillämpa stilar med Aspose.Cells omfattande stilalternativ efter att ha laddat HTML.
### Är Aspose.Cells för .NET kompatibelt med äldre versioner av .NET Framework?
Ja, Aspose.Cells för .NET stöder .NET Framework 4.0 och senare.
### Kan jag ladda andra typer av innehåll förutom HTML till Excel med Aspose.Cells?
Ja, Aspose.Cells stöder inläsning av olika format som CSV, JSON och XML till Excel.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
