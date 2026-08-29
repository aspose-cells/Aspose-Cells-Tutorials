---
category: general
date: 2026-07-20
description: Kopieer draaitabel in Java met Aspose.Cells. Leer hoe je een draaitabel
  naar een ander bestand kunt kopiëren, het bereik van de draaitabel kunt extraheren
  en het bereik naar een nieuw werkboek kunt kopiëren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy pivot table to another file
- copy range to new workbook
- how to copy pivot table
- extract pivot table range
language: nl
lastmod: 2026-07-20
og_description: Kopieer draaitabel in Java met Aspose.Cells. Volg deze gids om de
  draaitabel naar een ander bestand te kopiëren, het bereik ervan te extraheren en
  het bereik naar een nieuwe werkmap te kopiëren.
og_image_alt: Diagram illustrating how to copy pivot table from one workbook to another
  using Java
og_title: Kopieer draaitabel in Java – Stapsgewijze Aspose.Cells‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  headline: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  type: TechArticle
- description: Copy pivot table in Java using Aspose.Cells. Learn how to copy pivot
    table to another file, extract pivot table range, and copy range to new workbook.
  name: Copy Pivot Table in Java with Aspose.Cells – Complete Guide
  steps:
  - name: Expected Output
    text: '- `CopyWithPivot.xlsx` contains a single worksheet. - The worksheet shows
      the same pivot layout as the source. - All pivot fields, filters, and calculated
      items are intact. - Refreshing the pivot updates totals based on the newly copied
      data.'
  - name: Copying Multiple Pivot Tables
    text: If your source sheet has more than one pivot, repeat the `createRange`/`copy`
      pair for each table, adjusting the address accordingly. You can also loop through
      `sourceWorksheet.getPivotTables()` to automate discovery.
  - name: Preserving Styles and Formatting
    text: The `Range.copy` method copies cell values, formulas, and formatting by
      default. However, if you only need the data without styles, use `sourceRange.copy(destinationRange,
      new CopyOptions());` and tweak the `CopyOptions` flags.
  - name: Working with Large Workbooks
    text: 'For workbooks exceeding a few hundred MB, consider enabling **memory‑efficient
      loading**:'
  - name: Quick Recap
    text: '- Loaded a source workbook containing a pivot table. - Identified the exact
      **extract pivot table range** (`A1:G20`). - Created a fresh workbook and **copied
      range to new workbook**, preserving the pivot. - Saved the result, effectively
      **copying pivot table to another file**.'
  type: HowTo
- questions:
  - answer: Yes. Aspose handles format conversion automatically during `save()`. Just
      specify the desired extension in the output path.
    question: Can I copy a pivot table across different Excel formats (XLSX → XLS)?
  - answer: The copy will overwrite existing cells. To avoid data loss, either clear
      the area first (`destinationSheet.getCells().clearRange("A1:G20")`) or choose
      a different start cell.
    question: What if the destination workbook already contains data in the target
      range?
  - answer: 'The source workbook is opened in read‑write mode by default. If you only
      need to read, pass `LoadOptions` with `setReadOnly(true)`. ## Next Steps & Related
      Topics Now that you know **how to copy pivot table** programmatically, you might
      explore: - **Refreshing pivot caches** after copying (`pivotTab'
    question: Does this work with read‑only source files?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot Table
title: Draaitabel kopiëren in Java met Aspose.Cells – Complete gids
url: /nl/java/excel-pivot-tables/copy-pivot-table-in-java-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kopieer draaitabel in Java met Aspose.Cells – Complete Gids

Heb je ooit een **draaitabel moeten kopiëren** van het ene Excel‑bestand naar het andere, maar wist je niet waar te beginnen? Je bent niet de enige. In veel rapportage‑pipelines moeten we een draaitabel‑gedreven samenvatting van een master‑werkmap naar een lichtgewicht bestand verplaatsen voor distributie, en dit handmatig doen is een gedoe.  

In deze tutorial lopen we stap voor stap een nette, programmatiche oplossing door die je **draaitabel naar een ander bestand kopiëert**, het exacte bereik extraheert, en zelfs **bereik naar nieuwe werkmap kopieert** in één keer. Aan het einde heb je een herbruikbare snippet die werkt met elk Aspose.Cells‑geactiveerd Java‑project.

## Wat deze gids behandelt

- Het laden van een bron‑werkmap die al een draaitabel bevat  
- Het bepalen van het exacte **extract draaitabel bereik** dat je nodig hebt  
- Het aanmaken van een nieuwe werkmap en het plakken van het bereik terwijl de draaitabel‑logica behouden blijft  
- Het opslaan van het resultaat als een nieuw bestand, klaar voor downstream verwerking  

Geen externe tools, geen macro‑gymnastiek—alleen pure Java‑code en een handvol Aspose.Cells‑aanroepen. Als je al met Excel hebt gewerkt, zullen de concepten vertrouwd aanvoelen; als je nieuw bent met Aspose, abstraheert de bibliotheek de low‑level XML‑afhandeling, zodat je je kunt concentreren op de bedrijfslogica.

> **Prerequisites**  
> - Java 8 of nieuwer  
> - Aspose.Cells for Java (latest versie vanaf juli 2026)  
> - Basiskennis van Excel‑draaitabellen  

Laten we nu beginnen.

## Stap 1: Stel je project in en importeer Aspose.Cells

Voordat we een werkmap aanraken, zorg ervoor dat de Aspose.Cells‑JAR op je classpath staat. Als je Maven gebruikt, voeg dan de afhankelijkheid toe:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of 2026 -->
</dependency>
```

Als je een handmatige setup verkiest, plaats `aspose-cells-24.10.jar` in je `libs`‑map en verwijs ernaar in je IDE.

> **Pro tip:** Houd de bibliotheekversie afgestemd op je Java‑runtime om `UnsupportedClassVersionError` te voorkomen.

## Stap 2: Laad de bron‑werkmap die de draaitabel bevat

Het eerste wat we nodig hebben is een `Workbook`‑object dat verwijst naar het bestand waar de draaitabel zich bevindt. Dit is waar de **copy pivot table**‑operatie begint.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook that already has the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

Waarom laden we het op deze manier? Aspose leest het volledige bestand in het geheugen, waardoor we volledige toegang hebben tot werkbladen, cellen en de onderliggende draaitabel‑cache. Dit zorgt ervoor dat de draaitabeldefinitie (velden, filters, gegevensbron) intact blijft wanneer we later kopiëren.

## Stap 3: Identificeer het exacte bereik dat de draaitabel bevat

Een draaitabel is niet alleen een blok cellen; hij wordt ondersteund door een verborgen cache. Wanneer je echter het visuele bereik kopieert, draagt Aspose de cache automatisch mee. Om zeker te zijn, definiëren we het bereik expliciet—dit is de **extract pivot table range** stap.

```java
        // Define the range covering the pivot table (adjust as needed)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)                // first worksheet
                                          .getCells()
                                          .createRange("A1:G20"); // typical size; change if larger
```

Als je niet zeker bent van de afmetingen, kun je programmatically de draaitabel lokaliseren met `Worksheet.getPivotTables()`. Voor de beknoptheid gaan we uit van een bekend rechthoekig gebied, maar dezelfde logica werkt voor dynamische ontdekking.

## Stap 4: Maak een nieuwe werkmap aan om het gekopieerde bereik te ontvangen

Nu maken we een frisse werkmap die het bestemmingsbestand wordt. Hier gebeurt **copy range to new workbook**.

```java
        // Create an empty workbook that will receive the copy
        Workbook destinationWorkbook = new Workbook(); // starts with a default sheet
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Waarom een gloednieuwe werkmap? Een schone start garandeert dat er geen vreemde opmaak of verborgen bladen de interne verwijzingen van de draaitabel verstoren. Als je moet samenvoegen met een bestaand bestand, laad dan dat bestand in plaats van `new Workbook()`.

## Stap 5: Voer de kopie uit – draaitabel blijft behouden

Hier is het hart van de tutorial: het kopiëren van het bereik terwijl de draaitabel functioneel blijft. Aspose’s `Range.copy`‑methode doet het zware werk.

```java
        // Copy the source range (including the pivot) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

Wanneer deze regel wordt uitgevoerd, kloont Aspose de visuele cellen **en** de onderliggende draaitabel‑cache naar de nieuwe werkmap. Het resultaat is een volledig operationele draaitabel die je kunt vernieuwen, filteren of exporteren, net als het origineel.

> **Common question:** *Wat gebeurt er als de bestemming al een draaitabel met dezelfde naam heeft?*  
> Aspose hernoemt de gekopieerde draaitabel automatisch om botsingen te vermijden (bijv. “PivotTable1_1”).

## Stap 6: Sla de bestemmings‑werkmap op

Tot slot persisteren we het nieuwe bestand. Dit is de stap die daadwerkelijk **copy pivot table to another file** op schijf uitvoert.

```java
        // Save the workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

Na het uitvoeren van het programma, open `CopyWithPivot.xlsx` in Excel. Je ziet dezelfde draaitabel‑lay-out, filters en gegevensbron (die nu wijst naar het gekopieerde bereik). Het vernieuwen van de draaitabel zal de totalen herberekenen op basis van het nieuwe gegevensblok.

## Volledig werkend voorbeeld

Alles bij elkaar, hier is de complete, kant‑klaar‑te‑run klasse:

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");

        // 2️⃣ Define the range that includes the pivot table (e.g., A1:G20)
        Range sourceRange = sourceWorkbook.getWorksheets()
                                          .get(0)
                                          .getCells()
                                          .createRange("A1:G20");

        // 3️⃣ Create a new workbook to receive the copied range
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range to the destination worksheet; the pivot table is preserved
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the destination workbook with the copied pivot table
        destinationWorkbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Verwachte output

- `CopyWithPivot.xlsx` bevat één werkblad.  
- Het werkblad toont dezelfde draaitabel‑lay-out als de bron.  
- Alle draaitabel‑velden, filters en berekende items zijn intact.  
- Het vernieuwen van de draaitabel werkt de totalen bij op basis van de nieuw gekopieerde gegevens.

## Edge cases & variaties behandelen

### Meerdere draaitabellen kopiëren

Als je bronblad meer dan één draaitabel heeft, herhaal dan het `createRange`/`copy`‑paar voor elke tabel, en pas het adres dienovereenkomstig aan. Je kunt ook een lus gebruiken over `sourceWorksheet.getPivotTables()` om automatische ontdekking te realiseren.

### Stijlen en opmaak behouden

De `Range.copy`‑methode kopieert standaard celwaarden, formules en opmaak. Als je alleen de gegevens zonder stijlen nodig hebt, gebruik dan `sourceRange.copy(destinationRange, new CopyOptions());` en pas de `CopyOptions`‑vlaggen aan.

### Werken met grote werkmappen

Voor werkmappen die enkele honderden MB overschrijden, overweeg **memory‑efficient loading** in te schakelen:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook sourceWorkbook = new Workbook("bigfile.xlsx", loadOptions);
```

Dit vermindert het heap‑verbruik terwijl je nog steeds bereik‑kopiëren kunt uitvoeren.

## Veelgestelde vragen

**Q: Kan ik een draaitabel kopiëren tussen verschillende Excel‑formaten (XLSX → XLS)?**  
A: Ja. Aspose verwerkt formatconversie automatisch tijdens `save()`. Geef gewoon de gewenste extensie op in het output‑pad.

**Q: Wat als de bestemmings‑werkmap al gegevens bevat in het doelbereik?**  
A: De kopie zal bestaande cellen overschrijven. Om gegevensverlies te voorkomen, wis eerst het gebied (`destinationSheet.getCells().clearRange("A1:G20")`) of kies een andere startcel.

**Q: Werkt dit met alleen‑lezen bronbestanden?**  
A: De bron‑werkmap wordt standaard in lees‑schrijfmodus geopend. Als je alleen wilt lezen, geef `LoadOptions` met `setReadOnly(true)` door.

## Volgende stappen & gerelateerde onderwerpen

Nu je weet **hoe je een draaitabel programmatically kopieert**, kun je verder verkennen:

- **Draaitabel‑caches vernieuwen** na het kopiëren (`pivotTable.refresh();`)  
- **Draaitabel‑gegevens exporteren naar CSV** voor downstream analytics  
- **Programmatically slicers toevoegen** aan de gekopieerde draaitabel (`PivotTable.addSlicer(...)`)  
- **Grafieken die gekoppeld zijn aan draaitabellen kopiëren** met `Chart.copy()`  

Elk van deze bouwt voort op de basis die we net hebben gelegd, zodat je end‑to‑end Excel‑automatiserings‑pipelines in Java kunt opzetten.

---

### Snelle samenvatting

- Een bron‑werkmap geladen die een draaitabel bevat.  
- Het exacte **extract pivot table range** (`A1:G20`) geïdentificeerd.  
- Een frisse werkmap aangemaakt en **range to new workbook gekopieerd**, waarbij de draaitabel behouden bleef.  
- Het resultaat opgeslagen, waardoor **copy pivot table to another file** effectief is uitgevoerd.  

Probeer het met je eigen bestanden, pas het bereik aan, en zie hoe de draaitabel moeiteloos migreert. Als je ergens vastloopt, laat dan een reactie achter—happy coding!

![Copy pivot table diagram showing source and destination workbooks](https://example.com/images/copy-pivot-table-diagram.png)


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe je de bron van een Excel‑draaitabel bijwerkt met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Draaitabel‑laden optimaliseren in Java met Aspose.Cells: Een uitgebreide gids](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [Excel‑draaitabelmanipulatie met Aspose.Cells Java: Een uitgebreide gids](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}