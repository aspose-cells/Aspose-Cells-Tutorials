---
date: 2026-02-09
description: Leer hoe u gegevenslabels aan een Excel‑grafiek kunt toevoegen en het
  grafiektype kunt wijzigen met Aspose.Cells voor Java, plus tooltips en drill‑down‑interactiviteit.
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Gegevenslabels toevoegen aan Excel-grafiek met Aspose.Cells Java
url: /nl/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Gegevenslabels toevoegen aan Excel-diagram en diagramtype wijzigen – Aspose.Cells Java

Interactieve diagrammen geven uw Excel‑rapporten een nieuw niveau van inzicht, en **gegevenslabels toevoegen aan Excel-diagram** maakt de informatie direct leesbaar. In deze tutorial leert u hoe u **gegevenslabels toevoegt aan Excel-diagram**, het diagramtype wijzigt en interactieve Java‑oplossingen maakt met Aspose.Cells. We laten ook zien hoe u tooltips en een eenvoudige drill‑down‑hyperlink toevoegt zodat uw publiek de gegevens dieper kan verkennen.

## Snelle antwoorden
- **Welke bibliotheek wordt gebruikt?** Aspose.Cells for Java  
- **Kan ik het diagramtype wijzigen?** Ja – wijzig gewoon de `ChartType`‑enum wanneer u het diagram maakt.  
- **Hoe voeg ik tooltips toe aan een diagram?** Gebruik de data‑label‑API (`setHasDataLabels(true)`) en schakel weergave van waarden in.  
- **Wordt drill‑down ondersteund?** U kunt hyperlinks aan datapunten koppelen voor basis drill‑down‑gedrag.  
- **Voorvereisten?** Java‑IDE, Aspose.Cells‑JAR en een Excel‑bestand met voorbeeldgegevens.

## Voorvereisten

Voordat we beginnen, zorg dat u het volgende heeft:

- Java‑ontwikkelomgeving (JDK 8+ aanbevolen)  
- Aspose.Cells for Java‑bibliotheek (download van [hier](https://releases.aspose.com/cells/java/))  
- Een voorbeeld‑werkmap (`data.xlsx`) met de gegevens die u wilt visualiseren  

## Stap 1: Uw Java‑project instellen

1. Maak een nieuw Java‑project aan in uw favoriete IDE (IntelliJ IDEA, Eclipse, enz.).  
2. Voeg de Aspose.Cells‑JAR toe aan het build‑pad van uw project of aan de Maven/Gradle‑afhankelijkheden.

## Stap 2: Gegevens laden

Om met diagrammen te werken moet eerst een werkmap in het geheugen worden geladen.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Stap 3: Een diagram maken (en het type wijzigen)

U kunt elk diagramtype kiezen dat bij uw analyse past. Hieronder maken we een **kolomdiagram**, maar u kunt eenvoudig overschakelen naar een lijndiagram, cirkeldiagram of staafdiagram door de `ChartType`‑enum te wijzigen.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro tip:** Om **het Excel‑diagramtype te wijzigen**, vervangt u `ChartType.COLUMN` door `ChartType.LINE`, `ChartType.PIE`, enz.

## Stap 4: Interactiviteit toevoegen

### 4.1. Tooltips toevoegen (Tooltips aan diagram toevoegen)

Tooltips verschijnen wanneer de gebruiker over een datapunt zweeft. De volgende code schakelt data‑labels in en toont de waarde als tooltip.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Gegevenslabels toevoegen – **add data labels to excel chart**

Gegevenslabels bieden een permanente visuele aanwijzing direct op het diagram. U kunt ze weergeven als callouts voor betere leesbaarheid.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **Waarom gegevenslabels toevoegen?** Het direct op het diagram plaatsen van gegevenslabels elimineert de noodzaak voor gebruikers om te zweven of waarden te raden, waardoor de rapportduidelijkheid verbetert.

### 4.3. Drill‑Down implementeren (Hyperlink op een datapunt)

Een eenvoudige manier om drill‑down‑functionaliteit toe te voegen is een hyperlink aan een specifiek punt koppelen. Klikken op het punt opent een webpagina met gedetailleerde informatie.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Stap 5: De werkmap opslaan

Nadat het diagram is geconfigureerd, slaat u de werkmap op zodat de interactieve functies worden bewaard in het uitvoerbestand.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Veelvoorkomende problemen & oplossingen

| Probleem | Oplossing |
|----------|-----------|
| **Tooltips worden niet weergegeven** | Zorg ervoor dat `setHasDataLabels(true)` wordt aangeroepen vóór het configureren van `setShowValue(true)`. |
| **Hyperlink is niet klikbaar** | Controleer of het uitvoerformaat hyperlinks ondersteunt (bijv. XLSX, niet CSV). |
| **Diagramtype verandert niet** | Controleer of u de juiste `ChartType`‑enum hebt gewijzigd bij het toevoegen van het diagram. |

## Veelgestelde vragen

**V: Hoe kan ik het diagramtype wijzigen nadat het is gemaakt?**  
A: U moet een nieuw diagram maken met het gewenste `ChartType`. Aspose.Cells biedt geen in‑place typeconversie, dus verwijder het oude diagram en voeg een nieuw toe.

**V: Kan ik het uiterlijk van tooltips aanpassen?**  
A: Ja. Gebruik de `DataLabel`‑eigenschappen zoals `setFontSize`, `setFontColor` en `setBackgroundColor` om de tooltip‑tekst te stijlen.

**V: Hoe verwerk ik gebruikersinteracties in een webapplicatie?**  
A: Exporteer de werkmap naar een HTML‑ of XLSX‑bestand en gebruik JavaScript aan de client‑kant om klik‑events op diagramonderdelen af te vangen.

**V: Waar vind ik meer voorbeelden en documentatie?**  
A: Bezoek de [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) voor een volledige lijst van diagram‑gerelateerde klassen en methoden.

## Conclusie

U weet nu hoe u **gegevenslabels toevoegt aan Excel-diagram**, **het Excel-diagramtype wijzigt**, **interactieve diagram‑Java‑oplossingen** maakt, en deze verrijkt met tooltips, gegevenslabels en drill‑down‑hyperlinks met behulp van Aspose.Cells for Java. Deze verbeteringen maken uw Excel‑rapporten veel boeiender en inzichtelijker voor eindgebruikers.

---

**Laatst bijgewerkt:** 2026-02-09  
**Getest met:** Aspose.Cells for Java 24.12  
**Auteur:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}