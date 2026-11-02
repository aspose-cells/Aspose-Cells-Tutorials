---
date: 2026-08-21
description: Leer hoe u tooltips, data labels kunt toevoegen en het chart type kunt
  wijzigen in Excel-grafieken met Aspose.Cells for Java – stapsgewijze handleiding
  met interactieve voorbeelden.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Wijzig Excel Chart Type
og_description: Leer hoe u tooltips, data labels kunt toevoegen en het chart type
  kunt wijzigen in Excel-grafieken met Aspose.Cells for Java – stapsgewijze handleiding
  met interactieve voorbeelden.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Hoe tooltips en data labels toe te voegen aan Excel-grafieken in Java
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
title: Hoe tooltips en data labels toe te voegen aan Excel-grafieken in Java
url: /nl/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Voeg gegevenslabels toe aan Excel‑grafiek en wijzig grafiektype – Aspose.Cells Java

Interactieve grafieken geven uw Excel‑rapporten een nieuw inzichtsniveau, en **hoe u tooltips toevoegt** maakt de informatie direct leesbaar. In deze tutorial leert u hoe u **gegevenslabels toevoegt aan een Excel‑grafiek**, **het grafiektype wijzigt**, en interactieve Java‑oplossingen maakt met Aspose.Cells. We laten ook zien hoe u tooltips en een eenvoudige drill‑down‑hyperlink toevoegt zodat uw publiek de gegevens dieper kan verkennen.

## Snelle antwoorden
- **Welke bibliotheek wordt gebruikt?** Aspose.Cells for Java  
- **Kan ik het grafiektype wijzigen?** Ja – wijzig gewoon de `ChartType`‑enum wanneer u de grafiek maakt.  
- **Hoe voeg ik tooltips toe aan een grafiek?** Gebruik de gegevens‑label‑API (`setHasDataLabels(true)`) en schakel de weergave van waarden in.  
- **Wordt drill‑down ondersteund?** U kunt hyperlinks aan gegevenspunten koppelen voor basale drill‑down‑functionaliteit.  
- **Voorwaarden?** Java‑IDE, Aspose.Cells‑JAR en een Excel‑bestand met voorbeeldgegevens.

## Wat is hoe u tooltips toevoegt?
**Hoe u tooltips toevoegt** verwijst naar het proces waarbij hover‑tekst wordt ingeschakeld die de waarde van een gegevenspunt of aangepaste informatie weergeeft op een Excel‑grafiek. In Aspose.Cells wordt dit bereikt via de instellingen voor gegevenslabels van de grafiek. Tooltips helpen gebruikers snel de gegevens te begrijpen zonder de grafiek te overladen, en ze kunnen worden aangepast qua lettertype, kleur en opmaak.

## Waarom interactieve grafieken gebruiken met Aspose.Cells?
Aspose.Cells ondersteunt **meer dan 50 invoer‑ en uitvoerformaten**—inclusief XLSX, CSV, PDF en HTML—en kan werkmappen met **meer dan 1 000 bladen** verwerken zonder het volledige bestand in het geheugen te laden, waardoor snelle, server‑side grafiekgeneratie voor enterprise‑rapportage mogelijk is. Interactieve grafieken maken ook het insluiten van hyperlinks, dynamische gegevensupdates en export naar web‑vriendelijke formaten mogelijk, waardoor ze ideaal zijn voor dashboards en rapportage‑portalen.

## Voorwaarden

Voordat we beginnen, zorg dat u het volgende heeft:

- Java‑ontwikkelomgeving (JDK 8+ aanbevolen)  
- Aspose.Cells for Java‑bibliotheek (download vanaf de [Aspose.Cells for Java downloadpagina](https://releases.aspose.com/cells/java/))  
- Een voorbeeld‑werkmap (`data.xlsx`) met de gegevens die u wilt visualiseren  

## Stap 1: uw Java‑project instellen

1. Maak een nieuw Java‑project aan in uw favoriete IDE (IntelliJ IDEA, Eclipse, enz.).  
2. Voeg de Aspose.Cells‑JAR toe aan het build‑pad van uw project of aan de Maven/Gradle‑dependencies.

## Stap 2: gegevens laden

Om met grafieken te werken moet eerst een werkmap in het geheugen worden geladen.

De `Workbook`‑klasse vertegenwoordigt een Excel‑bestand, en `Worksheet` vertegenwoordigt een enkel blad binnen dat bestand.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Hoe het grafiektype wijzigen in Aspose.Cells?

Maak een nieuwe grafiek met de gewenste `ChartType`‑enum; Aspose.Cells wijzigt een bestaand grafiektype niet in‑place, dus moet u een nieuwe grafiek van het juiste type toevoegen en eventueel de oude verwijderen. Deze aanpak garandeert dat alle series en assen correct worden opnieuw opgebouwd voor de nieuwe visuele weergave.

## Stap 3: een grafiek maken (en het type wijzigen)

U kunt elk grafiektype kiezen dat bij uw analyse past. Hieronder maken we een **kolomgrafiek**, maar u kunt eenvoudig overschakelen naar een lijn‑, taart‑ of staafgrafiek door de `ChartType`‑enum te wijzigen.

Het `Chart`‑object biedt methoden om de visuele weergave van gegevens in het werkblad te configureren.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro tip:** Om **het Excel‑grafiektype te wijzigen**, vervangt u `ChartType.COLUMN` door `ChartType.LINE`, `ChartType.PIE`, enz.

## Hoe tooltips toevoegen aan een Excel‑grafiek?

Laad uw grafiek, schakel gegevenslabels in en zet de `showValue`‑vlag. De tooltip zal vervolgens de onderliggende celwaarde weergeven wanneer een gebruiker over een gegevenspunt zweeft in het gerenderde Excel‑bestand of de HTML‑weergave. U kunt ook het lettertype, de kleur en de achtergrond van de tooltip aanpassen aan de stijl van uw rapport.

De `DataLabel`‑klasse regelt het uiterlijk en de inhoud van gegevenslabels, die tevens als tooltips fungeren.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Stap 4: interactiviteit toevoegen

### 4.1. Tooltips toevoegen (tooltips aan grafiek toevoegen)

Tooltips verschijnen wanneer de gebruiker over een gegevenspunt zweeft. De volgende code schakelt gegevenslabels in en toont de waarde als tooltip.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Gegevenslabels toevoegen – **gegevenslabels toevoegen aan Excel‑grafiek**

Gegevenslabels bieden een permanente visuele aanwijzing direct op de grafiek. U kunt ze weergeven als callouts voor betere leesbaarheid.

De `DataLabel`‑klasse regelt het uiterlijk van labels op elke serie. Door `setHasDataLabels(true)` aan te roepen en eigenschappen zoals `setShowValue(true)` te configureren, embedt u de numerieke waarde direct op de grafiek, waardoor deze onmiddellijk zichtbaar is zonder enige interactie. Extra opties laten u serienaam, percentages of aangepaste tekst tonen voor rijkere context.

> **Waarom gegevenslabels toevoegen?** Het opnemen van gegevenslabels direct op de grafiek elimineert de noodzaak voor gebruikers om te hoveren of te raden, waardoor de rapporthelderheid verbetert.

### 4.3. Drill‑down implementeren (hyperlink op een gegevenspunt)

Een eenvoudige manier om drill‑down‑functionaliteit toe te voegen is een hyperlink aan een specifiek punt te koppelen. Klikken op het punt opent een webpagina met gedetailleerde informatie.

De `Hyperlink`‑klasse koppelt een klikbare link aan een grafiekelement, waardoor drill‑down‑navigatie mogelijk wordt.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Hoe gegevenslabels toevoegen aan een Excel‑grafiek?

De `DataLabel`‑klasse regelt het uiterlijk van labels op elke serie. Door `setHasDataLabels(true)` aan te roepen en eigenschappen zoals `setShowValue(true)` te configureren, embedt u de numerieke waarde direct op de grafiek, waardoor deze onmiddellijk zichtbaar is zonder enige interactie. Extra opties laten u serienaam, percentages of aangepaste tekst tonen voor rijkere context.

## Stap 5: de werkmap opslaan

Na het configureren van de grafiek, slaat u de werkmap op zodat de interactieve functies worden bewaard in het uitvoerbestand.

Het aanroepen van `workbook.save` schrijft de gewijzigde werkmap naar een bestand in het gekozen formaat.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Veelvoorkomende problemen & oplossingen

| Probleem | Oplossing |
|----------|-----------|
| **Tooltips worden niet weergegeven** | Zorg ervoor dat `setHasDataLabels(true)` wordt aangeroepen vóór het configureren van `setShowValue(true)`. |
| **Hyperlink is niet klikbaar** | Controleer of het uitvoerformaat hyperlinks ondersteunt (bijv. XLSX, niet CSV). |
| **Grafiektype verandert niet** | Controleer of u de juiste `ChartType`‑enum hebt aangepast bij het toevoegen van de grafiek. |

## Veelgestelde vragen

**V: Hoe kan ik het grafiektype wijzigen nadat het is gemaakt?**  
A: U moet een nieuwe grafiek maken met het gewenste `ChartType`. Aspose.Cells biedt geen in‑place typeconversie, dus verwijder de oude grafiek en voeg een nieuwe toe.

**V: Kan ik het uiterlijk van tooltips aanpassen?**  
A: Ja. Gebruik de `DataLabel`‑eigenschappen zoals `setFontSize`, `setFontColor` en `setBackgroundColor` om de tooltip‑tekst te stijlen.

**V: Hoe verwerk ik gebruikersinteracties in een webapplicatie?**  
A: Exporteer de werkmap naar een HTML‑ of XLSX‑bestand en gebruik JavaScript aan de client‑kant om klik‑events op grafiekelementen af te vangen.

**V: Waar vind ik meer voorbeelden en documentatie?**  
A: Bezoek de [Aspose.Cells Java API‑referentie](https://reference.aspose.com/cells/java/) voor een volledige lijst van grafiek‑gerelateerde klassen en methoden.

## Conclusie

U weet nu hoe u **gegevenslabels toevoegt aan een Excel‑grafiek**, **het Excel‑grafiektype wijzigt**, **interactieve Java‑grafiekoplossingen** maakt, en deze verrijkt met tooltips, gegevenslabels en drill‑down‑hyperlinks met Aspose.Cells for Java. Deze verbeteringen maken uw Excel‑rapporten veel boeiender en inzichtelijker voor eindgebruikers.

---

**Laatst bijgewerkt:** 2026-08-21  
**Getest met:** Aspose.Cells for Java 24.12  
**Auteur:** Aspose

## Gerelateerde tutorials

- [Hoe Excel‑grafieken en gegevenslabels te wijzigen met Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Excel‑grafiekaslabel‑extractie met Aspose.Cells Java: Een uitgebreide gids](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Bubbelgrafieken maken in Excel met Aspose.Cells for Java: Een stapsgewijze handleiding](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}