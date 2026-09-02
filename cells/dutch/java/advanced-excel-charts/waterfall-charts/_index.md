---
date: 2026-09-02
description: Leer hoe u een Excel-watervalgrafiek maakt in Java met Aspose.Cells,
  stel het gegevensbereik van de grafiek in, pas labels aan en exporteer naar XLSX.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Watervalgrafieken
og_description: Maak een Excel-watervalgrafiek met Aspose.Cells voor Java – stel het
  gegevensbereik van de grafiek in, voeg gegevenslabels toe en exporteer naar XLSX
  in enkele stappen.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Maak een Excel-watervalgrafiek met Aspose.Cells voor Java
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Maak een Excel-watervalgrafiek met Aspose.Cells voor Java
url: /nl/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Watervalgrafieken

## Introductie tot watervalgrafieken met Aspose.Cells voor Java

In deze tutorial leer je hoe je een **excel watervalgrafiek** maakt en **de gegevensreeks van de grafiek** instelt met Aspose.Cells voor Java. Watervalgrafieken zetten een reeks positieve en negatieve getallen om in een duidelijk visueel verhaal, waardoor ze ideaal zijn voor financiële overzichten, verkoopprestatie‑evaluaties en elke situatie waarin je wilt zien hoe individuele items bijdragen aan een totaal.

## Snelle antwoorden
- **Wat is een watervalgrafiek?** Een visualisatie die laat zien hoe een initiële waarde wordt verhoogd en verlaagd door een reeks tussenliggende waarden, eindigend met een eindtotaal.  
- **Welke bibliotheek wordt gebruikt?** Aspose.Cells voor Java.  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Kan ik het bestand opslaan als XLSX?** Ja – gebruik `workbook.save("FileName.xlsx")`.  
- **Is het geschikt voor Java‑datavisualisatie?** Absoluut; Aspose.Cells biedt rijke grafiekfuncties zonder dat Office geïnstalleerd hoeft te zijn.

## Wat is een watervalgrafiek?
Een watervalgrafiek toont opeenvolgende positieve en negatieve bijdragen aan een startwaarde, waardoor je begrijpt hoe elk onderdeel het eindresultaat beïnvloedt. Door winsten en verliezen naast elkaar te visualiseren, maakt het complexe financiële stromingen direct leesbaar.

## Waarom Aspose.Cells voor Java gebruiken om een watervalgrafiek toe te voegen?
Aspose.Cells stelt je in staat Excel‑grafieken te genereren op elke server, CI‑pipeline of desktop zonder Microsoft Excel. Het ondersteunt **15+ uitvoerformaten** (XLSX, PDF, HTML, CSV en meer), verwerkt werkboeken met **500+ rijen** in minder dan een seconde, en biedt programmatische controle over elk grafiekelement – van kleuren tot gegevenslabels.

## Vereisten

Voordat we in de code duiken, zorg ervoor dat je de volgende vereisten hebt:

- Aspose.Cells voor Java: Je moet Aspose.Cells voor Java geïnstalleerd hebben. Je kunt het downloaden vanaf de Aspose.Cells voor Java release‑pagina: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Java‑ontwikkelomgeving: Zorg ervoor dat Java op je systeem is geïnstalleerd en dat je een build‑tool (Maven/Gradle) klaar hebt staan.

Laten we nu stap voor stap beginnen met het maken van de watervalgrafiek.

## Hoe stel je het gegevensbereik van een watervalgrafiek in Java in
Laad een nieuw werkboek, vul het met gegevens, voeg een `Chart`‑object toe, definieer het reeks‑bereik en sla ten slotte het bestand op. Dit proces is eenvoudig: je maakt een werkboek, vult cellen met categorieën en waarden, maakt een grafiek, bindt de gegevensreeksen, en exporteert vervolgens het werkboek. Het resultaat is een volledig functionele watervalgrafiek klaar voor gebruik in rapporten of dashboards.

### Stap 1: import Aspose.Cells
Het `com.aspose.cells`‑pakket bevat alle klassen die nodig zijn voor Excel‑manipulatie, inclusief het maken van werkboeken, het verwerken van werkbladen en het genereren van grafieken.

### Stap 2: initialiseer workbook en worksheet
Een **Workbook** vertegenwoordigt een Excel‑bestand, en een **Worksheet** is een enkel blad binnen dat bestand. Het aanmaken van deze objecten biedt het canvas voor zowel ruwe gegevens als de grafiek.

### Stap 3: voer gegevens in
Kolom A bevat de categorielabels, terwijl kolom B de numerieke waarden voor de watervalgrafiek bevat. Deze indeling komt overeen met de typische winst‑en‑verliesstroom die in financiële analyses wordt gebruikt.

### Stap 4: maak de watervalgrafiek
Het **Chart**‑object creëert een visuele weergave; door het type in te stellen op `ChartType.WATERFALL` configureer je het als een watervalgrafiek. Gebruik de `add`‑methode om het gegevensbereik voor de reeks in te stellen (`"B2:B6"`), en koppel de categorische as aan `"A2:A6"`.

### Stap 5: sla het workbook op
Het opslaan van het werkboek schrijft de grafiek en gegevens naar het opgegeven bestandsformaat. Roep `workbook.save("WaterfallChart.xlsx")` aan om een XLSX‑bestand te genereren, of wijzig de format‑parameter om te exporteren naar PDF, CSV of HTML.

## Veelvoorkomende problemen en oplossingen

- **Chart appears blank** – Controleer of de gegevensbereik‑referenties (`B2:B6` en `A2:A6`) overeenkomen met de daadwerkelijke cellen die je waarden en categorieën bevatten.  
- **Negative values not displayed correctly** – Zorg ervoor dat het type reeks is ingesteld op `ChartType.WATERFALL`; andere grafiektype behandelen negatieve waarden anders.  
- **File not opening in Excel** – Gebruik de nieuwste Aspose.Cells‑release en bevestig dat de bestandsextensie overeenkomt met het formaat (`.xlsx` voor Excel).

## Veelgestelde vragen

### Hoe kan ik het uiterlijk van mijn watervalgrafiek aanpassen?
Je kunt eigenschappen wijzigen zoals `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` om de balkkleuren te veranderen, gegevenslabels inschakelen met `setShowDataLabels(true)`, en as‑titels aanpassen via `getCategoryAxis().setTitle("Stage")`. De Aspose.Cells API‑referentie biedt een volledige lijst van configureerbare opties.

### Kan ik meerdere watervalgrafieken in hetzelfde werkblad maken?
Ja. Nadat je de eerste grafiek hebt toegevoegd, herhaal je de stappen voor het maken van een grafiek met een ander gegevensbereik en een nieuw `Chart`‑object. Elke grafiek is onafhankelijk en kan overal op het blad worden geplaatst.

### Is Aspose.Cells compatibel met verschillende Java‑ontwikkelomgevingen?
Absoluut. De bibliotheek werkt met Eclipse, IntelliJ IDEA, NetBeans en elk buildsysteem dat Maven of Gradle ondersteunt. Er zijn geen extra plug‑ins vereist.

### Kan ik extra gegevensreeksen toevoegen aan mijn watervalgrafiek?
Je kunt meer reeksen toevoegen door `chart.getNSeries().add("C2:C6", true)` aan te roepen en elke reeks afzonderlijk te configureren. Hiermee kun je meerdere scenario’s naast elkaar vergelijken.

### Waar kan ik meer bronnen en voorbeelden vinden voor Aspose.Cells voor Java?
Verken de volledige documentatie op de Aspose.Cells Java API‑referentie: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q: Hoe stel ik het gegevensbereik van een financiële watervalgrafiek in?**  
A: Gebruik de `add`‑methode op de reeksen van de grafiek en geef het celbereik op dat je waarden bevat, bijvoorbeeld `"B2:B6"`.

**Q: Kan ik het werkboek exporteren naar PDF in plaats van XLSX?**  
A: Ja, roep `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` aan om een PDF‑versie te genereren.

**Q: Wat als ik een watervalgrafiek met meer categorieën moet maken?**  
A: Breid het gegevensbereik uit in zowel de waardekolom als de categoriekolom, en werk vervolgens de `add`‑ en `setCategoryData`‑aanroepen bij.

**Q: Is er een manier om positieve en negatieve balken automatisch te formatteren?**  
A: Loop door de `Series`‑collectie en stel de `FillFormat`‑kleur in op basis van het teken van elke waarde; Aspose.Cells laat je conditionele opmaak programmatisch toepassen.

**Q: Ondersteunt Aspose.Cells dynamische gegevensupdates voor grafieken?**  
A: Ja. Na het wijzigen van celwaarden hoef je alleen het werkboek opnieuw op te slaan – de grafiek zal automatisch de nieuwe gegevens weergeven.

---

**Last Updated:** 2026-09-02  
**Tested with:** Aspose.Cells voor Java (latest)  
**Author:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## Gerelateerde tutorials

- [Pas Excel‑grafiekgegevenslabels aan met Aspose.Cells voor Java: Een stapsgewijze handleiding](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Gegevenslabels toevoegen aan Excel‑grafiek met Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Hoe grafieken te maken en exporteren in Java met Aspose.Cells: Een volledige gids](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}