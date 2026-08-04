---
date: 2026-02-14
description: Leer hoe u een grafiek exporteert naar PNG, een gegevensreeks toevoegt,
  een gecombineerde lijn‑kolomgrafiek maakt, een werkmap opslaat als XLSX en een legenda
  aan de grafiek toevoegt met Aspose.Cells voor Java.
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: Grafiek exporteren naar PNG en gegevensreeks toevoegen voor gecombineerde grafiek
url: /nl/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

keep date)

**Tested With:** Aspose.Cells for Java latest version

**Author:** Aspose

All unchanged.

Then closing shortcodes.

Now produce final content with translations.

Check for any missed items: "step-by-step" etc not needed.

Make sure to preserve all shortcodes and placeholders.

Let's craft final answer.{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grafiek exporteren naar PNG en gegevensreeks toevoegen voor gecombineerde grafiek

In deze tutorial **voegt u gegevensreeksen** toe aan een Excel-werkmap, **combineert u lijngrafiek‑ en kolomgrafiekelementen**, en leert u hoe u **grafiek exporteert naar PNG** met Aspose.Cells for Java. We lopen elke stap door—van het instellen van de werkmap, het toevoegen van de grafiek aan een werkblad, het aanpassen van de legenda, tot **werkmap opslaan als xlsx** en een PNG‑afbeelding van de grafiek genereren. Aan het einde hebt u een kant‑klaar gecombineerde grafiek die u kunt insluiten in rapporten of dashboards.

## Quick Answers
- **Welke bibliotheek maakt gecombineerde grafieken?** Aspose.Cells for Java  
- **Hoe voeg ik een gegevensreeks toe?** Gebruik `chart.getNSeries().add(...)`  
- **Hoe kan ik een grafiek exporteren naar png?** Roep `chart.toImage("file.png", ImageFormat.getPng())` aan  
- **In welk bestandsformaat kan ik de werkmap opslaan?** Standaard `.xlsx` (werkmap opslaan als xlsx)  
- **Heb ik een licentie nodig voor productie?** Een geldige Aspose.Cells‑licentie is vereist  

## Wat is **export chart to PNG** in Aspose.Cells?
Een grafiek exporteren naar PNG maakt een rasterafbeelding van de Excel‑grafiek die kan worden weergegeven in webpagina’s, rapporten of e‑mails zonder dat de Excel‑applicatie nodig is.

## Waarom een **gecombineerde lijngrafiek‑kolomgrafiek** maken?
Een gecombineerde grafiek stelt u in staat verschillende datasets met verschillende visuele weergaven (bijv. een lijngrafiek boven een kolomgrafiek) in één weergave te tonen. Dit is perfect voor het vergelijken van trends met totalen, het benadrukken van correlaties, of het leveren van rijkere inzichten in een compact formaat.

## Vereisten
- Java Development Kit (JDK) 8 of hoger  
- Aspose.Cells for Java bibliotheek (download via de onderstaande link)  
- Basiskennis van Java‑syntaxis en Excel‑concepten  

## Aan de slag

Eerst downloadt u de Aspose.Cells for Java bibliotheek van de officiële site:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Zodra de JAR is toegevoegd aan de classpath van uw project, kunt u beginnen met het bouwen van de grafiek.

### Stap 1: Aspose.Cells‑klassen importeren
```java
import com.aspose.cells.*;
```

### Stap 2: Maak een nieuwe werkmap
```java
Workbook workbook = new Workbook();
```

### Stap 3: Toegang tot het eerste werkblad
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Stap 4: Voeg een gecombineerd grafiekobject toe aan het werkblad  
We beginnen met een lijngrafiek en voegen later een kolomreeks toe om een **gecombineerde lijngrafiek‑kolomgrafiek** effect te bereiken.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Gegevens toevoegen aan de grafiek

Nu de grafiekcontainer bestaat, moeten we deze van gegevens voorzien.

### Stap 5: Definieer de gegevensbereiken en **voeg gegevensreeksen toe**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** De eerste parameter (`"A1:A5"`) is het bereik voor de eerste reeks, en de tweede (`"B1:B5"`) maakt een tweede reeks die wordt gecombineerd met de eerste.

### Stap 6: Stel de categoriedata (X‑as) in
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## De grafiek aanpassen

Een goede grafiek vertelt een verhaal. Laten we er titels, as‑labels en een duidelijke legenda aan geven.

### Stap 7: **Stel grafiekas‑labels in** en titel
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Stap 8: **Voeg legenda toe aan grafiek** en pas de positie aan
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## De grafiek opslaan en exporteren

Na het aanpassen wilt u **werkmap opslaan als xlsx** en ook een afbeelding genereren.

### Stap 9: Sla de werkmap op als een Excel‑bestand (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Stap 10: **Export grafiek naar PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> De `chart.toImage`‑methode **genereert excel chart**‑afbeeldingen die kunnen worden gebruikt in webpagina’s, rapporten of e‑mails.

## Veelvoorkomende problemen & probleemoplossing

| Probleem | Oplossing |
|----------|-----------|
| **Geen gegevens zichtbaar** | Controleer of de celbereiken (`A1:A5`, `B1:B5`, `C1:C5`) daadwerkelijk gegevens bevatten voordat u de grafiek maakt. |
| **Legenda overlapt grafiek** | Stel `chart.getLegend().setOverlay(false)` in of verplaats de legenda naar een andere positie (bijv. `RIGHT`). |
| **Afbeeldingsbestand is leeg** | Zorg ervoor dat de grafiek minstens één reeks heeft en dat `chart.toImage` wordt aangeroepen na alle aanpassingen. |
| **Opslaan veroorzaakt een uitzondering** | Controleer of u schrijfrechten heeft voor de doelmap en dat het bestand niet geopend is in Excel. |

## Veelgestelde vragen

**Q: Hoe installeer ik Aspose.Cells for Java?**  
A: Download de JAR van de officiële site en voeg deze toe aan de classpath van uw project. De downloadlink is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Kan ik andere grafiektype maken naast lijn en kolom?**  
A: Ja, Aspose.Cells ondersteunt balk, taart, spreiding, gebied en nog veel meer grafiektype. Raadpleeg de API‑documentatie voor de volledige lijst.

**Q: Is een licentie vereist voor productiegebruik?**  
A: Een geldige Aspose.Cells‑licentie is vereist voor productie‑implementaties. Een gratis proefversie is beschikbaar voor evaluatie.

**Q: Hoe kan ik de kleuren van elke reeks wijzigen?**  
A: Gebruik `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (of soortgelijk) na het toevoegen van de reeks.

**Q: Waar kan ik meer code‑voorbeelden vinden?**  
A: Uitgebreide documentatie en extra voorbeelden zijn beschikbaar op de Aspose‑referentiesite: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2026-02-14  
**Tested With:** Aspose.Cells for Java latest version  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}