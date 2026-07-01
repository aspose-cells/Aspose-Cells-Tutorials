---
category: general
date: 2026-06-30
description: Hoe een bereik te kopiëren in Java met Aspose.Cells – een Excel-bereik
  dupliceren, draaitabel kopiëren en Excel-werkmap efficiënt laden.
draft: false
keywords:
- how to copy range
- copy pivot table
- pivot table to sheet
- duplicate excel range
- load excel workbook
language: nl
og_description: Hoe een bereik te kopiëren in Java met Aspose.Cells. Leer een Excel-bereik
  te dupliceren, een draaitabel te kopiëren en een Excel-werkmap in enkele minuten
  te laden.
og_title: Hoe bereik te kopiëren in Java – Stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  headline: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – duplicate Excel range,
    copy pivot table, and load Excel workbook efficiently.
  name: How to copy range in Java – Copy Pivot Table with Aspose.Cells
  steps:
  - name: Expected Output
    text: 'When you execute `CopyPivotDemo`, the console prints:'
  - name: What if the source workbook has multiple worksheets?
    text: You can loop through `sourceWorkbook.getWorksheets()` and copy each relevant
      range. Just be careful to maintain the same sheet names in the destination if
      you need to preserve references.
  - name: Does the copied pivot retain its data source?
    text: Yes. Aspose.Cells copies the pivot cache along with the range, so the destination
      workbook still points to the original data source within the same file. If you
      later move the data to a different sheet, you may need to refresh the pivot
      manually.
  - name: How to copy a pivot that uses an external data source?
    text: When the pivot’s data source is an external file, you’ll have to embed that
      data into the destination workbook first (e.g., copy the source data range)
      before copying the pivot. Otherwise the pivot will show “#REF!” errors.
  - name: Can I copy the pivot without the surrounding data?
    text: Absolutely. Just adjust `pivotRange` to cover only the pivot’s cells (usually
      the top‑left corner plus the data area). You can also use `sourceSheet.getPivotTables().get(0).getPivotTableArea()`
      to retrieve the exact range programmatically.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel Automation
title: Hoe een bereik te kopiëren in Java – Kopieer draaitabel met Aspose.Cells
url: /nl/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een bereik te kopiëren in Java – Kopieer draaitabel met Aspose.Cells

Heb je je ooit afgevraagd **hoe je een bereik** van de ene Excel-werkmap naar de andere kunt kopiëren zonder de integriteit van de draaitabel te verliezen? Je bent niet de enige. In veel rapportage‑pijplijnen is de noodzaak om *een Excel‑bereik te dupliceren* terwijl de draaitabel‑logica behouden blijft, een dagelijkse hoofdpijn. Gelukkig maakt Aspose.Cells voor Java dit een eitje, en in deze tutorial lopen we door een compleet, uitvoerbaar voorbeeld dat je ook laat zien hoe je **load Excel workbook**, een draaitabel kopieert en het resultaat opslaat.

Aan het einde van deze gids heb je een zelf‑containende Java‑programma dat:

* Laadt een bestaande werkmap (`load excel workbook`);
* Definieert de exacte cellen die een draaitabel bevatten;
* Kopieert die **pivot table to sheet** naar een gloednieuwe werkmap;
* Slaat het nieuwe bestand op, klaar voor downstream verwerking.

Geen externe scripts, geen handmatige stappen—alleen pure code.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

* Java 8 of nieuwer (de code werkt ook met Java 11+);
* Aspose.Cells for Java bibliotheek (je kunt het ophalen van Maven Central);
* Twee voorbeeld‑Excel‑bestanden – één bron met een draaitabel (`source.xlsx`) en een doelmap waar je `copy-pivot.xlsx` schrijft.

Dat is alles. Geen fancy IDE‑trucs nodig; elke teksteditor plus `javac` volstaat.

## Stap 1: Het project opzetten en Aspose.Cells importeren

Allereerst—laten we de bibliotheek aan boord krijgen. Als je Maven gebruikt, voeg dan deze afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Als je geen Maven gebruikt, download dan de JAR van de Aspose‑website en plaats deze op je classpath. Zodra dat geregeld is, maak je een nieuwe Java‑klasse genaamd `CopyPivotDemo`.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // The implementation will go here.
    }
}
```

> **Pro tip:** Houd je `src/main/java`‑map schoon en geef de klasse een betekenisvolle naam; dit maakt toekomstig onderhoud makkelijker.

## Stap 2: Laad de bron‑werkmap (`load excel workbook`)

Nu **laden we de Excel‑werkmap** die de draaitabel bevat die we willen kopiëren. De `Workbook`‑constructor neemt een bestandspad, dus zorg dat het pad correct is.

```java
// Step 2: Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

Waarom kiezen we het eerste werkblad? In de meeste eenvoudige gevallen staat de draaitabel op het eerste blad, maar je kunt de index wijzigen of de bladnaam gebruiken indien nodig. Deze flexibiliteit is een van de redenen waarom Aspose.Cells uitblinkt.

## Stap 3: Definieer het bereik dat de draaitabel bevat

Een draaitabel bestrijkt meestal een blok cellen. Laten we aannemen dat het `A1:G20` beslaat. Je kunt het adres aanpassen aan je werkelijke gegevens.

```java
// Step 3: Define the range that includes the pivot table
Range pivotRange = sourceSheet.getCells().createRange("A1:G20");
```

Als je niet zeker bent van het exacte adres, open dan de werkmap in Excel, selecteer de volledige draaitabel en kijk in het naamvak. Onthoud, **duplicate excel range** werkt het beste wanneer je het exacte gebied target—geen extra rijen, geen ontbrekende kolommen.

## Stap 4: Maak een nieuwe werkmap voor de bestemming

We hebben een nieuwe werkmap nodig die het gekopieerde bereik ontvangt. Hier zullen we de **copy pivot table** naar een nieuw blad kopiëren.

```java
// Step 4: Create a new workbook to receive the copied range
Workbook destinationWorkbook = new Workbook(); // starts with a default empty sheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

Op dit moment is de bestemmingswerkmap leeg, maar Aspose.Cells voegt automatisch een standaardblad toe, dat we als doel zullen gebruiken.

## Stap 5: Kopieer het bereik – draaitabel blijft intact

Hier is de magische regel die de **copy pivot table** uitvoert terwijl alle interne verbindingen behouden blijven.

```java
// Step 5: Copy the range (pivot table stays intact) to the destination sheet
destinationSheet.getCells().copy(pivotRange,
        destinationSheet.getCells().createRange("A1"));
```

De `copy`‑methode neemt twee argumenten: de bron‑`Range` en de bestemmings‑`Range`. Door de bestemming te starten bij `A1`, plaatsen we de draaitabel precies waar deze in de bron stond. Aspose.Cells kopieert de onderliggende pivot‑cache, zodat de nieuwe werkmap nog steeds weet hoe de draaitabel te vernieuwen.

## Stap 6: Sla de resulterende werkmap op

Tot slot schrijf je het nieuwe bestand naar schijf. Je kunt elk door Aspose ondersteund formaat kiezen (`.xlsx`, `.xls`, `.csv`, enz.). We blijven bij `.xlsx`.

```java
// Step 6: Save the resulting workbook
destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");
System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
```

Voer het programma uit, en je zou een nieuwe werkmap moeten zien met dezelfde draaitabel‑indeling. Open het in Excel—als alles goed ging, kun je de draaitabel vernieuwen zonder fouten.

### Verwachte output

Wanneer je `CopyPivotDemo` uitvoert, print de console:

```
Pivot table successfully copied to copy-pivot.xlsx
```

Het openen van `copy-pivot.xlsx` onthult een blad dat identiek is aan het draaitabel‑gebied van de bron, en de **pivot table to sheet** werkt precies als het origineel.

## Volledig werkend voorbeeld

Hieronder staat de complete, ready‑to‑run Java‑klasse die alle stappen samenvoegt. Kopieer‑plak het in je IDE, pas de bestandspaden aan, en start het.

```java
package com.example.excel;

import com.aspose.cells.*;

public class CopyPivotDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook (load excel workbook)
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot table
        // Adjust the address if your pivot occupies a different area
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Create a fresh workbook for the destination
        Workbook destinationWorkbook = new Workbook(); // empty workbook
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot table stays intact
        destinationSheet.getCells().copy(pivotRange,
                destinationSheet.getCells().createRange("A1"));

        // 5️⃣ Save the new workbook
        destinationWorkbook.save("YOUR_DIRECTORY/copy-pivot.xlsx");

        System.out.println("Pivot table successfully copied to copy-pivot.xlsx");
    }
}
```

> **Opmerking:** Als je draaitabel zich over meer dan één werkblad uitstrekt, herhaal dan de kopieerstap voor elk relevant blad, of gebruik `Workbook.copy` om volledige werkbladen te klonen.

## Veelgestelde vragen & randgevallen

### Wat als de bron‑werkmap meerdere werkbladen heeft?

Je kunt door `sourceWorkbook.getWorksheets()` itereren en elk relevant bereik kopiëren. Zorg er wel voor dat je dezelfde bladnamen in de bestemming behoudt als je verwijzingen moet behouden.

### Houdt de gekopieerde draaitabel zijn gegevensbron vast?

Ja. Aspose.Cells kopieert de pivot‑cache samen met het bereik, zodat de bestemmingswerkmap nog steeds naar de oorspronkelijke gegevensbron binnen hetzelfde bestand wijst. Als je later de gegevens naar een ander blad verplaatst, moet je de draaitabel mogelijk handmatig vernieuwen.

### Hoe een draaitabel te kopiëren die een externe gegevensbron gebruikt?

Wanneer de gegevensbron van de draaitabel een extern bestand is, moet je die gegevens eerst in de bestemmingswerkmap insluiten (bijv. het bron‑gegevensbereik kopiëren) voordat je de draaitabel kopieert. Anders zal de draaitabel “#REF!”‑fouten tonen.

### Kan ik de draaitabel kopiëren zonder de omringende gegevens?

Absoluut. Pas gewoon `pivotRange` aan zodat alleen de cellen van de draaitabel worden gedekt (meestal de linkerbovenhoek plus het gegevensgebied). Je kunt ook `sourceSheet.getPivotTables().get(0).getPivotTableArea()` gebruiken om het exacte bereik programmatisch op te halen.

## Tips voor real‑world projecten

* **Batchverwerking:** Als je tientallen werkmappen moet dupliceren, wikkel je de bovenstaande code in een methode en roep je deze aan binnen een lus die over een map itereert.
* **Prestaties:** Voor grote bestanden, hergebruik één `Workbook`‑instantie en roep `Workbook.calculateFormula()` pas aan nadat alle kopieën zijn voltooid.
* **Foutafhandeling:** Omring de kopielogica met try‑catch‑blokken en log `Exception.getMessage()`; Aspose gooit `CellsException` voor ongeldige bereiken.

## Conclusie

We hebben zojuist **how to copy range** in Java met Aspose.Cells behandeld, en laten zien hoe je **duplicate excel range**, **copy pivot table** en **load excel workbook** allemaal in één net programma kunt uitvoeren. De stappen zijn eenvoudig, de code is volledig uitvoerbaar, en de aanpak schaalt van een enkel‑blad demo tot enterprise‑niveau batch‑taken.

Klaar voor de volgende uitdaging? Probeer de gekopieerde draaitabel naar PDF te exporteren, of programmeermatig te vernieuwen na het toevoegen van nieuwe gegevens. Beide taken bouwen voort op dezelfde basis die we hier hebben gelegd, zodat je goed uitgerust bent om ze aan te pakken.

Heb je vragen of wil je je eigen aanpassingen delen? Laat een reactie achter—happy coding! 

![Diagram illustrating how a range with a pivot table is copied from one workbook to another](https://example.com/images/how-to-copy-range-diagram.png "how to copy range diagram")

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe een benoemd bereik met werkmap‑scope te implementeren in Aspose.Cells Java voor verbeterd Excel‑databeheer](/cells/english/java/tables-structured-references/implement-named-range-workbook-scope-aspose-cells-java/)
- [Hoe meerdere kolommen te kopiëren in Excel met Aspose.Cells Java: Een complete gids](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Excel Aspose Cells .NET Kopieer bereikgegevens](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}