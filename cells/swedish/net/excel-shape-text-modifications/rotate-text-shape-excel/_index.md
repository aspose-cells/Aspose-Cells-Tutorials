---
title: Rotera text med Shape i Excel
linktitle: Rotera text med Shape i Excel
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du roterar text med former i Excel med Aspose.Cells för .NET. Följ denna steg-för-steg-guide för perfekt Excel-presentation.
weight: 12
url: /sv/net/excel-shape-text-modifications/rotate-text-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Rotera text med Shape i Excel

## Introduktion
I Excel-världen är visuell representation lika viktig som själva data. Oavsett om du skapar en rapport eller designar en dynamisk instrumentpanel, kan hur informationen läggs ut dramatiskt påverka dess läsbarhet och övergripande utseende. Så, har du någonsin velat rotera text för att anpassa den stilfullt med former? Du har tur! I den här handledningen kommer vi att dyka ner i hur du roterar text med former med Aspose.Cells för .NET, vilket säkerställer att dina kalkylblad inte bara informerar utan också imponerar.
## Förutsättningar
Innan vi börjar, låt oss se till att du har allt du behöver:
1. Visual Studio: Se till att du har Visual Studio installerat på din maskin, eftersom det är där vi kommer att skriva vår kod.
2.  Aspose.Cells för .NET: Du behöver Aspose.Cells-biblioteket. Du kan[ladda ner den senaste versionen här](https://releases.aspose.com/cells/net/) eller prova det gratis med en[gratis provperiod](https://releases.aspose.com/).
3. Grundläggande kunskaper om C#: Bekantskap med C#- och .NET-miljöer kommer att vara till hjälp, även om vi guidar dig varje steg på vägen.
4.  Excel-fil: Ett exempel på Excel-fil, låt oss kalla det`sampleRotateTextWithShapeInsideWorksheet.xlsx`, behövs för att testa vår kod. Du bör placera den här filen i en katalog som du lätt kan komma åt.
Har du allt klart? Fantastisk! Låt oss hoppa in i den roliga delen.
## Importera paket
För att komma igång måste vi importera de nödvändiga paketen till vårt projekt. Så här gör du det:
### Skapa ett nytt projekt
1. Öppna Visual Studio.
2. Välj "Skapa ett nytt projekt."
3. Välj "Console App" och välj C# som ditt föredragna programmeringsspråk.
### Installera Aspose.Cells
Låt oss nu lägga till Aspose.Cells till ditt projekt. Du kan göra detta med NuGet Package Manager:
1. Öppna "Verktyg" i toppmenyn.
2. Välj "NuGet Package Manager" och sedan "Manage NuGet Packages for Solution."
3. Sök efter "Aspose.Cells."
4. Klicka på "Installera" för att lägga till det i ditt projekt.
### Lägg till med hjälp av direktiv
Överst i din C#-huvudfil måste du lägga till följande direktiv:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Nu är vi redo att börja koda!
Låt oss bryta ner processen i lättsmälta steg. Så här roterar du text med former i en Excel-fil:
## Steg 1: Ställ in dina katalogsökvägar
Först måste du ställa in dina käll- och utdatakataloger där dina Excel-filer kommer att lagras. Så här gör du:
```csharp
//Källkatalog
string sourceDir = "Your Document Directory"; // Ställ in din dokumentkatalog
//Utdatakatalog
string outputDir = "Your Document Directory"; // Ställ in din utdatakatalog
```
 Ersätta`"Your Document Directory"` med den faktiska vägen där din`sampleRotateTextWithShapeInsideWorksheet.xlsx` filen finns.
## Steg 2: Ladda Excel-exempelfilen
Låt oss nu ladda exemplet på Excel-filen. Detta är avgörande, eftersom vi vill manipulera befintliga data.
```csharp
//Ladda exempel på Excel-fil.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Steg 3: Öppna arbetsbladet
När filen har laddats måste vi komma åt det specifika kalkylblad vi vill ändra. I vårt fall är det det första arbetsbladet.
```csharp
//Öppna första kalkylbladet.
Worksheet ws = wb.Worksheets[0];
```
## Steg 4: Ändra en cell
Därefter kommer vi att ändra en specifik cell för att visa ett meddelande. I vårt exempel använder vi cell B4.
```csharp
//Gå till cell B4 och lägg till ett meddelande i den.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Det här steget handlar om kommunikation – att säkerställa att den som öppnar det här bladet förstår vad vi justerar.
## Steg 5: Få tillgång till den första formen
För att rotera text behöver vi en form att arbeta med. Här kommer vi åt den första formen i kalkylbladet.
```csharp
//Få tillgång till första formen.
Shape sh = ws.Shapes[0];
```
## Steg 6: Justera formtextjustering
Det är här magin händer. Vi kommer att justera formens textjusteringsegenskaper.
```csharp
//Få åtkomst till formtextjustering.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Rotera inte text med form genom att ställa in RotateTextWithShape som falskt.
shapeTextAlignment.RotateTextWithShape = false;
```
 Genom att ställa in`RotateTextWithShape` till false ser vi till att texten förblir upprätt och inte roterar med formen, vilket håller allt snyggt och organiserat.
## Steg 7: Spara Excel-filen
Slutligen, låt oss spara våra ändringar i en ny Excel-fil. Detta säkerställer att vi inte förlorar våra redigeringar och att vi har en snygg utdata.
```csharp
//Spara den utgående Excel-filen.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Och det är det! Din utdatafil är nu sparad, inklusive texten i cell B4 och justeringarna av formen.
## Steg 8: Kör koden
 I din`Main` metod, slå in alla ovanstående kodavsnitt och kör ditt projekt. Se ändringarna återspeglas i din utdatafil!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Slutsats
Att rotera text med former i Excel med Aspose.Cells för .NET kan tyckas vara en komplicerad process till en början, men det är ganska enkelt när du bryter ner det. Genom att följa dessa enkla steg kan du anpassa dina kalkylblad så att de ser mer professionella och visuellt tilltalande ut. Nu, oavsett om du gör det här för en kund eller dina personliga projekt, kommer alla att bli lyhörda för kvaliteten på ditt arbete!
## FAQ's
### Kan jag använda Aspose.Cells gratis?
 Ja! Du kan använda[gratis provperiod](https://releases.aspose.com/) att prova biblioteket.
### Vilka versioner av Excel stöder Aspose.Cells?
Aspose.Cells stöder en mängd olika Excel-format, inklusive XLS, XLSX, CSV och mer.
### Är det möjligt att rotera text med former i äldre Excel-versioner?
Ja, funktionen kan tillämpas på äldre format som stöds av Aspose.Cells.
### Var kan jag hitta mer dokumentation om Aspose.Cells?
 Du kan utforska det omfattande[dokumentation](https://reference.aspose.com/cells/net/) för fler insikter.
### Hur får jag support för Aspose.Cells?
 Du kan be om stöd genom att besöka[Aspose forum](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
