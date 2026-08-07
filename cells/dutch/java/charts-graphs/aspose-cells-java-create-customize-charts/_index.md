---
date: '2026-04-08'
description: Leer hoe je een kolomgrafiek genereert in Java met Aspose.Cells, inclusief
  het maken van een grafiek in Java, het toevoegen van een grafiekblad en het exporteren
  van een Excel-werkmap.
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Kolomgrafiek genereren met Aspose.Cells Java‑tutorial
url: /nl/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Kolomdiagram genereren met Aspose.Cells Java

In de hedendaagse data‑gedreven applicaties kan **het genereren van een kolomdiagram** snel en programmatisch ruwe cijfers omzetten in duidelijke visuele inzichten. Of je nu een rapportagedashboard, een analysetool of een eenvoudige exportfunctie bouwt, Aspose.Cells for Java biedt je een vloeiende API om **chart java** projecten te maken zonder met de Excel UI te werken. In deze tutorial leer je hoe je de bibliotheek instelt, **Excel‑cellen vult**, een **chart‑blad** toevoegt, de **chart‑titel** aanpast, en uiteindelijk **workbook excel exporteert** naar een bestand.

## Snelle antwoorden
- **Wat betekent “generate column chart”?** Het maakt een verticale staaf‑type visualisatie van tabelgegevens.  
- **Welke bibliotheek is vereist?** Aspose.Cells for Java (gratis proefversie beschikbaar).  
- **Heb ik een Excel‑installatie nodig?** Nee, de bibliotheek werkt onafhankelijk van Microsoft Excel.  
- **Kan ik exporteren naar andere formaten dan XLS?** Ja – PDF, PNG, SVG, enz., via `workbook.save()`.  
- **Is een licentie verplicht voor productie?** Ja, een aangeschafte of tijdelijke licentie is vereist.

## Wat is een generate column chart?
Een kolomdiagram toont dataseries als verticale balken, waardoor het eenvoudig is om waarden over categorieën zoals regio's, maanden of productlijnen te vergelijken. Aspose.Cells stelt je in staat dit diagram volledig in code te bouwen, waardoor je volledige controle hebt over gegevens, opmaak en uitvoerformaat.

## Waarom Aspose.Cells gebruiken om chart java te maken?
- **Geen COM‑interop** – werkt op elk OS met een JVM.  
- **Rijke opmaakopties** – afbeeldingen, verlopen, legenda's en aangepaste lettertypen.  
- **Hoge prestaties** – geschikt voor grote datasets.  
- **Meerdere exportformaten** – XLS, XLSX, PDF, PNG en meer.

## Vereisten
- **Java Development Kit (JDK) 8+** geïnstalleerd.  
- Basiskennis van Java en vertrouwdheid met Excel‑concepten.

### Vereiste bibliotheken
Voeg Aspose.Cells toe aan je project met een van de onderstaande codefragmenten.

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Licentie‑acquisitie
Aspose biedt een gratis proefversie en een tijdelijke licentie voor uitgebreid testen.

- **Gratis proefversie**: [Gratis downloaden](https://releases.aspose.com/cells/java/)  
- **Tijdelijke licentie**: [Hier aanvragen](https://purchase.aspose.com/temporary-license/)

## Aspose.Cells voor Java instellen

Maak eerst een `Workbook`‑instantie – dit wordt het canvas voor onze gegevens en diagram.

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## Stapsgewijze handleiding

### 1. Maak en benoem een werkblad
We slaan de ruwe gegevens op in een blad met de naam **Data**.

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Excel‑cellen vullen
Voeg regiogebieden en verkoopcijfers in die het kolomdiagram zal visualiseren.

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. Chart‑blad toevoegen
Het scheiden van het diagram van de ruwe gegevens houdt de werkmap overzichtelijk.

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. Kolomdiagram maken
Nu maken we daadwerkelijk **generate column chart** objecten.

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. Afbeelding instellen als achtergrondvulling in plotgebied
Een achtergrondafbeelding kan het diagram laten opvallen.

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. Diagramtitel instellen
Het aanpassen van de **set chart title** verbetert de leesbaarheid.

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. Seriesgegevens en legenda configureren
Koppel het gegevensbereik aan het diagram en positioneer de legenda.

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. Workbook Excel exporteren
Tot slot **export workbook excel** naar een XLS‑bestand (of een ander ondersteund formaat).

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## Praktische toepassingen
- **Business Reports** – Auto‑genereer verkoopdiagrammen voor maandelijkse PDF’s.  
- **Data Analysis Tools** – Integreer dynamische diagrammen in aangepaste analytics‑dashboards.  
- **Enterprise Dashboards** – Vernieuw diagramafbeeldingen direct voor realtime monitoring.

## Prestatieoverwegingen
- Voer batch‑updates van cellen uit bij grote datasets om overhead te verminderen.  
- Maak bronnen vrij (`workbook.dispose()`) als je veel werkmappen in een lus verwerkt.

## Veelvoorkomende problemen en oplossingen
- **Afbeelding wordt niet weergegeven** – Controleer het bestandspad en of het afbeeldingsformaat (PNG, JPEG) wordt ondersteund.  
- **Diagram verschijnt leeg** – Zorg ervoor dat de gegevensbereik‑referenties (`Data!B2:B8`) overeenkomen met de ingevulde cellen.  
- **Out‑of‑memory‑fouten** – Verwerk gegevens in delen en roep `System.gc()` aan na grote opslagen.

## Veelgestelde vragen

**Q: Hoe voeg ik meerdere series toe aan een kolomdiagram?**  
A: Roep `chart.getNSeries().add()` herhaaldelijk aan met verschillende gegevensbereiken, bijv. `"Data!C2:C8"` voor een tweede serie.

**Q: Kan ik de as‑labels wijzigen?**  
A: Ja. Gebruik `chart.getCategoryAxis().setTitle("Regions")` en `chart.getValueAxis().setTitle("Sales")`.

**Q: Naar welke formaten kan ik exporteren naast XLS?**  
A: Gebruik `workbook.save("chart.pdf")`, `workbook.save("chart.png")` of `workbook.save("chart.xlsx")` voor respectievelijk PDF, PNG en XLSX.

**Q: Is een licentie vereist voor ontwikkel‑builds?**  
A: Een gratis proefversie werkt voor evaluatie, maar een permanente of tijdelijke licentie is nodig voor productie‑implementaties.

**Q: Hoe kan ik de render‑snelheid verbeteren voor duizenden rijen?**  
A: Vul cellen in met `cells.importArray()` en minimaliseer diagramhertekeningen door het diagram pas te maken nadat alle gegevens zijn geladen.

---

**Laatst bijgewerkt:** 2026-04-08  
**Getest met:** Aspose.Cells 25.3 for Java  
**Auteur:** Aspose  

## Bronnen

- [Aspose.Cells-documentatie](https://reference.aspose.com/cells/java/)
- [Aspose.Cells downloaden](https://releases.aspose.com/cells/java/)
- [Licentie aanschaffen](https://purchase.aspose.com/buy)
- [Gratis proefversie](https://releases.aspose.com/cells/java/)
- [Tijdelijke licentie aanvragen](https://purchase.aspose.com/temporary-license/)
- [Supportforum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}