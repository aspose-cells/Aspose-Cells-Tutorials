---
category: general
date: 2026-07-03
description: Create Excel from JSON with Java and Aspose.Cells – step‑by‑step guide
  to export JSON to Excel, convert JSON to XLSX, and import JSON into Excel quickly.
draft: false
keywords:
- create excel from json
- export json to excel
- convert json to xlsx
- import json into excel
- generate excel from json
language: en
og_description: Create Excel from JSON using Aspose.Cells in Java. Learn how to export
  JSON to Excel, convert JSON to XLSX, and import JSON into Excel efficiently.
og_title: Create Excel from JSON – Java Guide with Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create Excel from JSON with Java and Aspose.Cells – step‑by‑step guide
    to export JSON to Excel, convert JSON to XLSX, and import JSON into Excel quickly.
  headline: Create Excel from JSON – Full Java Guide with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Aspose.Cells can flatten nested structures using dot notation (e.g., `Address.Street`).
      Just ensure your JSON is well‑formed and set `exportOptions.setFlattenObject(true)`.
    question: What if my JSON has nested objects?
  - answer: Absolutely. Place SmartMarker tags like `&=Name` in your template cells,
      load the template workbook, and call `processor.process()` the same way.
    question: Can I merge JSON into an existing template?
  - answer: The `Workbook` class implements `AutoCloseable` in newer versions, so
      you can wrap it in a try‑with‑resources block if you prefer.
    question: Do I need to close resources?
  - answer: For massive datasets, consider streaming the JSON or using the `setBatchSize`
      option to limit memory consumption.
    question: Performance concerns for huge arrays?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel
- JSON
title: Create Excel from JSON – Full Java Guide with Aspose.Cells
url: /java/excel-import-export/create-excel-from-json-full-java-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel from JSON – Full Java Guide with Aspose.Cells

Ever needed to **create Excel from JSON** but weren’t sure which library would keep the code tidy? You’re not alone. In many data‑driven apps the fastest way to share information with business users is to dump JSON straight into an XLSX file, and Aspose.Cells makes that a breeze.

In this tutorial we’ll walk through a complete, runnable example that **exports JSON to Excel**, shows you how to **convert JSON to XLSX**, and even demonstrates the subtle **import JSON into Excel** step that many developers overlook. By the end you’ll have a single Java method that transforms a JSON array into a polished workbook ready for distribution.

## What You’ll Need

- Java 17 or newer (the code compiles with earlier versions, but 17 is the current LTS)
- Aspose.Cells for Java 23.9 (or the latest release at the time of reading)
- A modest IDE or just `javac`/`java` from the command line
- No external JSON parsers – Aspose.Cells handles the raw string for us

That’s it. No Maven magic, no extra jars, just the Aspose.Cells JAR on the classpath.

## Step 1: Define the JSON Data to Be Merged  

The first thing we do is craft a JSON string that represents the table we want in Excel. In a real project you’d probably read this from a file or a REST endpoint, but hard‑coding keeps the example self‑contained.

```java
// Step 1: Define the JSON data to be merged
String jsonData = "[{\"Name\":\"Bob\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

**Why this matters:**  
The JSON array is interpreted by Aspose.Cells as a data source. Each object becomes a row, and each property becomes a column. Notice the simple key‑value pairs – the library can handle nested objects too, but that’s a topic for another day.

## Step 2: Create a New Workbook and Grab Its First Worksheet  

Now we spin up an empty workbook. Think of the workbook as the canvas, and the worksheet as the page where we’ll paint our data.

```java
// Step 2: Create a new workbook and obtain its first worksheet
Workbook workbook = new Workbook();                     // blank workbook
Worksheet worksheet = workbook.getWorksheets().get(0);  // first sheet (index 0)
```

**Why this matters:**  
Creating the workbook up front gives us full control over formatting later on. If you need multiple sheets, just repeat the `getWorksheets().add()` call.

## Step 3: Initialise the SmartMarker Processor  

Aspose.Cells ships with a powerful **SmartMarker** engine that can merge JSON, XML, or any data source directly into cells. Initialising it is straightforward.

```java
// Step 3: Initialise the SmartMarker processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

**Why this matters:**  
SmartMarker parses the markers we’ll place in the worksheet (or, in our case, defaults) and performs the merge. It’s the heart of the **generate excel from json** capability.

## Step 4: Configure Export Options – Treat the JSON Array as a Single Table  

Here’s the key setting that makes our JSON behave like a normal Excel table. By telling Aspose to treat the array as a single table, we avoid having each object become a separate sheet.

```java
// Step 4: Configure export options to treat the JSON array as a single table
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setArrayAsSingle(true);   // <-- crucial for a single table
```

**Why this matters:**  
If `setArrayAsSingle(false)` (the default), each JSON object would spawn its own table, scattering data across the workbook. Setting it to **true** consolidates everything, which is exactly what you want when you **convert json to xlsx**.

## Step 5: Process the Worksheet with the JSON Data  

Now the magic happens. We feed the worksheet, the raw JSON string, and our options into the processor. Aspose will create headers, fill rows, and apply basic formatting automatically.

```java
// Step 5: Process the worksheet with the JSON data using the configured options
processor.process(worksheet, jsonData, exportOptions);
```

**Why this matters:**  
This single line replaces dozens of lines of manual looping, cell creation, and type conversion. It’s the core of **import json into excel** in a clean, maintainable way.

## Step 6: Save the Resulting Workbook  

Finally we write the workbook to disk. The file extension `.xlsx` tells Excel (and any modern spreadsheet app) that this is an OpenXML workbook.

```java
// Step 6: Save the resulting workbook
workbook.save("output/jsonSingle.xlsx");
```

**Expected output:**  
Open `jsonSingle.xlsx` and you’ll see a sheet with two columns – **Name** and **Age** – and two rows containing “Bob, 30” and “Anna, 25”. The first row is automatically bolded as a header, thanks to SmartMarker’s default styling.

## Full Working Example  

Below is the complete, copy‑paste‑ready Java class. It includes the necessary imports, a `main` method, and comments that echo the explanations above.

```java
import com.aspose.cells.*;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Define JSON data
        String jsonData = "[{\"Name\":\"Bob\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Initialise SmartMarker processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 4️⃣ Configure export options – single table from array
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setArrayAsSingle(true); // key setting for a unified table

        // 5️⃣ Merge JSON into worksheet
        processor.process(worksheet, jsonData, exportOptions);

        // 6️⃣ Save the file
        workbook.save("output/jsonSingle.xlsx");
        System.out.println("Excel file created successfully at output/jsonSingle.xlsx");
    }
}
```

**Pro tip:** If you need custom column widths or styling, grab the `Table` object from the worksheet after processing:

```java
Table table = worksheet.getTables().get(0);
table.getDefaultStyle().setFontSize(11);
table.getDefaultStyle().setHorizontalAlignment(TextAlignmentType.LEFT);
```

That tiny snippet shows how easy it is to **generate excel from json** and then tweak the appearance.

## Common Questions & Edge Cases  

- **What if my JSON has nested objects?**  
  Aspose.Cells can flatten nested structures using dot notation (e.g., `Address.Street`). Just ensure your JSON is well‑formed and set `exportOptions.setFlattenObject(true)`.

- **Can I merge JSON into an existing template?**  
  Absolutely. Place SmartMarker tags like `&=Name` in your template cells, load the template workbook, and call `processor.process()` the same way.

- **Do I need to close resources?**  
  The `Workbook` class implements `AutoCloseable` in newer versions, so you can wrap it in a try‑with‑resources block if you prefer.

- **Performance concerns for huge arrays?**  
  For massive datasets, consider streaming the JSON or using the `setBatchSize` option to limit memory consumption.

## Conclusion  

You now have a solid, production‑ready pattern to **create Excel from JSON** using Java and Aspose.Cells. By configuring `ExportTableOptions.setArrayAsSingle(true)`, we effortlessly **export json to excel**, **convert json to xlsx**, and **import json into excel** without writing a single loop.

What’s next? Try adding formulas, conditional formatting, or even charts based on the JSON data. The same processor can handle CSV, XML, or custom Java objects, so the sky’s the limit.

If you found this guide helpful, feel free to experiment with other SmartMarker features, or check out Aspose’s documentation for advanced scenarios. Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Import JSON Data into Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Efficiently Import JSON to Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/import-export/import-json-to-excel-aspose-cells-java/)
- [Effortlessly Import JSON into Excel using Aspose.Cells for .NET](/cells/english/net/import-export/import-json-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}