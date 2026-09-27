---
date: '2026-09-27'
description: Leer hoe je een pie chart in Java maakt met Aspose.Cells. Stapsgewijze
  handleiding om een Excel pie chart aan te passen, een Maven‑dependency in te stellen
  en professionele diagrammen te genereren.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Maak een pie chart in Java met Aspose.Cells voor Java. Leer hoe je
  een Excel pie chart aanpast, een Maven‑dependency toevoegt en binnen enkele minuten
  professionele diagrammen genereert.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Maak een pie chart in Java met Aspose.Cells – Volledige Java‑gids
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Hoe maak je een pie chart in Java met Aspose.Cells
url: /nl/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe maak je een taartdiagram in Java met Aspose.Cells

## Inleiding
Het programmatically maken van een **pie chart** voelt vaak als een puzzel, vooral wanneer je fijne controle over kleuren, legenda's en titels nodig hebt. In deze gids leer je hoe je **create pie chart java** gebruikt met Aspose.Cells, en vervolgens het Excel‑taartdiagram aanpast aan je merk of rapportagestijl. We lopen door de omgeving‑configuratie, het vullen van data, het genereren van het diagram en visuele aanpassingen — alles zonder je Java‑IDE te verlaten.

**Wat je zult leren**
- Voeg de **Maven dependency Aspose.Cells** toe aan je project.
- Maak een werkmap, vul cellen met data en genereer een taartdiagram.
- Pas aangepaste kleuren, titels en legenda's toe op het diagram.
- Exporteer de werkmap naar een XLSX‑bestand klaar om te delen.

Voordat je begint, moet je vertrouwd zijn met basis Java‑syntaxis en Maven of Gradle geïnstalleerd hebben.

## Snelle antwoorden
- **Welke bibliotheek maakt taartdiagrammen in Java?** Aspose.Cells for Java.
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een betaalde licentie is vereist voor productie.
- **Welke Maven‑coördinaten zijn vereist?** `com.aspose:aspose-cells:24.10`.
- **Kan ik de kleuren van de segmenten wijzigen?** Ja, via de `setAreaColor`‑methode op elke serie.
- **Kan het diagram worden geëxporteerd naar XLSX?** Absoluut — roep gewoon `workbook.save("output.xlsx")` aan.

## Wat is een taartdiagram in Excel?
Een taartdiagram visualiseert een enkele gegevensreeks als proportionele segmenten van een cirkel, waardoor het gemakkelijk is om delen van een geheel te vergelijken. Elke segmenthoek komt overeen met zijn waarde ten opzichte van het totaal, waardoor je snel inzicht krijgt in de verdeling over categorieën zoals marktaandeel, budgettoewijzing of demografische percentages.

## Waarom Aspose.Cells gebruiken om een taartdiagram in Java te maken?
Aspose.Cells ondersteunt meer dan 50 diagramtypen en kan werkbladen met tot één miljoen rijen verwerken zonder het volledige bestand in het geheugen te laden. Dit prestatievoordeel stelt je in staat om grote rapporten te genereren op bescheiden hardware, terwijl je fijne controle hebt over de weergave van het diagram, gegevensbinding en exportformaten, waardoor het een superieure keuze is ten opzichte van veel open‑source bibliotheken.

## Vereisten
- **Java Development Kit (JDK)** 8 of nieuwer.
- **IDE** zoals IntelliJ IDEA of Eclipse.
- **Maven** of **Gradle** voor afhankelijkheidsbeheer.
- Een **trial‑ of gekochte Aspose.Cells‑licentie**.

### Vereiste bibliotheken en afhankelijkheden
Voeg het Aspose.Cells Maven‑artifact toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Of het Gradle‑equivalent:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Stappen voor het verkrijgen van een licentie
Aspose.Cells for Java is commercieel, maar je kunt beginnen met een gratis proefversie. Bezoek de [purchase page](https://purchase.aspose.com/buy) om een tijdelijke licentiesleutel te verkrijgen.

## Aspose.Cells voor Java instellen
Zorg er eerst voor dat de bibliotheek op je classpath staat. Na het toevoegen van de afhankelijkheid kun je de API initialiseren zoals hieronder weergegeven.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Implementatie‑gids

### Maak en configureer een werkmap
De `Workbook`‑klasse vertegenwoordigt een volledig Excel‑bestand in het geheugen.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Stap 1: een werkmap instantieren
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Dit maakt een nieuwe, lege werkmap die je meteen kunt beginnen te vullen.

### Toegang tot of wijziging van werkbladcellen
Een `Worksheet` vertegenwoordigt een enkel blad binnen de werkmap, met cellen, rijen en kolommen.  
Je schrijft de gegevens die het taartdiagram aandrijven naar een werkblad.

#### Stap 2: haal het eerste werkblad en de cellen op
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Vul de cellen met categorienamen en waarden die het diagram zal gebruiken.

### Maak een taartdiagram
`Chart`‑objecten visualiseren gegevens in een werkblad en ondersteunen verschillende typen zoals taart, kolom en lijn.

#### Stap 3: voeg een taartdiagram toe aan het werkblad
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Configureer taartdiagram‑series en gegevens
`Series` definieert het gegevensbereik en de opmaak voor een diagram, waarbij werkbladcellen worden gekoppeld aan visuele elementen.

#### Stap 4: stel de series in voor het diagram
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Configureer weergave van diagramlegenda en -titel
Een diagram `Legend` toont de namen van de series en kleuren, waardoor lezers elk segment kunnen identificeren.

#### Stap 5: pas diagramlegenda en -titel aan
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Pas kleuren van diagramseries aan
`setAreaColor` stelt de vulkleur van een diagramserie‑segment in met een RGB‑waarde.

#### Stap 6: wijzig de kleuren van taartsegmenten
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Kolommen automatisch aanpassen en werkmap opslaan
`autoFitColumns` past automatisch de kolombreedtes aan zodat ze passen bij de celinhoud.

#### Stap 7: pas kolombreedtes aan en sla het bestand op
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Veelvoorkomende gebruikssituaties
- **Demografische analyse:** Toon de bevolkingsverdeling over regio's.
- **Marktaandeelrapportage:** Visualiseer het aandeel van elke concurrent in één oogopslag.
- **Budgettoewijzing:** Benadruk hoe fondsen worden verdeeld over afdelingen.

## Prestatieoverwegingen
- Vrijgeven van objecten (`workbook.dispose()`) wanneer ze niet meer nodig zijn om native geheugen vrij te maken.
- Voor enorme datasets, gebruik `WorkbookDesigner` om gegevens te streamen in plaats van alles in één keer te laden.
- Profiel met Java Flight Recorder om eventuele knelpunten in de diagramgeneratie te ontdekken.

## Veelgestelde vragen

**Q: Kan ik meerdere taartdiagrammen in dezelfde werkmap genereren?**  
A: Ja, herhaal de stappen voor het maken van diagrammen voor elk gegevensbereik; elk diagram is onafhankelijk.

**Q: Ondersteunt Aspose.Cells 3‑D taartdiagrammen?**  
A: Ja; stel het diagramtype in op `ChartType.PIE_3D` bij het toevoegen van het diagram.

**Q: Hoe pas ik een aangepast thema toe op alle diagrammen?**  
A: Gebruik de `Workbook.setDefaultTheme`‑methode voordat je diagrammen maakt.

**Q: Naar welke bestandsformaten kan ik de werkmap exporteren?**  
A: Meer dan 30 formaten, waaronder XLSX, CSV, PDF en HTML.

**Q: Is een licentie vereist voor commerciële inzet?**  
A: Ja, een geldige licentie verwijdert evaluatiewatermerken en ontgrendelt de volledige functionaliteit.

## Conclusie
Je hebt nu een volledige, end‑to‑end handleiding voor **create pie chart java** met Aspose.Cells. Door de bovenstaande stappen te volgen kun je gepolijste Excel‑taartdiagrammen genereren, kleuren en titels aanpassen, en ze in elke rapportage‑pipeline integreren. Verken andere diagramtypen — kolom, lijn, radar — om je data‑visualisatietoolkit uit te breiden.

---

**Laatst bijgewerkt:** 2026-09-27  
**Getest met:** Aspose.Cells 24.10 for Java  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Excel-diagramgegevenslabels aanpassen met Aspose.Cells voor Java&#58; Een stapsgewijze handleiding](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Dynamische Excel-diagrammen maken met Aspose.Cells Java&#58; Een uitgebreide gids voor ontwikkelaars](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Excel-werkboeken maken en aanpassen met Aspose.Cells Java&#58; Een stapsgewijze handleiding](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}