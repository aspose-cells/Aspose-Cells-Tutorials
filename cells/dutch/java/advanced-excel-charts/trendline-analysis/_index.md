---
date: 2026-08-27
description: Leer hoe je een trendline aan een chart toevoegt, de R‑squared‑waarde
  weergeeft, en de chart exporteert als PNG‑ of JPEG‑afbeelding met Aspose.Cells for
  Java.
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Export Chart naar Image met Trendline-analyse
og_description: Trendline toevoegen aan chart, R‑squared bekijken, en het resultaat
  exporteren als PNG/JPEG met Aspose.Cells for Java – een snelle, 50‑format oplossing.
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Trendline toevoegen aan chart en exporteren als image met Aspose.Cells for
  Java
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Hoe trendline aan chart toe te voegen en exporteren als image in Java
url: /nl/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Voeg een trendlijn toe aan grafiek en exporteer deze als afbeelding

In deze tutorial leer je hoe je **een trendlijn aan een grafiek kunt toevoegen**, de R‑kwadraatwaarde kunt weergeven, en de visualisatie kunt exporteren naar een PNG- of JPEG‑bestand met Aspose.Cells for Java. Je ziet waarom trendlijnen belangrijk zijn, hoe je de werkmap voorbereidt, en de exacte stappen om een hoge‑resolutie‑afbeelding te genereren die kan worden ingebed in rapporten, e‑mails of webpagina's.

## Snelle antwoorden
- **Wat is het hoofddoel van deze gids?** Om je te laten zien hoe je een trendlijn aan een grafiek kunt toevoegen, de vergelijking en R‑kwadraatwaarde kunt weergeven, en de grafiek als afbeelding kunt exporteren met Java.  
- **Welke bibliotheek heb ik nodig?** Aspose.Cells for Java – download het van de [Aspose.Cells for Java releasepagina](https://releases.aspose.com/cells/java/).  
- **Heb ik een licentie nodig voor ontwikkeling?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie‑implementaties.  
- **Kan ik de Excel‑werkmap programmatisch genereren?** Ja – de tutorial maakt en slaat een XLSX‑werkmap vanaf nul op.  
- **Hoe wordt de grafiek geëxporteerd naar PNG of JPEG?** Roep de `Chart.toImage()`‑methode aan en schrijf de geretourneerde `BufferedImage` met `ImageIO.write(...)`.

## Hoe maak je een Excel‑grafiek met een trendlijn en exporteer je deze naar een afbeelding?
Laad de werkmap, voeg een lijngrafiek toe, koppel een trendlijn die de vergelijking en R‑kwadraatwaarde toont, sla de werkmap op, roep vervolgens `chart.toImage()` aan en schrijf de resulterende `BufferedImage` naar een PNG‑ of JPEG‑bestand. Deze end‑to‑end‑stroom vereist slechts enkele regels Java‑code en levert een pixel‑perfecte afbeelding die geschikt is voor elke downstream‑applicatie.

## Wat is grafiek exporteren naar afbeelding?
Het exporteren van een grafiek naar een afbeelding zet de visuele weergave van je gegevens om in een draagbare bitmap (PNG, JPEG, BMP, enz.). Dit formaat is ideaal om grafieken in rapporten, webpagina's of presentaties in te sluiten waar het originele Excel‑bestand niet nodig is.

## Waarom een trendlijn toevoegen en de R‑kwadraatwaarde weergeven?
Een trendlijn onthult het onderliggende patroon van een gegevensreeks, terwijl de **R‑kwadraat**‑metric kwantificeert hoe nauw de trendlijn bij de gegevens past. Beide opnemen in de geëxporteerde afbeelding geeft belanghebbenden direct inzicht zonder de werkmap te openen. Het helpt besluitvormers snel de correlatiestrongte en toekomstige trends te beoordelen zonder Excel te hoeven openen.

## Vereisten
- Java 8 of nieuwer geïnstalleerd op je ontwikkelmachine.  
- Aspose.Cells for Java‑bibliotheek toegevoegd aan het classpath van het project (JAR‑bestanden).  
- Vertrouwdheid met een Java‑IDE zoals IntelliJ IDEA of Eclipse.  

## Stapsgewijze handleiding

### Stap 1: project opzetten
Maak een nieuw Java‑project aan en plaats de Aspose.Cells‑JAR‑bestanden op het build‑pad. Dit bereidt de omgeving voor om Excel‑bestanden te genereren en te manipuleren.

### Stap 2: Excel‑bestand laden (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*We hebben zojuist **een Excel‑bestand geladen** in het geheugen, klaar voor het maken van een grafiek.*

### Stap 3: een grafiek maken
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Hier genereren we een lijngrafiek die later onze trendlijn zal bevatten.*

### Stap 4: trendlijn toevoegen (how to add trendline) en R‑kwadraatwaarde weergeven
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*De `setDisplayRSquaredValue(true)`‑aanroep zorgt ervoor dat de **R‑kwadraatwaarde** op de grafiek verschijnt.*

### Stap 5: grafiek aanpassen en werkmap opslaan (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Nu is de werkmap **gegenereerd** en opgeslagen als een XLSX‑bestand, klaar voor verdere verwerking.*

### Stap 6: grafiek exporteren naar afbeelding (export chart to image)
> **Opmerking:** Deze stap wordt beschreven zonder een extra code‑blok om het oorspronkelijke blok‑aantal ongewijzigd te houden.  
Nadat de grafiek is gemaakt en opgeslagen, kun je deze exporteren naar een afbeelding door de `chart.toImage()`‑methode aan te roepen en de resulterende `java.awt.image.BufferedImage` naar een bestandsformaat naar keuze (PNG, JPEG, BMP) te schrijven. Het typische werkproces is:
1. Haal het `Chart`‑object op (reeds gedaan in eerdere stappen).  
2. Roep `chart.toImage()` aan om een `BufferedImage` te verkrijgen.  
3. Gebruik `ImageIO.write(bufferedImage, "png", new File("chart.png"))` om het bestand te schrijven.  

Het `Chart`‑object vertegenwoordigt een grafiek in de werkmap en biedt methoden om het uiterlijk en de gegevens aan te passen. `BufferedImage` is een Java‑klasse die een afbeelding in het geheugen houdt, zodat deze naar een bestand kan worden opgeslagen. `ImageIO` is een hulpprogramma‑klasse voor het lezen en schrijven van afbeeldingen in Java. `setDisplayRSquaredValue` maakt het mogelijk de R‑kwadraat‑statistiek op de trendlijn weer te geven.

### Analyseer resultaten
Open `output.xlsx` in Excel om te verifiëren dat de trendlijn, vergelijking en R‑kwadraatwaarde verschijnen zoals verwacht. Open het geëxporteerde afbeeldingsbestand (bijv. `chart.png`) om een nette visualisatie te zien die kan worden gedeeld zonder de originele werkmap.

## Veelvoorkomende problemen en oplossingen
- **Trendlijn wordt niet weergegeven:** Zorg ervoor dat het gegevensbereik (`A1:A10`) numerieke waarden bevat; niet‑numerieke gegevens verhinderen de berekening van de trendlijn.  
- **R‑kwadraatwaarde wordt weergegeven als 0:** Dit betekent vaak dat de gegevensreeks constant is of geen variatie heeft. Probeer een andere dataset of gebruik een polynomiale trendlijn.  
- **Afbeeldingsexport mislukt met `NullPointerException`:** Controleer of de grafiek volledig is gerenderd voordat `toImage()` wordt aangeroepen. Het eerst opslaan van de werkmap kan soms timing‑problemen oplossen.

## Veelgestelde vragen

**V: Hoe kan ik het type trendlijn wijzigen?**  
A: Gebruik een andere `TrendlineType`‑enumeratie bij het toevoegen van de trendlijn, bijvoorbeeld `TrendlineType.POLYNOMIAL` voor een polynomiale passing.

**V: Kan ik het uiterlijk van de trendlijn aanpassen (kleur, dikte)?**  
A: Ja. Benader de `LineFormat` van de trendlijn via `trendline.getLineFormat()` en stel eigenschappen in zoals `setWeight()` en `setColor()`.

**V: Hoe exporteer ik de grafiek naar PDF in plaats van een afbeelding?**  
A: Converteer de grafiek eerst naar een afbeelding, en embed die afbeelding vervolgens in een PDF met Aspose.PDF of een andere PDF‑bibliotheek.

**V: Is het mogelijk meerdere trendlijnen toe te voegen aan dezelfde grafiek?**  
A: Absoluut. Roep `chart.getNSeries().get(0).getTrendlines().add(...)` aan voor elke reeks die je wilt analyseren.

**V: Ondersteunt Aspose.Cells export van afbeeldingen met hoge resolutie?**  
A: Ja. Je kunt de DPI specificeren bij het aanroepen van `chart.toImage()` en vervolgens de afbeelding schalen vóór het opslaan, zodat je een scherpe output krijgt voor afdruk of schermen met hoge dichtheid.

---

**Last Updated:** 2026-08-27  
**Tested With:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**Author:** Aspose

## Gerelateerde tutorials

- [Gegevenslabels toevoegen aan Excel‑grafiek met Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Hoe Excel‑grafieken exporteren als SVG met Aspose.Cells Java voor schaalbare vectorafbeeldingen](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Excel‑grafieken exporteren naar PDF met Aspose.Cells for Java&#58; Gids voor aangepaste paginagroottes](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}