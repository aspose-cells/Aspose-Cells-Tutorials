---
category: general
date: 2026-03-01
description: How to create PDF and save workbook as PDF, export Excel to HTML, and
  use expand function with Aspose.Cells for Java. Step‑by‑step code included.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: en
og_description: How to create PDF from a workbook using Aspose.Cells for Java. Learn
  to save workbook as PDF, export Excel to HTML, and use the EXPAND function.
og_title: How to Create PDF from a Workbook – Java Tutorial
tags:
- Aspose.Cells
- Java
- PDF generation
title: How to Create PDF from a Workbook – Complete Java Guide
url: /java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create PDF from a Workbook – Complete Java Guide

Ever wondered **how to create PDF** directly from an Excel workbook without juggling third‑party converters? You're not alone. Many developers hit a wall when they need a quick PDF export, an HTML preview, or fancy array formulas—all in one go.  

In this tutorial we’ll walk through a single, self‑contained Java program that does exactly that. We'll **save workbook as PDF**, show you how to **export Excel to HTML** while keeping frozen rows, and demonstrate the **use expand function** inside a worksheet. By the end you’ll have a runnable project you can drop into any Maven or Gradle build.

> **Pro tip:** All the code below works with Aspose.Cells 23.10 (or newer). If you’re on an older version, some method names might differ slightly.

---

## Prerequisites

- **Java 17** (or any LTS version) installed and configured.
- **Aspose.Cells for Java** library. Add the following Maven dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- An IDE or text editor of your choice (IntelliJ IDEA, VS Code, Eclipse…).

No external APIs, no web services—just pure Java and the Aspose.Cells SDK.

---

## Overview of the Solution

We'll split the implementation into **seven logical steps**:

1. Create a workbook and demonstrate the **EXPAND** function.  
2. Enable font variation selectors and **save the workbook as PDF**.  
3. Export the same workbook to HTML while preserving frozen rows.  
4. Use a Smart Marker with an `IF`‑parameter to inject conditional text.  
5. Apply a master‑detail Smart Marker for hierarchical data.  
6. Load a Markdown file that contains Base‑64‑encoded images.  
7. Configure GridJs options for alignment and borders, then insert data.

Each step is wrapped in its own method to keep the `main` method tidy and to illustrate **why** we do what we do, not just **what** we type.

---

## Step 1 – Create a Workbook and Use the EXPAND Function

The **EXPAND** function is a new dynamic‑array formula introduced in Office 365. It lets you spill a range into a larger area without manually copying cells.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Why this matters:**  
- `EXPAND` automatically pads the result with blanks, which is perfect when you later **save workbook as PDF**—the PDF will show a clean, rectangular table.  
- Calling `calculateFormula()` ensures the formula engine runs before we export anything.

---

## Step 2 – Enable Font Variation Selectors and **Save Workbook as PDF**

If you need to support advanced typography (e.g., emoji or CJK variation selectors), you must turn the feature on **before** saving.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Key point:** The primary keyword **how to create pdf** is answered here—by calling `workbook.save(..., SaveFormat.PDF)` after configuring the settings.

---

## Step 3 – **Export Excel to HTML** While Preserving Frozen Rows

Often stakeholders request a quick web preview. Aspose.Cells can export to HTML, and with `setPreserveFrozenRows(true)` we keep the same scrolling experience as in Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Why you care:** Frozen rows are a usability nicety; without them, the header rows disappear when users scroll down the page.

---

## Step 4 – Smart Marker with an IF‑Parameter

Smart Markers let you merge data into a template without writing loops. The `if`‑parameter adds conditional logic directly inside the marker.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

The output PDF will read **“VIP Customer: Acme Corp”** because `IsVIP` is `true`. Change the flag to `false` and you’ll get **“Regular Customer: Acme Corp”**—no extra code needed.

---

## Step 5 – Master‑Detail Smart Marker Using a Hierarchical Range

When you have parent‑child data (e.g., orders and line items), a master‑detail marker saves you from manual row insertion.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**What you gain:** The engine expands the master rows for each order and automatically nests the detail rows underneath—perfect for invoices or purchase reports.

---

## Step 6 – Load a Markdown Document with Embedded Base‑64 Images

If your source data lives in Markdown (common in documentation pipelines), Aspose.Cells can render it straight into a workbook.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Edge case note:** If the Base‑64 string is malformed, Aspose will skip the image but continue processing the rest of the document—no crash.

---

## Step 7 – Configure GridJs Options and Insert Data

GridJs is a lightweight JavaScript grid that Aspose can render into HTML. Aligning numbers and applying borders improves readability.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Why we care:** Proper alignment and borders make the generated HTML look like a polished spreadsheet—useful for dashboards.

---

## Putting It All Together – The `main` Method

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}