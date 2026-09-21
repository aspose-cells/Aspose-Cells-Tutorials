---
category: general
date: 2026-09-21
description: Leer hoe je een bereik in Java kunt kopiëren terwijl je de draaitabel
  behoudt. Deze stapsgewijze gids laat je zien hoe je een draaitabel veilig kunt exporteren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- preserve pivot table
- export pivot table
- how to preserve pivot
language: nl
lastmod: 2026-09-21
og_description: Hoe een bereik te kopiëren in Java terwijl de draaitabel behouden
  blijft. Volg deze complete gids om draaitabellen veilig te exporteren.
og_image_alt: Screenshot of Java code copying a range and preserving a pivot table
og_title: Hoe een bereik kopiëren en een draaitabel behouden in Java
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  headline: How to copy range and preserve a pivot table in Java
  type: TechArticle
- description: Learn how to copy range in Java while preserving the pivot table. This
    step‑by‑step guide shows you how to export a pivot table safely.
  name: How to copy range and preserve a pivot table in Java
  steps:
  - name: Load the source workbook
    text: '```java // Load the source workbook that contains the pivot table Workbook
      srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx"); Worksheet srcWs = srcWb.getWorksheets().get(0);
      ```'
  - name: Define the range that covers the pivot table
    text: '```java // Define the range covering the pivot table (including its data
      source) Range srcRange = srcWs.getCells().createRange("A1:G20"); ```'
  - name: Create an empty destination workbook
    text: '```java // Create a new, empty destination workbook Workbook destWb = new
      Workbook(); Worksheet destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range – the pivot table is preserved
    text: '```java // Copy the defined range to the destination sheet – the pivot
      table is preserved destWs.getCells().copyRange(srcRange, new CellArea("A1",
      "G20")); ```'
  - name: Save the destination workbook
    text: '```java // Save the destination workbook with the copied pivot table destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
      ```'
  - name: Copy pivot table across different workbook versions
    text: Aspose.Cells supports older `.xls` files as well as the newer `.xlsx` format.
      The same code works regardless of the file extension, making it a universal
      solution for **how to preserve pivot** across versions.
  - name: Preserving pivot table when using a filtered source
    text: 'If the source pivot is filtered, the filter state is also copied. Should
      you need to reset filters in the destination, call `PivotTable.refreshData()`
      after copying:'
  - name: Export pivot table as a static snapshot
    text: Sometimes you may want a static copy (values only) rather than a live pivot.
      Replace `copyRange` with `copyRange` followed by `pt.setEnableRefresh(false)`
      to disable further calculations.
  - name: Handling large workbooks
    text: For workbooks with many worksheets, limit the copy operation to the specific
      sheet to reduce memory usage. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to fine‑tune performance.
  type: HowTo
tags:
- Java
- Aspose.Cells
- pivot table
- Excel automation
- range copy
title: Hoe een bereik te kopiëren en een draaitabel te behouden in Java
url: /nl/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een bereik te kopiëren en een draaitabel te behouden in Java

Als je **how to copy range** nodig hebt die een draaitabel bevat, laat deze gids je een betrouwbare manier zien om de draaitabel intact te houden. Veel ontwikkelaars hebben moeite met het verliezen van de draaitabel bij het exporteren van gegevens, maar de onderstaande aanpak stelt je in staat om **copy pivot table**-gegevens te kopiëren zonder de functionaliteit te breken. Aan het einde van deze tutorial kun je de **preserve pivot table**-structuur, **export pivot table**-bestanden behouden, en begrijpen **how to preserve pivot** in verschillende scenario's.

Het voorbeeld maakt gebruik van Aspose.Cells for Java, een populaire bibliotheek voor Excel-automatisering. Er is geen extra gereedschap nodig naast een standaard Java-ontwikkelomgeving.

## Vereisten

* Java 17 (of later) geïnstalleerd.
* Maven of Gradle om afhankelijkheden te beheren.
* Aspose.Cells for Java (versie 23.9 of nieuwer). Voeg de volgende Maven‑dependency toe:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

* Een bron-werkmap (`Source.xlsx`) die de draaitabel bevat die je wilt kopiëren.

## Hoe een bereik te kopiëren en de draaitabel intact te houden

Het kernidee is om de **range** te kopiëren die de volledige draaitabel omsluit — inclusief de gegevensbron — met `copyRange`. Deze methode kopieert zowel de ruwe gegevens als de draaitabeldefinitie, waardoor de doel-werkmap een volledig functionele draaitabel ontvangt.

### Stap 1: Laad de bron-werkmap

```java
// Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Waarom deze stap?*  
Het laden van de werkmap geeft je toegang tot het werkblad dat de draaitabel bevat. De `Workbook`‑klasse abstraheert het volledige Excel‑bestand, terwijl `Worksheet` bewerkingen op celniveau biedt.

### Stap 2: Definieer het bereik dat de draaitabel omvat

```java
// Define the range covering the pivot table (including its data source)
Range srcRange = srcWs.getCells().createRange("A1:G20");
```

*Waarom deze stap?*  
Een draaitabel is niet één enkele cel; hij beslaat een blok dat kopteksten, gegevensrijen en de draaitabelcache omvat. Door een bereik op te geven dat de draaitabel volledig bevat, garandeer je dat `copyRange` ook de onderliggende cache kopieert, wat essentieel is voor het **preserve pivot table**‑gedrag.

### Stap 3: Maak een lege doel-werkmap

```java
// Create a new, empty destination workbook
Workbook destWb = new Workbook();
Worksheet destWs = destWb.getWorksheets().get(0);
```

*Waarom deze stap?*  
Beginnen met een lege werkmap voorkomt onbedoelde conflicten met bestaande bladen of benoemde bereiken. De doel-werkmap ontvangt het gekopieerde bereik, waardoor effectief **export pivot table**‑inhoud wordt overgebracht.

### Stap 4: Kopieer het bereik – de draaitabel blijft behouden

```java
// Copy the defined range to the destination sheet – the pivot table is preserved
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
```

*Waarom deze stap?*  
`copyRange` voert een diepe kopie uit: celwaarden, opmaak en draaitabel‑metadata worden overgedragen. Dit is de cruciale bewerking die **copy pivot table** mogelijk maakt zonder de functionaliteit te verliezen. Het `CellArea`‑object bepaalt waar het bereik in het doelblad terechtkomt.

### Stap 5: Sla de doel-werkmap op

```java
// Save the destination workbook with the copied pivot table
destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");
```

*Waarom deze stap?*  
Opslaan voltooit het **export pivot table**‑proces. Het resulterende bestand (`DestWithPivot.xlsx`) bevat een volledig operationele draaitabel die je kunt openen in Excel, Google Sheets of een andere spreadsheet‑viewer.

## Verifiëren dat de draaitabel behouden is gebleven

Open `DestWithPivot.xlsx` in Excel en controleer het volgende:

1. De draaitabel verschijnt op dezelfde locatie (A1:G20) als in de bron.
2. Het vernieuwen van de draaitabel werkt de gegevens correct bij, wat bewijst dat de cache is gekopieerd.
3. Alle opmaak (kolombreedtes, getalformaten) komt overeen met het origineel.

Als een van deze controles faalt, controleer dan of het bronbereik de draaitabel en de gegevensbron volledig omsluit. Een veelgemaakte fout is een bereik te selecteren dat niet tot de gegevenscache reikt, wat leidt tot een kapotte draaitabel.

## Aanvullende overwegingen

### Kopieer draaitabel over verschillende werkmapversies

Aspose.Cells ondersteunt zowel oudere `.xls`‑bestanden als het nieuwere `.xlsx`‑formaat. dezelfde code werkt ongeacht de bestandsextensie, waardoor het een universele oplossing is voor **how to preserve pivot** over versies.

### Het behouden van een draaitabel bij gebruik van een gefilterde bron

Als de bron‑draaientabel gefilterd is, wordt de filterstatus ook gekopieerd. Als je de filters in de doel‑werkmap moet resetten, roep dan `PivotTable.refreshData()` aan na het kopiëren:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.refreshData();   // Clears filters but keeps the pivot definition
```

### Exporteer draaitabel als een statisch momentopname

Soms wil je een statische kopie (alleen waarden) in plaats van een live‑draaientabel. Vervang `copyRange` door `copyRange` gevolgd door `pt.setEnableRefresh(false)` om verdere berekeningen uit te schakelen.

```java
destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));
PivotTable pt = destWs.getPivotTables().get(0);
pt.setEnableRefresh(false); // Makes the pivot static
```

### Omgaan met grote werkmappen

Voor werkmappen met veel werkbladen, beperk de kopieerbewerking tot het specifieke blad om het geheugenverbruik te verminderen. Gebruik `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` om de prestaties fijn af te stemmen.

## Volledig uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat je kunt kopiëren, plakken en uitvoeren. Pas de bestands‑paden aan zodat ze bij jouw omgeving passen.

```java
import com.aspose.cells.*;

public class CopyPivotRange {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook that contains the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Step 2: Define the range covering the pivot table (including its data source)
        // Adjust the range as needed to fully contain your pivot
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Step 3: Create a new, empty destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Step 4: Copy the defined range – the pivot table is preserved
        destWs.getCells().copyRange(srcRange, new CellArea("A1", "G20"));

        // Optional: If you need a static snapshot, disable refresh
        // PivotTable pt = destWs.getPivotTables().get(0);
        // pt.setEnableRefresh(false);

        // Step 5: Save the destination workbook with the copied pivot table
        destWb.save("YOUR_DIRECTORY/DestWithPivot.xlsx");

        System.out.println("Pivot table copied successfully. File saved as DestWithPivot.xlsx");
    }
}
```

**Verwachte output**

```
Pivot table copied successfully. File saved as DestWithPivot.xlsx
```

Wanneer je `DestWithPivot.xlsx` opent, zou je de oorspronkelijke draaitabel volledig functioneel moeten zien, wat bevestigt dat je succesvol **how to copy range** hebt uitgevoerd terwijl je de **preserve pivot table** behoudt.

## Veelvoorkomende valkuilen en pro‑tips

| Probleem | Waarom het gebeurt | Oplossing |
|----------|--------------------|-----------|
| Draaitabel verschijnt maar toont `#REF!`-fouten | Het gekopieerde bereik sloot het verborgen cache‑blad niet in | Breid het bronbereik uit om de volledige cache op te nemen (meestal de rijen onder de draaitabel) |
| Doel‑werkmap is groter dan verwacht | `copyRange` kopieert ook opmaak | Gebruik `CopyOptions` om opmaak uit te sluiten als de grootte een zorg is |
| Vernieuwen mislukt met “Data source not found” | Bron‑werkmap gebruikte externe gegevensverbindingen | Repliceer de verbinding in de doel‑werkmap of kopieer eerst het gegevensbron‑blad |

**Pro tip:** Voer altijd een snelle `destWs.getPivotTables().size()`‑controle uit na het kopiëren. Als de telling nul is, bevatte het bereik niet de draaitabeldefinitie en moet je het uitbreiden.

## Conclusie

In deze tutorial hebben we **how to copy range** aangetoond die een draaitabel bevat en gegarandeerd dat het **preserve pivot table**‑gedrag intact blijft. Door de bron‑werkmap te laden, een uitgebreid bereik te definiëren, `copyRange` te gebruiken en het doelbestand op te slaan, kun je betrouwbaar **export pivot table**‑gegevens exporteren en de vraag **how to preserve pivot** in Java‑projecten beantwoorden.

Volgende stappen die je kunt verkennen zijn onder andere:

* Het automatiseren van het kopiëren voor meerdere bladen (gebruik het secundaire trefwoord **copy pivot table** in een lus).
* Het converteren van de geëxporteerde werkmap naar CSV terwijl de ruwe gegevens behouden blijven (nog steeds **preserve pivot table**‑logica voor de bron).

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Copy Pivot Table in Java – Preserve It, Export to PPTX](/cells/english/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Export Pivot Table as an Image in C# – Step‑by‑Step Guide](/cells/english/net/pivot-tables/how-to-export-pivot-table-as-an-image-in-c-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}