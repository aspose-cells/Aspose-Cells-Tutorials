---
date: 2026-09-02
description: Lär dig hur du exporterar diagram till PNG, lägger till dataserier, kombinerar
  linje- och stapeldiagram, sparar arbetsbok som XLSX och lägger till legend i diagrammet
  med Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Exportera diagram till PNG och lägg till dataserier för kombinerat diagram
og_description: Exportera diagram till PNG med Aspose.Cells for Java, kombinera linje-
  och stapeldiagram, lägg till dataserier och spara arbetsboken som XLSX i en enda
  handledning.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Exportera diagram till PNG och lägg till dataserier för kombinerat diagram
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: Exportera diagram till PNG och lägg till dataserier för kombinerat diagram
url: /sv/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportera diagram till PNG och lägg till dataserier för kombinerat diagram

I den här handledningen kommer du att **lägga till dataserier** i en Excel-arbetsbok, **kombinera linje- och stapeldiagram**-element och lära dig hur du **exporterar diagram till PNG** med Aspose.Cells för Java. Vi går igenom varje steg — från att konfigurera arbetsboken, lägga till diagrammet i ett kalkylblad, anpassa förklaringen, till att **spara arbetsboken som XLSX** och generera en PNG-bild av diagrammet. I slutet har du ett färdigt kombinerat diagram som du kan bädda in i rapporter eller instrumentpaneler.

## Snabba svar
- **Vilket bibliotek skapar kombinerade diagram?** Aspose.Cells for Java.  
- **Hur lägger jag till en dataserie?** Anropa `chart.getNSeries().add(...)` med lämpligt område.  
- **Hur kan jag exportera diagram till PNG?** Använd `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **Vilket filformat kan jag spara arbetsboken som?** Standard `.xlsx` (spara arbetsboken som XLSX).  
- **Behöver jag en licens för produktion?** Ja – en giltig Aspose.Cells-licens krävs för produktionsdistributioner.

## Vad är export av diagram till PNG i Aspose.Cells?
Att exportera ett diagram till PNG skapar en rasterbild av Excel-diagrammet som kan visas på webbsidor, i rapporter eller e‑post utan att kräva Excel‑applikationen. Denna metod fångar den exakta visuella layouten, färgerna och datamarkörerna och producerar en portabel bildfil.

## Varför skapa ett kombinerat linje‑stapeldiagram?
Ett kombinerat linje‑stapeldiagram låter dig visa olika datamängder med distinkta visuella representationer (t.ex. en linjeserie över en stapelserie) i en enda vy. Detta tillvägagångssätt är idealiskt för att jämföra trender mot totalsummor, framhäva korrelationer eller leverera rikare insikter samtidigt som den visuella fotavtrycket hålls litet.

## Förutsättningar
- Java Development Kit (JDK) 8 eller högre  
- Aspose.Cells for Java‑biblioteket (ladda ner från länken nedan)  
- Grundläggande kunskap om Java‑syntax och Excel‑koncept  

## Komma igång

Först, ladda ner Aspose.Cells for Java‑biblioteket från den officiella webbplatsen:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

När JAR‑filen har lagts till i ditt projekts classpath kan du börja bygga diagrammet.

### Steg 1: importera aspose.cells-klasser
`Workbook` är Aspose.Cells kärnobjekt som representerar en hel Excel‑fil i minnet.  
```java
import com.aspose.cells.*;
```

### Steg 2: skapa en ny arbetsbok
`Worksheet` representerar ett enskilt blad i en `Workbook` och ger åtkomst till celler, rader och diagram.  
```java
Workbook workbook = new Workbook();
```

### Steg 3: åtkomst till det första kalkylbladet
`Chart` är objektet som innehåller alla diagramrelaterade inställningar, serier och renderingsalternativ.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Steg 4: lägg till ett kombinerat diagramobjekt i kalkylbladet  
Vi börjar med ett linjediagram och lägger senare till en stapelserie för att uppnå en **kombinerad linje‑stapeldiagram**‑effekt.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Lägg till data i diagrammet

Nu när diagrambehållaren finns, måste vi fylla den med data.

### Steg 5: definiera dataområdena och lägg till dataserier
`NSeries` är samlingen som lagrar varje dataserie för ett diagram. Att lägga till en serie länkar ett cellområde till diagrammet.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** Den första parametern (`"A1:A5"`) är området för den första serien, och den andra (`"B1:B5"`) skapar en andra serie som kommer att kombineras med den första.

### Steg 6: ange kategoridata (X‑axel)
`CategoryAxis` representerar diagrammets horisontella axel och styr de etiketter som visas längs X‑axeln.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Anpassa diagrammet

Ett bra diagram berättar en historia. Låt oss ge det titlar, axelrubriker och en tydlig förklaring.

### Steg 7: ange diagramaxelrubriker och titel
`Title` sätter huvudtiteln för diagrammet, och `Axis`‑objekt representerar X‑ och Y‑axlarna.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Steg 8: lägg till förklaringsdiagram och justera dess position
`Legend` styr placeringen och utseendet på serieförklaringen i diagrammet.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Spara och exportera diagrammet

Efter anpassning vill du **spara arbetsboken som XLSX** och även generera en bild.

### Steg 9: spara arbetsboken som en Excel‑fil (XLSX)
`Workbook.save` skriver den minnesbaserade arbetsboken till en fil i det angivna formatet.  
```java
workbook.save("CombinedChart.xlsx");
```

### Steg 10: exportera diagram till PNG
`Chart.toImage` renderar diagrammet som en bildfil i det valda formatet.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> Metoden `chart.toImage` **genererar Excel‑diagram**‑bilder som kan användas på webbsidor, i rapporter eller e‑post.

## Vanliga problem & felsökning

| Problem | Lösning |
|-------|----------|
| **Ingen data visas** | Verifiera att cellområdena (`A1:A5`, `B1:B5`, `C1:C5`) faktiskt innehåller data innan diagrammet skapas. |
| **Förklaring överlappar diagram** | Ange `chart.getLegend().setOverlay(false)` eller flytta förklaringen till en annan position (t.ex. `RIGHT`). |
| **Bildfil är tom** | Säkerställ att diagrammet har minst en serie och att `chart.toImage` anropas efter alla anpassningar. |
| **Spara kastar ett undantag** | Kontrollera att du har skrivrättigheter till mål katalogen och att filen inte är öppen i Excel. |

## Vanliga frågor

**Q: Hur installerar jag Aspose.Cells för Java?**  
A: Ladda ner JAR‑filen från den officiella webbplatsen och lägg till den i ditt projekts classpath. Nedladdningslänken är: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Kan jag skapa andra diagramtyper än linje och stapel?**  
A: Ja, Aspose.Cells stöder stapel, cirkel, spridning, område och många fler diagramtyper. Se API‑dokumentationen för den fullständiga listan.

**Q: Krävs en licens för produktionsanvändning?**  
A: En giltig Aspose.Cells‑licens krävs för produktionsdistributioner. En gratis provversion finns tillgänglig för utvärdering.

**Q: Hur kan jag ändra färgerna för varje serie?**  
A: Använd `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (eller liknande) efter att ha lagt till serien.

**Q: Var kan jag hitta fler kodexempel?**  
A: Omfattande dokumentation och ytterligare exempel finns på Aspose referenssida: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

**Senast uppdaterad:** 2026-09-02  
**Testad med:** Aspose.Cells för Java senaste versionen  
**Författare:** Aspose

## Relaterade handledningar

- [Hur man lägger till etiketter i Excel-diagram med Aspose.Cells för Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Hur man skapar Excel-diagram med trendlinje och exporterar till bild med Aspose.Cells för Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Exportera Excel-diagram till PDF med Aspose.Cells för Java: Guide för anpassade sidstorlekar](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}