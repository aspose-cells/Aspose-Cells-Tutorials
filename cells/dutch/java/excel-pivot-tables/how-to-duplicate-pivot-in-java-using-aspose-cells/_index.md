---
category: general
date: 2026-09-18
description: hoe een draaitabel dupliceren in Java met Aspose.Cells – een draaitabel
  snel en betrouwbaar tussen werkmappen kopiëren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: nl
lastmod: 2026-09-18
og_description: hoe een draaitabel te dupliceren in Java met Aspose.Cells. Volg deze
  volledige tutorial om een draaitabel tussen werkmappen te kopiëren met schone Java‑code.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Dupliceer een draaitabel in Java – stapsgewijze handleiding
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Hoe een draaitabel te dupliceren in Java met Aspose.Cells
url: /nl/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe een pivot te dupliceren in Java met Aspose.Cells

Als je **hoe een pivot te dupliceren** in een Java‑applicatie nodig hebt, laat deze gids je de exacte stappen zien. Door een Excel‑werkmap te laden, het celgebied van de pivot te definiëren en dat bereik naar een nieuwe werkmap te kopiëren, kun je een pivot‑tabel verplaatsen zonder de definitie of gegevens te verliezen.

Het kopiëren van een pivot‑tabel is een veelvoorkomende eis wanneer je rapporten genereert, analyses archiveert of een grote werkmap opsplitst in modulaire delen. In deze tutorial leer je hoe je **bereik tussen werkmappen kunt kopiëren**, hoe je **Excel‑werkmap in Java kunt laden**, en de nuances van **hoe je een pivot veilig kunt kopiëren**.

Je eindigt met een kant‑klaar Java‑programma dat een pivot‑tabel dupliceert van `Source.xlsx` naar `PivotCopied.xlsx` met behulp van Aspose.Cells voor Java.

## Vereisten

* JDK 8 of nieuwer geïnstalleerd.
* Maven (of een ander build‑tool) om afhankelijkheden te beheren.
* Aspose.Cells voor Java versie 23.10 of later. Voeg de volgende Maven‑afhankelijkheid toe aan je `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Een bron‑werkmap (`Source.xlsx`) die een pivot‑tabel bevat in het bereik **A1:H30**.

## Hoe een pivot te dupliceren in Java

Het basisidee is eenvoudig:

1. **Load the source workbook** – dit geeft je toegang tot het werkblad dat de pivot bevat.
2. **Define the cell area** – het celgebied dat de pivot omsluit.
3. **Create a destination workbook** – een leeg bestand dat het gekopieerde bereik zal ontvangen.
4. **Copy the range** – Aspose.Cells dupliceert automatisch de pivot‑definitie.
5. **Save the destination workbook** – je hebt nu een apart bestand met dezelfde pivot.

Hieronder staat een compleet, uitvoerbaar Java‑programma dat deze stappen volgt.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Waarom dit werkt

* **Aspose.Cells** beschouwt een pivot‑tabel als onderdeel van de celcollectie van het werkblad. Wanneer je `copyRange` aanroept, kopieert de bibliotheek niet alleen celwaarden maar ook de onderliggende pivot‑cache en definitie, zodat de nieuwe werkmap een volledig functionele duplicaat bevat.
* Het `CopyOptions`‑object behoudt standaard formules, opmaak en ingesloten objecten. Je kunt het aanpassen (bijv. `setCopyColumnWidths(true)`) als je extra controle nodig hebt.

## Bereik tussen werkmappen kopiëren – dieper inzicht

Hoewel het bovenstaande voorbeeld een enkel aaneengesloten blok kopieert, kan `copyRange` elk rechthoekig gebied aan. Als je pivot zich uitstrekt over niet‑aangrenzende bereiken, kun je `copyRange` meerdere keren aanroepen of `Worksheet.copy` gebruiken om het hele blad te dupliceren.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tip:** Bij het kopiëren van grote werkmappen, schakel `CopyOptions.setPreserveCellStyle(true)` in om onnodige stijl‑duplicatie te vermijden, wat de prestaties kan verbeteren.

## Hoe een pivot naar een werkmap te kopiëren – meerdere pivots verwerken

Als het bronblad meer dan één pivot bevat, kun je itereren over de pivot‑tabellen van het werkblad en elke afzonderlijk kopiëren:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Deze aanpak zorgt ervoor dat elke pivot zijn oorspronkelijke naam en gegevensbron behoudt.

## Excel‑werkmap in Java laden – veelvoorkomende valkuilen

* **Scheidingstekens voor bestands‑paden:** Gebruik schuine strepen (`/`) of `File.separator` om de code platform‑onafhankelijk te houden.
* **Ontbrekende licentie:** Aspose.Cells werkt in evaluatiemodus, maar de output bevat een watermerk. Registreer een licentie met `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` vóór het laden van de werkmap om het watermerk te verwijderen.
* **Grote bestanden:** Voor werkmappen groter dan 100 MB, overweeg `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` met streaming‑opties te gebruiken om het geheugenverbruik te verminderen.

## Volledig end‑to‑end voorbeeld samenvatting

Alles bij elkaar genomen, hier is het definitieve programma dat je kunt kopiëren‑plakken in je IDE:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Verwachte output:** Na uitvoering verschijnt `PivotCopied.xlsx` in de opgegeven map. Het openen in Excel toont dezelfde pivot‑tabelindeling, filters en gegevens als in `Source.xlsx`. Alle berekende velden en opmaak blijven behouden.

## Veelgestelde vragen

* **Werkt dit met oudere Excel‑formaten (.xls)?**  
  Ja. Aspose.Cells detecteert automatisch het formaat. Gebruik `new Workbook("file.xls")` en dezelfde kopieerlogica is van toepassing.

* **Wat als de pivot naar externe gegevensbronnen verwijst?**  
  De kopie behoudt de oorspronkelijke referentie naar de gegevensbron. Als de doelomgeving die bron niet kan bereiken, zal de pivot `#REF!`‑fouten tonen. Om dit te voorkomen, vernieuw de pivot na het kopiëren of wijzig de gegevensbron via `PivotTable.setDataSource(...)`.

* **Kan ik een pivot naar een specifieke bladnaam kopiëren?**  
  Zeker. Na het aanmaken van het doel‑werkblad, hernoem je het:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Conclusie

Je weet nu **hoe je pivot‑tabellen kunt dupliceren** in Java met Aspose.Cells, hoe je **bereik tussen werkmappen kunt kopiëren**, en de best practices voor **Excel‑werkmap in Java laden**. Door het vijf‑stappenproces—laden, definiëren, bestemming maken, kopiëren en opslaan—te volgen, kun je rapportgeneratie automatiseren, analyses archiveren of complexe werkmappen opsplitsen zonder de pivot‑functionaliteit te verliezen.

Vervolgens kun je gerelateerde onderwerpen verkennen, zoals **pivot naar werkmap kopiëren** met meerdere bladen, of de gedupliceerde pivot integreren in een grotere gegevens‑verwerkings‑pipeline met Apache POI voor niet‑Aspose‑scenario's. Experimenteer met verschillende `CopyOptions`‑instellingen om de prestaties voor enorme werkmappen te optimaliseren.

Veel programmeerplezier!

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden getoond. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe draaitabellen te maken in Excel met Aspose.Cells voor Java&#58; Een uitgebreide gids](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hoe de bron van een Excel‑pivot‑tabel bij te werken met Aspose.Cells voor Java&#58; Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Pivot‑velden groeperen in Excel‑werkboeken met Aspose.Cells voor Java - Uitgebreide gids](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}