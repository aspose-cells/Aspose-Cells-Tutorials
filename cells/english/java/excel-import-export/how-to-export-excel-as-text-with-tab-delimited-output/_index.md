---
category: general
date: 2026-11-22
description: Learn how to export Excel as text and create a tab‑delimited file. This
  guide shows setting quote all fields and saving spreadsheet text efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: en
lastmod: 2026-11-22
og_description: Export Excel as text and create a tab‑delimited file. Follow this
  step‑by‑step tutorial to quote all fields and save spreadsheet text with Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Export Excel as text – tab‑delimited file guide
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: How to export Excel as text with tab‑delimited output
url: /java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to export Excel as text with tab‑delimited output

If you need to **export Excel as text**, this tutorial walks you through the complete process of creating a tab‑delimited file from a workbook. Whether you are building a data‑migration pipeline or need a quick CSV‑style dump for downstream processing, the steps below let you **save spreadsheet text** with full control over delimiters and quoting.

Exporting spreadsheet data as plain text is often more portable than keeping the native `.xlsx` format. In this guide you’ll also learn how to **quote all fields**, which guarantees that values containing tabs, commas, or line breaks are safely encapsulated.

## What you’ll need

Before you start, make sure you have:

* Java 17 or later installed.
* The Aspose.Cells for Java library (the code uses `ExportOptions` and `ExportTableOptions` from this library). You can add it via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* An IDE or a simple text editor to compile and run the Java program.

## Export Excel as text – step‑by‑step

The following sections break the task into three logical steps. Each step explains **why** it matters, not just **what** to type.

### Step 1: Prepare the workbook and sample data

Creating a workbook gives you something to export. In a real project you would load an existing file with `new Workbook("input.xlsx")`; here we generate a tiny sheet so the example runs out‑of‑the‑box.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Why this step?*  
A workbook is the source object for any export operation. By adding a few rows you can verify that the **quote all fields** option really protects commas and other special characters.

### Step 2: Configure export options – delimiter, quoting, and output mode

The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`. You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)` so every cell is wrapped in double quotes. This eliminates ambiguity when a cell itself contains a tab or newline.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Why this step?*  
- **Delimiter** determines how columns are separated. A tab (`\t`) creates a **tab‑delimited file** that many data‑processing tools accept.  
- **Quote all fields** guarantees that even if a cell contains a delimiter, the resulting text remains parseable.  
- Setting `ExportAsString` tells Aspose.Cells to generate a string rather than a binary workbook, which is exactly what you need for **save spreadsheet text**.

### Step 3: Save the workbook as a tab‑delimited text file

Now you actually **export excel as text**. The `save` method takes the target path and the `ExportOptions` you configured.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

When the program finishes, you’ll find `output/table.txt` containing:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Why this step?*  
The `save` call writes the **tab‑delimited file** to disk, effectively **saving spreadsheet text** in a format that can be opened by Excel, Notepad, or any data‑import tool that understands tabs.

## How to quote all fields when exporting Excel as text

If you omit `setQuoteAllFields(true)`, cells that contain tabs, commas, or line breaks will break the structure of the output file. For example, the row `Bob, Jr.` would be split into two columns, corrupting the dataset. Always enable quoting when:

* Your source data may contain commas, tabs, or newlines.
* Downstream parsers expect quoted CSV/TSV files.
* You need a deterministic export regardless of cell content.

## Creating a tab‑delimited file without Aspose.Cells (optional)

If you prefer a pure‑Java solution without third‑party libraries, you can iterate over rows and write them manually:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

This snippet demonstrates the same **export spreadsheet tab‑delimited** logic: a tab delimiter, quoting every field, and writing the result as plain text. However, using Aspose.Cells simplifies handling large workbooks, preserves formatting, and reduces boilerplate.

## Common pitfalls and pro tips

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Missing tabs in output** | Delimiter left at default comma. | Explicitly call `setDelimiter('\t')`. |
| **Unquoted commas break columns** | `quoteAllFields` not enabled. | Use `setQuoteAllFields(true)` or quote manually. |
| **File not created** | Output directory does not exist. | Ensure `output/` folder exists or use `Files.createDirectories`. |
| **Encoding problems** | Default platform encoding may corrupt non‑ASCII characters. | Pass `ExportOptions.setEncoding(Encoding.getUTF8())` if needed. |

## Testing the result

After running the program:

1. Open `output/table.txt` in a plain‑text editor. You should see each value wrapped in double quotes and columns separated by a single tab character.  
2. Import the file into Excel (`Data → From Text/CSV`). Choose **Tab** as the delimiter; Excel will correctly place each quoted value into its own cell.  
3. Verify that special characters (commas, line breaks


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [how to export excel – Tab‑Delimited Text Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [How to save Excel as text with Aspose.Cells – step‑by‑step guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}