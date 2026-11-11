---
category: general
date: 2026-10-26
description: Leer hoe je een draaitabel naar een nieuw werkboek kunt kopiëren met
  Java, waarbij je de opmaak en de draaitabeldefinitie behoudt terwijl je een Excel-bereik
  met opmaak kopieert via Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: nl
lastmod: 2026-10-26
og_description: Kopieer draaitabel naar een nieuw werkboek in Java met Aspose.Cells.
  Deze gids laat zien hoe je een Excel-bereik kopieert, opmaak behoudt en efficiënt
  een leeg werkboek maakt.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Kopieer draaitabel naar een nieuw werkboek in Java – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hoe een draaitabel naar een nieuw werkboek kopiëren in Java
url: /nl/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel naar een nieuw werkboek kopiëren in Java

Als je een **draaitabel** van het ene Excel‑bestand naar het andere moet **kopiëren**, laat deze gids je een volledige, uitvoerbare oplossing zien. Je ziet hoe je de draaitabeldefinitie behoudt, alle opmaak behoudt en veelvoorkomende valkuilen bij het kopiëren van een Excel‑bereik vermijdt.

Het kopiëren van een draaitabel roept vaak vragen op zoals *hoe een draaitabel te kopiëren* zonder de gegevensbron te breken of stijlen te verliezen. Aan het einde van deze tutorial heb je een zelfstandige Java‑programma dat een leeg werkboek maakt, het gewenste bereik kopieert en het resultaat opslaat met de draaitabel intact.

## Wat je zult bereiken

* Een bron‑werkboek laden dat een draaitabel bevat.  
* **Leeg werkboek maken** dat de gekopieerde gegevens zal ontvangen.  
* **Excel‑bereik kopiëren** dat de draaitabel omvat, met opties die de draaitabel en opmaak behouden.  
* Het bestemmingsbestand opslaan en verifiëren dat de draaitabel exact werkt zoals het origineel.

### Vereisten

* Java 17 of hoger.  
* Aspose.Cells for Java (versie 23.10 of nieuwer).  
* Basiskennis van Java‑IDE’s (IntelliJ IDEA, Eclipse, enz.).  

> **Pro tip:** Gebruik de gratis Aspose.Cells evaluatielicentie voor snelle tests; vervang deze door een volledige licentie vóór productiegebruik.

## Draaitabel naar een nieuw werkboek kopiëren

De eerste stap is het instellen van de bron‑ en bestemmingswerkboeken. De bestemming begint met een **leeg werkboek maken**‑aanroep, die je een schoon bestand met één werkblad geeft.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Waarom dit werkt

* `new Workbook()` **maakt leeg werkboek** met een standaardblad, waardoor je geen bestaande gegevens hoeft te verwijderen.  
* `CopyOptions` vertelt Aspose.Cells om **draaitabel**‑metadata te kopiëren, niet alleen ruwe waarden. De `PASTE_ALL`‑modus draagt ook celstijlen, getalformaten en voorwaardelijke opmaak mee—wat voldoet aan de **kopieer bereik met opmaak**‑vereiste.  
* `copyRange` voert een **kopieer Excel‑bereik**‑operatie uit die de interne structuren van de bron respecteert, zodat de draaitabel functioneel blijft na het kopiëren.

## Hoe een draaitabel te kopiëren zonder opmaak te verliezen

Als je alleen de standaard `CopyOptions` gebruikt, kan enige stijl‑informatie weggelaten worden in oudere Aspose.Cells‑versies. Het expliciet instellen van het plak‑type garandeert dat **kopieer bereik met opmaak** wordt gerespecteerd.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

Het toevoegen van `setPasteSpecialType` zorgt ervoor dat kolombreedtes, rijhoogtes en zelfs gegevensvalidatieregels met het bereik meereizen. Dit is vooral nuttig wanneer de draaitabel zich over meerdere kolommen met aangepaste breedtes uitstrekt.

## Leeg werkboek maken vóór het kopiëren

Soms proberen ontwikkelaars te kopiëren naar een bestaand werkboek dat al gegevens bevat. Dat kan overlappende bereiken of onverwachte overschrijvingen veroorzaken. Beginnen met een **leeg werkboek maken**‑aanroep isoleert de bewerking:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Als je meer dan één blad in de bestemming nodig hebt, kun je ze na het kopiëren toevoegen:

```java
destWb.getWorksheets().add("Summary");
```

## Excel‑bereik met opmaak kopiëren met CopyOptions

Naast draaitabellen werkt hetzelfde patroon voor elk **kopieer Excel‑bereik** dat opmaakbehoud vereist—grafieken, tabellen of voorwaardelijke opmaak.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

De `CopyOptions`‑instantie blijft hetzelfde, zodat je consistent gedrag krijgt over verschillende bereiken.

### Randgevallen om te overwegen

| Situatie                              | Aanbevolen afhandeling |
|----------------------------------------|------------------------|
| Bron‑werkboek heeft meerdere draaitabellen   | Kopieer elk draaitabel‑bereik afzonderlijk of kopieer het hele blad. |
| Bestemming bevat al gegevens      | Kies een niet‑conflictende startcel (bijv. "H1") bij het aanroepen van `copyRange`. |
| Draaitabel‑gegevensbron is extern (bijv. DB) | Zorg dat het bestemmings‑werkboek naar dezelfde externe gegevensbron wijst, of vernieuw de draaitabel na het kopiëren. |
| Groot werkboek ( > 10 MB )             | Verhoog de Java‑heap‑grootte (`-Xmx2g`) om `OutOfMemoryError` te voorkomen. |

## Het resultaat verifiëren

Na het uitvoeren van het programma, open `destination.xlsx`. Je zou moeten zien:

* Hetzelfde draaitabel‑layout als in `source.xlsx`.  
* Alle celkleuren, getalformaten en kolombreedtes behouden.  
* De gegevensbron van de draaitabel wijst nog steeds naar het oorspronkelijke gegevensbereik binnen het nieuwe bestand, zodat het vernieuwen van de draaitabel de waarden correct bijwerkt.

Als de draaitabel verschijnt als een statische tabel, controleer dan of `CopyOptions.setPasteType(PasteType.PASTE_ALL)` is ingesteld. Zonder deze optie behandelt Aspose.Cells de draaitabel als gewone data.

## Conclusie

Je weet nu hoe je een **draaitabel** naar een nieuw werkboek in Java kunt **kopiëren** terwijl je opmaak, gegevensverbindingen en bladindeling behoudt. De volledige oplossing toont het laden van een bronbestand, **leeg werkboek maken**, het configureren van **kopieer Excel‑bereik**‑opties, en het opslaan van het resultaat.  

Vanaf hier kun je gerelateerde onderwerpen verkennen, zoals **hoe een draaitabel te kopiëren** tussen verschillende werkbladen, grafieken naast draaitabellen insluiten, of batchverwerking van meerdere werkboeken automatiseren. Experimenteer met de `CopyOptions`‑instellingen om ze aan te passen aan jouw specifieke automatiseringsbehoeften, en je hebt een robuuste Excel‑manipulatie‑toolkit binnen handbereik.


## Wat moet je hierna leren?


De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Create New Workbook in Java – Full Guide to Copy Pivot Table](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copy Pivot Table Between Workbooks – Step‑by‑Step Java Guide](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}