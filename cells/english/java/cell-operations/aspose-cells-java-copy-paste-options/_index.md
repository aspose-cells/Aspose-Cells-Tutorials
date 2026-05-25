---
title: "Automate Excel Reporting – Mastering CopyOptions & PasteOptions in Java with Aspose.Cells"
description: "Learn how to automate Excel reporting with Aspose.Cells in Java by using CopyOptions and PasteOptions to keep formulas accurate and paste only visible values."
date: "2026-02-22"
weight: 1
url: "/java/cell-operations/aspose-cells-java-copy-paste-options/"
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automate Excel Reporting with Aspose.Cells: CopyOptions & PasteOptions in Java

Are you looking to **automate Excel reporting** using Java? With Aspose.Cells you can programmatically copy, paste, and adjust formulas so your reports stay accurate and only the data you need is transferred. In this tutorial we’ll walk through two essential features—**CopyOptions.ReferToDestinationSheet** and **PasteOptions**—that let you preserve formula references and paste values from visible cells only.

## Quick Answers
- **What does `CopyOptions.ReferToDestinationSheet` do?** Adjusts formulas to point to the destination sheet when copying data.  
- **How can I paste only visible cells?** Set `PasteOptions.setOnlyVisibleCells(true)` with `PasteType.VALUES`.  
- **Which library version is required?** Aspose.Cells 25.3 or later.  
- **Do I need a license for production?** Yes, a permanent or temporary license removes evaluation limits.  
- **Can I use Maven or Gradle?** Both are supported; see the dependency snippets below.

## What is “automate Excel reporting”?
Automating Excel reporting means generating, consolidating, and formatting Excel workbooks programmatically, eliminating manual copy‑paste steps and reducing errors. Aspose.Cells provides a rich API that lets Java developers manipulate spreadsheets at scale.

## Why use CopyOptions and PasteOptions for reporting?
- **Maintain formula integrity** when moving data between sheets.  
- **Exclude hidden rows/columns** to keep reports clean and focused.  
- **Boost performance** by copying only the necessary data instead of entire ranges.

## Prerequisites
- Java 8 or higher.  
- Maven or Gradle for dependency management.  
- Aspose.Cells 25.3+ (trial, temporary, or permanent license).  

## Setting Up Aspose.Cells for Java

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

### License Acquisition
- **Free Trial** – Full feature set for evaluation.  
- **Temporary License** – Removes trial limitations while you test.  
- **Permanent License** – Recommended for production workloads.

Initialize Aspose.Cells in your Java code:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Step‑By‑Step Guide

### 1. CopyOptions with ReferToDestinationSheet

#### Overview
Setting `CopyOptions.ReferToDestinationSheet` to `true` rewrites formula references so they point to the new sheet after the copy operation.

#### Step 1: Initialize Workbook and Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: Configure CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Step 3: Execute Copy Operation
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Why this matters*: Formulas that originally referenced `Sheet1` will now correctly reference `DestSheet`, keeping your automated reports reliable.

**Troubleshooting Tip**: If formulas still reference the old sheet, ensure `setReferToDestinationSheet(true)` is called **before** the copy.

### 2. PasteOptions for Values‑Only from Visible Cells

#### Overview
`PasteOptions` lets you define what gets pasted. Using `PasteType.VALUES` together with `onlyVisibleCells=true` copies just the displayed values, ignoring hidden rows/columns and formatting.

#### Step 1: Initialize Workbook and Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Step 2: Configure PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Step 3: Execute Paste Operation
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Why this matters*: Ideal for extracting filtered data or generating clean reports without hidden rows or formatting noise.

**Troubleshooting Tip**: Verify that rows/columns are truly hidden in Excel before copying; otherwise, they will be included.

## Practical Applications
1. **Financial Consolidation** – Merge monthly sheets into a master workbook while keeping all formulas accurate.  
2. **Filtered Data Export** – Pull only visible rows from a filtered table into a summary sheet.  
3. **Scheduled Report Generation** – Automate nightly Excel report creation with precise cell values and correct references.

## Performance Considerations
- **Dispose of Workbooks** when done (`wb.dispose();`) to free native resources.  
- **Batch Operations** – Group multiple copy/paste calls to reduce overhead.  
- **Monitor Memory** – Large workbooks may require increased heap (`-Xmx2g`).

## Frequently Asked Questions

**Q1: What is `CopyOptions.ReferToDestinationSheet` used for?**  
A: It rewrites formula references so they point to the destination sheet after a copy, ensuring reporting formulas stay correct.

**Q2: How do I paste only visible cells?**  
A: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.

**Q3: Can I use Aspose.Cells without purchasing a license?**  
A: Yes, a free trial or temporary license is available for evaluation, but a permanent license is required for production.

**Q4: Why are some references still wrong after copying?**  
A: Double‑check that `ReferToDestinationSheet` is enabled **before** the copy operation and that the source formulas don’t contain external workbook links.

**Q5: What memory‑management best practices should I follow?**  
A: Dispose of `Workbook` objects when finished, process large files in chunks, and monitor JVM heap usage.

**Q6: Is it possible to combine CopyOptions and PasteOptions in one operation?**  
A: Yes, you can chain them by first copying with `CopyOptions` and then applying `PasteOptions` on the target range.

## Resources
- **Documentation**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free Trial**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary License**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support Forum**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose