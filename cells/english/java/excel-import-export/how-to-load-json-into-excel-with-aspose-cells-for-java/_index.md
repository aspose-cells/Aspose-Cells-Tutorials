---
category: general
date: 2026-10-07
description: Learn how to load JSON into Excel and generate XLSX from JSON using Aspose.Cells.
  This step‑by‑step guide also shows how to populate Excel from JSON and save workbook
  as XLSX.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: en
lastmod: 2026-10-07
og_description: Load JSON into Excel and generate XLSX from JSON using Aspose.Cells
  for Java. Follow this guide to populate Excel from JSON and save workbook as XLSX.
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: Load JSON into Excel with Aspose.Cells – complete Java guide
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: How to load JSON into Excel with Aspose.Cells for Java
url: /java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Load JSON into Excel with Aspose.Cells for Java

If you need to **load JSON into Excel**, this tutorial shows you a reliable way to do it with Aspose.Cells for Java. You’ll see how to generate XLSX from JSON, populate Excel from JSON, and finally **save workbook as XLSX**—all in a single, self‑contained program.

Working with JSON in spreadsheets is common when you export data from web services, APIs, or NoSQL stores. By the end of this guide you will have a ready‑to‑run Java class that creates a workbook from JSON and writes the result to a file on disk.

## Prerequisites

Before you start, make sure you have:

* Java 8 or newer installed (the code uses standard Java features).
* Aspose.Cells for Java library (version 23.10 or later). You can obtain it from the [Aspose website](https://downloads.aspose.com/cells/java) or via Maven Central.
* An IDE or a simple text editor and a terminal for compiling and running Java code.
* Basic familiarity with JSON syntax and Excel concepts.

> **Pro tip:** If you use Maven, add the following dependency to your `pom.xml` to avoid manual JAR management:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## Step 1: Set up the project and import required classes

Create a new Java class called `JsonToExcelDemo`. Import the Aspose.Cells classes that you will need for workbook creation, worksheet handling, and Smart Marker processing.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*Why this step matters:* Importing the correct classes ensures the compiler can locate Aspose.Cells APIs. The `Workbook` class represents the Excel file, while `SmartMarkerProcessor` drives the JSON‑to‑Excel conversion.

## Step 2: Define the JSON source that will be loaded into Excel

For this example we use a small JSON array containing two objects. In a real scenario you could read the JSON from a file, a REST endpoint, or a database.

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*Why this step matters:* The JSON string is the data source for the **populate Excel from JSON** operation. Keeping the JSON in a `String` variable makes it easy to pass to the `SmartMarkerProcessor`.

## Step 3: Create a new workbook and obtain the first worksheet

A fresh workbook gives you a clean slate. The first worksheet (index 0) is where we will insert the Smart Marker.

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*Why this step matters:* Aspose.Cells works with a `Workbook` object that can be saved later as an XLSX file. Accessing the first `Worksheet` lets us place the marker at a known cell address.

## Step 4: Insert a Smart Marker that tells Aspose.Cells how to treat the JSON

Smart Markers are placeholders that Aspose.Cells replaces with data from a source. The marker `&=JSONData.ArrayAsSingle` instructs the library to treat the whole JSON array as a single cell value.

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*Why this step matters:* Using `ArrayAsSingle` avoids the default behavior of expanding each array element into separate rows. This is useful when you want the JSON text to appear verbatim in a cell, or when you plan to split it later with formulas.

## Step 5: Configure the SmartMarkerProcessor with the JSON data source

Now bind the JSON string to the logical name `JSONData`. The processor will replace the marker with the actual data.

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*Why this step matters:* `setDataSource` links the name used in the marker (`JSONData`) with the actual JSON payload. `process()` performs the heavy lifting: parsing the JSON, applying the marker logic, and writing the result into the worksheet.

## Step 6: Save the resulting workbook as an XLSX file

Finally, write the workbook to disk. The `SaveFormat.XLSX` constant guarantees the correct Office Open XML format.

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*Why this step matters:* Saving the file completes the **generate XLSX from JSON** workflow. The produced file can be opened in Excel, LibreOffice, or any other spreadsheet program that supports XLSX.

### Full source code

Putting all the pieces together, here is the complete, runnable program that **creates workbook from JSON**, **populates Excel from JSON**, and **saves workbook as XLSX**.

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### Expected result

When you open `JsonSingleCell.xlsx` you will see the JSON array displayed in cell **A1** exactly as the original string:

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

If you prefer each object on a separate row, replace the marker with `&=JSONData` (without `.ArrayAsSingle`). The processor will then expand the array into individual rows, demonstrating a different **populate Excel from JSON** technique.

## Common variations and edge cases

| Situation | Adjustment |
|-----------|------------|
| **Large JSON payload ( > 10 MB )** | Increase the JVM heap size (`-Xmx2g`) and consider streaming the JSON to avoid `OutOfMemoryError`. |
| **Nested objects** | Use hierarchical markers like `&=JSONData.Name` and `&=JSONData.Age` inside a table to map each property to a column. |
| **JSON file instead of a string** | Read the file into a `String` with `java.nio.file.Files.readString(Path.of("data.json"))` and pass it to `setDataSource`. |
| **Need to keep the original JSON format** | Keep the `.ArrayAsSingle` suffix, or wrap the JSON in CDATA if you plan to use Excel formulas that parse JSON later. |
| **Multiple worksheets** | Create additional worksheets (`workbook.getWorksheets().add("Sheet2")`) and repeat the marker insertion on each sheet. |

> **Warning:** Smart Markers are case‑sensitive. Ensure the logical name (`JSONData`) matches exactly between the marker and `setDataSource`.

## Testing the solution

1. Compile the program:

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. Run it:

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. Verify that `JsonSingleCell.xlsx` appears in the working directory and opens without errors.


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create Excel Workbook from JSON – Complete Aspose.Cells Guide](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Create Excel Workbook C# – Insert JSON and Save as XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [Save Excel Workbook from JSON – Complete Guide](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}