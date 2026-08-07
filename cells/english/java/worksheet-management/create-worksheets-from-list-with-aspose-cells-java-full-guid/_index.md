---
category: general
date: 2026-07-16
description: Create worksheets from list using Aspose.Cells Java. Step‑by‑step tutorial
  to allow duplicate sheet names and populate workbook from template efficiently.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets from list
- allow duplicate sheet names
- duplicate sheet names excel
- populate workbook from template
language: en
lastmod: 2026-07-16
og_description: Create worksheets from list with Aspose.Cells Java. Learn to allow
  duplicate sheet names and populate workbook from template in a clear, practical
  guide.
og_image_alt: Screenshot of an Excel workbook with multiple generated worksheets
og_title: Create worksheets from list – Aspose.Cells Java Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Create worksheets from list using Aspose.Cells Java. Step‑by‑step tutorial
    to allow duplicate sheet names and populate workbook from template efficiently.
  headline: Create worksheets from list with Aspose.Cells Java – Full Guide
  type: TechArticle
- description: Create worksheets from list using Aspose.Cells Java. Step‑by‑step tutorial
    to allow duplicate sheet names and populate workbook from template efficiently.
  name: Create worksheets from list with Aspose.Cells Java – Full Guide
  steps:
  - name: 1. Very Large Lists
    text: If your list contains thousands of rows, consider streaming the data or
      processing in batches to avoid excessive memory consumption. Aspose.Cells supports
      **`WorkbookDesigner`** for streaming large data sets.
  - name: 2. Custom Sheet Naming Logic
    text: 'You can use any .NET/Java string format in `setDetailSheetNewName`. For
      example:'
  - name: 3. When Duplicate Sheet Names Are Not Desired
    text: If you *do* want unique sheet names, simply omit `setAllowDuplicateSheetNames(true)`
      and rely on a naming pattern that guarantees uniqueness (e.g., include the primary
      key).
  - name: 4. Populating Multiple Templates in One Workbook
    text: You can repeat the `process` call on different worksheets, each with its
      own `SmartMarkerOptions`. This lets you **populate workbook from template**
      multiple times in a single run.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Smart Markers
title: Create worksheets from list with Aspose.Cells Java – Full Guide
url: /java/worksheet-management/create-worksheets-from-list-with-aspose-cells-java-full-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create worksheets from list with Aspose.Cells Java – Full Guide

Ever wondered how to **create worksheets from list** without writing a hundred lines of boilerplate? You’re not the only one. When you need a fresh sheet for each order, invoice, or data row, doing it manually is a nightmare. The good news? Aspose.Cells for Java makes it a piece of cake, and you can even let the engine **allow duplicate sheet names** when that suits your scenario.

In this tutorial we’ll walk through every step required to **populate workbook from template**, configure the SmartMarker engine to spin up a new sheet per detail row, and handle the quirky case of duplicate sheet names in Excel. By the end you’ll have a runnable program that you can drop into any Maven or Gradle project.

---

## What You’ll Build

- Load an existing Excel template that contains SmartMarker placeholders.  
- Feed a Java `List<Map<String,Object>>` (our master‑detail data) into the processor.  
- Generate a separate worksheet for each detail row using `SmartMarkerOptions`.  
- Enable `allow duplicate sheet names` so the same sheet title can appear multiple times if needed.  
- Save the populated workbook to a new file.

No external libraries beyond Aspose.Cells are required, and the code works on Java 8‑21.

---

## Prerequisites

- **Aspose.Cells for Java** (download the JAR or add the Maven dependency).  
- Java Development Kit (JDK) 8 or newer.  
- An Excel template (`input.xlsx`) placed in a known directory.  
- Basic familiarity with Java collections.

If you’re already using Maven, add this snippet to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

---

## Step 1: Load the Template and **Create Worksheets from List**

The first thing we do is open the workbook that holds our SmartMarker layout. Think of the workbook as a canvas; each sheet we generate later will be a new layer on that canvas.

```java
// Step 1: Load the workbook that contains the smart marker template
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Why this matters:** Loading the template once keeps the file I/O overhead low, and the `Workbook` object gives us direct access to the `SmartMarkerProcessor`.

---

## Step 2: Prepare the Master‑Detail Data Source

Our goal is to **create worksheets from list**, so we need a collection where each element represents a row of detail data. In this example we simulate a list of orders; each order itself is a `Map<String,Object>`.

```java
// Step 2: Prepare the master‑detail data source (e.g., a list of orders)
Map<String, Object> masterDetailData = new HashMap<>();
masterDetailData.put("Orders", getOrders()); // getOrders() returns List<Map<String,Object>>
```

Below is a quick implementation of `getOrders()` that you can copy‑paste. Feel free to replace it with a DB call or a JSON parse.

```java
private static List<Map<String, Object>> getOrders() {
    List<Map<String, Object>> orders = new ArrayList<>();

    // Sample order 1
    Map<String, Object> order1 = new HashMap<>();
    order1.put("OrderID", 1001);
    order1.put("Customer", "Acme Corp");
    order1.put("Amount", 1250.75);
    orders.add(order1);

    // Sample order 2 (duplicate sheet name scenario)
    Map<String, Object> order2 = new HashMap<>();
    order2.put("OrderID", 1002);
    order2.put("Customer", "Acme Corp"); // Same customer name → same sheet name
    order2.put("Amount", 980.00);
    orders.add(order2);

    // Add as many orders as you like
    return orders;
}
```

> **Tip:** The key `"Orders"` must match the SmartMarker region name in your template (`&=Orders.OrderID`, etc.).  

---

## Step 3: **Allow Duplicate Sheet Names** – Configuring SmartMarker Options

By default Aspose.Cells will refuse to create two sheets with the same name and will throw an exception. When you intentionally want duplicate names—perhaps because the sheet name is derived from a non‑unique field—you can turn on the **allow duplicate sheet names** flag.

```java
// Step 3: Configure SmartMarker options to generate a new sheet per detail row
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
smartMarkerOptions.setDetailSheetNewName("Orders_{0}"); // {0} → row index (0‑based)
smartMarkerOptions.setAllowDuplicateSheetNames(true); // enable duplicate sheet names
```

> **Why use `{0}`?** The placeholder inserts the current row index, guaranteeing each sheet gets a unique suffix even if the base name repeats. If you truly want identical names, you could use a static string and rely on `allow duplicate sheet names` to silence the conflict.

---

## Step 4: Process the SmartMarkers

Now the heavy lifting happens: the processor reads each row from the `Orders` list, clones the template sheet, replaces the markers, and creates a new worksheet according to the naming rule we set.

```java
// Step 4: Process the smart markers using the data and the configured options
workbook.getWorksheets().get(0).getSmartMarkerProcessor()
        .process(masterDetailData, smartMarkerOptions);
```

> **What’s happening under the hood?**  
> - The processor scans the first worksheet for markers like `&=Orders.OrderID`.  
> - For each entry in `Orders`, it creates a copy of that sheet.  
> - It fills the placeholders with the map values.  
> - Finally, it renames the sheet based on `DetailSheetNewName`.

Because we set **allow duplicate sheet names**, the processor won’t abort if two rows generate the same base name.

---

## Step 5: Save the Populated Workbook

After processing, you simply write the workbook back to disk. The output file will contain a separate sheet for each order.

```java
// Step 5: Save the populated workbook to a new file
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

Open `output.xlsx` and you’ll see something like:

- **Orders_0** – contains data for order 1001  
- **Orders_1** – contains data for order 1002  

If you had disabled `allow duplicate sheet names` and both rows produced the same name (e.g., “Orders”), Aspose would have thrown an exception. With the flag enabled, you can decide whether to keep the duplicate or rely on the `{0}` suffix for uniqueness.

---

## Handling Edge Cases and Best Practices

### 1. Very Large Lists
If your list contains thousands of rows, consider streaming the data or processing in batches to avoid excessive memory consumption. Aspose.Cells supports **`WorkbookDesigner`** for streaming large data sets.

### 2. Custom Sheet Naming Logic
You can use any .NET/Java string format in `setDetailSheetNewName`. For example:

```java
smartMarkerOptions.setDetailSheetNewName("Order_${Customer}_${OrderID}");
```

Just remember to escape special characters (`$`, `{`, `}`) if they appear in your data.

### 3. When Duplicate Sheet Names Are Not Desired
If you *do* want unique sheet names, simply omit `setAllowDuplicateSheetNames(true)` and rely on a naming pattern that guarantees uniqueness (e.g., include the primary key).

### 4. Populating Multiple Templates in One Workbook
You can repeat the `process` call on different worksheets, each with its own `SmartMarkerOptions`. This lets you **populate workbook from template** multiple times in a single run.

---

## Full Working Example

Putting everything together, here’s a self‑contained Java class you can compile and run:

```java
import com.aspose.cells.*;
import java.util.*;

public class DuplicateDetailSheetDemo {
    public static void main(String[] args) throws Exception {
        // Load the template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Prepare master‑detail data (list of orders)
        Map<String, Object> masterDetailData = new HashMap<>();
        masterDetailData.put("Orders", getOrders());

        // Configure SmartMarker options: new sheet per row + allow duplicates
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Orders_{0}"); // {0} → row index
        smartMarkerOptions.setAllowDuplicateSheetNames(true); // enable duplicate sheet names

        // Process the markers and generate sheets
        workbook.getWorksheets().get(0).getSmartMarkerProcessor()
                .process(masterDetailData, smartMarkerOptions);

        // Save the result
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }

    // Sample data generator – replace with real data source as needed
    private static List<Map<String, Object>> getOrders() {
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Customer", "Acme Corp");
        order1.put("Amount", 1250.75);
        orders.add(order1);

        Map<String, Object> order2 = new HashMap<>();
        order2.put("OrderID", 1002);
        order2.put("Customer", "Acme Corp"); // Same customer → duplicate sheet name scenario
        order2.put("Amount", 980.00);
        orders.add(order2);

        // Add more orders as needed
        return orders;
    }
}
```

**Expected output:** After running, `output.xlsx` contains two worksheets named `Orders_0` and `Orders_1`, each filled with the corresponding order’s details. If you changed `DetailSheetNewName` to a static string like `"Orders"` and kept `allow duplicate sheet names` enabled, both sheets would be called `Orders`, demonstrating the **duplicate sheet names excel** capability.

---

## Conclusion

You now know how to **create worksheets from list** using Aspose.Cells for Java, how to **allow duplicate sheet names**, and the exact steps to **populate workbook from template** with SmartMarkers. The approach is clean, fast, and scales from a handful of rows to thousands.

What’s next? Try adding images, applying cell styles, or generating summary sheets that aggregate data across all generated worksheets. You can also explore the **SmartMarker conditional formatting** feature to highlight


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Create an Excel Workbook using Aspose.Cells in Java&#58; A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create and Customize Excel Workbooks Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)
- [Hide Excel Worksheets Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/english/java/worksheet-management/hide-worksheets-excel-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}