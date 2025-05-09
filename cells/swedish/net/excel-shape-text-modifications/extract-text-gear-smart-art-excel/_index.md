---
"description": "Lär dig hur du extraherar text från kugghjulsliknande SmartArt-diagram i Excel med Aspose.Cells för .NET. Steg-för-steg-guide och kodexempel ingår."
"linktitle": "Extrahera text från kugghjulstyp Smart Art i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Extrahera text från kugghjulstyp Smart Art i Excel"
"url": "/sv/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från kugghjulstyp Smart Art i Excel

## Introduktion
När du arbetar med Excel kan du stöta på SmartArt-grafik som hjälper dig att förmedla dina budskap på ett visuellt tilltalande sätt. Bland dessa grafik är kugghjulsliknande SmartArt en favorit för sina hierarkiska och riktningsbaserade flöden, som ofta används i projektledning eller systemmodellering. Men tänk om du behöver extrahera text från dessa former programmatiskt? Det är här Aspose.Cells för .NET kommer väl till pass! I det här blogginlägget kommer vi att guida dig genom en steg-för-steg-guide om hur du extraherar text från kugghjulsliknande SmartArt-former i Excel med hjälp av Aspose.Cells för .NET.
## Förkunskapskrav
Innan vi börjar finns det några viktiga förutsättningar du behöver ha på plats. Oroa dig inte, det är enkelt, och jag ska guida dig genom det.
### .NET-miljö
Se till att du har en .NET-utvecklingsmiljö konfigurerad på din dator. Det kan vara Visual Studio eller någon annan IDE som stöder .NET-utveckling.
### Aspose.Cells för .NET
Därefter behöver du installera Aspose.Cells-biblioteket. Det här är kraftpaketet som gör att du kan hantera Excel-filer sömlöst. Du kan ladda ner det från [Aspose-utgåvorsida](https://releases.aspose.com/cells/net/)Om du vill utforska det först, dra nytta av [gratis provperiod](https://releases.aspose.com/).
### Grundläggande kunskaper i C#
Grundläggande förståelse för C#-programmering är precis vad du behöver för att följa den här handledningen. Om du är nybörjare, oroa dig inte – jag kommer att utforma stegen så att de är så nybörjarvänliga som möjligt.
### Exempel på Excel-fil
För den här handledningen behöver du också en exempelfil i Excel som innehåller SmartArt-former av kugghjulstyp. Du kan enkelt skapa en eller hitta en mall online. Se bara till att SmartArt-filen innehåller minst en kugghjulsform.
## Importera paket
För att börja koda måste du importera de nödvändiga paketen. Så här gör du:
### Skapa ett nytt projekt
1. Öppna din .NET IDE.
2. Skapa ett nytt projekt. Välj till exempel "Konsolprogram" under .NET-alternativen.
3. Ge ditt projekt ett namn och ange önskat ramverk. 
### Lägg till referenser
För att använda Aspose.Cells måste du lägga till biblioteksreferenserna i ditt projekt:
1. Högerklicka på ditt projektnamn i lösningsutforskaren.
2. Välj "Hantera NuGet-paket".
3. Sök efter "Aspose.Cells" och installera det.
När det är installerat är du redo att börja koda!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Nu ska vi gå igenom koden du kommer att använda för att extrahera texten. Vi gör detta steg för steg.
## Steg 1: Konfigurera källkatalogen
Börja med att definiera katalogen där din Excel-fil finns:
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
```
Se till att byta ut `"Your Document Directory"` med den faktiska sökvägen till din Excel-fil.
## Steg 2: Läs in Excel-arbetsboken
Härnäst ska vi ladda Excel-arbetsboken. Så här kan vi komma åt dess innehåll:
```csharp
// Ladda exempelfil i Excel som innehåller en smart konstform av typen kugghjul.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Den här delen laddar din exempelarbetsbok i Excel.
## Steg 3: Öppna det första arbetsbladet
Nu när vi har laddat arbetsboken, låt oss öppna det första kalkylbladet där vår SmartArt finns:
```csharp
// Åtkomst till första arbetsbladet.
Worksheet ws = wb.Worksheets[0];
```
Detta hämtar det första kalkylbladet för vidare hantering.
## Steg 4: Komma åt den första formen
Nästa steg är att komma åt den första formen i vårt kalkylblad. Genom att göra detta kan vi navigera genom våra SmartArt-grafiker:
```csharp
// Åtkomst till första formen.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Här fokuserar vi på den första formen, som vi antar är den SmartArt vi behöver.
## Steg 5: Hämta gruppformen
När vi har vår form är det dags att få resultatet av vår SmartArt-representation:
```csharp
// Få resultatet av kugghjulstypen smart konstform i form av en gruppform.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Detta hämtar vår SmartArt av kugghjulstyp som en grupperad form.
## Steg 6: Extrahera enskilda former
Nu ska vi extrahera de enskilda formerna som utgör vår SmartArt:
```csharp
// Hämta listan över individuella former som består av gruppformer.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Den här arrayen kommer att innehålla alla individuella former som vi behöver loopa igenom.
## Steg 7: Extrahera och skriv ut text
Slutligen kan vi loopa igenom vår shapes-array och extrahera texten från valfri kugghjulsform:
```csharp
// Extrahera texten för kugghjulsformer och skriv ut dem på konsolen.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
I den här loopen kontrollerar vi formtypen och skriver ut texten om det är en kugghjulsform.
## Steg 8: Bekräftelse av körning
Slutligen kan du lägga till ett bekräftelsemeddelande när processen är klar:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Med detta är din extrahering klar, och du bör se din textutdata i konsolen!
## Slutsats
Grattis! Du har precis lärt dig hur man extraherar text från kugghjulsliknande SmartArt-former i Excel med hjälp av Aspose.Cells för .NET. Den här praktiska tekniken öppnar dörrar för att automatisera rapporter eller dokumentation som bygger på visuell datarepresentation. Oavsett om du är en erfaren utvecklare eller precis har börjat, kan kontroll och extrahering av information från SmartArt effektivisera ditt arbetsflöde och göra dig mer effektiv. Glöm inte att utforska de detaljerade [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/) för ytterligare förmågor.
## Vanliga frågor
### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som låter utvecklare enkelt skapa och manipulera Excel-filer.
### Kan jag använda Aspose.Cells med andra språk?
Ja! Aspose.Cells finns tillgängligt i flera programmeringsspråk, inklusive Java och Python.
### Behöver jag köpa Aspose.Cells för .NET?
Aspose.Cells erbjuder en gratis provperiod, men för längre tids användning krävs ett köp. Du hittar köpalternativ [här](https://purchase.aspose.com/buy).
### Finns det support tillgänglig för Aspose.Cells-användare?
Absolut! Du kan hitta stöd från samhället på [Aspose.Cells-forumet](https://forum.aspose.com/c/cells/9).
### Kan jag extrahera andra SmartArt-typer med den här metoden?
Ja, med smärre ändringar kan du extrahera text från olika SmartArt-former genom att ändra villkoren i din kod.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}