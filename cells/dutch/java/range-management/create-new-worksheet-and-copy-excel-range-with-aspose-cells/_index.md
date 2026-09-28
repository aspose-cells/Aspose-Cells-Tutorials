---
category: general
date: 2026-09-11
description: Maak een nieuw werkblad en kopieer een Excel‑bereik met Aspose.Cells.
  Leer hoe je een bereik tussen bladen kunt kopiëren terwijl je draaitabellen behoudt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: nl
lastmod: 2026-09-11
og_description: Maak een nieuw werkblad en kopieer een Excel-bereik met Aspose.Cells.
  Deze tutorial toont de exacte stappen om een bereik tussen bladen te kopiëren en
  draaitabellen intact te houden.
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: Maak een nieuw werkblad en kopieer Excel-bereik – Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: Maak een nieuw werkblad en kopieer Excel‑bereik met Aspose.Cells
url: /nl/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nieuwe werkblad maken en Excel‑bereik kopiëren met Aspose.Cells

Als je **een nieuw werkblad moet maken** en gegevens in een Excel‑bestand wilt verplaatsen, maakt Aspose.Cells het eenvoudig. Deze gids laat precies zien hoe je een Excel‑bereik van het ene blad naar het andere kopieert, terwijl eventuele draaitabellen in het bereik behouden blijven.

Je leert hoe je **excel‑bereik kopieert**, hoe je **bereik tussen bladen kopieert**, en waarom de Aspose.Cells `copy`‑methode draaitabeldefinities intact houdt. Er zijn geen externe tools nodig – alleen een Java‑project met de Aspose.Cells‑bibliotheek.

## Vereisten

Voordat je begint, zorg dat je het volgende hebt:

- Java 17 of hoger geïnstalleerd
- Aspose.Cells for Java (versie 23.12 of nieuwer) toegevoegd aan de classpath van je project
- Een bron‑werkmap (`input.xlsx`) die een draaitabel bevat in het bereik dat je wilt kopiëren
- Basiskennis van Java‑syntaxis en Maven/Gradle‑dependency‑beheer

## Stap 1: Het project opzetten en Aspose.Cells importeren

Maak een eenvoudig Maven‑project (of Gradle, als je dat liever hebt) en voeg de Aspose.Cells‑dependency toe:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

Importeer vervolgens de benodigde klassen in je Java‑bronbestand:

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Waarom deze stap belangrijk is*: Het importeren van de juiste klassen geeft je toegang tot `Workbook`, `Worksheet`, `Range` en de `copy`‑methode die de bereik‑overdracht afhandelt.

## Stap 2: De bron‑werkmap laden

Open de werkmap die de gegevens bevat die je wilt kopiëren. De volgende code laadt `input.xlsx` vanuit een door jou opgegeven map:

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Uitleg*: `Workbook` vertegenwoordigt het volledige Excel‑bestand. Eén keer laden geeft je lees‑/schrijftoegang tot elk blad en elke celcollectie.

## Stap 3: Het bron‑bereik identificeren dat de draaitabel bevat

Selecteer het werkblad dat de draaitabel bevat en definieer het exacte celblok dat je wilt kopiëren. In dit voorbeeld kopiëren we de cellen A1 tot en met D20:

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Waarom dit belangrijk is*: Door een `Range`‑object te maken, vertel je Aspose.Cells precies welke cellen (inclusief eventuele ingesloten objecten zoals draaitabellen) moeten worden gedupliceerd.

## Stap 4: **Nieuw werkblad maken** dat de gekopieerde gegevens ontvangt

Voeg nu een nieuw blad toe aan dezelfde werkmap. Dit is het punt waarop het primaire zoekwoord verschijnt:

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Uitleg*: Het toevoegen van een nieuw blad isoleert de gekopieerde gegevens, waardoor je gemakkelijk kunt verifiëren dat de **copy excel range**‑operatie geslaagd is zonder het oorspronkelijke blad te beïnvloeden.

## Stap 5: Het bereik kopiëren – de draaitabel wordt automatisch behouden

Gebruik de `copy`‑methode om het bereik van het bronblad naar het bestemmingsblad te verplaatsen. Aspose.Cells kopieert formules, opmaak en draaitabeldefinities:

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Waarom dit werkt*: De `copy`‑methode voert een diepe kopie uit van de broncellen. Het kopieert niet alleen waarden; het dupliceert de volledige celstructuur, inclusief de pivot‑cache. Daarom kun je **copy range aspose.cells** uitvoeren en nog steeds een functionele draaitabel op het nieuwe blad zien.

## Stap 6: De werkmap opslaan met het nieuwe werkblad

Schrijf tenslotte de gewijzigde werkmap naar schijf:

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Resultaat*: `output.xlsx` bevat nu het oorspronkelijke blad plus een nieuw blad genaamd **Copy** dat exact hetzelfde bereik bevat, inclusief de draaitabel.

## Volledig werkend voorbeeld

Alle onderdelen samengevoegd, hier is het complete, uitvoerbare programma:

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Verwachte output**: Open `output.xlsx` in Excel. Je ziet een blad met de naam **Copy** waarvan de cellen A1:D20 dezelfde gegevens, opmaak en een actieve draaitabel bevatten die identiek is aan het origineel.

## Veelgestelde vragen en randgevallen

- **Wat als het bron‑bereik samengevoegde cellen bevat?**  
  De `copy`‑methode kopieert ook de samenvoeg‑informatie, zodat samengevoegde cellen ongewijzigd op het bestemmingsblad verschijnen.

- **Kan ik naar een andere werkmap kopiëren?**  
  Ja. Laad een tweede `Workbook`‑instantie, maak een bestemmings‑`Range` in die werkmap, en roep `sourceRange.copy(destinationRange)` aan. De methode handelt cross‑workbook‑kopiëren automatisch af.

- **Wat als het bestemmingsblad al gegevens bevat?**  
  De kopie‑operatie overschrijft alle bestaande cellen die overlappen met het bestemmings‑bereik. Zorg ervoor dat het bestemmingsgebied leeg is of gebruik een andere startcel (bijv. `"B2"`), om gegevensverlies te voorkomen.

- **Wordt de pivot‑cache gedupliceerd?**  
  Aspose.Cells hergebruikt de oorspronkelijke pivot‑cache, wat betekent dat de nieuwe draaitabel gekoppeld blijft aan dezelfde brongegevens. Als je een onafhankelijke cache nodig hebt, moet je de draaitabel na het kopiëren opnieuw aanmaken.

## Tips en best practices

- **Pro tip**: Gebruik `Workbook.setForceFormulaRecalculation(true)` vóór het opslaan als je bereik formules bevat die afhankelijk zijn van gegevens buiten het gekopieerde blok.
- **Let op** grote bereiken: het kopiëren van enorme bladen kan veel geheugen verbruiken. Overweeg om in kleinere stukken te kopiëren als je een `OutOfMemoryError` tegenkomt.
- **Prestatie‑tip**: Schakel scherm‑updating uit (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) bij het werken met zeer grote bestanden om het kopieerproces te versnellen.

## Conclusie

Je weet nu hoe je **nieuw werkblad maakt** en **excel‑bereik kopieert** tussen bladen met Aspose.Cells, waarbij draaitabellen en alle cel‑attributen behouden blijven. Deze techniek stelt je in staat om programmatisch gegevensblokken te dupliceren, rapport‑templates te bouwen of werkmappen te herstructureren zonder handmatig knippen‑en‑plakken.

Ga vervolgens verder met gerelateerde onderwerpen zoals **copy range aspose.cells** voor cross‑workbook‑operaties, het automatiseren van draaitabel‑verversingen, of het exporteren van het gekopieerde blad naar PDF. Experimenteer met verschillende bron‑bereiken en bladnamen om aan jouw specifieke automatiseringsscenario te voldoen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap‑uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}