---
category: general
date: 2026-09-08
description: Hoe bereik te kopiëren in Java met Aspose.Cells – leer hoe je een draaitabel
  kopieert, een draaitabel dupliceert en een draaitabel exporteert terwijl je de opmaak
  behoudt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: nl
lastmod: 2026-09-08
og_description: Hoe bereik te kopiëren in Java met Aspose.Cells. Deze tutorial laat
  zien hoe je een draaitabel kopieert, een draaitabel dupliceert en een draaitabel
  exporteert terwijl de opmaak behouden blijft.
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: Hoe een bereik te kopiëren in Java – volledige Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hoe een bereik te kopiëren in Java met Aspose.Cells
url: /nl/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een bereik te kopiëren in Java met Aspose.Cells

Als je **hoe een bereik te kopiëren** in Java nodig hebt, maakt Aspose.Cells de taak eenvoudig. Of je nu een regulier celblok of een volledig uitgeruste draaitabel verplaatst, de bibliotheek behandelt de kopieerbewerking terwijl formules, stijlen en de draaitabelcache intact blijven. In deze gids leer je **draaitabel kopiëren**, **draaitabel dupliceren**, en zelfs **draaitabel exporteren** naar een nieuw werkboek met volledige opmaak.

## Vereisten

- Java 17 (of een andere ondersteunde JDK) geïnstalleerd en geconfigureerd in je IDE.
- Maven of Gradle voor afhankelijkheidsbeheer (de voorbeelden gebruiken Maven).
- Een bron‑Excel‑bestand (`source.xlsx`) dat een draaitabel bevat in het bereik `A1:H20`.
- Basiskennis van Java‑programmeren.

## Stap 1: Voeg Aspose.Cells toe aan je project

Aspose.Cells is een commerciële bibliotheek, maar er is een gratis evaluatieversie beschikbaar. Voeg de afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Als je de voorkeur geeft aan Gradle, is de equivalente invoer:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Het toevoegen van de JAR geeft je toegang tot de `Workbook`, `Worksheet`, `Range` en `CopyOptions` klassen die door deze gids heen worden gebruikt.

## Stap 2: Laad het bron‑werkboek en selecteer het eerste werkblad

Het eerste deel van **hoe een bereik te kopiëren** is het openen van het werkboek dat de gegevens bevat die je wilt verplaatsen.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **Waarom dit belangrijk is:** Het openen van het werkboek creëert een in‑memory representatie die de API kan manipuleren zonder het oorspronkelijke bestand op schijf aan te raken.

## Stap 3: Definieer het bereik dat de draaitabel bevat

Een draaitabel bevindt zich binnen een rechthoekig blok. Je moet dat blok specificeren zodat Aspose.Cells weet wat er gekopieerd moet worden.

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **Opmerking:** De `createRange` methode **kopieert** nog niets; hij maakt alleen een `Range` object dat naar de cellen wijst die je wilt dupliceren.

## Stap 4: Maak een nieuw werkboek en haal het eerste werkblad op

Maak nu het bestemmings‑werkboek aan waarin het gekopieerde bereik zal worden geplaatst.

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **Waarom een nieuw werkboek?** Het gebruik van een nieuw bestand garandeert dat geen verborgen stijlen of benoemde bereiken interfereren met de kopieerbewerking, wat vooral belangrijk is wanneer je **draaitabel exporteert** naar een apart bestand.

## Stap 5: Kopieer het bereik (inclusief de draaitabel) naar het bestemmingsblad

Dit is de kern van **hoe een bereik te kopiëren met opmaak**. Het `CopyOptions` object vertelt Aspose.Cells om alles te behouden: waarden, formules, stijlen en de draaitabelcache.

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **Draaitabel kopiëren:** Omdat het bronbereik de draaitabel bevat, dupliceert de API automatisch de draaitabelcache, zodat het nieuwe werkblad een volledig functionele draaitabel bevat die zich exact hetzelfde gedraagt als het origineel.

## Stap 6: Sla het bestemmings‑werkboek op

Schrijf tenslotte het resultaat naar schijf.

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

Wanneer je `dest.xlsx` opent, zie je een exacte replica van de oorspronkelijke draaitabel, compleet met de opmaak, slicers en berekende velden.

## Verwachte output

- `dest.xlsx` bevat een werkblad met de naam **Sheet1**.
- Cellen `A1:H20` bevatten dezelfde gegevens en draaitabel als de bron.
- Alle celstijlen (lettertypen, kleuren, randen) worden behouden.
- De draaitabel is volledig interactief; bij het vernieuwen wordt de onderliggende data in het gekopieerde bereik weergegeven.

## Hoe een bereik te kopiëren met opmaak – dieper duiken

Het vorige voorbeeld toont het eenvoudigste scenario, maar je kunt variaties tegenkomen die een iets andere aanpak vereisen.

### Draaitabel kopiëren naar een bestaand werkboek

Als je een **draaitabel moet dupliceren** binnen een werkboek dat al gegevens bevat, gebruik dan dezelfde `copyRange` oproep maar richt je op een ander bestemmingsadres:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### Alleen draaitabel exporteren (zonder omliggende gegevens)

Soms wil je alleen de draaitabel, niet de brongegevens. Identificeer het weergavebereik van de draaitabel via de `getPivotTable` methode:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### Voorwaardelijke opmaak behouden

Voorwaardelijke opmaakregels maken deel uit van de stijlcollectie. De `PasteType.ALL` vlag kopieert ze al, maar je kunt dit expliciet aangeven:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### Randgevallen en probleemoplossing

| Situatie | Waar op te letten | Aanbevolen oplossing |
|----------|-------------------|----------------------|
| Bron- en bestemmingswerkboeken gebruiken verschillende Excel‑versies | Sommige nieuwere draaitabel‑functies (bijv. datamodel) worden mogelijk niet correct weergegeven | Gebruik de nieuwste Aspose.Cells‑versie en stel `Workbook.setFileFormatType(FileFormatType.XLSX)` in voor beide werkboeken |
| Zeer grote draaitabellen (> 10 000 rijen) veroorzaken geheugenbelasting | Out‑of‑memory fouten tijdens het kopiëren | Schakel `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` in vóór het laden |
| Bestemmingsblad bevat al een benoemd bereik met dezelfde naam als de bron | Naamconflict leidt tot falen van `CopyOptions` | Roep `copyOptions.setIgnoreNameConflicts(true)` aan |

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren‑plakken in een Java‑klasse. Het bevat alle imports, foutafhandeling en commentaren.

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

Voer het programma uit en open vervolgens `dest.xlsx` om te verifiëren dat de draaitabel precies werkt zoals het origineel.

## Conclusie

Je weet nu **hoe een bereik te kopiëren** in Java met Aspose.Cells, inclusief hoe je **draaitabel kunt kopiëren**, **draaitabel kunt dupliceren**, en **draaitabel kunt exporteren** terwijl alle opmaak behouden blijft. De bibliotheek abstraheert de low‑level details van de XML‑structuur van Excel, zodat je je kunt concentreren op de bedrijfslogica.

### Volgende stappen

- Verken **bereik kopiëren met opmaak** voor grafieken en afbeeldingen (gebruik `PasteType.PICTURES`).
- Automatiseer batchverwerking: loop over meerdere bronbestanden en consolideer hun draaitabellen in een samenvattend werkboek.
- Combineer deze techniek met Aspose.Slides om PowerPoint‑rapporten te genereren die de gekopieerde draaitabel embedden.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe Excel‑draaitabelbron bij te werken met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Draaitabel‑laden optimaliseren in Java met Aspose.Cells – Een uitgebreide gids](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Hoe draaitabel te kopiëren in C# – Excel naar PPTX converteren, bereik kopiëren & tekstvak maken](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}