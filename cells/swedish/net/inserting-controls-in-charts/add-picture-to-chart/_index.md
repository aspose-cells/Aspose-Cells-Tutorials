---
title: Lägg till bild i diagrammet
linktitle: Lägg till bild i diagrammet
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du enkelt lägger till bilder i Excel-diagram med Aspose.Cells för .NET. Förbättra dina diagram och presentationer med bara några enkla steg.
weight: 11
url: /sv/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till bild i diagrammet

## Introduktion

Är du trött på tråkiga listor som saknar en personlig touch? Vill du lära dig hur du piffar upp dina Excel-bilder genom att lägga till bilder? Tja, du har tur! I den här handledningen kommer vi att dyka in i Aspose.Cells-världen för .NET och lära oss hur du lägger till bilder i diagram i Excel. Så ta din favoritkopp kaffe och låt oss börja!

## Förutsättningar

Innan vi hoppar in i det snälla med kodning, finns det några förutsättningar du måste ha för att följa smidigt:

- Visual Studio: Det är här du kommer att skriva och köra din .NET-kod. Se till att du har den installerad.
-  Aspose.Cells för .NET: Du behöver det här biblioteket för att arbeta med Excel-filer. Du kan[ladda ner den här](https://releases.aspose.com/cells/net/).
- Grundläggande förståelse för C#: Även om jag ska guida dig genom koden, kommer det att göra saker tydligare om du har grepp om C#s grunder.

### Installationssteg

1. Installera Aspose.Cells: Du kan lägga till Aspose.Cells till ditt Visual Studio-projekt via NuGet Package Manager. Gör detta genom att navigera till Verktyg > NuGet Package Manager > Hantera NuGet Packages for Solution och söka efter "Aspose.Cells." Klicka på Installera.
2. Konfigurera ditt projekt: Skapa ett nytt C#-konsolapplikationsprojekt i Visual Studio.

## Importera paket

När du har ställt in allt är nästa steg att importera de nödvändiga paketen till ditt projekt. Så här gör du:

### Importera de nödvändiga namnområdena

Överst i din C#-kodfil måste du importera följande namnrymder:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Detta säger till ditt program, "Hej! Jag ska använda dessa coola funktioner från Aspose.Cells.”

Nu när vi har våra förutsättningar på plats, låt oss dela upp processen i små steg. 

## Steg 1: Definiera dina kataloger

Först och främst måste vi ställa in sökvägarna för våra in- och utdatafiler. Detta steg är avgörande eftersom vi behöver veta var vi kan hitta vår befintliga Excel-fil och var vi ska spara den ändrade filen.

```csharp
//Källkatalog
string sourceDir = "Your Document Directory/";

//Utdatakatalog
string outputDir = "Your Output Directory/";
```

 Ersätta`Your Document Directory` och`Your Output Directory` med faktiska sökvägar på din dator. 

## Steg 2: Ladda den befintliga arbetsboken

Låt oss nu ladda den befintliga Excel-filen där vi vill lägga till vår bild i diagrammet.

```csharp
// Öppna den befintliga filen.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Den här koden öppnar arbetsboken och gör den redo för redigering.

## Steg 3: Förbered bildströmmen

Innan vi lägger till bilden måste vi läsa bilden vi vill infoga i diagrammet. 

```csharp
// Hämta en bildfil till streamen.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Se till att du har bilden sparad i den angivna katalogen.

## Steg 4: Rikta in diagrammet

Låt oss nu specificera vilket diagram vi ska lägga till vår bild på. I det här exemplet riktar vi oss mot det första diagrammet i det första kalkylbladet.

```csharp
// Få designerdiagrammet i det andra bladet.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Du kan komma åt vilket kalkylblad som helst genom att ändra indexet i enlighet med detta.

## Steg 5: Lägg till bilden i diagrammet

Med diagrammet valt är det dags att lägga till bilden! 

```csharp
// Lägg till en ny bild i diagrammet.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

 Här,`50` och`50` är X- och Y-koordinaterna där bilden kommer att placeras, och`200` är bildens bredd och höjd.

## Steg 6: Anpassa bildens linjeformat

Vill du lägga till lite stil till din bild? Du kan anpassa dess gräns! Så här gör du:

```csharp
// Få bildens linjeformattyp.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Ställ in streckstilen.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Ställ in linjevikten.
lineformat.Weight = 4;    
```

Detta utdrag låter dig välja hur bården ser ut och hur tjock den är. Välj vilken stil som helst som resonerar med din presentation!

## Steg 7: Spara den modifierade arbetsboken

Efter allt det hårda arbetet, låt oss spara dina ändringar genom att köra följande kodrad:

```csharp
// Spara excel-filen.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Nu har din bild framgångsrikt integrerats i diagrammet och din utdatafil är klar för visning!

## Steg 8: Indikera framgång

Slutligen kan du lägga till ett enkelt meddelande för att bekräfta att din operation lyckades:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Slutsats

I den här handledningen har vi utforskat hur du kan injicera lite personlighet i dina Excel-diagram genom att lägga till bilder med Aspose.Cells för .NET. Med bara några enkla steg kan du lyfta dina presentationer från vardagliga till minnesvärda. Så vad väntar du på? Ge det en chans och låt dina diagram lysa!

## FAQ's

### Kan jag lägga till flera bilder i ett enda diagram?
 Ja! Du kan ringa till`AddPictureInChart` metod flera gånger för att lägga till så många bilder som du vill.

### Vilka bildformat stöder Aspose.Cells?
Aspose.Cells stöder en mängd olika bildformat, inklusive PNG, JPEG, BMP och GIF.

### Kan jag anpassa bildens position?
 Säkert! X- och Y-koordinaterna i`AddPictureInChart` metod möjliggör exakt positionering.

### Är Aspose.Cells gratis att använda?
Aspose.Cells erbjuder en gratis provperiod, men för alla funktioner krävs en licens. Du kan hitta priset[här](https://purchase.aspose.com/buy).

### Var kan jag hitta fler exempel?
 Kolla in[Aspose.Cells dokumentation](https://reference.aspose.com/cells/net/) för mer detaljerade exempel och funktioner.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
