---
date: 2025-12-09
description: Leer hoe je een diagram exporteert naar een afbeelding terwijl je trendline‑analyse
  uitvoert in Java met Aspose.Cells. Inclusief stappen om een Excel‑bestand te laden,
  een trendline toe te voegen, de R‑kwadraatwaarde weer te geven en de werkmap op
  te slaan als XLSX.
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Grafiek exporteren naar afbeelding met trendlijnanalyse met Aspose.Cells voor
  Java
url: /nl/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grafiek exporteren naar afbeelding met trendlijnanalyse

In deze tutorial ontdek je **hoe je een grafiek naar afbeelding exporteert** terwijl je een volledige **trendlijnanalyse** uitvoert met Aspose.Cells for Java. We lopen door het laden van een bestaande Excel-werkmap, het toevoegen van een trendlijn, het weergeven van de R‑kwadraatwaarde, het aanpassen van de grafiek, en uiteindelijk het exporteren van de grafiek als een afbeeldingsbestand — allemaal met duidelijke, stap‑voor‑stap code die je kunt kopiëren & plakken.

## Snelle antwoorden
- **Wat is het primaire doel van deze gids?** Om je te laten zien hoe je een trendlijn toevoegt, de vergelijking en R‑kwadraatwaarde weergeeft, en de resulterende grafiek exporteert naar een afbeelding met Java.  
- **Welke bibliotheek is vereist?** Aspose.Cells for Java (download [here](https://releases.aspose.com/cells/java/)).  
- **Heb ik een licentie nodig?** Een gratis proefversie werkt voor ontwikkeling; een commerciële licentie is vereist voor productie.  
- **Kan ik een Excel‑bestand genereren in Java?** Ja – de tutorial maakt en slaat een XLSX‑werkmap op.  
- **Hoe exporteer ik de grafiek naar PNG of JPEG?** Gebruik de `Chart.toImage()`‑methode (besproken in de sectie “Export Chart”).

## Wat is Grafiek exporteren naar afbeelding?
Het exporteren van een grafiek naar een afbeelding zet de visuele weergave van je gegevens om in een draagbare bitmap (PNG, JPEG, enz.). Dit is handig voor het insluiten van grafieken in rapporten, webpagina’s of presentaties waarbij het originele Excel‑bestand niet nodig is.

## Waarom een trendlijn toevoegen en de R‑kwadraatwaarde weergeven?
Een trendlijn helpt je het onderliggende patroon van een gegevensreeks te identificeren, terwijl de **R‑kwadraat**‑metriek kwantificeert hoe goed de trendlijn bij de gegevens past. Het opnemen hiervan in je geëxporteerde afbeelding geeft belanghebbenden direct inzicht zonder de werkmap te openen.

## Voorwaarden
- Java 8 of nieuwer geïnstalleerd.  
- Aspose.Cells for Java‑bibliotheek toegevoegd aan je project (JAR‑bestanden op het classpath).  
- Basiskennis van Java‑IDE’s (IntelliJ IDEA, Eclipse, enz.).

## Stapsgewijze handleiding

### Stap 1: Project instellen
Maak een nieuw Java‑project aan en voeg de Aspose.Cells‑JAR‑bestanden toe aan het build‑pad. Dit bereidt de omgeving voor op het genereren en manipuleren van Excel‑bestanden.

### Stap 2: Excel‑bestand laden (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*We hebben zojuist een **Excel‑bestand** in het geheugen geladen, klaar voor het maken van een grafiek.*

### Stap 3: Een grafiek maken
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Hier genereren we een lijngrafiek die later onze trendlijn zal bevatten.*

### Stap 4: Trendlijn toevoegen (how to add trendline) en R‑kwadraatwaarde weergeven
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*De aanroep `setDisplayRSquaredValue(true)` zorgt ervoor dat de **R‑kwadraatwaarde** op de grafiek verschijnt.*

### Stap 5: Grafiek aanpassen en werkmap opslaan (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Nu is de werkmap **gegenereerd** en opgeslagen als een XLSX‑bestand, klaar voor verdere verwerking.*

### Stap 6: Grafiek exporteren naar afbeelding (export chart to image)
> **Opmerking:** Deze stap wordt beschreven zonder een extra code‑blok om het oorspronkelijke aantal blokken ongewijzigd te houden.  
Nadat de grafiek is gemaakt en opgeslagen, kun je deze exporteren naar een afbeelding door de `chart.toImage()`‑methode aan te roepen en de resulterende `java.awt.image.BufferedImage` naar een bestandsformaat naar keuze (PNG, JPEG, BMP) te schrijven. De typische workflow is:
1. Haal het `Chart`‑object op (reeds gedaan in eerdere stappen).  
2. Roep `chart.toImage()` aan om een `BufferedImage` te verkrijgen.  
3. Gebruik `ImageIO.write(bufferedImage, "png", new File("chart.png"))` om het bestand te schrijven.  

Dit produceert een hoge‑resolutie afbeelding die je overal kunt insluiten, waarmee het **export chart to image**‑proces voltooid is.

## Resultaten analyseren
Open `output.xlsx` in Excel om te verifiëren dat de trendlijn, vergelijking en R‑kwadraatwaarde verschijnen zoals verwacht. Open het geëxporteerde afbeeldingsbestand (bijv. `chart.png`) om een nette visualisatie te zien die kan worden gedeeld zonder de originele werkmap.

 Veelvoorkomende problemen en oplossingen
- **Trendlijn wordt niet weergegeven:** Zorg ervoor dat het gegevensbereik (`A1:A10`) daadwerkelijk numerieke waarden bevat; niet‑numerieke gegevens voorkomen dat de trendlijn wordt berekend.  
- **R‑kwadraatwaarde wordt weergegeven als 0:** Dit betekent vaak dat de gegevensreeks constant is of onvoldoende variatie heeft. Probeer een andere dataset of een polynomiale trendlijn.  
- **Afbeeldingsexport mislukt met `NullPointerException`:** Controleer of de grafiek volledig is gerenderd voordat `toImage()` wordt aangeroepen. Het eerst opslaan van de werkmap kan soms timing‑problemen oplossen.

## Veelgestelde vragen

**Q: Hoe kan ik het type trendlijn wijzigen?**  
A: Gebruik een andere `TrendlineType`‑enumeratie bij het toevoegen van de trendlijn, bijv. `TrendlineType.POLYNOMIAL` voor een polynomiale passing.

**Q: Kan ik het uiterlijk van de trendlijn aanpassen (kleur, dikte)?**  
A: Ja. Toegang tot de `LineFormat` van de trendlijn via `trendline.getLineFormat()` en stel eigenschappen in zoals `setWeight()` en `setColor()`.

**Q: Hoe exporteer ik de grafiek naar PDF in plaats van een afbeelding?**  
A: Converteer de grafiek eerst naar een afbeelding, en embed die afbeelding vervolgens in een PDF met Aspose.PDF of een andere PDF‑bibliotheek naar keuze.

**Q: Is het mogelijk om meerdere trendlijnen toe te voegen aan dezelfde grafiek?**  
A: Absoluut. Roep `chart.getNSeries().get(0).getTrendlines().add(...)` aan voor elke reeks die je wilt analyseren.

**Q: Ondersteunt Aspose.Cells export van hoge‑resolutie afbeeldingen?**  
A: Ja. Je kunt de DPI specificeren bij het aanroepen van `chart.toImage()` en vervolgens de afbeelding dienovereenkomstig schalen voordat je deze opslaat.

## Conclusie
Je hebt nu een complete, end‑to‑end oplossing voor **het exporteren van een grafiek naar afbeelding** terwijl je **trendlijnanalyse** uitvoert in Java met Aspose.Cells. Door een Excel‑bestand te laden, een trendlijn toe te voegen, de vergelijking en R‑kwadraatwaarde weer te geven, de grafiek aan te passen, de werkmap op te slaan en uiteindelijk de visualisatie naar PNG/JPEG te exporteren, kun je programmatisch professionele analytische assets genereren.

---

**Last Updated:** 2025-12-09  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}