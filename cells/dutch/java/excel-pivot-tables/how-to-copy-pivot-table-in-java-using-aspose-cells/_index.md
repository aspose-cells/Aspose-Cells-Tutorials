---
category: general
date: 2026-07-06
description: Hoe een draaitabel te kopiëren in Java met Aspose.Cells – stapsgewijze
  handleiding om Excel‑draaitabellen programmatisch te dupliceren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: nl
lastmod: 2026-07-06
og_description: Hoe een draaitabel te kopiëren in Java met Aspose.Cells laat u Excel-draaitabellen
  snel en betrouwbaar dupliceren.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Hoe een draaitabel kopiëren in Java – Complete Aspose.Cells-gids
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Hoe een draaitabel te kopiëren in Java met Aspose.Cells
url: /nl/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een pivot table te kopiëren in Java met Aspose.Cells

Heb je je ooit afgevraagd **hoe je pivot**‑tabellen in een Excel‑bestand kunt kopiëren zonder de werkmap handmatig te openen? Je bent niet de enige. In veel rapportage‑pijplijnen moet je **Excel pivot**‑tabellen on‑the‑fly dupliceren — misschien om een momentopname te maken, om ze naar een nieuw blad te verplaatsen, of om een sjabloon voor downstream‑gebruikers te genereren.

In deze tutorial lopen we een volledig, uitvoerbaar voorbeeld door dat precies laat zien hoe dit werkt. Met de Aspose.Cells for Java‑bibliotheek laden we een werkmap, zoeken we het bron‑pivot‑bereik, kopiëren het naar een nieuwe locatie en slaan we het resultaat op. Geen vage verwijzingen, alleen een concrete oplossing die je vandaag nog in je project kunt gebruiken.

---

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

* **Java Development Kit (JDK) 8+** – de code compileert met elke recente JDK.  
* **Aspose.Cells for Java** versie 25.11 of nieuwer – de `Range.copy`‑methode die pivot‑tabellen ondersteunt, werd geïntroduceerd in deze release.  
* Een **input.xlsx**‑bestand dat al een pivot‑table bevat (je kunt er een maken in Excel voor testdoeleinden).  
* Een build‑tool naar keuze (Maven, Gradle, of gewone `javac`). We laten de Maven‑dependency zien voor een snelle start.  

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Stap 1: Laad de bron‑werkmap

Het eerste wat we doen is het Excel‑bestand openen dat de oorspronkelijke pivot‑table bevat. Aspose.Cells behandelt de werkmap als een in‑memory object, zodat je deze kunt manipuleren zonder Excel te starten.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Waarom dit belangrijk is:** Het laden van de werkmap geeft ons toegang tot werkbladen, cellen en, cruciaal, de pivot‑cache die de pivot‑table ondersteunt. Zonder deze stap heeft de bibliotheek niets om te kopiëren.

---

## Stap 2: Haal het werkblad op dat de pivot bevat

Als je werkmap meerdere bladen heeft, moet je naar het juiste blad wijzen. Hier pakken we simpelweg het eerste blad, maar je kunt ook `get("SheetName")` gebruiken voor een op naam gebaseerde lookup.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tip:** Wanneer je met veel bladen werkt, cache dan de index of naam in een configuratiebestand om hard‑coded getallen te vermijden.

---

## Stap 3: Definieer het bron‑bereik dat de pivot‑table omvat

Vanaf versie 25.11 laat Aspose.Cells je een pivot‑table behandelen als een regulier celbereik. Geef de linkerboven‑ en rechteronder‑cellen op die de volledige pivot omsluiten.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Randgeval:** Als je pivot dynamisch uitbreidt (bijv. later worden er rijen toegevoegd), overweeg dan `worksheet.getPivotTables().get(0).getDataRange()` te gebruiken om het exacte bereik programmatisch op te halen.

---

## Stap 4: Definieer het bestemmings‑bereik waar de pivot naartoe wordt gekopieerd

Kies een lege cel waar je de gekopieerde pivot wilt laten verschijnen. In deze demo beginnen we bij **F1**, zodat er een gat ontstaat tussen het origineel en de kopie.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Waarom niet een nieuw blad?** Je kunt ook een nieuw werkblad aanmaken (`workbook.getWorksheets().add("Copy")`) en de cellen daarvan als bestemming gebruiken. Dezelfde `copy`‑methode werkt over bladen heen.

---

## Stap 5: Kopieer de pivot‑table naar de nieuwe locatie

Nu gebeurt de magie. De `copy`‑methode kloont de pivot, de cache, opmaak en zelfs eventuele gekoppelde slicers (vanaf de nieuwste versie).

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Belangrijk:** De kopie‑operatie is *diep*; hij maakt **geen** referentie terug naar de oorspronkelijke pivot. Je kunt de nieuwe pivot onafhankelijk aanpassen zonder het origineel te beïnvloeden.

---

## Stap 6: Sla de werkmap op met de gedupliceerde pivot

Tot slot schrijven we de aangepaste werkmap terug naar schijf. Je kunt het origineel overschrijven of een nieuw bestand maken; hier kiezen we voor het laatste om de bron ongewijzigd te laten.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Wanneer je **output.xlsx** in Excel opent, zie je de oorspronkelijke pivot in kolommen A‑D en een perfecte kopie beginnend in kolom F. Beide pivots kunnen afzonderlijk worden vernieuwd.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is de complete Java‑klasse die je direct kunt compileren en uitvoeren:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Verwacht resultaat:** Het openen van `output.xlsx` toont de originele pivot (A1:D20) en een identieke pivot beginnend bij F1. Beide tabellen behouden hun filters, stijlen en berekende velden.

---

## Veelvoorkomende variaties behandelen

| Situatie | Wat aan te passen |
|-----------|-------------------|
| **Meerdere pivots** op hetzelfde blad | Loop door `worksheet.getPivotTables()` en kopieer elke pivot met een eigen bestemmings‑bereik. |
| **Dynamisch gegevensbereik** | Gebruik `worksheet.getPivotTables().get(0).getDataRange()` om het brongebied automatisch te detecteren. |
| **Kopiëren naar een andere werkmap** | Laad een tweede `Workbook`‑instantie, maak een bestemmings‑werkblad aan, en roep `sourceRange.copy(destWorksheet.getCells().createRange("A1"))` aan. |
| **Slicers behouden** | Vanaf 25.12 worden slicers automatisch gekopieerd wanneer het bereik ze omvat. Controleer in Excel na het opslaan. |

---

## Pro‑tips & valkuilen

* **Versiecontrole:** De `copy`‑methode die pivots ondersteunt, is toegevoegd in **Aspose.Cells 25.11**. Als je een oudere versie gebruikt, krijg je een uitzondering. Controleer altijd de `aspose-cells`‑versie in je `pom.xml`.  
* **Prestaties:** Het kopiëren van grote pivots kan veel geheugen verbruiken. Als je alleen de gegevens nodig hebt, overweeg dan de pivot te exporteren naar een platte tabel in plaats van het hele object te klonen.  
* **Vernieuwingsgedrag:** De gedupliceerde pivot behoudt zijn eigen cache. Als je de onderliggende data wijzigt, roep dan `pivotTable.refresh()` aan op de nieuwe pivot om opnieuw te berekenen.  
* **Opmaak‑eigenaardigheden:** Sommige aangepaste getal‑opmaken overleven de kopie niet in zeer oude Excel‑versies (<2007). Test met de Excel‑versie van je doelgroep.

---

## Conclusie

Je beschikt nu over een solide, end‑to‑end‑antwoord op **hoe je pivot**‑tabellen kunt kopiëren met Aspose.Cells for Java, en je hebt gezien hoe je **Excel pivot**‑tabellen in enkele regels code kunt dupliceren. De aanpak werkt voor één of meerdere pivots, over werkbladen heen, en zelfs tussen verschillende werkmappen.

Volgende stappen kunnen zijn:

* Het automatiseren van de kopie voor elke pivot in een batch‑job.  
* Code toevoegen om de gedupliceerde pivot te hernoemen (bijv. `pivotTable.setName("Copy_of_Sales")`).  
* De routine integreren in een grotere rapportageservice die PDF‑ of CSV‑exports genereert.

Probeer het, pas de bereiken aan op jouw echte data, en laat de bibliotheek het zware werk doen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat complete werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Excel Pivot Table Manipulation with Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}