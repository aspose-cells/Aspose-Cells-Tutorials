---
category: general
date: 2026-09-27
description: Learn how to generate dynamic sheet names in Excel with Java while you
  populate an Excel template and create sheets from data for robust reporting.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: en
lastmod: 2026-09-27
og_description: Dynamic sheet names let you generate multiple sheets from a data set.
  This tutorial shows how to populate an Excel template in Java and create sheets
  from data using Aspose.Cells.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: Generate dynamic sheet names in Excel with Java
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to generate dynamic sheet names in Excel with Java
url: /java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to generate dynamic sheet names in Excel with Java

If you need **dynamic sheet names** when you populate an Excel template in Java, this guide walks you through the complete process. You’ll see how to *generate multiple sheets* from a collection of data, and how each sheet receives a unique name automatically. By the end you’ll have a runnable example that creates sheets from data and saves the result with the desired naming convention.

Generating sheets on the fly is a common requirement for reporting dashboards, invoice batches, or any scenario where the number of detail sections isn’t known ahead of time. The Aspose.Cells Smart Marker engine makes this task concise and reliable, and the code below demonstrates the recommended approach.

## Using dynamic sheet names with Aspose.Cells

Aspose.Cells for Java provides a **Smart Marker** processor that can read placeholders in a template workbook and expand them into rows, columns, or even new worksheets. By configuring `SmartMarkerOptions.DetailSheetNewName` you control the name of each generated sheet. The placeholder `{0}` is replaced with the zero‑based index of the current data row, giving you fully **dynamic sheet names** such as `Detail_0`, `Detail_1`, …​.

> **Pro tip:** Keep the template workbook in a dedicated resources folder and use a relative path when possible. This avoids hard‑coding absolute paths that break on different environments.

## Step 1: Load the Excel template (populate excel template java)

First, load the workbook that contains the Smart Marker tags. The template should have a sheet named, for example, `Detail` with a marker like `&=Orders!A1` that tells the processor where to start inserting rows.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*Why this step matters:* The template defines the layout (headers, formulas, formatting) that will be copied to each generated sheet. Without a proper template, the output would lose styling and formulas.

## Step 2: Prepare the data source to create sheets from data

Next, build a data source that the Smart Marker processor can iterate over. In this example we use a `Map<String, Object>` where the key `"Orders"` matches the marker name in the template.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*Why this step matters:* The Smart Marker engine reads the array, creates a row for each inner `Object[]`, and—because we will ask it to generate new sheets—creates a separate worksheet for each row. This is the core of **create sheets from data**.

## Step 3: Configure SmartMarkerOptions to generate multiple sheets with unique names

Now tell Aspose.Cells how to name each new worksheet. The `{0}` placeholder is replaced with the current row index.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*Why this step matters:* Without setting `DetailSheetNewName`, the processor would reuse the original sheet name for every row, overwriting data. This option is what enables **dynamic sheet names**.

## Step 4: Process the SmartMarkers and generate the workbook

Run the processor with the data source and the options we just configured.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*Why this step matters:* The processor expands the markers, creates the required number of worksheets, copies the template layout, and fills each sheet with the corresponding row data.

## Step 5: Save and verify the result

Finally, write the workbook to disk. Open the file in Excel to see the automatically created sheets.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**Expected output**

When you open `MasterDetailResult.xlsx` you should see three new worksheets:

* `Detail_0` – contains order 101 (Alice, 250.00)  
* `Detail_1` – contains order 102 (Bob, 175.50)  
* `Detail_2` – contains order 103 (Carol, 320.75)

Each sheet retains the formatting, column widths, and any formulas that existed in the original `Detail` template sheet.

## Complete runnable example

Putting all sections together gives you a self‑contained program you can compile and run:

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### How to run

1. Add the Aspose.Cells for Java JAR to your project’s classpath (available from Maven Central or the Aspose website).  
2. Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project root.  
3. Execute the `main` method. The `output/` folder will contain the generated file.

## Common variations and edge cases

| Situation | What to change |
|-----------|----------------|
| **Different naming pattern** | Use `"OrderSheet_{0}_v{1}"` and include additional placeholders like `{1}` for a second index (e.g., a page number). |
| **Large data sets** | Increase the JVM heap (`-Xmx2g`) to avoid `OutOfMemoryError` when generating hundreds of sheets. |
| **Conditional sheet creation** | Before calling `process`, filter the data array so rows that don’t meet a criterion are omitted, thereby preventing unnecessary sheets. |
| **Preserving formulas that reference other sheets** | Keep the original sheet name as a hidden placeholder (e.g., `DetailTemplate`) and use `SmartMarkerOptions.setDetailSheetNewName` only for the visible name; formulas that refer to the hidden name will still resolve correctly. |

## Tips for robust Excel automation

* **Validate the data source** – Ensure every inner array has the same number of elements as the columns defined in the template; mismatched lengths cause runtime errors.  
* **Use named ranges** in the template for clearer Smart Marker syntax (`&=Orders!A1`).  
* **Close resources** – Although Aspose.Cells manages streams internally, explicitly calling `templateWorkbook.dispose()` in a `finally` block can free native memory faster.  
* **Test with edge values** – Zero rows should produce a workbook with only the original template sheet; an empty data source verifies that your code handles “no data” gracefully.

## Conclusion

You now know how to **generate dynamic sheet names** in Excel using Java, how to **populate an Excel template** and **create sheets from data**, and how to **generate multiple sheets** automatically with Aspose.Cells Smart Markers. By following the steps above you can adapt the pattern to any reporting scenario—whether you need dozens of detail sheets, custom naming conventions, or conditional sheet creation.

Ready to extend this solution? Try adding charts to each generated sheet, or export the workbook to PDF using `Workbook.save("result.pdf", SaveFormat.PDF)`. Both techniques build on the same dynamic‑sheet foundation you’ve just mastered. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Dynamic Excel Sheets in Java with Aspose.Cells: A Comprehensive Guide](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dynamic Excel Sheets Aspose Cells Java Guide](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}