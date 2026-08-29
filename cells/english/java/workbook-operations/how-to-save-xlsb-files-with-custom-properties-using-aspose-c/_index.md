---
category: general
date: 2026-08-20
description: Learn how to save xlsb files and add custom property in Java. This guide
  covers how to create workbook, write custom property, and preserve it.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to save xlsb
- add custom property
- how to add property
- how to create workbook
- write custom property
language: en
lastmod: 2026-08-20
og_description: How to save xlsb files using Aspose.Cells for Java. Follow this step‑by‑step
  tutorial to add custom property, create workbook, and write custom property.
og_image_alt: Screenshot showing Java code that demonstrates how to save xlsb with
  a custom property
og_title: How to save xlsb files with custom properties – Java guide
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to save xlsb files and add custom property in Java. This
    guide covers how to create workbook, write custom property, and preserve it.
  headline: How to save xlsb files with custom properties using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to save xlsb files and add custom property in Java. This
    guide covers how to create workbook, write custom property, and preserve it.
  name: How to save xlsb files with custom properties using Aspose.Cells for Java
  steps:
  - name: Why use custom properties?
    text: '* They travel with the file, making it easy for downstream processes to
      read metadata without opening the sheet. * They are stored in the workbook’s
      XML parts, which means they survive the binary XLSB compression.'
  - name: 5.1 Adding properties to an existing XLSB file
    text: 'If you need to modify a workbook that already exists on disk:'
  - name: 5.2 Overwriting an existing property
    text: 'Attempting to add a property with a duplicate name throws an exception.
      To update instead, locate the property first:'
  - name: 5.3 Saving to a `ByteArrayOutputStream`
    text: 'Sometimes you want to send the XLSB file over HTTP without touching the
      file system:'
  - name: 5.4 Handling large workbooks
    text: 'XLSB is designed for high‑performance scenarios. When dealing with >10
      000 rows, consider enabling the **memory‑optimized** save option:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- XLSB
- CustomProperties
title: How to save xlsb files with custom properties using Aspose.Cells for Java
url: /java/workbook-operations/how-to-save-xlsb-files-with-custom-properties-using-aspose-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to save xlsb files with custom properties using Aspose.Cells for Java

If you need to know **how to save xlsb** while preserving additional metadata, this tutorial gives you a complete, ready‑to‑run solution. You’ll learn to create a workbook, add a custom property, and write that property so it survives the XLSB conversion.  

Saving an XLSB file isn’t just about the binary format; you often want to embed information such as project identifiers, version numbers, or audit flags. This guide shows exactly **how to add property** data to a worksheet and then **how to save xlsb** without losing it.

## Prerequisites

Before you start, make sure you have:

* Java Development Kit (JDK) 8 or newer  
* Maven or Gradle for dependency management  
* An active Aspose.Cells for Java license (the free evaluation works for testing)  

You do not need any additional libraries; Aspose.Cells handles XLSB creation and custom properties internally.

## What the tutorial covers

* **how to create workbook** programmatically with Aspose.Cells  
* **write custom property** to a worksheet  
* **how to save xlsb** while keeping the custom data intact  
* Common pitfalls such as overwriting existing properties or saving to a stream  

By the end of the article you will have a self‑contained Java class that you can drop into any project.

![how to save xlsb example](/images/how-to-save-xlsb.png "how to save xlsb example showing Java code and output file")

## Step 1: Set up the Aspose.Cells dependency

Add the latest Aspose.Cells for Java artifact to your project. With Maven, include:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version> <!-- use the current version -->
</dependency>
```

If you prefer Gradle:

```gradle
implementation 'com.aspose:aspose-cells:23.10'
```

> **Pro tip:** Keep the version number in sync with the official release notes to benefit from performance improvements and bug fixes related to XLSB handling.

## Step 2: How to create workbook

Creating a workbook is the first logical step when you want to **how to save xlsb** later. The `Workbook` class represents the entire Excel file in memory.

```java
import com.aspose.cells.*;

public class XlsbCustomPropertyDemo {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Instantiate a new, empty workbook
        Workbook workbook = new Workbook();

        // Step 2.2: Access the default worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

The `Workbook()` constructor creates an in‑memory workbook with a single default worksheet. This is the cleanest way to **how to create workbook** without loading an existing file.

## Step 3: Write custom property to the worksheet

Aspose.Cells exposes a `CustomPropertyCollection` through `Worksheet.getCustomProperties()`. You can **add custom property** entries of type `String`, `Integer`, `DateTime`, etc. Here we demonstrate adding a simple project identifier.

```java
        // Step 3.1: Add a custom property named "ProjectId"
        sheet.getCustomProperties().add("ProjectId", "12345");

        // Optional: Add more properties if needed
        sheet.getCustomProperties().add("ReviewedBy", "Jane Doe");
        sheet.getCustomProperties().add("Revision", 3);
```

The method `add(String name, Object value)` handles the conversion internally, so you don’t need to convert the value to a string first. This satisfies the **write custom property** requirement and shows **how to add property** in a type‑safe manner.

### Why use custom properties?

* They travel with the file, making it easy for downstream processes to read metadata without opening the sheet.  
* They are stored in the workbook’s XML parts, which means they survive the binary XLSB compression.  

## Step 4: How to save xlsb while preserving the custom data

Now that the workbook contains the desired metadata, you can finally **how to save xlsb**. Use the `Workbook.save` overload that accepts a file path and a `SaveFormat` enum.

```java
        // Step 4.1: Define the output path (adjust to your environment)
        String outputPath = "output/WorkbookWithCustomProp.xlsb";

        // Step 4.2: Save the workbook in XLSB format
        workbook.save(outputPath, SaveFormat.XLSB);

        System.out.println("Workbook saved successfully to " + outputPath);
    }
}
```

When the file is opened in Excel, you can verify the custom property by navigating to **File → Info → Properties → Advanced Properties → Custom**. The values you added in Step 3 will be listed there, confirming that the **how to save xlsb** operation retained the metadata.

## Step 5: Advanced scenarios and edge cases

### 5.1 Adding properties to an existing XLSB file

If you need to modify a workbook that already exists on disk:

```java
Workbook existing = new Workbook("input/ExistingFile.xlsb");
Worksheet ws = existing.getWorksheets().get(0);
ws.getCustomProperties().add("NewFlag", true);
existing.save("output/ModifiedFile.xlsb", SaveFormat.XLSB);
```

### 5.2 Overwriting an existing property

Attempting to add a property with a duplicate name throws an exception. To update instead, locate the property first:

```java
CustomPropertyCollection props = ws.getCustomProperties();
if (props.contains("ProjectId")) {
    props.get("ProjectId").setValue("67890"); // Update existing value
} else {
    props.add("ProjectId", "67890"); // Add if missing
}
```

### 5.3 Saving to a `ByteArrayOutputStream`

Sometimes you want to send the XLSB file over HTTP without touching the file system:

```java
ByteArrayOutputStream stream = new ByteArrayOutputStream();
workbook.save(stream, SaveFormat.XLSB);
byte[] xlsbBytes = stream.toByteArray();
// Use xlsbBytes in a servlet response, REST API, etc.
```

### 5.4 Handling large workbooks

XLSB is designed for high‑performance scenarios. When dealing with >10 000 rows, consider enabling the **memory‑optimized** save option:

```java
Workbook wb = new Workbook();
wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
wb.save(outputPath, SaveFormat.XLSB);
```

## Common pitfalls and how to avoid them

| Symptom | Cause | Fix |
|---------|-------|-----|
| Custom property disappears after opening the file | Saved as XLSX instead of XLSB | Ensure `SaveFormat.XLSB` is used |
| Duplicate property exception | Property already exists | Use `contains()` check before `add()` |
| File not found when loading | Relative path resolves to wrong directory | Use absolute paths or `Paths.get(...)` |
| NullPointerException on `getCustomProperties()` | Worksheet reference is null | Verify `workbook.getWorksheets().get(index)` returns a valid object |

## Full, runnable example

Below is the complete program that you can copy, compile, and run directly.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Access the first worksheet in the workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Add custom properties to the worksheet
        worksheet.getCustomProperties().add("ProjectId", "12345");
        worksheet.getCustomProperties().add("ReviewedBy", "Jane Doe");
        worksheet.getCustomProperties().add("Revision", 1);

        // Step 4: Save the workbook as an XLSB file – the custom properties are preserved
        String outPath = "output/WorkbookWithCustomProp.xlsb";
        workbook.save(outPath, SaveFormat.XLSB);

        System.out.println("Workbook saved successfully to " + outPath);
    }
}
```

**Expected output**

```
Workbook saved successfully to output/WorkbookWithCustomProp.xlsb
```

Open the generated `WorkbookWithCustomProp.xlsb` in Microsoft Excel, go to **File → Info → Properties → Advanced Properties → Custom**, and you’ll see the three properties you added.

## Conclusion

You now know **how to save xlsb** files while **add custom property** data using Aspose.Cells for Java. The tutorial covered **how to create workbook**, demonstrated **write custom property**, explained **how to add property** safely, and showed several advanced scenarios such as updating existing files and streaming the result.

Next, you might explore:

* **how to add property** to charts or named ranges


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [How to Save Excel Workbook in Java Using Aspose.Cells](/cells/english/java/automation-batch-processing/excel-automation-java-aspose-cells-guide/)
- [How to Save XLSB with a Custom Property – Step‑by‑Step C# Guide](/cells/english/net/document-properties/how-to-save-xlsb-with-a-custom-property-step-by-step-c-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}