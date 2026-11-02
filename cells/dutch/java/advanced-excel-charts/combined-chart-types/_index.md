---
date: 2026-09-02
description: Leer hoe u een grafiek exporteert naar PNG, een gegevensreeks toevoegt,
  een lijngrafiek en kolomgrafiek combineert, een werkmap opslaat als XLSX en een
  legenda toevoegt met behulp van Aspose.Cells for Java.
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: Export grafiek naar PNG en voeg gegevensreeks toe voor gecombineerde grafiek
og_description: Export grafiek naar PNG met Aspose.Cells for Java, combineer lijn-
  en kolomgrafiek, voeg gegevensreeks toe en sla de werkmap op als XLSX in één tutorial.
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: Export grafiek naar PNG en voeg gegevensreeks toe voor gecombineerde grafiek
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
title: Export grafiek naar PNG en voeg gegevensreeks toe voor gecombineerde grafiek
url: /nl/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiek exporteren naar PNG en gegevensreeksen toevoegen voor gecombineerde grafiek

In deze tutorial **voegt u gegevensreeksen** toe aan een Excel-werkmap, **combineert u lijn- en kolomgrafiek**-elementen, en leert u hoe u **grafiek exporteert naar PNG** met Aspose.Cells for Java. We lopen elke stap door—van het instellen van de werkmap, het toevoegen van de grafiek aan een werkblad, het aanpassen van de legenda, tot **het opslaan van de werkmap als XLSX** en het genereren van een PNG-afbeelding van de grafiek. Aan het einde heeft u een kant-en-klare gecombineerde grafiek die u kunt insluiten in rapporten of dashboards.

## Snelle antwoorden
- **Welke bibliotheek maakt gecombineerde grafieken?** Aspose.Cells for Java.  
- **Hoe voeg ik een gegevensreeks toe?** Call `chart.getNSeries().add(...)` with the appropriate range.  
- **Hoe kan ik de grafiek exporteren naar PNG?** Use `chart.toImage("chart.png", ImageFormat.getPng())`.  
- **In welk bestandsformaat kan ik de werkmap opslaan?** Standard `.xlsx` (save workbook as XLSX).  
- **Heb ik een licentie nodig voor productie?** Yes – a valid Aspose.Cells license is required for production deployments.

## Wat is grafiek exporteren naar PNG in Aspose.Cells?

Het exporteren van een grafiek naar PNG maakt een rasterafbeelding van de Excel-grafiek die kan worden weergegeven in webpagina's, rapporten of e‑mails zonder dat de Excel‑applicatie nodig is. Deze methode legt de exacte visuele lay-out, kleuren en gegevensmarkeringen vast, waardoor een draagbaar afbeeldingsbestand ontstaat.

## Waarom een gecombineerde lijn‑kolomgrafiek maken?

Een gecombineerde lijn‑kolomgrafiek stelt u in staat verschillende datasets met verschillende visuele weergaven (bijv. een lijnreeks boven een kolomreeks) in één weergave te tonen. Deze aanpak is ideaal om trends te vergelijken met totalen, correlaties te benadrukken, of rijkere inzichten te leveren terwijl de visuele voetafdruk klein blijft.

## Vereisten
- Java Development Kit (JDK) 8 of hoger  
- Aspose.Cells for Java bibliotheek (download van de onderstaande link)  
- Basiskennis van Java-syntaxis en Excel-concepten  

## Aan de slag

Download eerst de Aspose.Cells for Java bibliotheek van de officiële site:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Zodra de JAR aan de classpath van uw project is toegevoegd, kunt u beginnen met het bouwen van de grafiek.

### Stap 1: importeer aspose.cells klassen
`Workbook` is het kernobject van Aspose.Cells dat een volledige Excel‑bestand in het geheugen vertegenwoordigt.  
```java
import com.aspose.cells.*;
```

### Stap 2: maak een nieuwe werkmap
`Worksheet` vertegenwoordigt een enkel blad binnen een `Workbook` en biedt toegang tot cellen, rijen en grafieken.  
```java
Workbook workbook = new Workbook();
```

### Stap 3: krijg toegang tot het eerste werkblad
`Chart` is het object dat alle grafiek‑gerelateerde instellingen, reeksen en renderopties bevat.  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Stap 4: voeg een gecombineerd grafiekobject toe aan het werkblad  
We beginnen met een lijngrafiek en voegen later een kolomreeks toe om een **gecombineerde lijn‑kolomgrafiek** effect te bereiken.  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Gegevens toevoegen aan de grafiek

Nu de grafiekcontainer bestaat, moeten we deze van gegevens voorzien.

### Stap 5: definieer de gegevensbereiken en voeg gegevensreeksen toe
`NSeries` is de collectie die elke gegevensreeks voor een grafiek opslaat. Het toevoegen van een reeks koppelt een bereik van cellen aan de grafiek.  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** De eerste parameter (`"A1:A5"`) is het bereik voor de eerste reeks, en de tweede (`"B1:B5"`) maakt een tweede reeks die met de eerste wordt gecombineerd.

### Stap 6: stel de categoriedata (X‑as) in
`CategoryAxis` vertegenwoordigt de horizontale as van de grafiek en regelt de labels die langs de X‑as worden weergegeven.  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## De grafiek aanpassen

Een goede grafiek vertelt een verhaal. Laten we deze titels, aslabels en een duidelijke legenda geven.

### Stap 7: stel aslabels en titel van de grafiek in
`Title` stelt de hoofdtitel van de grafiek in, en `Axis`‑objecten vertegenwoordigen de X‑ en Y‑assen.  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Stap 8: voeg een legenda toe aan de grafiek en pas de positie aan
`Legend` regelt de plaatsing en het uiterlijk van de reeksenlegenda in de grafiek.  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## De grafiek opslaan en exporteren

Na het aanpassen wilt u **de werkmap opslaan als XLSX** en ook een afbeelding genereren.

### Stap 9: sla de werkmap op als een Excel‑bestand (XLSX)
`Workbook.save` schrijft de in‑geheugen werkmap naar een bestand in het opgegeven formaat.  
```java
workbook.save("CombinedChart.xlsx");
```

### Stap 10: exporteer grafiek naar PNG
`Chart.toImage` rendert de grafiek als een afbeeldingsbestand in het gekozen formaat.  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> De `chart.toImage`‑methode **genereert Excel‑grafiek**‑afbeeldingen die kunnen worden gebruikt in webpagina's, rapporten of e‑mails.

## Veelvoorkomende problemen & foutopsporing

| Probleem | Oplossing |
|----------|-----------|
| **Geen gegevens zichtbaar** | Controleer of de celbereiken (`A1:A5`, `B1:B5`, `C1:C5`) daadwerkelijk gegevens bevatten voordat u de grafiek maakt. |
| **Legenda overlapt grafiek** | Stel `chart.getLegend().setOverlay(false)` in of verplaats de legenda naar een andere positie (bijv. `RIGHT`). |
| **Afbeeldingsbestand is leeg** | Zorg ervoor dat de grafiek minstens één reeks heeft en dat `chart.toImage` wordt aangeroepen na alle aanpassingen. |
| **Opslaan geeft een uitzondering** | Controleer of u schrijfrechten heeft voor de doelmap en dat het bestand niet geopend is in Excel. |

## Veelgestelde vragen

**Q: Hoe installeer ik Aspose.Cells for Java?**  
A: Download de JAR van de officiële site en voeg deze toe aan de classpath van uw project. De downloadlink is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Kan ik andere grafiektype maken naast lijn en kolom?**  
A: Ja, Aspose.Cells ondersteunt staaf-, taart-, spreidings-, gebieds- en vele andere grafiektype. Raadpleeg de API‑documentatie voor de volledige lijst.

**Q: Is een licentie vereist voor productiegebruik?**  
A: Een geldige Aspose.Cells‑licentie is vereist voor productie‑implementaties. Een gratis proefversie is beschikbaar voor evaluatie.

**Q: Hoe kan ik de kleuren van elke reeks wijzigen?**  
A: Gebruik `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (of iets dergelijks) na het toevoegen van de reeks.

**Q: Waar kan ik meer code‑voorbeelden vinden?**  
A: Uitgebreide documentatie en extra voorbeelden zijn beschikbaar op de Aspose‑referentiesite: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).

---

**Laatst bijgewerkt:** 2026-09-02  
**Getest met:** Aspose.Cells for Java latest version  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Hoe labels toe te voegen aan Excel‑grafieken met Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [Hoe een Excel‑grafiek te maken met trendlijn en te exporteren naar afbeelding met Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Excel‑grafieken exporteren naar PDF met Aspose.Cells for Java: Gids voor aangepaste paginagroottes](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}