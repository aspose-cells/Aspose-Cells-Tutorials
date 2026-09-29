---
category: general
date: 2026-03-01
description: Copy pivot table in Java while preserving the pivot, then export Excel
  to PPTX, disable Excel AutoFilter, and use Smart Marker for JSON arrays – full step‑by‑step
  guide.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: en
og_description: Copy pivot table in Java, preserve the pivot definition, export to
  PPTX, disable AutoFilter, and use Smart Marker – complete guide for developers.
og_title: Copy Pivot Table in Java – Preserve It, Export to PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copy Pivot Table in Java – Preserve It, Export to PPTX
url: /java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copy Pivot Table in Java – Preserve It, Export to PPTX

Ever needed to **copy pivot table** from one workbook to another without losing the underlying pivot definition? You're not the only one scratching your head over this. In many real‑world projects you’ll find yourself moving data around, and the last thing you want is a broken pivot that throws errors at runtime.  

In this tutorial we’ll walk through a complete solution that not only **copy pivot table** but also shows you how to **preserve pivot table** when copying, **export Excel to PPTX**, **disable Excel AutoFilter**, and **use smart marker** to shove a JSON array into a single cell. By the end you’ll have a single, runnable Java program that covers all four scenarios.

## Prerequisites

- Java 8 or newer (the code works with Java 11 as well)  
- Aspose.Cells for Java library (version 23.9 or later) – you can grab it from Maven Central  
- Basic familiarity with Excel concepts like pivot tables, tables, and text boxes  

If you’re missing the Aspose.Cells JAR, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Now, let’s dive in.

## Step 1: Copy Pivot Table – Preserving the Pivot Definition

When you simply copy the cell range that houses a pivot table, the pivot metadata often gets left behind. Aspose.Cells gives us a neat way to keep the definition intact by using `copyRange` with a `CopyOptions` instance.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Why this works:** `CopyOptions` tells Aspose.Cells to carry over everything, including the pivot cache and field settings. Without it, you’d end up with plain values and lose the ability to refresh the pivot.

**Edge case:** If your source pivot spans more than the hard‑coded `A1:G20`, adjust the range accordingly or use `sourceSheet.getPivotTables().get(0).getDataRange()` to fetch it dynamically.

![Copy pivot table example](image.png "Copy pivot table in Java")

*Image alt text: copy pivot table in Java diagram*

## Step 2: Export a Worksheet with an Editable TextBox to PPTX

Often you need to turn an Excel sheet into a PowerPoint slide—think of weekly dashboards that need to be presented. Aspose.Cells can directly save a worksheet as a PPTX file while preserving shapes like text boxes.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**What’s happening:** The `save` method with `SaveFormat.PPTX` converts the entire sheet, including any editable TextBox, into a PowerPoint slide. The text inside the box remains editable when you open the PPTX in PowerPoint.

**Tip:** If you have multiple sheets and only want a specific one, call `wb.getWorksheets().removeAt(index)` for the others before saving.

## Step 3: Disable Excel AutoFilter from a Table

AutoFilter is handy for end‑users, but sometimes you need to programmatically turn it off—perhaps before exporting data or when generating a clean report. Here’s how to **disable excel autofilter** on an Excel table.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Why you might need this:** Exporting to formats that don’t support AutoFilter (like CSV or PDF) can cause stray filter icons to appear. Disabling it ensures a clean output.

**Common pitfall:** If the sheet has no tables, `getTables().get(0)` will throw an `IndexOutOfBoundsException`. Always check `sheet.getTables().size()` first in production code.

## Step 4: Use Smart Marker – Insert a JSON Array as a Single Cell Value

Smart Marker is Aspose’s templating engine. One handy trick is to treat an entire JSON array as a single cell value, which is perfect for logging or passing structured data downstream. Let’s **use smart marker** to achieve this.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**How it works:** The `${json}` marker in the workbook gets replaced by the whole JSON string because we set `ArrayAsSingle`. Without this option, Aspose would try to expand each array element into separate rows.

**Variation:** If you need the array split across rows, simply omit `ArrayAsSingle` and let Smart Marker handle the expansion automatically.

## Full Working Example – All Steps Combined

Below is a single Java class that strings together every operation we’ve covered. Run it as a regular `main` method; just adjust the file paths to match your environment.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}