---
"description": "Lär dig hur du enkelt lägger till bilder i Excel-diagram med Aspose.Cells för .NET. Förbättra dina diagram och presentationer i bara några få enkla steg."
"linktitle": "Lägg till bild i diagrammet"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Lägg till bild i diagrammet"
"url": "/sv/net/inserting-controls-in-charts/add-picture-to-chart/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till bild i diagrammet

## Introduktion

Är du trött på tråkiga diagram som saknar personlig touch? Vill du lära dig hur du kan krydda dina Excel-grafik genom att lägga till bilder? Då har du tur! I den här handledningen dyker vi ner i Aspose.Cells värld för .NET och lär oss hur man lägger till bilder i diagram i Excel. Så ta din favoritkopp kaffe och låt oss sätta igång!

## Förkunskapskrav

Innan vi går in på kodningens grunder finns det några förkunskaper du behöver ha för att följa processen smidigt:

- Visual Studio: Det är här du skriver och kör din .NET-kod. Se till att du har det installerat.
- Aspose.Cells för .NET: Du behöver det här biblioteket för att arbeta med Excel-filer. Du kan [ladda ner den här](https://releases.aspose.com/cells/net/).
- Grundläggande förståelse för C#: Jag kommer att guida dig genom koden, men om du har koll på grunderna i C# kommer det att bli tydligare.

### Installationssteg

1. Installera Aspose.Cells: Du kan lägga till Aspose.Cells i ditt Visual Studio-projekt via NuGet Package Manager. Gör detta genom att gå till Verktyg > NuGet Package Manager > Hantera NuGet-paket för lösningen och söka efter "Aspose.Cells". Klicka på Installera.
2. Konfigurera ditt projekt: Skapa ett nytt C#-konsolapplikationsprojekt i Visual Studio.

## Importera paket

När du har konfigurerat allt är nästa steg att importera de nödvändiga paketen till ditt projekt. Så här gör du:

### Importera de namnrymder som krävs

Överst i din C#-kodfil måste du importera följande namnrymder:

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

Detta säger till ditt program: ”Hej! Jag ska använda de här coola funktionerna från Aspose.Cells.”

Nu när vi har våra förutsättningar på plats, låt oss dela upp processen i små steg. 

## Steg 1: Definiera dina kataloger

Först och främst måste vi ställa in sökvägarna för våra in- och utdatafiler. Detta steg är avgörande eftersom vi behöver veta var vi hittar vår befintliga Excel-fil och var vi sparar den modifierade filen.

```csharp
//Källkatalog
string sourceDir = "Your Document Directory/";

//Utdatakatalog
string outputDir = "Your Output Directory/";
```

Ersätta `Your Document Directory` och `Your Output Directory` med faktiska sökvägar på din dator. 

## Steg 2: Läs in den befintliga arbetsboken

Nu ska vi ladda den befintliga Excel-filen där vi vill lägga till vår bild i diagrammet.

```csharp
// Öppna den befintliga filen.
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

Den här koden öppnar arbetsboken och gör den redo för redigering.

## Steg 3: Förbered bildströmmen

Innan vi lägger till bilden måste vi läsa av bilden vi vill infoga i diagrammet. 

```csharp
// Hämta en bildfil till strömmen.
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

Se till att du har sparat bilden i den angivna katalogen.

## Steg 4: Rikta in dig på diagrammet

Nu ska vi ange vilket diagram vi ska lägga till vår bild i. I det här exemplet riktar vi in oss på det första diagrammet i det första kalkylbladet.

```csharp
// Hämta designerdiagrammet i det andra arket.
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

Du kan komma åt vilket kalkylblad som helst genom att ändra indexet därefter.

## Steg 5: Lägg till bilden i diagrammet

Med diagrammet valt är det dags att lägga till bilden! 

```csharp
// Lägg till en ny bild i diagrammet.
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

Här, `50` och `50` är X- och Y-koordinaterna där bilden kommer att placeras, och `200` är bildens bredd och höjd.

## Steg 6: Anpassa bildens linjeformat

Vill du ge din bild lite extra stil? Du kan anpassa dess kantlinje! Så här gör du:

```csharp
// Hämta bildens linjeformattyp.
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

// Ställ in streckstilen.
lineformat.DashStyle = MsoLineDashStyle.Solid;

// Ställ in linjetjockleken.
lineformat.Weight = 4;    
```

Det här utdraget låter dig välja hur ramen ser ut och hur tjock den är. Välj vilken stil som helst som passar din presentation!

## Steg 7: Spara den modifierade arbetsboken

Efter allt det hårda arbetet, låt oss spara dina ändringar genom att köra följande kodrad:

```csharp
// Spara Excel-filen.
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

Nu är din bild integrerad i diagrammet och din utdatafil är klar för visning!

## Steg 8: Ange framgång

Slutligen kan du lägga till ett enkelt meddelande för att bekräfta att din operation lyckades:

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## Slutsats

I den här handledningen har vi utforskat hur du kan ge dina Excel-diagram lite personlighet genom att lägga till bilder med hjälp av Aspose.Cells för .NET. Med bara några enkla steg kan du lyfta dina presentationer från vardagliga till minnesvärda. Så vad väntar du på? Testa det och låt dina diagram glänsa!

## Vanliga frågor

### Kan jag lägga till flera bilder i ett enda diagram?
Ja! Du kan ringa `AddPictureInChart` metoden flera gånger för att lägga till så många bilder som du vill.

### Vilka bildformat stöder Aspose.Cells?
Aspose.Cells stöder en mängd olika bildformat, inklusive PNG, JPEG, BMP och GIF.

### Kan jag anpassa bildens position?
Absolut! X- och Y-koordinaterna i `AddPictureInChart` Metoden möjliggör exakt positionering.

### Är Aspose.Cells gratis att använda?
Aspose.Cells erbjuder en gratis provperiod, men för alla funktioner krävs en licens. Du kan hitta priserna [här](https://purchase.aspose.com/buy).

### Var kan jag hitta fler exempel?
Kolla in [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/) för mer detaljerade exempel och funktioner.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}