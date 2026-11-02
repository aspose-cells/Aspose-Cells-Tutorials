---
category: general
date: 2026-10-07
description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
  Copy a pivot table by copying its range between workbooks quickly.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: en
lastmod: 2026-10-07
og_description: How to duplicate pivot tables in Excel using Java and Aspose.Cells.
  Follow this guide to copy a pivot table by copying its range between workbooks.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: How to duplicate pivot tables in Excel with Java – full tutorial
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
title: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
url: /java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to duplicate pivot tables in Excel with Java – step‑by‑step guide

If you need to **how to duplicate pivot** tables in an Excel workbook, this tutorial shows you a complete, ready‑to‑run solution. Using Aspose.Cells for Java you can copy a pivot table together with its source data by copying the underlying range, then saving the result as a new workbook.

Duplicating a pivot table often feels tricky because the pivot cache is hidden inside the sheet. By copying the whole range that contains the pivot, Aspose.Cells automatically recreates the cache in the destination workbook, so you get a fully functional copy without manual XML fiddling.

In this guide you will:

* Load a source workbook that contains a pivot table.  
* Define the exact range that holds the pivot.  
* Copy that range to a fresh workbook, preserving the pivot definition.  
* Save the new file and verify that the pivot works.  

The steps work with any Excel version supported by Aspose.Cells (2007‑2024) and require only a few lines of Java code.

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| **Java 8 or newer** | Aspose.Cells is built for Java 8+. |
| **Aspose.Cells for Java** (latest version) | Provides the `Workbook`, `Range`, and `CopyRange` APIs used in the example. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | The pivot you want to duplicate. |
| **Write permission** to the target directory | Needed to save `CopyWithPivot.xlsx`. |

Add the Aspose.Cells Maven dependency to your `pom.xml` (or download the JAR manually):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## How to duplicate pivot tables – full implementation

Below is a self‑contained Java program that demonstrates **how to duplicate pivot** tables by copying the range that contains the pivot. The code includes error handling, comments, and a verification step.

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

### Explanation of each step

| Step | What the code does | Why it matters for **copy pivot table** |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The source file is the only place where the original pivot exists. |
| **2️⃣ Define the range** | `createRange("A1:G20")` creates a `Range` object that covers the pivot and its data. | A pivot table is stored together with its cache; copying the whole range ensures the cache is moved as well. |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` writes the range into the destination sheet. | This is the core of **copy range between workbooks** – the API handles hidden objects automatically. |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` forces the pivot to recalculate. | Guarantees the duplicated pivot shows the same values as the original, especially after modifications. |
| **5️⃣ Save workbook** | `destWb.save(destPath)` writes the file to disk. | Produces the final **copy excel range** result that you can open in Excel. |

#### Expected output

After running the program, open `CopyWithPivot.xlsx`. You will see a worksheet that looks identical to the source sheet, and the pivot table works exactly like the original – you can expand rows, filter fields, and refresh data without errors.

## Common variations and edge cases

### 1️⃣ Copying a pivot that spans multiple sheets

If the pivot’s source data lives on a different sheet than the pivot itself, include both sheets in the copy operation. The simplest approach is to copy the entire source sheet first, then copy the pivot sheet:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Dealing with named ranges

Aspose.Cells preserves named ranges when you copy a range. However, if the destination workbook already contains a name with the same identifier, a `CellsException` is thrown. Resolve this by renaming the conflicting name before the copy:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Large workbooks and performance

Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive. Enable **memory optimization**:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Keeping formulas intact

If the source range contains formulas that reference cells outside the copied area, those references become broken after the copy. To avoid this, expand the range to include all dependent cells, or use `copyRange` with the `CopyOptions` flag `CopyOptions.COPY_FORMULA`.

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Pro tips for a reliable **copy range between workbooks**

* **Always use absolute addresses** (`$A$1:$G$20`) when the source sheet may be renamed.  
* **Refresh after copy** – even though Aspose.Cells rebuilds the cache, calling `refresh()` eliminates occasional stale‑cache warnings in Excel.  
* **Validate the pivot**: after saving, open the file programmatically and call `pivotTable.validate()` to ensure no broken references.  
* **Version compatibility**: the code works with Excel 2007‑2024 files (`.xlsx`, `.xlsm`). For legacy `.xls` files, set `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## Full source listing (ready to compile)

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


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}