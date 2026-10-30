---
category: general
date: 2026-08-17
description: Java create excel file with Aspose.Cells, add a custom property and save
  workbook as XLSB in just a few lines of code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- java create excel file
- add custom property
- how to create xlsb
- how to add custom property
- save workbook as xlsb
language: en
lastmod: 2026-08-17
og_description: Java create excel file with Aspose.Cells, add a custom property and
  save workbook as XLSB in just a few lines of code.
og_image_alt: Screenshot of a Java program that creates an Excel file, adds a custom
  property, and saves it as XLSB
og_title: Java create excel file, add custom property and save as XLSB
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Java create excel file with Aspose.Cells, add a custom property and
    save workbook as XLSB in just a few lines of code.
  headline: Java create excel file, add custom property and save as XLSB
  type: TechArticle
- description: Java create excel file with Aspose.Cells, add a custom property and
    save workbook as XLSB in just a few lines of code.
  name: Java create excel file, add custom property and save as XLSB
  steps:
  - name: Create a new workbook and access its first worksheet
    text: The first operation in any Excel automation task is to create a `Workbook`
      object. This object represents the entire Excel file in memory.
  - name: How to add custom property
    text: Custom properties let you store key‑value pairs that are not part of the
      cell data. They are useful for tagging a file with a project ID, version number,
      or any business‑specific metadata.
  - name: How to create XLSB and save workbook as XLSB
    text: Once the custom property is in place, you can persist the workbook in the
      binary XLSB format. XLSB files are smaller and open faster than the XML‑based
      XLSX.
  - name: Full working example
    text: 'Putting the three steps together gives you a complete, runnable program:'
  type: HowTo
tags:
- java
- excel
- custom property
- xlsb
title: Java create excel file, add custom property and save as XLSB
url: /java/workbook-operations/java-create-excel-file-add-custom-property-and-save-as-xlsb/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java create excel file, add custom property and save as XLSB

If you need to **java create excel file** that carries additional metadata, this guide shows you exactly how. Using Aspose.Cells for Java you can add a custom property to a worksheet and then **save workbook as xlsb** with just three straightforward steps.

In this tutorial you will learn how to:

* Initialize a new workbook with Aspose.Cells.
* **Add custom property** to a worksheet (for example, a project identifier).
* **How to create xlsb** files that preserve those properties.
* **Save workbook as xlsb** for fast loading in Excel.

No external tools are required—only the Aspose.Cells library and a Java‑compatible IDE.

## Prerequisites

* Java Development Kit 8 or newer.
* Maven or Gradle to manage the Aspose.Cells dependency.
* Basic familiarity with Java syntax.
* An IDE such as IntelliJ IDEA, Eclipse, or VS Code.

Add the Aspose.Cells dependency to your `pom.xml` (Maven) or `build.gradle` (Gradle). For Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

## Java create excel file – step‑by‑step guide

### Step 1: Create a new workbook and access its first worksheet

The first operation in any Excel automation task is to create a `Workbook` object. This object represents the entire Excel file in memory.

```java
import com.aspose.cells.*;

public class CustomPropsXlsb {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook (an in‑memory XLSX container)
        Workbook workbook = new Workbook();

        // Grab the first worksheet – it is created by default
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Why this matters*: `Workbook` is the entry point for all subsequent actions. Even if you plan to save the file as **XLSB**, you still start with a regular workbook because Aspose.Cells abstracts the file format until you call `save`.

### Step 2: How to add custom property

Custom properties let you store key‑value pairs that are not part of the cell data. They are useful for tagging a file with a project ID, version number, or any business‑specific metadata.

```java
        // Add a custom property named "ProjectId" with value "12345"
        worksheet.getCustomProperties().add("ProjectId", "12345");
```

*Why you should use this*: When other applications or downstream processes read the workbook, they can retrieve `ProjectId` without scanning cell contents. This keeps the data model clean and separates metadata from user data.

### Step 3: How to create XLSB and save workbook as XLSB

Once the custom property is in place, you can persist the workbook in the binary XLSB format. XLSB files are smaller and open faster than the XML‑based XLSX.

```java
        // Save the workbook as an XLSB file; the custom property is preserved
        workbook.save("output/custom_props.xlsb", SaveFormat.XLSB);
    }
}
```

*Explanation*: The `SaveFormat.XLSB` constant tells Aspose.Cells to serialize the workbook into the binary format. All custom properties, styles, and formulas are retained automatically.

### Full working example

Putting the three steps together gives you a complete, runnable program:

```java
import com.aspose.cells.*;

public class CustomPropsXlsb {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Add a custom property called "ProjectId"
        worksheet.getCustomProperties().add("ProjectId", "12345");

        // Step 3: Save the workbook as an XLSB file
        workbook.save("output/custom_props.xlsb", SaveFormat.XLSB);
    }
}
```

**Expected output**: After running the program, the folder `output` contains `custom_props.xlsb`. Opening the file in Microsoft Excel and navigating to **File → Info → Properties → Advanced Properties → Custom** will show the `ProjectId` entry with the value `12345`.

## How to add custom property to an existing workbook

If you already have an XLSX or XLSB file and need to inject a property, the code changes only slightly:

```java
Workbook workbook = new Workbook("input/existing_file.xlsx");
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getCustomProperties().add("ReviewedBy", "Alice");
workbook.save("output/updated_file.xlsb", SaveFormat.XLSB);
```

*Tip*: Always call `save` with the desired format (`XLSB` in this case) even when the source file is XLSX. This converts the file while preserving the newly added property.

## How to create XLSB without Aspose.Cells (alternative)

Although Aspose.Cells is the most straightforward library, you can also generate XLSB using Apache POI’s `XSSF` streaming API combined with a third‑party converter. However, that approach requires extra steps to maintain custom properties, so **java create excel file** with Aspose.Cells remains the recommended solution for production code.

## Save workbook as XLSB – performance considerations

* **File size**: XLSB typically reduces size by 30‑50 % compared with XLSX, especially for large data sets.
* **Load time**: Binary format loads faster in Excel because the XML parsing step is skipped.
* **Compatibility**: All modern versions of Excel (2007+) support XLSB. Older spreadsheet programs may not.

If you need the smallest possible file, consider compressing the XLSB with a zip utility after saving.

## Common pitfalls and how to avoid them

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Custom property disappears after saving | Property added to the wrong object (e.g., workbook instead of worksheet) | Use `worksheet.getCustomProperties()` as shown in the example |
| `SaveFormat.XLSB` not recognized | Using an older Aspose.Cells version | Upgrade to the latest version (≥ 24.9) |
| Output folder does not exist | `save` does not create missing directories | Create the folder programmatically (`new File("output").mkdirs();`) before saving |

## Pro tip: Reuse the property for data validation

You can read the custom property later to enforce business rules:

```java
String projectId = worksheet.getCustomProperties().get("ProjectId").getValue().toString();
if (!projectId.equals(expectedId)) {
    throw new IllegalStateException("Project ID mismatch");
}
```

This pattern keeps validation logic decoupled from the worksheet’s actual data.

## Conclusion

You now know how to **java create excel file**, **add custom property**, **how to create xlsb**, and **save workbook as xlsb** using Aspose.Cells. The complete example demonstrates the entire workflow—from initializing a workbook to persisting a binary XLSB file that carries your metadata.

Next steps you might explore:

* Add multiple custom properties (e.g., version, author).
* Apply cell formatting and formulas before saving.
* Generate XLSB files in a multi‑threaded batch process for large data imports.

Feel free to experiment with different property names and values to see how Excel surfaces them in the **Custom** tab. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create Excel File Java and Style It with Aspose.Cells](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}