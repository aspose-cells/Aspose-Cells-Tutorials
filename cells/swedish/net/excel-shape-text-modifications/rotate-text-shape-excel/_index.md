---
"description": "Lär dig hur du roterar text med former i Excel med hjälp av Aspose.Cells för .NET. Följ den här steg-för-steg-guiden för perfekta Excel-presentationer."
"linktitle": "Rotera text med form i Excel"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Rotera text med form i Excel"
"url": "/sv/net/excel-shape-text-modifications/rotate-text-shape-excel/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Rotera text med form i Excel

## Introduktion
I Excels värld är visuell representation lika viktig som själva informationen. Oavsett om du skapar en rapport eller designar en dynamisk instrumentpanel kan hur informationen är utformad dramatiskt påverka dess läsbarhet och övergripande utseende. Så har du någonsin velat rotera text för att elegant justera den med former? Då har du tur! I den här handledningen går vi in på hur man roterar text med former med Aspose.Cells för .NET, vilket säkerställer att dina kalkylblad inte bara informerar utan också imponerar.
## Förkunskapskrav
Innan vi börjar, låt oss se till att du har allt du behöver:
1. Visual Studio: Se till att du har Visual Studio installerat på din dator, eftersom det är där vi kommer att skriva vår kod.
2. Aspose.Cells för .NET: Du behöver Aspose.Cells-biblioteket. Du kan [ladda ner den senaste versionen här](https://releases.aspose.com/cells/net/) eller prova det gratis med en [gratis provperiod](https://releases.aspose.com/).
3. Grundläggande kunskaper i C#: Bekantskap med C# och .NET-miljön är meriterande, men vi vägleder dig i varje steg på vägen.
4. Excel-fil: En exempel-Excel-fil, låt oss kalla den `sampleRotateTextWithShapeInsideWorksheet.xlsx`, behövs för att testa vår kod. Du bör placera den här filen i en katalog som du lätt kan komma åt.
Är allt klart? Fantastiskt! Nu kör vi på det roliga.
## Importera paket
För att komma igång behöver vi importera de nödvändiga paketen till vårt projekt. Så här gör du:
### Skapa ett nytt projekt
1. Öppna Visual Studio.
2. Välj "Skapa ett nytt projekt".
3. Välj "Konsolapp" och välj C# som ditt föredragna programmeringsspråk.
### Installera Aspose.Cells
Nu ska vi lägga till Aspose.Cells i ditt projekt. Du kan göra detta med hjälp av NuGet Package Manager:
1. Öppna "Verktyg" i toppmenyn.
2. Välj "NuGet-pakethanteraren" och sedan "Hantera NuGet-paket för lösningen".
3. Sök efter "Aspose.Cells".
4. Klicka på "Installera" för att lägga till det i ditt projekt.
### Lägg till med hjälp av direktiv
Överst i din huvudsakliga C#-fil måste du lägga till följande direktiv:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
Nu är vi redo att börja koda!
Låt oss dela upp processen i lättförståeliga steg. Så här roterar du text med former i en Excel-fil:
## Steg 1: Konfigurera dina katalogsökvägar
Först måste du konfigurera dina käll- och utdatakataloger där dina Excel-filer ska lagras. Så här gör du:
```csharp
//Källkatalog
string sourceDir = "Your Document Directory"; // Ange din dokumentkatalog
//Utdatakatalog
string outputDir = "Your Document Directory"; // Ställ in din utdatakatalog
```
Ersätta `"Your Document Directory"` med den faktiska vägen dit din `sampleRotateTextWithShapeInsideWorksheet.xlsx` filen finns.
## Steg 2: Ladda exempelfilen i Excel
Nu ska vi ladda exempelfilen i Excel. Detta är avgörande eftersom vi vill manipulera befintliga data.
```csharp
//Ladda exempelfil i Excel.
Workbook wb = new Workbook(sourceDir + "sampleRotateTextWithShapeInsideWorksheet.xlsx");
```
## Steg 3: Öppna arbetsbladet
När filen har laddats behöver vi komma åt det specifika arbetsbladet vi vill ändra. I vårt fall är det det första arbetsbladet.
```csharp
//Åtkomst till första arbetsbladet.
Worksheet ws = wb.Worksheets[0];
```
## Steg 4: Ändra en cell
Härnäst ska vi ändra en specifik cell för att visa ett meddelande. I vårt exempel använder vi cell B4.
```csharp
//Gå till cell B4 och lägg till ett meddelande i den.
Cell b4 = ws.Cells["B4"];
b4.PutValue("Text is not rotating with shape because RotateTextWithShape is false.");
```
Det här steget handlar om kommunikation – att se till att den som öppnar det här arket förstår vad vi justerar.
## Steg 5: Komma åt den första formen
För att rotera text behöver vi en form att arbeta med. Här kommer vi åt den första formen i kalkylbladet.
```csharp
//Åtkomst till första formen.
Shape sh = ws.Shapes[0];
```
## Steg 6: Justera textjusteringen för formen
Det är här magin händer. Vi justerar textjusteringsegenskaperna för formen.
```csharp
//Åtkomst till textjustering för former.
Aspose.Cells.Drawing.Texts.ShapeTextAlignment shapeTextAlignment = sh.TextBody.TextAlignment;
//Rotera inte text med form genom att ställa in RotateTextWithShape som falskt.
shapeTextAlignment.RotateTextWithShape = false;
```
Genom att ställa in `RotateTextWithShape` till falskt, vi ser till att texten förblir upprätt och inte roterar med formen, vilket håller allt snyggt och organiserat.
## Steg 7: Spara den utgående Excel-filen
Slutligen, låt oss spara våra ändringar i en ny Excel-fil. Detta säkerställer att vi inte förlorar våra redigeringar och får ett snyggt resultat.
```csharp
//Spara den utgående Excel-filen.
wb.Save(outputDir + "outputRotateTextWithShapeInsideWorksheet.xlsx");
```
Och det var allt! Din utdatafil är nu sparad, inklusive texten i cell B4 och de justeringar som gjorts i formen.
## Steg 8: Kör koden
I din `Main` metod, slå in alla ovanstående kodavsnitt och kör ditt projekt. Se ändringarna återspeglas i din utdatafil!
```csharp
Console.WriteLine("RotateTextWithShapeInsideWorksheet executed successfully.");
```
## Slutsats
Att rotera text med former i Excel med Aspose.Cells för .NET kan verka som en komplicerad process till en början, men det är ganska enkelt när du väl har analyserat det. Genom att följa dessa enkla steg kan du anpassa dina kalkylblad så att de ser mer professionella och visuellt tilltalande ut. Oavsett om du gör detta för en klient eller för dina personliga projekt kommer alla att lovorda kvaliteten på ditt arbete!
## Vanliga frågor
### Kan jag använda Aspose.Cells gratis?
Ja! Du kan använda [gratis provperiod](https://releases.aspose.com/) att prova på biblioteket.
### Vilka versioner av Excel stöds av Aspose.Cells?
Aspose.Cells stöder en mängd olika Excel-format, inklusive XLS, XLSX, CSV och fler.
### Är det möjligt att rotera text med former i äldre Excel-versioner?
Ja, funktionen kan tillämpas på äldre format som stöds av Aspose.Cells.
### Var kan jag hitta mer dokumentation om Aspose.Cells?
Du kan utforska den omfattande [dokumentation](https://reference.aspose.com/cells/net/) för mer insikter.
### Hur får jag support för Aspose.Cells?
Du kan be om stöd genom att besöka [Aspose-forumet](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}