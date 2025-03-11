---
title: Använd 3D-format på diagram
linktitle: Använd 3D-format på diagram
second_title: Aspose.Cells .NET Excel Processing API
description: Upptäck hur du skapar fantastiska 3D-diagram i Excel med Aspose.Cells för .NET. Följ vår enkla steg-för-steg-guide.
weight: 10
url: /sv/net/advanced-chart-operations/apply-3d-format-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Använd 3D-format på diagram

## Introduktion

I en tid där datavisualisering är av största vikt går sättet vi presenterar vår data på utöver grundläggande grafer och diagram. Med verktyg som Aspose.Cells för .NET kan du lyfta dina datapresentationer med fantastiska 3D-diagram som inte bara fångar uppmärksamhet utan också förmedlar information effektivt. Den här guiden går igenom stegen för att tillämpa ett 3D-format på ett diagram med hjälp av Aspose.Cells, för att omvandla dina rådata till en engagerande skärm.

## Förutsättningar

Innan vi dyker in i det tråkiga med att tillämpa ett 3D-format på ett diagram, låt oss se till att du har allt du behöver.

### Programvarukrav

- Visual Studio: Se till att du har Visual Studio installerat för att fungera med .NET-applikationer.
-  Aspose.Cells för .NET: Om du inte har gjort det ännu, ladda ner och installera Aspose.Cells från[här](https://releases.aspose.com/cells/net/).

### Inställning av kodningsmiljö

1. Skapa ett nytt .NET-projekt: Öppna Visual Studio, välj "Skapa ett nytt projekt" och välj ett konsolprogram.
2. Lägg till Aspose.Cells-referens: Via NuGet Package Manager, lägg till Aspose.Cells genom att söka efter det eller via Package Manager-konsolen:

```bash
Install-Package Aspose.Cells
```

3. Installera utdatakatalog: Ange en utdatakatalog där dina genererade filer kommer att sparas – det här kan vara så enkelt som att skapa en mapp på skrivbordet.

Nu när du är klar är det dags att hoppa in i koden och skapa några bländande 3D-diagram!

## Importera paket

För att börja måste du importera de nödvändiga namnrymden. Detta hjälper dig att komma åt klasserna och metoderna som tillhandahålls av Aspose.Cells. Så här gör du det:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
using Aspose.Cells.Charts;
```

Det här avsnittet kommer att dela upp processen i hanterbara steg, vilket ger dig en tydlig förståelse för varje steg.

## Steg 1: Initiera din arbetsbok

 Först måste du skapa en instans av`Workbook` klass. Detta objekt kommer att fungera som grunden för ditt Excel-dokument.

```csharp
//Utdatakatalog
string outputDir = "Your Document Directory";
Workbook book = new Workbook();
```
 Tänk på det här`Workbook` som en tom duk – redo för dig att fylla den med färgglad data och effektfulla visualiseringar.

## Steg 2: Byt namn på det första arbetsbladet

Låt oss sedan byta namn på det första kalkylbladet. Detta ger klarhet i vilken data vi arbetar med.

```csharp
book.Worksheets[0].Name = "DataSheet";
```

Namn bör vara intuitiva. I det här fallet döper vi det till "Datablad" så att vi vet var vår data finns.

## Steg 3: Skapa data för diagrammet

Nu lägger vi till lite data till vårt "Datablad." Låt oss fylla den med värden som vårt diagram kommer att använda.

```csharp
Worksheet dataSheet = book.Worksheets["DataSheet"];
dataSheet.Cells["B1"].PutValue(1);
dataSheet.Cells["B2"].PutValue(2);
dataSheet.Cells["B3"].PutValue(3);
dataSheet.Cells["A1"].PutValue("A");
dataSheet.Cells["A2"].PutValue("B");
dataSheet.Cells["A3"].PutValue("C");
```

Precis som ett recept beror på ingredienser, beror ditt diagrams effektivitet på kvaliteten och organisationen av dina indata.

## Steg 4: Skapa ett nytt diagramarbetsblad

Dags att skapa ett nytt kalkylblad för själva diagrammet. Detta hjälper till att hålla din datavisualisering organiserad.

```csharp
Worksheet sheet = book.Worksheets.Add("MyChart");
```

Se det här kalkylbladet som ditt stadium – där prestandan för dina data utvecklas.

## Steg 5: Lägg till ett diagram

Här kommer vi att lägga till ett kolumndiagram till det nyskapade kalkylbladet.  

```csharp
ChartCollection charts = sheet.Charts;
int chartSheetIdx = charts.Add(ChartType.Column, 5, 0, 25, 15);
```

Vi definierar ett utrymme för vårt diagram och anger vilken typ det är. Tänk bara på det som att välja typ av ram för ditt konstverk.

## Steg 6: Anpassa diagrammets utseende

Låt oss nu anpassa vårt diagrams utseende genom att ställa in bakgrundsfärger. 

```csharp
Aspose.Cells.Charts.Chart chart = book.Worksheets["MyChart"].Charts[0];
chart.PlotArea.Area.BackgroundColor = Color.White;
chart.ChartArea.Area.BackgroundColor = Color.White;
chart.PlotArea.Area.ForegroundColor = Color.White;
chart.ChartArea.Area.ForegroundColor = Color.White;
chart.ShowLegend = false;
```

En ren vit bakgrund gör ofta att färgerna på dina data sticker ut, vilket förbättrar synligheten.

## Steg 7: Lägg till dataserier i diagrammet

Det är dags att mata vårt diagram med data. Vi lägger till en dataserie från vårt "Datablad" för att säkerställa att vårt diagram återspeglar den data vi behöver.

```csharp
chart.NSeries.Add("DataSheet!B1:B3", true);
chart.NSeries.CategoryData = "DataSheet!A1:A3";
```

Detta är analogt med en kock som förbereder en maträtt med specifika ingredienser. Varje datapunkt är viktig!

## Steg 8: Få åtkomst till och formatera dataserien

Nu när vi har länkat våra data, låt oss ta tag i dataserien och börja tillämpa några 3D-effekter.

```csharp
Aspose.Cells.Charts.Series ser = chart.NSeries[0];
ShapePropertyCollection spPr = ser.ShapeProperties;
Format3D fmt3d = spPr.Format3D;
```

Vi håller på att förbereda oss för att lägga lite flärd till vår maträtt – tänk på det som krydda som förhöjer den övergripande smaken.

## Steg 9: Använd 3D-fasningseffekter

Därefter kommer vi att lägga till en avfasningseffekt för att ge vårt diagram en viss dimension.

```csharp
Bevel bevel = fmt3d.TopBevel;
bevel.Type = BevelPresetType.Circle;
bevel.Height = 2;
bevel.Width = 5;
```

Precis som en skulptör formar sten, skapar vi djup som gör vårt diagram levande!

## Steg 10: Anpassa ytmaterial och belysning

Låt oss få vårt diagram att lysa klart! Vi kommer att justera ytmaterial och ljusinställningar.

```csharp
fmt3d.SurfaceMaterialType = PresetMaterialType.WarmMatte;
fmt3d.SurfaceLightingType = LightRigType.ThreePoint;
fmt3d.LightingAngle = 20;
```

Rätt belysning och material kan förvandla ett platt föremål till en fängslande bild. Tänk på en filmuppsättning sakkunnigt upplyst för att förbättra varje scen.

## Steg 11: Sista handen om seriens utseende

Nu för att slutföra utseendet på vår dataserie genom att justera dess färg.

```csharp
ser.Area.BackgroundColor = Color.Maroon;
ser.Area.ForegroundColor = Color.Maroon;
ser.Border.Color = Color.Maroon;
```

Rätt färg kan framkalla vissa känslor och reaktioner – rödbrun ger en touch av elegans och sofistikering.

## Steg 12: Spara din arbetsbok

Äntligen är det dags att rädda ditt mästerverk! Glöm inte att ange destinationen där du vill lagra den.

```csharp
book.Save(outputDir + "outputApplying3DFormat.xlsx");
Console.WriteLine("Applying3DFormat executed successfully.");
```

Att spara ditt verk är som att placera din konst i ett galleri; det är ett ögonblick att vårda och dela.

## Slutsats

Grattis! Du har framgångsrikt skapat ett visuellt tilltalande 3D-diagram med Aspose.Cells för .NET. Genom att följa dessa steg har du nu ett kraftfullt verktyg för att förbättra dina datapresentationer, vilket gör dem inte bara informativa utan också visuellt fängslande. När du förfinar dina diagram, kom ihåg att varje visualisering är en berättelse – gör den engagerande, tydlig och effektfull!

## FAQ's

### Vad är Aspose.Cells för .NET?
Aspose.Cells för .NET är ett kraftfullt bibliotek som tillåter utvecklare att manipulera Excel-dokument programmatiskt, inklusive att skapa diagram och diagram.

### Kan jag anpassa diagramtyper i Aspose.Cells?
Ja! Aspose.Cells stöder olika diagramtyper som Column, Line, Pie och många fler, som enkelt kan anpassas.

### Finns det en gratis testversion tillgänglig för Aspose.Cells?
 Absolut! Du kan ladda ner en gratis testversion från[här](https://releases.aspose.com/).

### Kan jag använda andra effekter på diagram förutom 3D-format?
Ja, du kan använda olika effekter som skuggor, gradienter och olika stilar för att förbättra dina diagram bortom 3D.

### Var kan jag hitta support för Aspose.Cells?
 För support kan du besöka[Aspose Forum](https://forum.aspose.com/c/cells/9) för samhällsstöd och hjälp.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
