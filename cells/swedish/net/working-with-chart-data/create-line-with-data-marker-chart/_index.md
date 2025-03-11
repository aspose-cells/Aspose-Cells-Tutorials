---
title: Skapa linje med datamarkördiagram
linktitle: Skapa linje med datamarkördiagram
second_title: Aspose.Cells .NET Excel Processing API
description: Lär dig hur du skapar ett linjediagram med datamarkörer i Excel med Aspose.Cells för .NET. Följ den här steg-för-steg-guiden för att enkelt skapa och anpassa diagram.
weight: 10
url: /sv/net/working-with-chart-data/create-line-with-data-marker-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Skapa linje med datamarkördiagram

## Introduktion

Har du någonsin undrat hur man skapar fantastiska diagram i Excel programmatiskt? Nåväl, spänn fast dig, för idag går vi in på att skapa ett linjediagram med datamarkörer med Aspose.Cells för .NET. Denna handledning guidar dig genom varje steg, och säkerställer att du har ett fast grepp om diagramgenerering, även om du precis har börjat med Aspose.Cells.

## Förutsättningar

Innan vi börjar, se till att du har allt på plats för att följa med sömlöst.

1. Aspose.Cells för .NET Library – Du måste installera detta. Du kan ta tag i den[här](https://releases.aspose.com/cells/net/).
2. .NET Framework – Se till att din utvecklingsmiljö är konfigurerad med den senaste versionen av .NET.
3. IDE (Integrated Development Environment) – Visual Studio rekommenderas.
4.  En giltig Aspose.Cells-licens – Om du inte har en, kan du begära en[tillfällig licens](https://purchase.aspose.com/temporary-license/) eller kolla in deras[gratis provperiod](https://releases.aspose.com/).

Redo att gå? Låt oss bryta ner det!

## Importera nödvändiga paket

För att börja, se till att du importerar följande namnområden till ditt projekt. Dessa kommer att tillhandahålla de nödvändiga klasserna och metoderna för att skapa ditt diagram.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

När du har gjort det kan vi börja koda!

## Steg 1: Konfigurera din arbetsbok och arbetsblad

Först och främst måste du skapa en ny arbetsbok och komma åt det första kalkylbladet.

```csharp
//Utdatakatalog
static string outputDir = "Your Document Directory";
		
// Instantiera en arbetsbok
Workbook workbook = new Workbook();

// Öppna första kalkylbladet
Worksheet worksheet = workbook.Worksheets[0];
```

Tänk på arbetsboken som din Excel-fil och kalkylbladet som det specifika bladet i den. I det här fallet arbetar vi med det första arket.

## Steg 2: Fyll kalkylbladet med data

Nu när vi har vårt kalkylblad, låt oss fylla det med lite data. Vi skapar slumpmässiga datapunkter för två serier av värden.

```csharp
// Ange kolumns titel
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Slumpmässiga data för att generera diagrammet
Random R = new Random();

// Skapa slumpmässiga data och spara i cellerna
for (int i = 1; i < 21; i++)
{
    worksheet.Cells[i, 0].Value = i;
    worksheet.Cells[i, 1].Value = 0.8;
}

for (int i = 21; i < 41; i++)
{
    worksheet.Cells[i, 0].Value = i - 20;
    worksheet.Cells[i, 1].Value = 0.9;
}
```

Här använder vi slumptal för att simulera data, men i verkliga applikationer kan du fylla i den med faktiska värden från din datauppsättning.

## Steg 3: Lägg till diagrammet i arbetsbladet

Därefter lägger vi till diagrammet i kalkylbladet och väljer typen – i det här fallet ett diagram med linje med datamarkörer.

```csharp
// Lägg till ett diagram i arbetsbladet
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Öppna det nyskapade diagrammet
Chart chart = worksheet.Charts[idx];
```

Detta utdrag lägger till ett linjediagram med datamarkörer till kalkylbladet och placerar det i ett specifikt intervall (1,3 till 20,20). Ganska enkelt, eller hur?

## Steg 4: Anpassa diagrammets utseende

När diagrammet har skapats kan du stila det efter eget tycke. Låt oss ändra bakgrund, titel och diagramstil.

```csharp
// Ställ in diagramstil
chart.Style = 3;

// Ställ in autoskalningsvärdet på sant
chart.AutoScaling = true;

// Ställ in förgrundsfärgen på vit
chart.PlotArea.Area.ForegroundColor = Color.White;

//Ange egenskaper för diagramrubrik
chart.Title.Text = "Sample Chart";

// Ställ in diagramtyp
chart.Type = ChartType.LineWithDataMarkers;
```

Här ger vi diagrammet ett rent utseende genom att ställa in en vit bakgrund, autoskala och ge det en meningsfull titel.

## Steg 5: Definiera serier och rita datapunkter

Nu när vårt diagram ser bra ut måste vi definiera dataserien som kommer att plottas.

```csharp
// Ställ in egenskaper för kategoriaxeltitel
chart.CategoryAxis.Title.Text = "Units";

// Definiera två serier för diagrammet
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Dessa serier motsvarar intervallen av datapunkter som vi fyllde i tidigare.

## Steg 6: Lägg till färger och anpassa seriemarkörer

Låt oss göra det här diagrammet ännu mer tilltalande genom att lägga till anpassade färger till våra datamarkörer.

```csharp
// Anpassa första serien
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Anpassa andra serien
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Genom att anpassa färgerna gör du diagrammet inte bara funktionellt utan också visuellt engagerande!

## Steg 7: Ställ in X- och Y-värden för varje serie

Till sist, låt oss tilldela X- och Y-värdena för var och en av våra serier.

```csharp
// Ställ in X- och Y-värden för den första serien
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Ställ in X- och Y-värden för den andra serien
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Värdena är baserade på data vi fyllde i i steg 2.

## Steg 8: Spara arbetsboken

Nu när allt är klart, låt oss spara arbetsboken så att vi kan se diagrammet i aktion.

```csharp
// Spara arbetsboken
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Och det är det! Du har precis skapat ett linjediagram med datamarkörer med Aspose.Cells för .NET.

## Slutsats

Att skapa diagram programmatiskt i Excel kan verka skrämmande, men med Aspose.Cells för .NET är det lika enkelt som att följa ett steg-för-steg-recept. Från att ställa in din arbetsbok till att anpassa diagrammets utseende, detta kraftfulla bibliotek hanterar allt. Oavsett om du bygger rapporter, instrumentpaneler eller datavisualiseringar låter Aspose.Cells dig göra det på ett enkelt sätt.

## FAQ's

### Kan jag anpassa diagrammet ytterligare?  
Absolut! Aspose.Cells erbjuder massor av anpassningsalternativ, från teckensnitt till rutnät och mer.

### Behöver jag en licens för att använda Aspose.Cells?  
 Ja, en licens krävs för full funktionalitet. Du kan få en[tillfällig licens](https://purchase.aspose.com/temporary-license/) eller börja med a[gratis provperiod](https://releases.aspose.com/).

### Hur kan jag lägga till fler dataserier?  
 Lägg bara till ytterligare serier med hjälp av`NSeries.Add` metod, som anger cellområdena för den nya datan.

### Kan jag exportera diagrammet som en bild?  
 Ja, du kan exportera diagram direkt som bilder med hjälp av`Chart.ToImage` metod.

### Stöder Aspose.Cells 3D-diagram?  
Ja, Aspose.Cells stöder ett brett utbud av diagramtyper, inklusive 3D-diagram.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
