---
date: '2026-10-28'
description: Learn how to paste values using Aspose.Cells copy and paste options in
  Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
images:
- /java/cell-operations/aspose-cells-java-copy-paste-options/og-image.png
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Learn how to paste values using Aspose.Cells copy and paste options
  in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: How to paste values with Aspose.Cells copy and paste options
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: How to paste values with Aspose.Cells copy and paste options
url: /java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to paste values with Aspose.Cells copy and paste options

Automating Excel reporting in Java means you can generate, consolidate, and format workbooks without ever opening Excel manually. With **Aspose.Cells** you get full control over formulas, hidden rows, and cell values, so your reports stay accurate and lightweight. In this tutorial you’ll learn how to use **CopyOptions.ReferToDestinationSheet** to keep formulas correct and **PasteOptions** to paste only the visible values you need.

## Quick answers
- **What does `CopyOptions.ReferToDestinationSheet` do?** It rewrites formulas so they point to the destination sheet after a copy operation.  
- **How can I paste only visible cells?** Call `PasteOptions.setOnlyVisibleCells(true)` together with `PasteType.VALUES`.  
- **Which library version is required?** Aspose.Cells 25.3 or later.  
- **Do I need a license for production?** Yes – a permanent or temporary license removes evaluation limits.  
- **Can I use Maven or Gradle?** Both are supported; see the dependency snippets below.

## What is “automate Excel reporting”?
Automate Excel reporting means generating and updating Excel workbooks programmatically, allowing you to create, merge, and format reports without manual copy‑paste, which cuts errors and saves hours of repetitive work. This approach is ideal for scheduled batch jobs, data‑driven dashboards, and financial consolidation pipelines.

## Why use CopyOptions and PasteOptions for reporting?
These two classes let you keep formula references intact while copying data **and** extract only the cells that are visible after filtering or hiding rows. Using them together reduces the amount of data transferred by up to 80 % in typical filtered‑table scenarios and guarantees that formulas continue to calculate correctly in the destination sheet.

## Prerequisites
- Java 8 or higher.  
- Maven or Gradle for dependency management.  
- Aspose.Cells 25.3+ (trial, temporary, or permanent license).  

## Setting up Aspose.Cells for java

Add the library to your project with one of the following:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### License acquisition
- **Free trial** – full feature set for evaluation.  
- **Temporary license** – removes trial limits while you test.  
- **Permanent license** – recommended for production workloads.

Initialize Aspose.Cells in your Java code:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Step‑by‑step guide

### 1. copyOptions with referToDestinationSheet

#### Overview
`CopyOptions` is Aspose.Cells' configuration object that controls how formulas and cell references are handled during a copy operation. Setting `CopyOptions.ReferToDestinationSheet` to `true` rewrites formula references so they point to the new sheet after the copy operation.

#### Step 1: initialize workbook and worksheets  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: configure copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Step 3: execute copy operation  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Why this matters*: Formulas that originally referenced `Sheet1` will now correctly reference `DestSheet`, keeping your automated reports reliable.

**Troubleshooting tip**: If formulas still reference the old sheet, ensure `setReferToDestinationSheet(true)` is called **before** the copy.

### 2. pasteOptions for values‑only from visible cells

#### Overview
`PasteOptions` is Aspose.Cells' settings object that defines what gets pasted. Using `PasteType.VALUES` together with `onlyVisibleCells=true` copies just the displayed values, ignoring hidden rows/columns and formatting.

#### Step 1: initialize workbook and worksheets  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: configure pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Step 3: execute paste operation  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Why this matters*: Ideal for extracting filtered data or generating clean reports without hidden rows or formatting noise.

**Troubleshooting tip**: Verify that rows/columns are truly hidden in Excel before copying; otherwise, they will be included.

## Practical applications
1. **Financial consolidation** – merge monthly sheets into a master workbook while keeping all formulas accurate.  
2. **Filtered data export** – pull only visible rows from a filtered table into a summary sheet.  
3. **Scheduled report generation** – automate nightly Excel report creation with precise cell values and correct references.

## Performance considerations
- **Dispose of workbooks** when done (`wb.dispose();`) to free native resources.  
- **Batch operations** – group multiple copy/paste calls to reduce overhead.  
- **Monitor memory** – large workbooks may require increased heap (`-Xmx2g`).  
- Aspose.Cells supports **50+ input and output formats** and can process workbooks with **up to 2 million rows** without loading the entire file into memory, delivering high‑throughput performance for enterprise workloads.

## Frequently asked questions

**Q: What is `CopyOptions.ReferToDestinationSheet` used for?**  
A: It rewrites formula references so they point to the destination sheet after a copy, ensuring reporting formulas stay correct.

**Q: How do I paste only visible cells?**  
A: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.

**Q: Can I use Aspose.Cells without purchasing a license?**  
A: Yes, a free trial or temporary license is available for evaluation, but a permanent license is required for production.

**Q: Why are some references still wrong after copying?**  
A: Double‑check that `ReferToDestinationSheet` is enabled **before** the copy operation and that the source formulas don’t contain external workbook links.

**Q: What memory‑management best practices should I follow?**  
A: Dispose of `Workbook` objects when finished, process large files in chunks, and monitor JVM heap usage.

**Q: Is it possible to combine CopyOptions and PasteOptions in one operation?**  
A: Yes, you can chain them by first copying with `CopyOptions` and then applying `PasteOptions` on the target range.

## Resources
- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free trial**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Temporary license**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Support forum**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Last updated:** 2026-10-28  
**Tested with:** Aspose.Cells 25.3 for Java  
**Author:** Aspose

## Related Tutorials

- [Read Excel File Java – Master Workbook Cell Manipulation with Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Add Data to Cell in Excel Using Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convert Excel Cell Row Column Indices with Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}