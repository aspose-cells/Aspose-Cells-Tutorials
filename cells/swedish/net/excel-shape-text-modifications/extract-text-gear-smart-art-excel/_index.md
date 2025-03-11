---
title: Extrahera text från Gear Type Smart Art i Excel
linktitle: Extrahera text från Gear Type Smart Art i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du extraherar text från SmartArt av kugghjulstyp i Excel med Aspose.Cells för .NET. Steg-för-steg-guide och kodexempel ingår.
weight: 10
url: /sv/net/excel-shape-text-modifications/extract-text-gear-smart-art-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera text från Gear Type Smart Art i Excel

## Introduktion
När du arbetar med Excel kan du stöta på SmartArt-grafik som hjälper till att förmedla dina budskap på ett visuellt tilltalande sätt. Bland dessa grafik är SmartArt av kugghjulstyp en favorit för sina hierarkiska och riktade flöden, som ofta används i projektledning eller systemmodellering. Men vad händer om du behöver extrahera text från dessa former programmatiskt? Det är här Aspose.Cells för .NET kommer väl till pass! I det här blogginlägget kommer vi att leda dig genom en steg-för-steg-guide om hur du extraherar text från SmartArt-former av kugghjulstyp i Excel med Aspose.Cells för .NET.
## Förutsättningar
Innan vi dyker in finns det några väsentliga förutsättningar du måste ha på plats. Oroa dig inte; det är enkelt och jag guidar dig igenom det.
### .NET-miljö
Se till att du har en .NET-utvecklingsmiljö inställd på din dator. Detta kan vara Visual Studio eller valfri IDE som stöder .NET-utveckling.
### Aspose.Cells för .NET
 Därefter måste du installera Aspose.Cells-biblioteket. Detta är kraftpaketet som gör att du kan manipulera Excel-filer sömlöst. Du kan ladda ner den från[Sidan Aspose Releases](https://releases.aspose.com/cells/net/) . Om du vill utforska det först, dra nytta av[gratis provperiod](https://releases.aspose.com/).
### Grundläggande kunskaper i C#
En grundläggande förståelse för C#-programmering är precis vad du behöver följa tillsammans med denna handledning. Om du är ny på det, oroa dig inte – jag utformar stegen så att de är så nybörjarvänliga som möjligt.
### Exempel på Excel-fil
För den här handledningen behöver du också ett exempel på Excel-fil som innehåller SmartArt-former av kugghjulstyp. Du kan enkelt skapa en eller hitta en mall online. Se bara till att SmartArt innehåller minst en form av kugghjulstyp.
## Importera paket
För att börja koda måste du importera de nödvändiga paketen. Så här gör du:
### Skapa ett nytt projekt
1. Öppna din .NET IDE.
2. Skapa ett nytt projekt. Välj till exempel "Console Application" under .NET-alternativen.
3. Ge ditt projekt ett namn och sätt den önskade ramen. 
### Lägg till referenser
För att använda Aspose.Cells måste du lägga till biblioteksreferenserna till ditt projekt:
1. Högerklicka på ditt projektnamn i Solution Explorer.
2. Välj "Hantera NuGet-paket".
3. Sök efter "Aspose.Cells" och installera den.
När det är installerat är du redo för kodning!
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Låt oss nu dela upp koden du ska använda för att extrahera texten. Vi kommer att göra detta steg för steg.
## Steg 1: Konfigurera källkatalogen
Börja med att definiera katalogen där din Excel-fil finns:
```csharp
// Källkatalog
string sourceDir = "Your Document Directory";
```
 Se till att byta ut`"Your Document Directory"` med den faktiska sökvägen till din Excel-fil.
## Steg 2: Ladda Excel-arbetsboken
Därefter kommer vi att ladda Excel-arbetsboken. Så här kan vi komma åt dess innehåll:
```csharp
// Ladda exempel på Excel-fil som innehåller kugghjulstyp smart art shape.
Workbook wb = new Workbook(sourceDir + "sampleExtractTextFromGearTypeSmartArtShape.xlsx");
```
Det här stycket kommer att ladda ditt exempel på Excel-arbetsbok.
## Steg 3: Öppna det första arbetsbladet
Nu när vi har laddat arbetsboken, låt oss komma åt det första kalkylbladet där vår SmartArt finns:
```csharp
// Öppna första kalkylbladet.
Worksheet ws = wb.Worksheets[0];
```
Detta hämtar det första kalkylbladet för vidare manipulation.
## Steg 4: Få tillgång till den första formen
Därefter måste vi komma åt den första formen i vårt kalkylblad. Genom att göra detta kan vi navigera genom vår SmartArt-grafik:
```csharp
// Få tillgång till första formen.
Aspose.Cells.Drawing.Shape sh = ws.Shapes[0];
```
Här fokuserar vi på den första formen, som vi antar är den SmartArt vi behöver.
## Steg 5: Skaffa gruppformen
När vi väl har vår form är det dags att få resultatet av vår SmartArt-representation:
```csharp
// Få resultatet av redskapstyp smart konstform i form av gruppform.
Aspose.Cells.Drawing.GroupShape gs = sh.GetResultOfSmartArt();
```
Detta hämtar vår SmartArt av kugghjulstyp som en grupperad form.
## Steg 6: Extrahera individuella former
Låt oss nu extrahera de individuella formerna som utgör vår SmartArt:
```csharp
// Få listan över individuella former som består av gruppform.
Aspose.Cells.Drawing.Shape[] shps = gs.GetGroupedShapes();
```
Denna array kommer att hålla alla individuella former som vi behöver gå igenom.
## Steg 7: Extrahera och skriv ut text
Slutligen kan vi gå igenom vår formarray och extrahera texten från valfri form av kugghjulstyp:
```csharp
// Extrahera texten från kugghjulstyper och skriv ut dem på konsolen.
for (int i = 0; i < shps.Length; i++)
{
    Aspose.Cells.Drawing.Shape s = shps[i];
    if (s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear9 || s.Type == Aspose.Cells.Drawing.AutoShapeType.Gear6)
    {
        Console.WriteLine("Gear Type Shape Text: " + s.Text);
    }
}
```
den här slingan kontrollerar vi typen av form och skriver ut texten om det är en form av kugghjulstyp.
## Steg 8: Exekveringsbekräftelse
Slutligen kanske du vill lägga till ett bekräftelsemeddelande när processen har slutförts framgångsrikt:
```csharp
Console.WriteLine("ExtractTextFromGearTypeSmartArtShape executed successfully.");
```
Med detta är din extraktion klar, och du bör se din textutmatning i konsolen!
## Slutsats
 Grattis! Du har precis lärt dig hur du extraherar text från SmartArt-former av kugghjulstyp i Excel med Aspose.Cells för .NET. Denna praktiska teknik öppnar dörrar för att automatisera rapporter eller dokumentation som bygger på visuell datarepresentation. Oavsett om du är en erfaren utvecklare eller bara har börjat, kan kontrollera och extrahera information från SmartArt effektivisera ditt arbetsflöde och göra dig mer effektiv. Glöm inte att utforska detaljerna[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för ytterligare kapacitet.
## FAQ's
### Vad är Aspose.Cells?
Aspose.Cells är ett .NET-bibliotek som låter utvecklare skapa och manipulera Excel-filer enkelt.
### Kan jag använda Aspose.Cells med andra språk?
Ja! Aspose.Cells är tillgängligt i flera programmeringsspråk, inklusive Java och Python.
### Behöver jag köpa Aspose.Cells för .NET?
 Aspose.Cells erbjuder en gratis provperiod, men för utökad användning krävs ett köp. Du kan hitta köpalternativ[här](https://purchase.aspose.com/buy).
### Finns det support tillgängligt för Aspose.Cells-användare?
 Absolut! Du kan hitta samhällsstöd på[Aspose.Cells forum](https://forum.aspose.com/c/cells/9).
### Kan jag extrahera andra SmartArt-typer med den här metoden?
Ja, med små modifieringar kan du extrahera text från olika SmartArt-former genom att ändra villkoren i din kod.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
