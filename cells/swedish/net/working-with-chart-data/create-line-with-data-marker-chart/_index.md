---
"description": "Lär dig hur du skapar ett diagram av typen Line with Data Markers i Excel med hjälp av Aspose.Cells för .NET. Följ den här steg-för-steg-guiden för att enkelt generera och anpassa diagram."
"linktitle": "Skapa linje med datamarkördiagram"
"second_title": "Aspose.Cells .NET Excel-bearbetnings-API"
"title": "Skapa linje med datamarkördiagram"
"url": "/sv/net/working-with-chart-data/create-line-with-data-marker-chart/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Skapa linje med datamarkördiagram

## Introduktion

Har du någonsin undrat hur man skapar fantastiska diagram i Excel programmatiskt? Nåväl, spänn fast säkerhetsbältet, för idag ska vi dyka ner i att skapa ett Line with Data Marker-diagram med hjälp av Aspose.Cells för .NET. Den här handledningen guidar dig genom varje steg och säkerställer att du har en bra förståelse för diagramgenerering, även om du precis har börjat med Aspose.Cells.

## Förkunskapskrav

Innan vi börjar, se till att du har allt på plats för att kunna följa med smidigt.

1. Aspose.Cells för .NET-biblioteket – Du måste installera detta. Du kan hämta det [här](https://releases.aspose.com/cells/net/).
2. .NET Framework – Se till att din utvecklingsmiljö är konfigurerad med den senaste versionen av .NET.
3. IDE (Integrated Development Environment) – Visual Studio rekommenderas.
4. En giltig Aspose.Cells-licens – Om du inte har en kan du begära en [tillfällig licens](https://purchase.aspose.com/temporary-license/) eller kolla in deras [gratis provperiod](https://releases.aspose.com/).

Redo att köra? Nu ska vi gå igenom det!

## Importera nödvändiga paket

Till att börja med, se till att du importerar följande namnrymder till ditt projekt. Dessa kommer att tillhandahålla de klasser och metoder som krävs för att skapa ditt diagram.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Charts;
using System.Drawing;
```

När du har förstått det kan vi börja koda!

## Steg 1: Konfigurera din arbetsbok och ditt arbetsblad

Först och främst måste du skapa en ny arbetsbok och komma åt det första kalkylbladet.

```csharp
//Utdatakatalog
static string outputDir = "Your Document Directory";
		
// Instansiera en arbetsbok
Workbook workbook = new Workbook();

// Åtkomst till första kalkylbladet
Worksheet worksheet = workbook.Worksheets[0];
```

Tänk på arbetsboken som din Excel-fil och kalkylbladet som det specifika arket i den. I det här fallet arbetar vi med det första arket.

## Steg 2: Fyll i arbetsbladet med data

Nu när vi har vårt kalkylblad, låt oss fylla det med lite data. Vi skapar slumpmässiga datapunkter för två värdeserier.

```csharp
// Ange kolumnrubrik
worksheet.Cells[0, 0].Value = "X";
worksheet.Cells[0, 1].Value = "Y";

// Slumpmässiga data för att generera diagrammet
Random R = new Random();

// Skapa slumpmässiga data och spara dem i cellerna
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

Här använder vi slumptal för att simulera data, men i verkliga tillämpningar kan du fylla i dem med faktiska värden från din datauppsättning.

## Steg 3: Lägg till diagrammet i arbetsbladet

Nästa steg är att lägga till diagrammet i kalkylbladet och välja typ – i det här fallet ett diagram med linje med datamarkörer.

```csharp
// Lägg till ett diagram i kalkylbladet
int idx = worksheet.Charts.Add(ChartType.LineWithDataMarkers, 1, 3, 20, 20);

// Få åtkomst till det nyskapade diagrammet
Chart chart = worksheet.Charts[idx];
```

Det här kodavsnittet lägger till ett linjediagram med datamarkörer i kalkylbladet och placerar det i ett specifikt intervall (1, 3 till 20, 20). Ganska enkelt, eller hur?

## Steg 4: Anpassa diagrammets utseende

När diagrammet är skapat kan du utforma det efter dina önskemål. Nu ändrar vi bakgrund, titel och diagramstil.

```csharp
// Ange diagramstil
chart.Style = 3;

// Ställ in autoskalningsvärdet till sant
chart.AutoScaling = true;

// Ställ in förgrundsfärgen på vit
chart.PlotArea.Area.ForegroundColor = Color.White;

// Ange egenskaper för diagramtitel
chart.Title.Text = "Sample Chart";

// Ange diagramtyp
chart.Type = ChartType.LineWithDataMarkers;
```

Här ger vi diagrammet ett rent utseende genom att ange en vit bakgrund, autoskalera och ge det en meningsfull titel.

## Steg 5: Definiera serier och plotta datapunkter

Nu när vårt diagram ser bra ut behöver vi definiera dataserien som ska plottas.

```csharp
// Ange egenskaper för kategoriaxeltitel
chart.CategoryAxis.Title.Text = "Units";

// Definiera två serier för diagrammet
int s2_idx = chart.NSeries.Add("A2: A21", true);
int s3_idx = chart.NSeries.Add("A22: A41", true);
```

Dessa serier motsvarar de datapunkter som vi fyllde i tidigare.

## Steg 6: Lägg till färger och anpassa seriemarkörer

Låt oss göra det här diagrammet ännu mer tilltalande genom att lägga till anpassade färger till våra datamarkörer.

```csharp
// Anpassa första serien
chart.NSeries[s2_idx].Marker.Area.ForegroundColor = Color.Yellow;
chart.NSeries[s2_idx].Marker.Border.IsVisible = false;

// Anpassa den andra serien
chart.NSeries[s3_idx].Marker.Area.ForegroundColor = Color.Green;
chart.NSeries[s3_idx].Marker.Border.IsVisible = false;
```

Genom att anpassa färgerna gör du diagrammet inte bara funktionellt utan även visuellt tilltalande!

## Steg 7: Ange X- och Y-värden för varje serie

Slutligen, låt oss tilldela X- och Y-värdena för var och en av våra serier.

```csharp
// Ställ in X- och Y-värden för den första serien
chart.NSeries[s2_idx].XValues = "A2: A21";
chart.NSeries[s2_idx].Values = "B2: B21";

// Ställ in X- och Y-värden för den andra serien
chart.NSeries[s3_idx].XValues = "A22: A41";
chart.NSeries[s3_idx].Values = "B22: B41";
```

Värdena är baserade på de data vi fyllde i i steg 2.

## Steg 8: Spara arbetsboken

Nu när allt är klart, låt oss spara arbetsboken så att vi kan se diagrammet i aktion.

```csharp
// Spara arbetsboken
workbook.Save(outputDir + @"LineWithDataMarkerChart.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```

Och det var allt! Du har just skapat ett linjediagram med datamarkörer med hjälp av Aspose.Cells för .NET.

## Slutsats

Att skapa diagram programmatiskt i Excel kan verka skrämmande, men med Aspose.Cells för .NET är det lika enkelt som att följa ett steg-för-steg-recept. Från att konfigurera din arbetsbok till att anpassa diagrammets utseende hanterar detta kraftfulla bibliotek allt. Oavsett om du skapar rapporter, dashboards eller datavisualiseringar låter Aspose.Cells dig göra det på ett ögonblick.

## Vanliga frågor

### Kan jag anpassa diagrammet ytterligare?  
Absolut! Aspose.Cells erbjuder massor av anpassningsalternativ, från teckensnitt till rutnät och mer.

### Behöver jag en licens för att använda Aspose.Cells?  
Ja, en licens krävs för full funktionalitet. Du kan få en [tillfällig licens](https://purchase.aspose.com/temporary-license/) eller börja med en [gratis provperiod](https://releases.aspose.com/).

### Hur kan jag lägga till fler dataserier?  
Lägg bara till ytterligare serier med hjälp av `NSeries.Add` metod, som anger cellintervallen för den nya datan.

### Kan jag exportera diagrammet som en bild?  
Ja, du kan exportera diagram direkt som bilder med hjälp av `Chart.ToImage` metod.

### Stöder Aspose.Cells 3D-diagram?  
Ja, Aspose.Cells stöder ett brett utbud av diagramtyper, inklusive 3D-diagram.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}