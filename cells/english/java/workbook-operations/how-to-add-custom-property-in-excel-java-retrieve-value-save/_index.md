---
category: general
date: 2026-06-18
description: How to add custom property in Excel using Java. Learn to retrieve custom
  property value and save workbook as XLSB with a complete, runnable example.
draft: false
keywords:
- how to add custom property
- retrieve custom property value
- save workbook as xlsb
- create custom property in excel
language: en
og_description: How to add custom property in Excel using Java. This guide shows you
  how to retrieve the custom property value and save the workbook as XLSB.
og_title: How to Add Custom Property in Excel (Java) – Step‑by‑Step
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to add custom property in Excel using Java. Learn to retrieve custom
    property value and save workbook as XLSB with a complete, runnable example.
  headline: How to Add Custom Property in Excel (Java) – Retrieve Value & Save as
    XLSB
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: How to Add Custom Property in Excel (Java) – Retrieve Value & Save as XLSB
url: /java/workbook-operations/how-to-add-custom-property-in-excel-java-retrieve-value-save/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Add Custom Property in Excel (Java) – Retrieve Value & Save as XLSB

How to add custom property in Excel using Java is a common need when you want to tag worksheets with metadata. In this tutorial we’ll also retrieve custom property value and **save workbook as XLSB**, so you get a complete, end‑to‑end solution that you can drop into any project.

Imagine you’re building a reporting engine that generates dozens of spreadsheets each night. You’d love to embed a “ProjectId” or “ReportVersion” directly into the file so downstream systems can filter or audit them later. That’s exactly what custom properties give you—tiny pieces of data stored inside the workbook without cluttering the visible cells.

We’ll cover:

* Creating a custom property in Excel (the “ProjectId” example).  
* Retrieving that custom property value to verify it works.  
* Saving the modified workbook as an **XLSB** file, which is the binary format that keeps file size down and load times fast.  

**Prerequisites**

* Java 17 or newer.  
* Aspose.Cells for Java (the library that lets you manipulate Excel files without Microsoft Office).  
* A valid Aspose.Cells license – the free evaluation works for this demo, but a license removes the evaluation watermark.  

If you’ve never used Aspose.Cells before, don’t worry. The API is straightforward, and the code below is ready‑to‑run after you add the JAR to your classpath.

![how to add custom property in Excel using Java](image-url-placeholder "How to add custom property in Excel using Java")

---

## How to Add Custom Property – Step 1

First, we need to load an existing workbook (or create a new one) and then attach a custom property to the first worksheet. The property is just a key/value pair stored in the worksheet’s `CustomProperties` collection.

```java
import com.aspose.cells.*;

public class CustomPropertyDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook from a file (you can also create a new workbook)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

        // Step 2: Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        // This is the core of how to add custom property in Excel.
        sheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the value of the custom property we just added
        // (We'll also show you how to retrieve custom property value later.)
        Object projectIdValue = sheet.getCustomProperties().get("ProjectId").getValue();

        // Step 5: Display the retrieved value on the console
        System.out.println("ProjectId = " + projectIdValue);

        // Step 6: Save the modified workbook to a new file in XLSB format
        // This demonstrates how to save workbook as XLSB.
        workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
    }
}
```

**Why this works**

* `Workbook` is the entry point for any Excel file—think of it as the container for all sheets, styles, and metadata.  
* `Worksheet.getCustomProperties()` returns a collection that behaves like a dictionary; calling `.add(name, value)` creates the property if it doesn’t exist.  
* The property value can be any primitive type (int, double, String, boolean) – Aspose.Cells handles the conversion for you.  

Running the program prints:

```
ProjectId = 12345
```

Now you’ve successfully **added a custom property** and confirmed it exists.

---

## Retrieve Custom Property Value

You might wonder, “What if I need to read the property later, perhaps in a different module?” The same `CustomProperties` collection lets you fetch by name. Below is a focused snippet that demonstrates **retrieve custom property value** without re‑adding it.

```java
// Assume workbook is already loaded and sheet points to the correct worksheet
CustomPropertyCollection props = sheet.getCustomProperties();

// Check if the property exists to avoid NullPointerException
if (props.contains("ProjectId")) {
    Object value = props.get("ProjectId").getValue();
    System.out.println("Retrieved ProjectId = " + value);
} else {
    System.out.println("ProjectId property not found.");
}
```

**Key points**

* `contains` is a safe guard—real‑world code should always verify existence before reading.  
* The returned `Object` can be cast to the expected type if you need arithmetic operations (e.g., `(int) value`).  

This small pattern solves most auditing scenarios where you need to pull metadata from a workbook that was generated weeks ago.

---

## Save Workbook as XLSB

Why choose XLSB over the more common XLSX? Binary XLSB files are typically **30‑40 % smaller** and open faster, especially for large data sets. Aspose.Cells makes saving to this format a one‑liner, as seen in **Step 6** of the first code block.

If you need to keep the workbook in memory (perhaps to send it over a web service), you can write to a `ByteArrayOutputStream` instead:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
workbook.save(baos, SaveFormat.XLSB);
byte[] xlsbBytes = baos.toByteArray();
// Now you can attach xlsbBytes to an email, upload to S3, etc.
```

The `SaveFormat.XLSB` enum guarantees the binary format, and the same call works for any workbook, whether you just added a custom property or performed extensive calculations.

---

## Create Custom Property in Excel – Full End‑to‑End Example

Below is a polished, self‑contained program that ties together **how to add custom property**, **retrieve custom property value**, and **save workbook as XLSB**. Feel free to copy‑paste this into your IDE, adjust the file paths, and run it immediately.

```java
import com.aspose.cells.*;

public class ExcelCustomPropertyExample {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load an existing XLSB workbook (or create a new one)
            Workbook workbook = new Workbook("YOUR_DIRECTORY/custom.xlsb");

            // 2️⃣ Grab the first worksheet – you could loop through all sheets if needed
            Worksheet sheet = workbook.getWorksheets().get(0);

            // 3️⃣ Create a custom property called "ProjectId"
            // This is the essential step for how to add custom property.
            sheet.getCustomProperties().add("ProjectId", 12345);
            System.out.println("Custom property 'ProjectId' added.");

            // 4️⃣ Retrieve the property to prove it works – demonstrates retrieve custom property value
            CustomPropertyCollection props = sheet.getCustomProperties();
            if (props.contains("ProjectId")) {
                Object val = props.get("ProjectId").getValue();
                System.out.println("Retrieved ProjectId = " + val);
            }

            // 5️⃣ Optionally, add another property (string type) to show flexibility
            sheet.getCustomProperties().add("ReportVersion", "v2.1");
            System.out.println("Added ReportVersion property.");

            // 6️⃣ Save the workbook as an XLSB file – this is the save workbook as XLSB step.
            workbook.save("YOUR_DIRECTORY/customOut.xlsb", SaveFormat.XLSB);
            System.out.println("Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb");

        } catch (Exception e) {
            // Real‑world code should log the exception; here we just print stack trace.
            e.printStackTrace();
        }
    }
}
```

**Expected console output**

```
Custom property 'ProjectId' added.
Retrieved ProjectId = 12345
Added ReportVersion property.
Workbook saved as XLSB at YOUR_DIRECTORY/customOut.xlsb
```

Open `customOut.xlsb` in Excel, go to **File → Info → Properties → Advanced Properties → Custom**, and you’ll see both `ProjectId` and `ReportVersion` listed—proof that **create custom property in Excel** really happened.

---

## Common Pitfalls & Pro Tips

| Pitfall | Why it Happens | Fix |
|---------|----------------|-----|
| Forgetting to call `workbook.save(...)` |


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Excel Workbook Custom Property Management Using Aspose.Cells .NET](/cells/english/net/workbook-operations/excel-workbook-property-management-aspose-cells-net/)
- [How to Export Custom Excel Properties to PDF Using Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}