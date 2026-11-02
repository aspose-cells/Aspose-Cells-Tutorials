---
date: 2026-08-21
description: Lär dig hur du lägger till tooltips, data labels och ändrar chart type
  i Excel charts med Aspose.Cells for Java – steg‑för‑steg guide med interaktiva exempel.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Ändra Excel Chart Type
og_description: Lär dig hur du lägger till tooltips, data labels och ändrar chart
  type i Excel charts med Aspose.Cells for Java – steg‑för‑steg guide med interaktiva
  exempel.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Hur man lägger till tooltips och data labels i Excel charts i Java
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Hur man lägger till tooltips och data labels i Excel charts i Java
url: /sv/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Lägg till datalabels i Excel-diagram och ändra diagramtyp – Aspose.Cells Java

Interaktiva diagram ger dina Excel-rapporter en ny nivå av insikt, och **hur man lägger till verktygstips** gör informationen omedelbart läsbar. I den här handledningen kommer du att lära dig hur du **lägger till datalabels i Excel-diagram**, **ändrar diagramtypen**, och skapar interaktiva Java‑lösningar med Aspose.Cells. Vi visar också hur du lägger till verktygstips och en enkel drill‑down‑hyperlänk så att din publik kan utforska data på djupet.

## Snabba svar
- **Vilket bibliotek används?** Aspose.Cells for Java  
- **Kan jag ändra diagramtypen?** Ja – ändra bara `ChartType`‑enum när du skapar diagrammet.  
- **Hur lägger jag till verktygstips i ett diagram?** Använd data‑label‑API:t (`setHasDataLabels(true)`) och aktivera värdevisning.  
- **Stöds drill‑down?** Du kan bifoga hyperlänkar till datapunkter för grundläggande drill‑down‑beteende.  
- **Förutsättningar?** Java‑IDE, Aspose.Cells JAR och en Excel‑fil med exempeldata.

## Vad är hur man lägger till verktygstips?
**Hur man lägger till verktygstips** avser processen att aktivera svävande text som visar ett datapunkts värde eller anpassad information i ett Excel-diagram. I Aspose.Cells uppnås detta genom diagrammets data‑label‑inställningar. Verktygstips hjälper användare att snabbt förstå data utan att fylla diagrammet, och de kan anpassas för teckensnitt, färg och format.

## Varför använda interaktiva diagram med Aspose.Cells?
Aspose.Cells stöder **50+ in‑ och utdataformat**—inklusive XLSX, CSV, PDF och HTML—och kan bearbeta arbetsböcker med **över 1 000 blad** utan att ladda hela filen i minnet, vilket ger snabb server‑sidig diagramgenerering för företagsrapportering. Interaktiva diagram möjliggör även inbäddning av hyperlänkar, dynamiska datauppdateringar och export till webbvänliga format, vilket gör dem idealiska för instrumentpaneler och rapportportaler.

## Förutsättningar

Innan vi börjar, se till att du har följande:

- Java‑utvecklingsmiljö (JDK 8+ rekommenderas)  
- Aspose.Cells for Java‑bibliotek (ladda ner från [Aspose.Cells for Java download page](https://releases.aspose.com/cells/java/))  
- En exempel‑arbetsbok (`data.xlsx`) som innehåller de data du vill visualisera  

## Steg 1: konfigurera ditt Java‑projekt

1. Skapa ett nytt Java‑projekt i din favorit‑IDE (IntelliJ IDEA, Eclipse osv.).  
2. Lägg till Aspose.Cells‑JAR‑filen i projektets byggsökväg eller Maven/Gradle‑beroenden.

## Steg 2: läsa in data

För att arbeta med diagram måste du först ha en arbetsbok inläst i minnet.

Klassen `Workbook` representerar en Excel‑fil, och `Worksheet` representerar ett enskilt blad i den filen.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Hur man ändrar diagramtyp i Aspose.Cells?

Skapa ett nytt diagram med önskad `ChartType`‑enum; Aspose.Cells ändrar inte en befintlig diagramtyp på plats, så du måste lägga till ett nytt diagram av rätt typ och eventuellt ta bort det gamla. Detta tillvägagångssätt garanterar att alla serier och axlar byggs om korrekt för den nya visuella representationen.

## Steg 3: skapa ett diagram (och ändra dess typ)

Du kan välja vilken diagramtyp som helst som passar din analys. Nedan skapar vi ett **stapeldiagram**, men du kan enkelt byta till ett linje‑, paj‑ eller stapeldiagram genom att ändra `ChartType`‑enum.

Objektet `Chart` erbjuder metoder för att konfigurera den visuella representationen av data i arbetsbladet.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Proffstips:** För att **ändra Excel‑diagramtyp**, ersätt `ChartType.COLUMN` med `ChartType.LINE`, `ChartType.PIE` osv.

## Hur man lägger till verktygstips i ett Excel‑diagram?

Läs in ditt diagram, aktivera datalabels och sätt `showValue`‑flaggan. Verktygstipset kommer då att visa det underliggande cellvärdet när en användare svävar över en datapunkt i den renderade Excel‑filen eller HTML‑vyn. Du kan också anpassa verktygstipsets teckensnitt, färg och bakgrund för att matcha din rapports stil.

Klassen `DataLabel` styr utseendet och innehållet i datalabels, som också fungerar som verktygstips.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Steg 4: lägga till interaktivitet

### 4.1. Lägga till verktygstips (lägg till verktygstips i diagram)

Verktygstips visas när användaren svävar över en datapunkt. Följande kod aktiverar datalabels och visar värdet som ett verktygstips.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Lägga till datalabels – **lägg till datalabels i excel‑diagram**

Datalabels ger en permanent visuell ledtråd i själva diagrammet. Du kan visa dem som anmärkningar för bättre läsbarhet.

Klassen `DataLabel` styr utseendet på etiketter för varje serie. Genom att anropa `setHasDataLabels(true)` och konfigurera egenskaper som `setShowValue(true)` bäddar du in det numeriska värdet direkt i diagrammet, vilket gör det omedelbart synligt utan någon interaktion. Ytterligare alternativ låter dig visa serienamn, procentsatser eller anpassad text för rikare sammanhang.

> **Varför lägga till datalabels?** Att inkludera datalabels direkt i diagrammet eliminerar behovet av att användare måste sväva eller gissa värden, vilket förbättrar rapportens tydlighet.

### 4.3. Implementera drill‑down (hyperlänk på en datapunkt)

Ett enkelt sätt att lägga till drill‑down‑funktionalitet är att bifoga en hyperlänk till en specifik punkt. När man klickar på punkten öppnas en webbsida med detaljerad information.

Klassen `Hyperlink` bifogar en klickbar länk till ett diagramelement, vilket möjliggör drill‑down‑navigering.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Hur man lägger till datalabels i ett Excel‑diagram?

Klassen `DataLabel` styr utseendet på etiketter för varje serie. Genom att anropa `setHasDataLabels(true)` och konfigurera egenskaper som `setShowValue(true)` bäddar du in det numeriska värdet direkt i diagrammet, vilket gör det omedelbart synligt utan någon interaktion. Ytterligare alternativ låter dig visa serienamn, procentsatser eller anpassad text för rikare sammanhang.

## Steg 5: spara arbetsboken

Efter att ha konfigurerat diagrammet, spara arbetsboken så att de interaktiva funktionerna lagras i utdatafilen.

Anropet `workbook.save` skriver den modifierade arbetsboken till en fil i det valda formatet.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Vanliga problem & lösningar

| Problem | Lösning |
|-------|----------|
| **Verktygstips visas inte** | Se till att `setHasDataLabels(true)` anropas innan `setShowValue(true)` konfigureras. |
| **Hyperlänk är inte klickbar** | Verifiera att utdataformatet stödjer hyperlänkar (t.ex. XLSX, inte CSV). |
| **Diagramtyp ändras inte** | Dubbelkolla att du ändrade rätt `ChartType`‑enum när du lade till diagrammet. |

## Vanliga frågor

**Q: Hur kan jag ändra diagramtypen efter att den skapats?**  
A: Du måste skapa ett nytt diagram med önskad `ChartType`. Aspose.Cells erbjuder ingen konvertering på plats, så ta bort det gamla diagrammet och lägg till ett nytt.

**Q: Kan jag anpassa verktygstipsens utseende?**  
A: Ja. Använd `DataLabel`‑egenskaper som `setFontSize`, `setFontColor` och `setBackgroundColor` för att formatera verktygstipstexten.

**Q: Hur hanterar jag användarinteraktioner i en webbapplikation?**  
A: Exportera arbetsboken till en HTML‑ eller XLSX‑fil och använd JavaScript på klientsidan för att fånga klickhändelser på diagramelement.

**Q: Var kan jag hitta fler exempel och dokumentation?**  
A: Besök [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) för en fullständig lista över diagramrelaterade klasser och metoder.

## Slutsats

Du vet nu hur du **lägger till datalabels i Excel‑diagram**, **ändrar Excel‑diagramtyp**, **skapar interaktiva diagram‑Java‑lösningar**, och berikar dem med verktygstips, datalabels och drill‑down‑hyperlänkar med Aspose.Cells för Java. Dessa förbättringar gör dina Excel‑rapporter mycket mer engagerande och insiktsfulla för slutanvändare.

---

**Senast uppdaterad:** 2026-08-21  
**Testad med:** Aspose.Cells for Java 24.12  
**Författare:** Aspose

## Relaterade handledningar

- [Hur man ändrar Excel-diagram och datalabels med Aspose.Cells för Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Extrahera Excel-diagramaxel‑etiketter med Aspose.Cells Java: En omfattande guide](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Skapa bubbeldiagram i Excel med Aspose.Cells för Java: En steg‑för‑steg‑guide](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}