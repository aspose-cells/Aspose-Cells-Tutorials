---
category: general
date: 2026-11-16
description: How to copy cells between Excel workbooks in Java – load a workbook,
  copy range between workbooks (including a pivot table), and save the workbook file.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: en
lastmod: 2026-11-16
og_description: How to copy cells between Excel workbooks in Java. Learn to load an
  Excel workbook, copy a range (including a pivot table) between workbooks, and save
  the workbook file.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: How to copy cells between Excel workbooks in Java – complete guide
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: How to copy cells between Excel workbooks in Java
url: /java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to copy cells between Excel workbooks in Java

If you need to **copy cells** from one Excel workbook to another using Java, this guide shows you a reliable way to do it. You’ll learn how to **load Excel workbook Java**, copy a range that may contain a pivot table, and finally **save workbook file** with the copied data.

This tutorial covers:

* Loading a source workbook and selecting a worksheet.  
* Defining the exact range you want to move (including a pivot table).  
* Creating a destination workbook and copying the range.  
* Saving the destination file.  

The example uses the Aspose.Cells for Java library, which works with Excel files without requiring Microsoft Office. The code runs on Java 8+ and any modern IDE (IntelliJ IDEA, Eclipse, VS Code, etc.).

---

## Prerequisites

Before you start, make sure you have:

| Requirement | Reason |
|-------------|--------|
| Java Development Kit (JDK) 8 or newer | Required to compile and run the code. |
| Maven or Gradle build tool | Simplifies adding the Aspose.Cells dependency. |
| Aspose.Cells for Java library (latest version) | Provides the `Workbook`, `Worksheet`, and `Range` classes used in the example. |
| Two Excel files (`source.xlsx` and an empty folder for `dest.xlsx`) | The source file must contain the data and, optionally, a pivot table you want to copy. |

Add the Aspose.Cells dependency to your `pom.xml` (Maven) or `build.gradle` (Gradle). Example for Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## How to copy cells with Aspose.Cells

The following steps walk you through the complete process. Each step includes the Java code, an explanation of **why** the step matters, and a tip to avoid common pitfalls.

### Step 1: Load the source workbook

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Why?**  
`Workbook` represents the entire Excel file. Loading it gives you access to all worksheets, cells, and objects such as pivot tables. Using the first worksheet is common, but you can select any sheet by name (`srcWb.getWorksheets().get("Sheet2")`).

**Pro tip:**  
If the source file is large, consider loading it in *memory‑efficient* mode: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Step 2: Define the range that includes the pivot table

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Why?**  
A `Range` object abstracts a rectangular block of cells. By specifying `"A1:G20"` you tell Aspose.Cells exactly which cells—including any embedded pivot table—to copy. The library automatically copies underlying data, styles, and pivot definitions.

**Edge case:**  
If the pivot table spans beyond the defined range, expand the address (e.g., `"A1:Z100"`). You can also use `srcWs.getCells().getMaxDataColumn()` and `getMaxDataRow()` to calculate the used area dynamically.

### Step 3: Create the destination workbook

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Why?**  
A fresh workbook ensures that no unwanted formatting or hidden sheets interfere with the copied content. The default workbook already contains one worksheet, which we will use as the target.

### Step 4: Copy the range to the destination workbook

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Why?**  
`copyRange` handles all cell attributes: values, formulas, formatting, and even pivot caches. By copying to `"A1"` you place the range at the top‑left corner of the destination sheet, preserving the original layout.

**Common question:** *Will the pivot table remain functional?*  
Yes. Aspose.Cells copies the pivot table definition and its cache, so the pivot works exactly as in the source workbook.

### Step 5: Save the destination workbook

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Why?**  
Calling `save` writes the in‑memory workbook to a physical `.xlsx` file. You can also save to other formats (`.xls`, `.csv`, `.pdf`) by changing the file extension or using `SaveOptions`.

**Tip:**  
If you need to stream the file to a web response, use `destWb.save(OutputStream, SaveFormat.XLSX);` instead of a file path.

---

## Copy range between workbooks – full source code

Below is the complete, ready‑to‑run Java class. Replace `YOUR_DIRECTORY` with the actual folder on your machine.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Expected result:**  
`dest.xlsx` contains an exact replica of the range `A1:G20` from `source.xlsx`. If the source range held a pivot table, the destination file shows the same pivot with its data source correctly linked to the copied cells.

You can open `dest.xlsx` in Excel, LibreOffice, or any viewer that supports `.xlsx` to verify that the values, formatting, and pivot functionality are preserved.

---

## Copy pivot table workbook – what you should know

* **Pivot cache is copied automatically.** The library transfers the underlying cache, so the pivot does not need to be refreshed manually.
* **External data sources are not transferred.** If the pivot pulls data from an external database, you must ensure the destination workbook can access the same source, or recreate the cache locally.
* **Large pivot tables may increase memory usage.** For very big workbooks, consider increasing the JVM heap (`-Xmx2g`) to avoid `OutOfMemoryError`.

---

## Save workbook file in different formats

Aspose.Cells lets you save the result to many formats without extra code changes:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Choose the format that matches your downstream process. The same `copyRange` logic works regardless of the final format.

---

## Load Excel workbook Java – additional tips

* **Loading encrypted files:** Use `LoadOptions` with a password:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

These options can speed up the **load excel workbook java** step, especially for large files.

---

## Conclusion

You now know **how to copy cells** between Excel workbooks in Java, how to **copy range between workbooks** that contains a **pivot table**, and how to **save workbook file** in the format you need. By following the steps above, you can integrate Excel data manipulation into any Java application—whether you’re building a reporting engine, an ETL pipeline, or a simple file‑conversion utility.

**Next steps** you might explore:

* Use **copy range between workbooks** to merge multiple reports into


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}