---
category: general
date: 2026-06-08
description: Create Excel programmatically with Java. Learn how to write numeric value,
  set digits, and save workbook Excel file using Aspose.Cells.
draft: false
keywords:
- create excel programmatically
- write numeric value
- save workbook excel
- save excel file
- how to set digits
language: en
og_description: Create Excel programmatically in Java. This guide shows how to write
  numeric value, control digit precision, and save the Excel file.
og_title: Create Excel programmatically – Complete Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel programmatically with Java. Learn how to write numeric
    value, set digits, and save workbook Excel file using Aspose.Cells.
  headline: Create Excel programmatically in Java – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Create a separate `ExportTableOptions` instance for each cell and assign
      it individually.
    question: What if I need more than one cell with different digit settings?
  - answer: Yes—use `Range.getExportTableOptions().set(exportOptions)` on a `Range`
      object that spans multiple cells.
    question: Can I apply the same setting to an entire range?
  - answer: No. The raw double (`12345.6789`) stays unchanged; only the visual representation
      is limited to the specified significant digits.
    question: Does this affect the underlying value?
  - answer: Aspose.Cells supports both `.xlsx` and `.xls`. Just change the file extension
      in `workbook.save()` and the library handles the conversion automatically.
    question: What about older Excel formats (`.xls`)?
  type: FAQPage
tags:
- Java
- Excel
- Aspose.Cells
title: Create Excel programmatically in Java – Step‑by‑Step Guide
url: /java/spreadsheet-automation/create-excel-programmatically-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel programmatically in Java – Complete Guide

Ever needed to **create Excel programmatically** but weren’t sure where to start? In my experience, the biggest roadblock is figuring out how to *write numeric value* with the exact precision you need while still being able to **save workbook Excel** files without a hitch.  

In this tutorial we’ll walk through a real‑world example that shows exactly **how to set digits**, write a number into a cell, and finally **save Excel file** to disk—all using the Aspose.Cells for Java library. No fluff, just a working solution you can copy‑paste into your project.

## Prerequisites

- Java 8 or newer (the code works with Java 11+ as well)  
- Maven or Gradle to pull in the Aspose.Cells dependency  
- Basic familiarity with Java syntax (if you can write a `main` method, you’re good)  

> *Pro tip:* If you don’t already have a license, you can start with the free evaluation version of Aspose.Cells – it’s fully functional for the examples below.

## Step 1: Set Up the Project and Import Aspose.Cells

First, add the Aspose.Cells Maven artifact to your `pom.xml`. If you prefer Gradle, the same coordinates work there too.

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

Once the dependency is resolved, you can import the required classes in your Java file:

```java
import com.aspose.cells.*;
```

## Step 2: Create a New Workbook – the Core of **create excel programmatically**

Now we actually **create Excel programmatically**. A `Workbook` object represents the entire spreadsheet file.

```java
// Step 2: Instantiate a new workbook (blank Excel file)
Workbook workbook = new Workbook();
```

That single line gives you a clean canvas—think of it as an empty Excel file ready to be populated.

## Step 3: Access the First Worksheet

Every workbook ships with at least one worksheet by default. Grab it so we can start placing data.

```java
// Step 3: Grab the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

You could also create additional sheets, but for this demo the default sheet is enough.

## Step 4: **Write numeric value** with Controlled Precision

Here’s where the magic happens. We’ll put a number into cell **A1**, then tell Aspose.Cells to **how to set digits**—specifically, we want only four significant digits to appear when the file is exported.

```java
// Step 4: Put a numeric value into cell A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue(12345.6789); // raw value with many decimals
```

### Defining Export Options – **how to set digits**

Aspose.Cells lets you control the number of significant digits via `ExportTableOptions`. Setting it to `4` means the exported Excel will show `1.235E+04` (or the equivalent rounded value) while keeping the underlying data intact.

```java
// Step 5: Create export options to keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setSignificantDigits(4);

// Apply the options to the cell
cell.getExportTableOptions().set(exportOptions);
```

> **Why use `ExportTableOptions`?**  
> It preserves the original numeric precision in memory, yet forces the visual representation to respect the digit limit you specify—perfect for reports where you need consistent rounding without losing data fidelity.

## Step 5: **Save workbook Excel** – the Final Piece of the Puzzle

With the data and formatting in place, it’s time to **save Excel file** to disk. Choose any directory you like; just make sure the application has write permissions.

```java
// Step 6: Save the workbook with the configured options
String outputPath = "significant-digits.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Running the program will generate `significant-digits.xlsx` in the working directory. Open it in Microsoft Excel, and you’ll see the number in **A1** displayed with only four significant digits.

## Full Working Example

Putting everything together, here’s a self‑contained class you can compile and run instantly:

```java
import com.aspose.cells.*;

public class ExcelProgrammaticDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Write a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(12345.6789);

        // 4️⃣ Define export options – keep only 4 significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(4);
        cell.getExportTableOptions().set(exportOptions);

        // 5️⃣ Save the workbook (this is how we **save workbook Excel**)
        String filePath = "significant-digits.xlsx";
        workbook.save(filePath);
        System.out.println("Excel file created: " + filePath);
    }
}
```

### Expected Output

When you run the program, the console prints:

```
Excel file created: significant-digits.xlsx
```

Opening `significant-digits.xlsx` shows **A1** containing `1.235E+04` (or `1235` depending on Excel’s display settings), confirming that the **how to set digits** option worked as intended.

## Common Questions & Edge Cases

- **What if I need more than one cell with different digit settings?**  
  Create a separate `ExportTableOptions` instance for each cell and assign it individually.

- **Can I apply the same setting to an entire range?**  
  Yes—use `Range.getExportTableOptions().set(exportOptions)` on a `Range` object that spans multiple cells.

- **Does this affect the underlying value?**  
  No. The raw double (`12345.6789`) stays unchanged; only the visual representation is limited to the specified significant digits.

- **What about older Excel formats (`.xls`)?**  
  Aspose.Cells supports both `.xlsx` and `.xls`. Just change the file extension in `workbook.save()` and the library handles the conversion automatically.

## Next Steps

Now that you know how to **create Excel programmatically**, **write numeric value**, and **save workbook Excel** with precise digit control, you might want to explore:

- Adding **styles** and **conditional formatting** to highlight important numbers.  
- Exporting the workbook to **PDF** or **CSV** for reporting pipelines.  
- Using **auto‑fit** and **column width** adjustments to make the final file look polished.  

Each of those topics builds on the foundation we’ve laid here, so feel free to experiment and extend the code.

---

![Excel workbook created programmatically](https://example.com/images/create-excel-programmatically.png "create excel programmatically")

*Image alt text:* create excel programmatically – Java example showing a filled spreadsheet

--- 

**Congratulations!** You’ve just mastered the essential steps to **create Excel programmatically** in Java, from inserting a numeric value to controlling digit precision and finally **saving the Excel file**. Keep playing with the API—there’s a whole world of spreadsheet automation waiting for you. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}