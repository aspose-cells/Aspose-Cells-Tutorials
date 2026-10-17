---
category: general
date: 2026-10-16
description: Hoe een draaitabel te kopiëren in Java met Aspose.Cells – leer hoe je
  een bereik naar een ander blad kopieert en een bereik tussen werkbladen efficiënt
  kopieert.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: nl
lastmod: 2026-10-16
og_description: Hoe een draaitabel te kopiëren in Java met Aspose.Cells. Deze tutorial
  laat zien hoe je een bereik naar een ander blad kopieert en een bereik tussen werkbladen
  kopieert met volledige code.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Hoe een draaitabel tussen werkbladen in Java te kopiëren – stapsgewijze
  handleiding
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Hoe een draaitabel tussen werkbladen te kopiëren in Java
url: /nl/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een draaitabel tussen werkbladen te kopiëren in Java

Als je **how to copy pivot table** van het ene blad naar het andere in dezelfde werkmap moet kopiëren, biedt deze gids een complete, kant‑klaar oplossing. Je ziet hoe je het bronbereik dat de draaitabel bevat kopieert, de functionaliteit behoudt en het resultaat verifieert — allemaal met Aspose.Cells for Java.

Het kopiëren van een draaitabel is een veelvoorkomende taak wanneer je rapporten programmatically genereert, en het correct uitvoeren voorkomt het verlies van de draaitabel‑cache of het breken van formules. Aan het einde van deze tutorial kun je **copy range to another sheet** en **copy range between worksheets** uitvoeren zonder handmatige stappen.

## Wat je zult leren

* Laad een bestaand Excel‑bestand met een draaitabel.
* Definieer het bronbereik dat de draaitabel bevat.
* Definieer een bestemmingsbereik op een ander werkblad.
* Gebruik `CopyOptions` om de draaitabel ongewijzigd te houden.
* Verifieer dat de gekopieerde draaitabel naar verwachting werkt.

**Prerequisites**

* Java 17 of later.
* Aspose.Cells for Java (versie 23.12 of nieuwer).  
* Een Excel‑bestand (`input.xlsx`) dat een draaitabel op het eerste blad bevat.

---

## Hoe een draaitabel te kopiëren met Aspose.Cells

De kern van de bewerking is een vier‑stappenproces: laad de werkmap, lokaliseer het bronbereik, stel het bestemmingsbereik in en voer de kopie uit. Hieronder wordt elke stap in detail uitgelegd.

### Stap 1: Laad de werkmap

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Waarom deze stap?*  
Het laden van de werkmap brengt het volledige bestand in het geheugen, waardoor je toegang krijgt tot werkbladen, cellen en de draaitabel‑cache. Aspose.Cells leest het bestandsformaat automatisch, dus je hoeft je geen zorgen te maken over `.xls` versus `.xlsx`.

### Stap 2: Lokaliseer het bronbereik dat de draaitabel bevat

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Waarom deze stap?*  
Een draaitabel wordt opgeslagen in een celblok dat ook naar een verborgen cache verwijst. Door het exacte bereik (`A1:G20` in dit voorbeeld) te selecteren, zorg je ervoor dat de cache gekoppeld blijft wanneer het bereik wordt gekopieerd.

### Stap 3: Definieer het bestemmingsbereik op een ander blad

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Waarom deze stap?*  
Het kiezen van een bestemming op een ander werkblad stelt je in staat **copy range to another sheet**. De linkerbovenste cel (`A1`) is een veelvoorkomend startpunt, maar je kunt het overal plaatsen door het adres te wijzigen.

### Stap 4: Kopieer het bronbereik terwijl je de draaitabel behoudt

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Waarom deze stap?*  
`CopyOptions` bepaalt wat er wordt overgebracht. Het gebruik van `PasteType.PASTE_ALL` garandeert dat de draaitabel, de opmaak en onderliggende formules worden gedupliceerd. Zonder deze opties worden mogelijk alleen ruwe waarden gekopieerd, waardoor de draaitabelfunctionaliteit wordt verbroken.

### Stap 5: Sla de werkmap op en verifieer het resultaat

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

Open `output.xlsx` in Excel en bevestig dat:

* Het tweede blad bevat een volledig functionerende draaitabel die identiek is aan de originele.
* Het vernieuwen van de draaitabel werkt de gegevens bij, wat bewijst dat de cache intact is.

---

## Bereik naar een ander blad kopiëren met Java

Als je doel simpelweg **copy range to another sheet** is zonder een draaitabel, werkt dezelfde code met een regulier celbereik. De enige wijziging is het bronadres. De `CopyOptions`‑configuratie blijft hetzelfde, waardoor formules en opmaak behouden blijven.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Dit fragment toont de flexibiliteit van de API voor zowel draaitabel‑ als niet‑draaitabelscenario's.

---

## Bereik tussen werkbladen kopiëren zonder formules te verliezen

Wanneer je **copy range between worksheets** uitvoert, kunnen formules die naar andere bladen verwijzen verbroken raken als de relatieve verwijzingen veranderen. Om dit te voorkomen:

1. Gebruik `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` als je alleen formules nodig hebt.
2. Houd het bestemmingsblad in dezelfde werkmap zodat interne verwijzingen geldig blijven.
3. Roep na het kopiëren `workbook.calculateFormula();` aan om een herberekening af te dwingen.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

---

## Pro‑tips en veelvoorkomende valkuilen

| Situatie | Tip |
|-----------|-----|
| **Draaitabel‑cache wordt niet bijgewerkt** | Roep na het kopiëren `destSheet.getPivotTables().get(0).refresh();` aan om de cache te vernieuwen. |
| **Kopiëren naar een andere werkmap** | Gebruik `Workbook destWorkbook = new Workbook();` en vervolgens `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`. Vergeet niet de draaitabel‑cache apart te kopiëren indien nodig. |
| **Grote draaitabellen** | Verhoog de Java‑heap‑grootte (`-Xmx2g`) om `OutOfMemoryError` tijdens het kopiëren te voorkomen. |
| **Stijlen behouden** | Stel `copyOptions.setPasteType(PasteType.PASTE_ALL)` in; anders worden alleen waarden gekopieerd. |

---

## Verwachte output

Het uitvoeren van het volledige programma produceert `output.xlsx`. Wanneer geopend in Excel:

* **Sheet2!A1:G20** toont dezelfde draaitabel als **Sheet1!A1:G20**.
* De lijst met draaitabelvelden, rij‑/kolomlabels en gegevenswaarden komen overeen met de bron.
* Het vernieuwen van de draaitabel werkt de cijfers bij, wat bevestigt dat de cache functioneel is.

De console zal afdrukken:

```
Pivot table copied successfully.
```

---

## Conclusie

In deze tutorial heb je geleerd **how to copy pivot table** van het ene werkblad naar het andere te gebruiken met Aspose.Cells for Java. Door de werkmap te laden, het juiste bronbereik te selecteren, een bestemming te definiëren en `CopyOptions` te configureren, kun je betrouwbaar **copy range to another sheet** en **copy range between worksheets** uitvoeren terwijl je alle draaitabelfunctionaliteit behoudt.  

Vervolgens kun je verkennen:

* Het geëxporteerde gekopieerde draaitabel naar PDF of HTML.
* Het automatiseren van draaitabel‑verversingen over meerdere werkmappen.
* Het gebruik van `CopyOptions` om alleen specifieke elementen te kopiëren (bijv. waarden, opmaak).

Voel je vrij om te experimenteren met verschillende bereik‑adressen, werkmap‑structuren, of zelfs kopieën tussen werkmappen. Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe bereik te kopiëren in Java – Kopieer draaitabel met Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Hoe draaitabel te kopiëren in Java – Complete Aspose.Cells-gids](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Draaitabel kopiëren Excel – Stapsgewijze gids met Java](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}