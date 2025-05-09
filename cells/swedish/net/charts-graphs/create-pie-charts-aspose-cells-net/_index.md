---
"date": "2025-04-05"
"description": "Lär dig hur du skapar dynamiska cirkeldiagram med riktlinjer med Aspose.Cells för .NET. Följ den här guiden för att förbättra dina kunskaper inom datavisualisering."
"title": "Skapa cirkeldiagram med riktlinjer i Aspose.Cells .NET – En omfattande guide"
"url": "/sv/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Skapa cirkeldiagram med riktlinjer med hjälp av Aspose.Cells .NET

## Introduktion
Förbättra din datavisualisering genom att skapa mer informativa cirkeldiagram med Aspose.Cells för .NET. Den här steg-för-steg-guiden visar hur du lägger till riktlinjer i cirkeldiagramsegment, vilket gör det enklare att identifiera motsvarande datakategorier med en snabb blick. Genom att följa den här handledningen kommer dina visualiseringar att vara både visuellt tilltalande och mycket funktionella.

**Vad du kommer att lära dig:**
- Konfigurera Aspose.Cells för .NET i din miljö
- Skapa anpassade cirkeldiagram med hjälp av C#
- Spara diagrammet som en bild eller i en Excel-arbetsbok

Se till att du har allt klart för att kunna följa upp effektivt.

## Förkunskapskrav
Innan du börjar, se till att du uppfyller dessa förutsättningar:

- **Bibliotek och versioner**Installera Aspose.Cells för .NET. Se till att ditt projekt är konfigurerat med den senaste versionen.
- **Miljöinställningar**Den här guiden förutsätter en kompatibel .NET-miljö för Aspose.Cells.
- **Kunskapsförkunskaper**Grundläggande kunskaper i C#-programmering och Excel-operationer är meriterande.

## Konfigurera Aspose.Cells för .NET
För att börja, installera Aspose.Cells i ditt projekt via:

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

**Pakethanterare**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Skaffa en licens för full funktionalitet genom att välja bland följande alternativ:
- **Gratis provperiod**Starta din kostnadsfria provperiod på [Aspose nedladdningssida](https://releases.aspose.com/cells/net/).
- **Tillfällig licens**: Skaffa ett tillfälligt körkort [här](https://purchase.aspose.com/temporary-license/).
- **Köpa**För fullständiga funktioner, köp en licens [här](https://purchase.aspose.com/buy).

Initiera Aspose.Cells i ditt projekt genom att skapa en instans av `Workbook` klass.

## Implementeringsguide

### Skapa arbetsboken och arbetsbladet
1. **Initiera arbetsboken**
   Skapa en ny arbetsbok i XLSX-format:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **Åtkomst till det första arbetsbladet**
   Använd det första arbetsbladet för att mata in data:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Lägga till data för cirkeldiagram**
   Fyll ditt kalkylblad med kategorier och värden:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Lägg till återstående kategorinamn...
   worksheet.Cells["B1"].PutValue(10.4);
   // Lägg till motsvarande värden...
   ```

### Lägga till ett cirkeldiagram i arbetsbladet
1. **Skapa cirkeldiagrammet**
   Generera ett cirkeldiagram och lägg till det i ditt arbetsblads diagramsamling:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Konfigurera serie- och kategoridata**
   Länka data för serien och kategorierna:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Anpassa dataetiketter**
   Stäng av visning av förklaringar, ställ in dataetiketter för att visa kategorinamn och procentsatser:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Implementera ledarlinjer
1. **Aktivera ledarlinjer**
   Aktivera riktlinjer för tydligare visuella kopplingar:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Justera dataetiketternas position**
   Säkerställ synlighet genom att justera etiketternas positioner:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Spara diagrammet och arbetsboken
1. **Spara som bild**
   Rendera diagrammet till en bildfil:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Spara arbetsboken**
   Spara arbetsboken för att visa diagrammet i Excel:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Praktiska tillämpningar
- **Finansiella rapporter**Representerar tydligt budgetfördelningar.
- **Marknadsanalys**Visualisera marknadsandelsdata effektivt i presentationer eller rapporter.
- **Försäljningsanalys**Visa enkelt försäljningsfördelning mellan olika regioner/produkter.

Integrationsmöjligheterna inkluderar export av dessa visualiseringar till webbapplikationer eller bäddning av dem i automatiserade rapporteringsverktyg.

## Prestandaöverväganden
När du använder Aspose.Cells, tänk på följande för optimal prestanda:
- Minimera stora datamängder som laddas in i minnet samtidigt.
- Använd effektiva loopar och undvik onödiga beräkningar inuti loopar.
- Rensa regelbundet resurser som arbetsboksobjekt för att förhindra minnesläckor.

## Slutsats
Du har lärt dig hur man skapar cirkeldiagram med riktlinjer med Aspose.Cells för .NET. Den här funktionen förbättrar tydligheten i dina datavisualiseringar, vilket gör dem mer tillgängliga och effektiva. 

**Nästa steg:**
Utforska ytterligare anpassningar av diagramutseenden eller experimentera med andra diagramtyper som finns tillgängliga i Aspose.Cells.

## FAQ-sektion
1. **Vad är en ledlinje i ett cirkeldiagram?**
   Hänvisningslinjer kopplar dataetiketter till sina respektive segment, vilket förbättrar läsbarheten.

2. **Kan jag använda Aspose.Cells gratis?**
   Ja, du kan börja med en gratis provperiod, men alla funktioner kräver en licens.

3. **Är det möjligt att exportera diagram som bilder?**
   Absolut! Använd `ImageOrPrintOptions` för att spara ditt diagram i bildformat som PNG eller JPEG.

4. **Hur justerar jag dataetiketternas positioner manuellt?**
   Ändra X- och Y-koordinaterna för dataetiketter inom seriepunktsslingan.

5. **Kan Aspose.Cells integreras med andra system?**
   Ja, det kan användas tillsammans med databaser, webbtjänster och mer för automatiserade rapporteringslösningar.

## Resurser
- [Aspose.Cells-dokumentation](https://reference.aspose.com/cells/net/)
- [Ladda ner Aspose.Cells](https://releases.aspose.com/cells/net/)
- [Köplicens](https://purchase.aspose.com/buy)
- [Gratis provperiod](https://releases.aspose.com/cells/net/)
- [Tillfällig licens](https://purchase.aspose.com/temporary-license/)
- [Supportforum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}