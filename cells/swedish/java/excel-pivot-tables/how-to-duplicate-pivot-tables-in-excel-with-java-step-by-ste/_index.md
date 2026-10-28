---
category: general
date: 2026-10-07
description: Lär dig hur du duplicerar pivottabeller i Excel med Java och Aspose.Cells.
  Kopiera en pivottabell genom att snabbt kopiera dess område mellan arbetsböcker.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: sv
lastmod: 2026-10-07
og_description: Hur man duplicerar pivottabeller i Excel med Java och Aspose.Cells.
  Följ den här guiden för att kopiera en pivottabell genom att kopiera dess område
  mellan arbetsböcker.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Hur man duplicerar pivottabeller i Excel med Java – fullständig handledning
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
title: Hur man duplicerar pivottabeller i Excel med Java – steg‑för‑steg‑guide
url: /sv/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man duplicerar pivottabeller i Excel med Java – steg‑för‑steg‑guide

Om du behöver **hur man duplicerar pivot** tabeller i en Excel‑arbetsbok, visar den här handledningen en komplett, färdig‑att‑köra lösning. Med Aspose.Cells för Java kan du kopiera en pivottabell tillsammans med dess källdata genom att kopiera det underliggande området, sedan spara resultatet som en ny arbetsbok.

Att duplicera en pivottabell känns ofta knepigt eftersom pivot‑cachen är dold i bladet. Genom att kopiera hela området som innehåller pivottabellen återskapar Aspose.Cells automatiskt cachen i mål‑arbetsboken, så du får en fullt funktionell kopia utan manuell XML‑hantering.

I den här guiden kommer du att:

* Ladda en källarbetsbok som innehåller en pivottabell.  
* Definiera det exakta området som innehåller pivottabellen.  
* Kopiera det området till en ny arbetsbok, bevarande pivottabellens definition.  
* Spara den nya filen och verifiera att pivottabellen fungerar.  

Stegen fungerar med alla Excel‑versioner som stöds av Aspose.Cells (2007‑2024) och kräver bara några rader Java‑kod.

## Förutsättningar

| Krav | Varför det är viktigt |
|------|-----------------------|
| **Java 8 or newer** | Aspose.Cells är byggt för Java 8+. |
| **Aspose.Cells for Java** (latest version) | Tillhandahåller `Workbook`, `Range` och `CopyRange` API:erna som används i exemplet. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Pivottabellen du vill duplicera. |
| **Write permission** to the target directory | Behövs för att spara `CopyWithPivot.xlsx`. |

Lägg till Aspose.Cells Maven‑beroendet i din `pom.xml` (eller ladda ner JAR‑filen manuellt):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Så duplicerar du pivottabeller – fullständig implementation

Nedan finns ett självständigt Java‑program som demonstrerar **hur man duplicerar pivot** tabeller genom att kopiera området som innehåller pivottabellen. Koden innehåller felhantering, kommentarer och ett verifieringssteg.

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

### Förklaring av varje steg

| Steg | Vad koden gör | Varför det är viktigt för **copy pivot table** |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` läser `Source.xlsx`. | Källfilen är den enda platsen där den ursprungliga pivottabellen finns. |
| **2️⃣ Define the range** | `createRange("A1:G20")` skapar ett `Range`‑objekt som täcker pivottabellen och dess data. | En pivottabell lagras tillsammans med sin cache; genom att kopiera hela området säkerställs att cachen också flyttas. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` skriver området till destinationsbladet. | Detta är kärnan i **copy range between workbooks** – API‑et hanterar dolda objekt automatiskt. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` tvingar pivottabellen att beräkna om. | Säkerställer att den duplicerade pivottabellen visar samma värden som originalet, särskilt efter ändringar. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` skriver filen till disk. | Skapar det slutgiltiga **copy excel range**‑resultatet som du kan öppna i Excel. |

#### Förväntat resultat

Efter att programmet har körts, öppna `CopyWithPivot.xlsx`. Du kommer att se ett kalkylblad som ser identiskt ut med källbladet, och pivottabellen fungerar exakt som originalet – du kan expandera rader, filtrera fält och uppdatera data utan fel.

## Vanliga variationer och kantfall

### 1️⃣ Kopiera en pivottabell som sträcker sig över flera blad

Om pivotens källdata finns på ett annat blad än själva pivottabellen, inkludera båda bladen i kopieringsoperationen. Det enklaste tillvägagångssättet är att först kopiera hela källbladet och sedan kopiera pivottabellbladet:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Hantera namngivna områden

Aspose.Cells bevarar namngivna områden när du kopierar ett område. Om mål‑arbetsboken redan innehåller ett namn med samma identifierare kastas ett `CellsException`. Lös detta genom att byta namn på det konflikterande namnet innan kopieringen:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Stora arbetsböcker och prestanda

Att kopiera mycket stora områden (hundratusentals rader) kan vara minnesintensivt. Aktivera **memory optimization**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Behålla formler intakta

Om källområdet innehåller formler som refererar till celler utanför det kopierade området, blir dessa referenser brutna efter kopieringen. Undvik detta genom att utöka området så att alla beroende celler inkluderas, eller använd `copyRange` med flaggan `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Pro‑tips för en pålitlig **copy range between workbooks**

* **Använd alltid absoluta adresser** (`$A$1:$G$20`) när källbladet kan bli omdöpt.  
* **Uppdatera efter kopiering** – även om Aspose.Cells bygger om cachen, eliminerar ett anrop till `refresh()` ibland varningar om föråldrad cache i Excel.  
* **Validera pivottabellen**: efter sparning, öppna filen programatiskt och anropa `pivotTable.validate()` för att säkerställa att inga brutna referenser finns.  
* **Versionkompatibilitet**: koden fungerar med Excel‑filer från 2007‑2024 (`.xlsx`, `.xlsm`). För äldre `.xls`‑filer, sätt `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Fullständig källkod (klar att kompilera)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Hur man kopierar pivottabell i Java – komplett Aspose.Cells‑guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Hur man skapar pivottabeller i Excel med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Hur man uppdaterar källan för Excel‑pivottabell med Aspose.Cells för Java: En omfattande guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}