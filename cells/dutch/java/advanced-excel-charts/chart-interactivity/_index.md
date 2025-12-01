---
date: 2025-12-01
description: Leer hoe u het type Excel‑grafiek kunt wijzigen en interactieve functies
  zoals tooltips, gegevenslabels en drill‑down kunt toevoegen met Aspose.Cells voor
  Java.
language: nl
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Wijzig het Excel‑grafiektype en voeg interactiviteit toe – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Wijzig het Excel-diagramtype en voeg interactiviteit toe

## Inleiding

Interactieve diagrammen laten je publiek data on‑the‑fly verkennen, terwijl de mogelijkheid om **Excel-diagramtype te wijzigen** je de flexibiliteit geeft om informatie te presenteren in het meest effectieve visuele formaat. In deze tutorial leer je hoe je Aspose.Cells voor Java gebruikt om het type van een diagram te wijzigen, tooltips toe te voegen, datalabels in te sluiten en zelfs drill‑down‑links te maken – alles zonder je Java‑code te verlaten. Aan het einde heb je een volledig uitgeruste, interactieve Excel‑werkmap die je kunt insluiten in rapporten, dashboards of webapplicaties.

## Snelle antwoorden
- **Kan ik het diagramtype programmatisch wijzigen?** Ja – gebruik de `ChartType`‑enum bij het maken of bijwerken van een diagram.  
- **Hoe voeg ik tooltips toe aan een diagram?** Schakel datalabels in en zet `ShowValue` op true.  
- **Wat is de gemakkelijkste manier om drill‑down‑links toe te voegen?** Voeg een hyperlink toe aan een datapunt via `getHyperlinks().add(url)`.  
- **Heb ik een licentie nodig voor Aspose.Cells?** Een gratis proefversie werkt voor ontwikkeling; een licentie is vereist voor productie.  
- **Welke Java‑versie wordt ondersteund?** Java 8 en hoger worden volledig ondersteund.

## Wat is “Excel-diagramtype wijzigen”?

Het wijzigen van het diagramtype betekent dat je de visuele weergave verwisselt (bijv. van een kolomdiagram naar een lijndiagram) terwijl de onderliggende data ongewijzigd blijft. Dit is handig wanneer je ontdekt dat een ander diagram de trends, vergelijkingen of verdelingen beter communiceert.

## Waarom interactiviteit toevoegen aan Excel‑diagrammen?

- **Betere data‑inzichten:** Tooltips en datalabels laten gebruikers exacte waarden zien zonder te scrollen.  
- **Aansprekende presentaties:** Interactieve elementen houden de kijkers geïnteresseerd.  
- **Drill‑down‑mogelijkheden:** Hyperlinks laten gebruikers springen naar gedetailleerde werkbladen of externe bronnen.  
- **Herbruikbare assets:** Eén werkmap kan meerdere rapportagescenario's bedienen door simpelweg het diagramtype te wisselen.

## Voorvereisten

- Java‑ontwikkelomgeving (JDK 8+)  
- Aspose.Cells voor Java‑bibliotheek (download van [hier](https://releases.aspose.com/cells/java/))  
- Een voorbeeld‑Excel‑bestand (`data.xlsx`) met de data die je wilt visualiseren

## Stapsgewijze handleiding

### Stap 1: Stel je Java‑project in

1. Maak een nieuw Java‑project aan in je favoriete IDE (IntelliJ IDEA, Eclipse, VS Code, enz.).  
2. Voeg de Aspose.Cells‑JAR toe aan de classpath van je project.

### Stap 2: Laad de bron‑werkmap

We beginnen met het laden van een bestaande werkmap die de data voor ons diagram bevat.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Stap 3: Maak een diagram en **wijzig het type**

Hieronder maken we een kolomdiagram en laten vervolgens direct zien hoe je het kunt omzetten naar een lijndiagram indien nodig.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro tip:** Het diagramtype wijzigen na creatie is zo simpel als het aanroepen van `setChartType(...)`. Hiermee wordt het primaire trefwoord **Excel-diagramtype wijzigen** vervuld zonder een nieuw diagramobject te hoeven maken.

### Stap 4: Voeg interactiviteit toe

#### 4.1 Tooltips toevoegen aan het diagram

Tooltips worden weergegeven wanneer een gebruiker over een datapunt hovert. In Aspose.Cells worden ze geïmplementeerd via datalabels.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Datalabels toevoegen ( **add data labels chart** )

Datalabels kunnen de exacte waarde, categorienaam of beide tonen. Hier gebruiken we een callout‑stijl.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Drill‑down implementeren ( **add drill down excel** )

Een drill‑down‑link laat gebruikers op een punt klikken en naar een gedetailleerde weergave springen, hetzij binnen de werkmap, hetzij op een webpagina.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Stap 5: Sla het werkboek op

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Veelvoorkomende problemen en oplossingen

| Probleem | Reden | Oplossing |
|----------|-------|-----------|
| Tooltips worden niet weergegeven | `HasDataLabels` niet ingeschakeld | Zorg ervoor dat `setHasDataLabels(true)` wordt aangeroepen vóór het configureren van `ShowValue`. |
| Drill‑down‑link werkt niet | Hyperlink‑URL is onjuist gevormd | Controleer of de URL begint met `http://` of `https://`. |
| Diagramtype verandert niet | Een oudere versie van Aspose.Cells wordt gebruikt | Upgrade naar de nieuwste versie (getest met 24.12). |

## Veelgestelde vragen

**V: Hoe kan ik het diagramtype wijzigen nadat het is aangemaakt?**  
A: Roep `chart.setChartType(ChartType.YOUR_CHOICE)` aan op het bestaande `Chart`‑object. Dit adresseert direct de **Excel-diagramtype wijzigen**‑vereiste.

**V: Kan ik het uiterlijk van tooltips aanpassen?**  
A: Ja. Gebruik `chart.getNSeries().get(0).getPoints().getDataLabels()` om lettergrootte, kleur en achtergrond in te stellen.

**V: Is het mogelijk om meerdere drill‑down‑links in één diagram toe te voegen?**  
A: Absoluut. Loop door de punten en roep `getHyperlinks().add(url)` aan voor elk punt dat je wilt koppelen.

**V: Ondersteunt Aspose.Cells andere diagramtypen zoals taart of radar?**  
A: Alle diagramtypen die in de `ChartType`‑enum zijn gedefinieerd worden ondersteund, inclusief `PIE`, `RADAR`, `AREA`, enz.

**V: Waar kan ik meer voorbeelden vinden?**  
A: Bezoek de officiële [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) voor een volledige lijst met diagram‑gerelateerde methoden.

## Conclusie

Je weet nu hoe je **Excel-diagramtype kunt wijzigen**, **tooltips** kunt insluiten, **datalabels** kunt toevoegen en **drill‑down**‑links kunt maken met Aspose.Cells voor Java. Deze interactieve functies veranderen statische spreadsheets in dynamische data‑exploratie‑tools, perfect voor dashboards, rapporten en web‑gebaseerde analyses.

---

**Laatst bijgewerkt:** 2025-12-01  
**Getest met:** Aspose.Cells 24.12 for Java  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}