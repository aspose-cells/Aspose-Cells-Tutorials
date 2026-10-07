---
category: general
date: 2026-10-07
description: Leer hoe u draaitabellen in Excel kunt dupliceren met Java en Aspose.Cells.
  Kopieer een draaitabel door snel het bereik tussen werkmappen te kopiëren.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: nl
lastmod: 2026-10-07
og_description: Hoe draaitabellen in Excel te dupliceren met Java en Aspose.Cells.
  Volg deze gids om een draaitabel te kopiëren door het bereik tussen werkmappen te
  kopiëren.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Hoe draaitabellen in Excel te dupliceren met Java – volledige tutorial
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Hoe je draaitabellen in Excel dupliceert met Java – stapsgewijze handleiding
url: /nl/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe draaitabellen in Excel dupliceren met Java – stap‑voor‑stap gids

Als je **how to duplicate pivot** tabellen in een Excel-werkmap moet dupliceren, laat deze tutorial je een complete, kant‑klaar oplossing zien. Met Aspose.Cells for Java kun je een draaitabel samen met de brongegevens kopiëren door het onderliggende bereik te kopiëren, en vervolgens het resultaat opslaan als een nieuwe werkmap.

Het dupliceren van een draaitabel voelt vaak lastig aan omdat de pivot‑cache verborgen is in het blad. Door het volledige bereik dat de draaitabel bevat te kopiëren, maakt Aspose.Cells automatisch de cache opnieuw aan in de doelwerkmap, zodat je een volledig functionele kopie krijgt zonder handmatig XML‑geklungel.

In deze gids zul je:

* Een bronwerkmap laden die een draaitabel bevat.  
* Het exacte bereik definiëren dat de draaitabel bevat.  
* Dat bereik naar een nieuwe werkmap kopiëren, waarbij de definitie van de draaitabel behouden blijft.  
* Het nieuwe bestand opslaan en verifiëren dat de draaitabel werkt.  

De stappen werken met elke Excel‑versie die door Aspose.Cells wordt ondersteund (2007‑2024) en vereisen slechts een paar regels Java‑code.

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| **Java 8 or newer** | Aspose.Cells is gebouwd voor Java 8+. |
| **Aspose.Cells for Java** (latest version) | Biedt de `Workbook`, `Range` en `CopyRange` API's die in het voorbeeld worden gebruikt. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | De draaitabel die je wilt dupliceren. |
| **Write permission** to the target directory | Nodig om `CopyWithPivot.xlsx` op te slaan. |

Voeg de Aspose.Cells Maven‑dependency toe aan je `pom.xml` (of download de JAR handmatig):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Hoe draaitabellen dupliceren – volledige implementatie

Hieronder staat een zelfstandige Java‑programma dat **how to duplicate pivot** tabellen demonstreert door het bereik dat de draaitabel bevat te kopiëren. De code bevat foutafhandeling, commentaren en een verificatiestap.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Uitleg van elke stap

| Stap | Wat de code doet | Waarom het belangrijk is voor **copy pivot table** |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` leest `Source.xlsx`. | Het bronbestand is de enige plaats waar de originele draaitabel bestaat. |
| **2️⃣ Define the range** | `createRange("A1:G20")` maakt een `Range`‑object dat de draaitabel en de bijbehorende gegevens omvat. | Een draaitabel wordt opgeslagen samen met zijn cache; door het volledige bereik te kopiëren, wordt de cache ook verplaatst. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` schrijft het bereik naar het bestemmingsblad. | Dit is de kern van **copy range between workbooks** – de API behandelt verborgen objecten automatisch. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` dwingt de draaitabel om opnieuw te berekenen. | Garandeert dat de gedupliceerde draaitabel dezelfde waarden toont als het origineel, vooral na wijzigingen. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` schrijft het bestand naar de schijf. | Produceert het uiteindelijke **copy excel range** resultaat dat je in Excel kunt openen. |

#### Verwachte output

Na het uitvoeren van het programma, open `CopyWithPivot.xlsx`. Je zult een werkblad zien dat er identiek uitziet als het bronblad, en de draaitabel werkt precies zoals het origineel – je kunt rijen uitbreiden, velden filteren en gegevens vernieuwen zonder fouten.

## Veelvoorkomende variaties en randgevallen

### 1️⃣ Een draaitabel kopiëren die zich over meerdere bladen uitstrekt

Als de brongegevens van de draaitabel zich op een ander blad bevinden dan de draaitabel zelf, neem dan beide bladen op in de kopieerbewerking. De eenvoudigste aanpak is eerst het volledige bronblad te kopiëren, en vervolgens het draaitabelblad:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Omgaan met benoemde bereiken

Aspose.Cells behoudt benoemde bereiken wanneer je een bereik kopieert. Als de doelwerkmap echter al een naam met dezelfde identifier bevat, wordt een `CellsException` gegooid. Los dit op door de conflicterende naam te hernoemen vóór het kopiëren:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Grote werkmappen en prestaties

Het kopiëren van zeer grote bereiken (honderdduizenden rijen) kan veel geheugen verbruiken. Schakel **memory optimization** in:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Formules intact houden

Als het bronbereik formules bevat die verwijzen naar cellen buiten het gekopieerde gebied, worden die verwijzingen na het kopiëren verbroken. Om dit te voorkomen, breid je het bereik uit om alle afhankelijke cellen op te nemen, of gebruik je `copyRange` met de `CopyOptions`‑vlag `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Pro‑tips voor een betrouwbare **copy range between workbooks**

* **Gebruik altijd absolute adressen** (`$A$1:$G$20`) wanneer het bronblad mogelijk wordt hernoemd.  
* **Ververs na kopiëren** – hoewel Aspose.Cells de cache opnieuw opbouwt, verwijdert het aanroepen van `refresh()` af en toe waarschuwingen over verouderde cache in Excel.  
* **Valideer de draaitabel**: na het opslaan, open het bestand programmatisch en roep `pivotTable.validate()` aan om te verzekeren dat er geen gebroken verwijzingen zijn.  
* **Versie‑compatibiliteit**: de code werkt met Excel‑bestanden van 2007‑2024 (`.xlsx`, `.xlsm`). Voor oudere `.xls`‑bestanden, stel `LoadOptions.setLoadFormat(LoadFormat.XLS)` in.

## Volledige broncode (klaar om te compileren)



## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Hoe draaitabel kopiëren in Java – Complete Aspose.Cells-gids](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Hoe draaitabellen maken in Excel met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hoe de bron van een Excel‑draaitabel bijwerken met Aspose.Cells for Java: Een uitgebreide gids](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}