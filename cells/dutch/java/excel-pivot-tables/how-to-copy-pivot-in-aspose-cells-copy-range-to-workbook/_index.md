---
category: general
date: 2026-08-08
description: Hoe een draaitabel te kopiëren in Aspose.Cells en een bereik naar een
  werkmap te kopiëren met Java. Leer de exacte stappen om een draaitabel te dupliceren
  met CopyOptions.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: nl
lastmod: 2026-08-08
og_description: Hoe een draaitabel te kopiëren in Aspose.Cells en een bereik naar
  een werkmap te kopiëren met Java. Volg deze volledige gids om een draaitabel te
  dupliceren met CopyOptions.
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: Hoe een draaitabel te kopiëren in Aspose.Cells – bereik naar werkmap kopiëren
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: Hoe een draaitabel te kopiëren in Aspose.Cells – bereik naar werkmap kopiëren
url: /nl/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel te kopiëren in Aspose.Cells – bereik naar werkmap kopiëren

Als je **hoe je een draaitabel moet kopiëren** in een Excel‑bestand met Aspose.Cells, laat deze gids je het exacte proces zien. Aan het einde van de tutorial kun je **bereik naar werkmap kopiëren** terwijl je de definitie van de draaitabel behoudt.

Het voorbeeld gebruikt Java, maar dezelfde concepten zijn van toepassing op elke .NET‑taal die met Aspose.Cells werkt. Er zijn geen externe tools nodig—alleen de Aspose.Cells for Java‑bibliotheek en een basisontwikkelomgeving.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

* Java Development Kit (JDK) 8 of hoger.
* Maven of Gradle om afhankelijkheden te beheren (het voorbeeld gebruikt Maven).
* Aspose.Cells for Java 23.9 (of de nieuwste versie) toegevoegd aan je project.
* Een invoer‑werkmap (`input.xlsx`) die minstens één draaitabel bevat op het eerste werkblad.

Het hebben van deze items voorkomt runtime‑fouten wanneer de code de werkmap benadert.

## Hoe een draaitabel te kopiëren met Aspose.Cells

Deze sectie loopt stap voor stap door wat nodig is om **hoe je een draaitabel moet kopiëren** van het ene deel van een blad naar een ander, met behulp van de `CopyOptions`‑klasse.

### Stap 1: Voeg Aspose.Cells toe aan je project

Als je Maven gebruikt, voeg dan de volgende afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*Waarom deze stap belangrijk is*: De bibliotheek levert de `Workbook`, `CopyOptions` en andere klassen die nodig zijn voor **aspose.cells copy range**‑bewerkingen. Zonder de afhankelijkheid kan de compiler die types niet vinden.

### Stap 2: Laad de bron‑werkmap

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Het laden van het bestand maakt een in‑memory‑representatie van het spreadsheet. Het `Workbook`‑object geeft je toegang tot werkbladen, cellen en draaitabellen.

### Stap 3: Configureer kopieeropties om de draaitabel op te nemen

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` vertelt Aspose.Cells dat de bewerking de metadata van de draaitabel moet behouden. Als je deze vlag weglaat, wordt de draaitabel gereduceerd tot statische gegevens, waardoor de interactiviteit verloren gaat.

### Stap 4: Kopieer het gewenste bereik met de draaitabel

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

De `copyRange`‑methode kopieert cellen, opmaak, en—door de opties die in de vorige stap zijn ingesteld—eventuele draaitabellen die het bereik kruisen. Dit is de kern van de **copy range to workbook**‑functionaliteit.

### Stap 5: Sla de aangepaste werkmap op

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

Opslaan schrijft de wijzigingen naar een nieuw bestand (`output.xlsx`). Je kunt dit bestand nu in Excel openen en zien dat de draaitabel precies is gedupliceerd op de plek waar het bereik is gekopieerd.

## Volledig, uitvoerbaar voorbeeld

Door alle onderdelen samen te voegen, is hier het volledige programma dat je kunt compileren en uitvoeren:

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### Verwacht resultaat

* `output.xlsx` bevat dezelfde gegevens als `input.xlsx`.
* De draaitabel die oorspronkelijk het bronbereik bezette, verschijnt in de doelcellen, volledig functioneel (filters, vernieuwingsmogelijkheid, enz.).
* Alle celopmaak, formules en kolombreedtes worden behouden omdat `copyRange` het volledige celblok kopieert.

## Veelgestelde vragen en randgevallen

**Wat als het doelbereik overlapt met een bestaande draaitabel?**  
Aspose.Cells zal de doelcellen overschrijven. Om gegevensverlies te voorkomen, zorg dat het doelgebied leeg is of verplaats eerst de bestaande draaitabel.

**Kan ik een draaitabel over verschillende werkbladen kopiëren?**  
Ja. Gebruik `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);` waarbij `targetSheetIndex` naar het doelblad wijst.

**Kopieert `setCopyPivotTable(true)` de onderliggende gegevensbron?**  
De methode kopieert alleen de verwijzing naar de pivot‑cache. Als de brongegevens zich in dezelfde werkmap bevinden, zal de doel‑draaientabel naar dezelfde cache wijzen. Om de cache te dupliceren, moet je handmatig een nieuwe pivot‑cache maken.

**Hoe kopieer je een groot bereik efficiënt?**  
Bij het kopiëren van zeer grote bereiken, overweeg dan alleen `CopyOptions.setCopyFormula(true)` en `setCopyDataValidation(true)` te gebruiken indien nodig. Het verminderen van het aantal opties kan de prestaties verbeteren.

## Tips voor betrouwbaar gebruik van **aspose.cells copy range**

* **Pro tip:** Roep altijd `workbook.calculateFormula()` aan na het kopiëren als het bereik formules bevat die afhankelijk zijn van de pivot‑cache.
* **Let op:** Verborgen werkbladen. `copyRange` werkt alleen op zichtbare werkbladen, tenzij je expliciet het verborgen blad via index aanroept.
* **Versiecontrole:** De `setCopyPivotTable`‑vlag is beschikbaar vanaf Aspose.Cells 20.9. Zorg ervoor dat jouw bibliotheekversie dit ondersteunt.

## Conclusie

Je weet nu **hoe je een draaitabel moet kopiëren** in Aspose.Cells en hoe je **bereik naar werkmap kunt kopiëren** terwijl je de volledige functionaliteit van de draaitabel behoudt. De stappen—het toevoegen van de bibliotheek, het laden van de werkmap, het configureren van `CopyOptions`, het uitvoeren van de kopie en het opslaan—vormen een herhaalbaar patroon dat je kunt aanpassen aan andere kopiëren‑en‑plakken‑scenario's.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **aspose.cells copy range** voor grafieken, voorwaardelijke opmaak en gegevensvalidatie. Experimenteer met het kopiëren tussen verschillende bestandsformaten (XLSX → XLS) om je automatiseringsmogelijkheden uit te breiden. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe draaitabellen te maken in Excel met Aspose.Cells voor Java&#58; Een uitgebreide gids](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hoe de bron van een Excel‑draaientabel bij te werken met Aspose.Cells voor Java&#58; Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hoe slicers te implementeren in draaitabellen met Aspose.Cells voor Java&#58; Een uitgebreide gids](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}