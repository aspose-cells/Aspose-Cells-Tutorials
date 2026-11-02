---
category: general
date: 2026-10-01
description: Learn how to copy pivot tables between Excel workbooks using Java. This
  step‑by‑step guide also shows how to copy range between workbooks and duplicate
  Excel ranges safely.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: en
lastmod: 2026-10-01
og_description: How to copy pivot tables between Excel workbooks using Java. Follow
  this guide to copy range to workbook, duplicate Excel ranges, and preserve pivot
  data.
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: How to copy pivot tables between Excel workbooks in Java – complete guide
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: How to copy pivot tables between Excel workbooks in Java
url: /java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy pivot tables between Excel workbooks in Java

If you need to **how to copy pivot** tables from one Excel file to another, this guide gives you a ready‑to‑run solution. By the end of the first two sentences you’ll know exactly which API calls preserve the pivot definition while copying the data range.

You’ll also learn how to **copy range between workbooks**, **duplicate Excel range** objects, and safely **copy range to workbook** without losing formulas or formatting. No external scripts are required—just a single Java project that uses Aspose.Cells for Java.

## Prerequisites

Before you start, make sure you have:

* Java Development Kit 17 or later.
* Maven or Gradle to manage dependencies.
* A valid Aspose.Cells for Java license (the free evaluation works for testing).
* Two Excel files: `source.xlsx` (contains the pivot table) and an empty `destination.xlsx` (or let the code create it).

## Step 1: Set up the Maven project

Create a `pom.xml` that includes Aspose.Cells. This dependency gives you the `Workbook`, `Worksheet`, and `Range` classes used in the example.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** Keep the Aspose.Cells version up to date; newer releases add better support for complex pivot cache structures.

## Step 2: Load the source workbook that contains the pivot table

The first code block demonstrates **how to copy excel** data by loading the source file. The `Workbook` constructor reads the entire file into memory, preserving all sheet objects, including pivots.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*Why this matters:* Aspose.Cells stores pivot tables as part of the worksheet’s internal model. Loading the workbook ensures the pivot cache is available for later copying.

## Step 3: Define the range that includes the pivot table

A pivot table may span multiple rows and columns. In most cases you can copy the whole used range of the sheet. The `createRange` method builds a `Range` object that the copy operation will handle.

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

If the pivot expands beyond `H20`, simply change the address string. This step is the core of **duplicate excel range** handling; the range object knows about formulas, styles, and hidden rows.

## Step 4: Create a new workbook that will receive the copied range

You can either start with a blank workbook or load an existing destination file. Here we create a fresh workbook, which is the cleanest way to **copy range to workbook**.

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **Note:** If you need to copy the pivot into a specific sheet name, rename `destWs` with `destWs.setName("Report")` before pasting.

## Step 5: Copy the range – Aspose.Cells automatically preserves the pivot

The `copy` method transfers everything inside the source range, including the pivot definition, cache, and formatting. No extra code is required to keep the pivot functional.

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*Why it works:* Aspose.Cells treats the pivot as a collection of hidden cells and metadata attached to the range. When you call `copy`, the library replicates that metadata in the target workbook.

## Step 6: Save the destination workbook

Finally, write the result to disk. The saved file contains an identical pivot table that you can refresh or modify just like the original.

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

Running the program prints a confirmation and produces `destination.xlsx` with a fully functional pivot.

## Full, runnable example

Putting all steps together, the complete Java class looks like this:

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### Expected output

* Console: `Pivot table copied successfully.`
* `destination.xlsx` opens in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing the pivot shows the same data source, proving that **how to copy pivot** works as intended.

## Handling common variations

### Copying multiple worksheets

If your project requires copying several sheets, loop through the workbook’s worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will be preserved independently.

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### Preserving external data connections

Pivot tables that rely on external data sources keep the connection string after copying. However, the destination file must have access to the same data source. Verify the connection by opening the pivot and checking the **Data** tab.

### Dealing with merged cells

If the source range contains merged cells, Aspose.Cells copies the merge layout automatically. Still, validate the result if the destination workbook uses a different default column width.

## Best practices for reliable copying

| Practice | Reason |
|----------|--------|
| Use the exact used range (`srcWs.getCells().getMaxDisplayRange()`) instead of a hard‑coded address | Guarantees the entire pivot and its source data are included. |
| Apply a license before heavy operations | Prevents the evaluation watermark and improves performance. |
| Refresh the pivot after copying (`pivotTable.refresh()`) if the source data changed | Ensures the destination reflects the latest values. |
| Write unit tests that open the destination workbook and assert `pivotTable.getPivotFields().size()` matches the source | Detects accidental loss of fields during future code changes. |

## Conclusion

You now know **how to copy pivot** tables between Excel workbooks in Java, as well as how to **copy range between workbooks**, **duplicate excel range**, and **copy range to workbook** while preserving all formatting and formulas. The example uses Aspose.Cells, which abstracts away the low‑level XML handling required by the OpenXML SDK.

Next, explore related topics such as **updating pivot cache programmatically**, **exporting pivot data to CSV**, or **creating pivot tables from scratch**. Each of those builds on the same concepts demonstrated here.

Happy coding, and feel free to experiment with larger ranges, multiple pivots, or custom styling – the same pattern applies across all scenarios.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create Pivot Tables in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [How to Copy Multiple Columns in Excel Using Aspose.Cells Java: A Complete Guide](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}