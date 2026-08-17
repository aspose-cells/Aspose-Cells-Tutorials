---
category: general
date: 2026-08-17
description: Hoe een werkblad te dupliceren in Java met Aspose.Cells, waarbij de draaitabel
  behouden blijft, de draaitabel naar een nieuw werkboek kopiëren en een werkboek
  maken van een blad.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: nl
lastmod: 2026-08-17
og_description: Hoe een werkblad te dupliceren in Java met Aspose.Cells, de draaitabel
  behouden, de draaitabel naar een nieuw werkboek kopiëren en een werkboek maken van
  een blad—alle stappen uitgelegd.
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: Hoe een werkblad te dupliceren en draaitabellen te behouden – Java‑gids
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: Hoe een werkblad te dupliceren en draaitabellen te behouden in Java
url: /nl/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een werkblad te dupliceren en draaitabellen te behouden in Java

Het dupliceren van een werkblad terwijl de draaitabel intact blijft, is een veelvoorkomende behoefte bij het automatiseren van Excel-rapportage. Deze gids laat zien hoe je een draaitabel naar een nieuw werkboek kopieert met Aspose.Cells for Java, en behandelt ook hoe je de draaitabel behoudt wanneer je een werkboek vanuit een blad maakt.

Je leert hoe je een bestaand werkboek laadt, het werkblad dat een draaitabel bevat dupliceert, en het resultaat opslaat als een nieuw bestand. De tutorial gaat ervan uit dat je een basis Java-ontwikkelomgeving hebt en een geldige Aspose.Cells-licentie (de gratis evaluatie werkt voor testen). Er zijn geen externe tools nodig naast de Aspose.Cells JAR.

## Vereisten

* Java Development Kit (JDK) 8 of nieuwer.
* Maven of Gradle om de Aspose.Cells‑dependency te beheren.
* Een Excel‑bestand (`source.xlsx`) dat minstens één draaitabel bevat op het eerste werkblad.
* Een map waarin je het bronbestand kunt lezen en het gedupliceerde werkboek kunt schrijven.

Voeg de Aspose.Cells‑dependency toe aan je `pom.xml` (Maven) of `build.gradle` (Gradle). Voor Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## Hoe een werkblad met een draaitabel te dupliceren

De kernbewerking bestaat uit een proces van drie stappen: laden, kopiëren en opslaan. Elke stap wordt hieronder uitgelegd.

### Stap 1 – Laad het werkboek dat de draaitabel bevat

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*Waarom deze stap belangrijk is*: Het `Workbook`‑object vertegenwoordigt het volledige Excel‑bestand. Door het eerste werkblad op te halen (`get(0)`), richt je je op het blad dat de draaitabel bevat die je wilt dupliceren.

### Stap 2 – Maak een nieuw werkboek en dupliceer het volledige werkblad

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` kloont het werkblad **inclusief** alle ingesloten objecten, formules en pivot‑caches. Dit is de aanbevolen manier om **hoe een draaitabel te kopiëren** omdat de definitie van de draaitabel en de gegevensbron samen worden overgedragen.

### Stap 3 – Sla het nieuwe werkboek op

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

Na uitvoering bevat `copy_with_pivot.xlsx` een exacte kopie van het oorspronkelijke blad, en werkt de draaitabel zonder extra configuratie.

**Verwacht resultaat**: Het openen van `copy_with_pivot.xlsx` in Excel toont het gedupliceerde werkblad met dezelfde draaitabel‑indeling, filters en berekende velden als het bronbestand.

## Hoe een draaitabel naar een ander werkboek te kopiëren

Als je een draaitabel wilt verplaatsen zonder het hele blad te kopiëren, kun je de pivot‑cache extraheren en aan een nieuw werkblad koppelen. Het volgende fragment demonstreert die aanpak:

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

Deze code beantwoordt **hoe een draaitabel te kopiëren** door alleen het draaitabel‑object te kopiëren, niet het volledige werkblad. De methode `addCopy` op de `PivotTables`‑collectie zorgt ervoor dat de pivot‑cache wordt gedupliceerd, wat voldoet aan de vereisten van **hoe een draaitabel te behouden**.

## Hoe een draaitabel te behouden bij het maken van een werkboek vanuit een blad

Soms begin je met een blad dat niet tot een werkboek behoort (bijvoorbeeld je genereert een blad in het geheugen). Om **een werkboek vanuit een blad te maken** terwijl je de draaitabel behoudt, volg je deze stappen:

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

Door het werkblad toe te voegen aan een nieuw `Workbook` nadat de draaitabel volledig is gedefinieerd, garandeer je dat **hoe een draaitabel te behouden** werkt, zelfs wanneer het werkblad buiten een bestaand bestand is ontstaan.

## Praktische tips en veelvoorkomende valkuilen

| Tip | Waarom het belangrijk is |
|-----|--------------------------|
| Gebruik `addCopy` in plaats van `copy` | `addCopy` kloont de onderliggende pivot‑cache; een eenvoudige `copy` kan de verbinding met de gegevensbron verliezen. |
| Houd bron‑ en bestemmingsbestanden op hetzelfde bestandssysteem | Relatieve paden in de gegevensbron van de draaitabel worden correct opgelost, waardoor “source not found”‑fouten verminderen. |
| Controleer de pivot‑cache na het kopiëren | Roep `pivot.refresh()` aan als de brongegevens zijn gewijzigd tussen het kopiëren en de opslaan‑bewerking. |
| Maak werkboeken vrij wanneer je klaar bent | `sourceWorkbook.dispose();` bevrijdt native resources, wat belangrijk is voor grote bestanden. |

## Randgevallen die je kunt tegenkomen

* **Meerdere werkbladen met onderling afhankelijke draaitabellen** – Kopieer elk werkblad afzonderlijk; gedeelde caches worden automatisch gedupliceerd, maar je moet mogelijk externe gegevensverbindingen opnieuw toewijzen.
* **Draaitabellen gebaseerd op externe SQL‑query's** – Zorg ervoor dat de bestemmingsomgeving toegang heeft tot dezelfde database; anders toont de draaitabel “#REF!”‑fouten.
* **Grote werkboeken (>100 MB)** – Gebruik `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` om de geheugenbelasting tijdens de kopieerbewerking te verminderen.

## Volledig, uitvoerbaar voorbeeld

Hieronder staat het volledige programma dat alle besproken stappen bevat. Sla het op als `CopyPivotTable.java`, pas de bestands‑paden aan, en voer het uit met je favoriete IDE of via `javac`/`java`.



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe draaitabellen te maken in Excel met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hoe de bron van een Excel‑draaitabel bij te werken met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Hoe slicers te implementeren in draaitabellen met Aspose.Cells voor Java: Een uitgebreide gids](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}