---
date: 2025-12-06
description: Leer hoe u gegevensreeksen kunt toevoegen, gecombineerde grafiektype
  kunt maken, een Excel-werkmap kunt opslaan en een grafiek kunt exporteren naar PNG
  met Aspose.Cells voor Java.
language: nl
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Gegevensreeksen toevoegen om een gecombineerde grafiek te maken met Aspose.Cells
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gegevensreeks toevoegen om gecombineerde grafiek te maken met Aspose.Cells

In deze tutorial **voegt u gegevensreeksen** toe aan een Excel-werkmap en leert u hoe u **gecombineerde grafiektype** kunt maken met Aspose.Cells for Java. We lopen elke stap door—van het instellen van de werkmap, het toevoegen van reeksen, het aanpassen van de legenda, tot het **opslaan van de Excel-werkmap** en het exporteren van de **grafiek naar PNG**. Aan het einde heeft u een kant‑klaar gecombineerde grafiek die u kunt insluiten in rapporten of dashboards.

## Snelle antwoorden
- **Welke bibliotheek maakt gecombineerde grafieken?** Aspose.Cells for Java  
- **Hoe voeg ik een gegevensreeks toe?** Gebruik `chart.getNSeries().add(...)`  
- **Kan ik de grafiek exporteren als afbeelding?** Ja, met `chart.toImage(...)` (PNG)  
- **In welk bestandsformaat kan ik de werkmap opslaan?** Standaard `.xlsx` (Excel)  
- **Heb ik een licentie nodig voor productie?** Een geldige Aspose.Cells‑licentie is vereist  

## Wat is **add data series** in Aspose.Cells?
Het toevoegen van een gegevensreeks vertelt de grafiek welke cellen de waarden bevatten die u wilt plotten. Elke reeks kan een lijn, kolom of een ander grafiektype vertegenwoordigen, en u kunt ze combineren om een **gecombineerde grafiek** te maken.

## Waarom een **gecombineerde grafiek** maken?
Een gecombineerde grafiek stelt u in staat verschillende datasets met verschillende visuele weergaven (bijv. een lijngrafiek boven een kolomgrafiek) in één weergave te tonen. Dit is ideaal om trends te vergelijken met totalen, correlaties te benadrukken, of rijkere inzichten te leveren in een compact formaat.

## Voorwaarden
- Java Development Kit (JDK) 8 of hoger  
- Aspose.Cells for Java bibliotheek (download via de onderstaande link)  
- Basiskennis van Java-syntaxis en Excel-concepten  

## Aan de slag

Eerst downloadt u de Aspose.Cells for Java bibliotheek van de officiële site:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Zodra de JAR aan de classpath van uw project is toegevoegd, kunt u beginnen met het bouwen van de grafiek.

### Stap 1: Importeer Aspose.Cells‑klassen
```java
import com.aspose.cells.*;
```

### Stap 2: Maak een nieuwe werkmap
```java
Workbook workbook = new Workbook();
```

### Stap 3: Open het eerste werkblad
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Stap 4: Voeg een gecombineerd grafiekobject toe  
We beginnen met een lijngrafiek en voegen later andere reeksen toe om een **gecombineerde grafiek** effect te bereiken.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Gegevens toevoegen aan de grafiek

Nu de grafiekcontainer bestaat, moeten we deze van gegevens voorzien.

### Stap 5: Definieer de gegevensbereiken en **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** De eerste parameter (`"A1:A5"`) is het bereik voor de eerste reeks, en de tweede (`"B1:B5"`) maakt een tweede reeks die met de eerste wordt gecombineerd.

### Stap 6: Stel de categoriedata (X‑as) in
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## De grafiek aanpassen

Een goede grafiek vertelt een verhaal. Laten we het titels, aslabels en een duidelijke legenda geven.

### Stap 7: Stel de grafiektitel en aslabels in
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Stap 8: **Add legend chart** en pas de positie aan
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## De grafiek opslaan en exporteren

Na het aanpassen wilt u de **Excel-werkmap opslaan** en ook een afbeelding genereren.

### Stap 9: Sla de werkmap op als een Excel‑bestand
```java
workbook.save("CombinedChart.xlsx");
```

### Stap 10: Exporteer de **grafiek naar PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> De `chart.toImage`‑methode **genereert Excel‑grafiek**‑afbeeldingen die kunnen worden gebruikt in webpagina’s, rapporten of e‑mails.

## Veelvoorkomende problemen & foutopsporing

| Probleem | Oplossing |
|----------|-----------|
| **Geen gegevens zichtbaar** | Controleer of de celbereiken (`A1:A5`, `B1:B5`, `C1:C5`) daadwerkelijk gegevens bevatten voordat u de grafiek maakt. |
| **Legenda overlapt grafiek** | Stel `chart.getLegend().setOverlay(false)` in of verplaats de legenda naar een andere positie (bijv. `RIGHT`). |
| **Afbeeldingsbestand is leeg** | Zorg ervoor dat de grafiek minstens één reeks heeft en dat `chart.toImage` wordt aangeroepen na alle aanpassingen. |
| **Opslaan veroorzaakt een uitzondering** | Controleer of u schrijfrechten heeft voor de doelmap en dat het bestand niet geopend is in Excel. |

## Veelgestelde vragen

**V: Hoe installeer ik Aspose.Cells for Java?**  
A: Download de JAR van de officiële site en voeg deze toe aan de classpath van uw project. De downloadlink is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**V: Kan ik andere grafiektype maken naast lijn en kolom?**  
A: Ja, Aspose.Cells ondersteunt staaf-, taart-, spreidings-, gebieds- en vele andere grafiektype. Raadpleeg de API‑documentatie voor de volledige lijst.

**V: Is een licentie vereist voor productiegebruik?**  
A: Een geldige Aspose.Cells‑licentie is vereist voor productie‑implementaties. Een gratis proefversie is beschikbaar voor evaluatie.

**V: Hoe kan ik de kleuren van elke reeks wijzigen?**  
A: Gebruik `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (of iets dergelijks) na het toevoegen van de reeks.

**V: Waar kan ik meer code‑voorbeelden vinden?**  
A: Uitgebreide documentatie en extra voorbeelden zijn beschikbaar op de Aspose‑referentiesite: [hier](https://reference.aspose.com/cells/java/).

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

---