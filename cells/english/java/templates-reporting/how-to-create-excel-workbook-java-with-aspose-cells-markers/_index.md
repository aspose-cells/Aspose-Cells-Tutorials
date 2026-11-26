---
category: general
date: 2026-11-25
description: Create Excel workbook Java code example using Aspose.Cells smart markers
  to bind JSON arrays as single values.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: en
lastmod: 2026-11-25
og_description: Create Excel workbook Java with Aspose.Cells to easily export JSON
  arrays as single cells. Follow the step‑by‑step guide.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Create Excel workbook Java – Aspose.Cells smart marker guide
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to create Excel workbook Java with Aspose.Cells markers
url: /java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create Excel workbook Java with Aspose.Cells markers

If you need to **create Excel workbook Java** code that writes a JSON array into a single cell, this tutorial shows you exactly how. Using Aspose.Cells smart markers you can treat an entire array as one value, avoiding manual loops and cell‑by‑cell writes.

You’ll learn how to set up a workbook, define a smart marker, bind a `Map` data source that contains a JSON‑style array, and finally save the file. The example works with Java 17+, Maven, and the free Aspose.Cells for Java trial library.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers"}

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 or later | The latest language features and security updates |
| Maven 3.6+ | Simplifies dependency management |
| Aspose.Cells for Java (v23.12 or newer) | Provides the `Workbook`, `Worksheet`, and smart‑marker APIs used in the sample |
| Basic knowledge of Java collections | You’ll create a `Map<String, Object>` that acts as the data source |

Add the Aspose.Cells dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Create Excel workbook Java – full example

The following program is a **complete, runnable** solution. Copy it into a file named `ExcelSmartMarkerDemo.java`, compile, and run.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### What the code does

1. **Creates a fresh workbook** – `new Workbook()` gives you an in‑memory Excel file with a default sheet.  
2. **Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells Aspose.Cells to replace the marker with the *entire* array, joined by commas.  
3. **Builds a `Map` data source** – The key `"jsonArray"` matches the marker name; the value is a `String[]`.  
4. **Calls `setSmartMarkerData`** – This binds the map to the marker and performs the replacement.  
5. **Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx` to disk.

When you open the generated Excel file, cell **A1** contains:

```
One, Two, Three
```

The array is rendered as a single, comma‑separated string because of the `ArrayAsSingle` option.

---

## Using Aspose.Cells smart marker to bind JSON data

Aspose.Cells smart markers are a powerful way to map complex objects (including JSON‑like structures) directly onto worksheets. The syntax `{{fieldName:Option}}` works much like a template engine:

* **fieldName** – the key in your data source (`Map`, POJO, or `DataTable`).  
* **Option** – controls how collections are handled. `ArrayAsSingle` treats the whole collection as one value; other options like `Array` would expand the array across rows.

**Why use a smart marker instead of a loop?**  
A loop requires manual cell address calculations, error‑prone indexing, and extra code for styling. Smart markers let you write declarative placeholders, keep your Java code short, and let the library handle layout details.

---

## Setting up the Java Map data source

The `Map<String, Object>` is the simplest data container for Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*The key (`jsonArray`) must match the marker name exactly.*  
You can also use a `List<String>`, a custom POJO, or even a nested `Map` for more complex JSON structures. Aspose.Cells will traverse the object graph automatically.

**Tip:** If you need to format the concatenated string differently (e.g., using semicolons), preprocess the array in Java before assigning it to the map:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Saving the workbook and verifying output

```java
workbook.save("JsonSingleValue.xlsx");
```

The `save` method supports many formats (`.xlsx`, `.xls`, `.csv`, `.pdf`). For this tutorial we keep the default Excel Open XML format.

**Verification steps**

1. Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google Sheets.  
2. Confirm that cell **A1** reads `One, Two, Three`.  
3. Check that no extra rows or columns were added – the smart marker performed an in‑place replacement.

If the cell shows the raw marker text (`{{jsonArray:ArrayAsSingle}}`), double‑check that:

* The marker name matches the map key exactly (case‑sensitive).  
* `setSmartMarkerData` is called **after** the marker is placed.  
* The Aspose.Cells version supports the `ArrayAsSingle` option (available since v20.3).

---

## Common variations and edge cases

| Scenario | Adjustment |
|----------|------------|
| **Different delimiter** | Use `ArrayAsSingle` together with a custom join in Java (see tip above). |
| **Multiple arrays in one sheet** | Place additional markers like `{{anotherArray:ArrayAsSingle}}` in other cells and add corresponding entries to the map. |
| **Nested JSON objects** | Supply a nested `Map<String, Object>`; reference fields with dot notation (`{{parent.child}}`). |
| **Large data sets** | For thousands of rows, prefer the `Array` option to let Aspose.Cells expand rows automatically, which


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}