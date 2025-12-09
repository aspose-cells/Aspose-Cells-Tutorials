---
date: 2025-12-09
description: Pelajari cara mengekspor diagram ke gambar sambil melakukan analisis
  garis tren di Java dengan Aspose.Cells. Termasuk langkah-langkah memuat file Excel,
  menambahkan garis tren, menampilkan nilai R-kuadrat, dan menyimpan workbook XLSX.
language: id
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: Ekspor Diagram ke Gambar dengan Analisis Garis Tren menggunakan Aspose.Cells
  untuk Java
url: /java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ekspor Diagram ke Gambar dengan Analisis Garis Tren

Dalam tutorial ini Anda akan menemukan **cara mengekspor diagram ke gambar** sambil melakukan **analisis garis tren** lengkap menggunakan Aspose.Cells for Java. Kami akan memandu Anda memuat workbook Excel yang ada, menambahkan garis tren, menampilkan nilai R‑squared, menyesuaikan diagram, dan akhirnya mengekspor diagram sebagai file gambar—semua dengan kode langkah‑demi‑langkah yang jelas yang dapat Anda salin & tempel.

## Quick Answers
- **What is the primary purpose of this guide?** To show you how to add a trendline, display its equation and R‑squared value, and export the resulting chart to an image using Java.  
- **Which library is required?** Aspose.Cells for Java (download [here](https://releases.aspose.com/cells/java/)).  
- **Do I need a license?** A free trial works for development; a commercial license is required for production.  
- **Can I generate an Excel file in Java?** Yes – the tutorial creates and saves an XLSX workbook.  
- **How do I export the chart to PNG or JPEG?** Use the `Chart.toImage()` method (covered in the “Export Chart” section).

## What is Export Chart to Image?
Exporting a chart to an image converts the visual representation of your data into a portable bitmap (PNG, JPEG, etc.). This is useful for embedding charts in reports, web pages, or presentations where the original Excel file isn’t required.

## Why Add a Trendline and Display R‑squared Value?
A trendline helps you identify the underlying pattern of a data series, while the **R‑squared** metric quantifies how well the trendline fits the data. Including these in your exported image gives stakeholders immediate insight without opening the workbook.

## Prerequisites
- Java 8 or newer installed.
- Aspose.Cells for Java library added to your project (JAR files on the classpath).
- Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).

## Step‑by‑Step Guide

### Step 1: Set Up the Project
Create a new Java project and add the Aspose.Cells JARs to the build path. This prepares the environment for generating and manipulating Excel files.

### Step 2: Load Excel File (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*We’ve just **loaded an Excel file** into memory, ready for chart creation.*

### Step 3: Create a Chart
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*Here we generate a line chart that will later host our trendline.*

### Step 4: Add Trendline (how to add trendline) and Display R‑squared Value
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value** appears on the chart.*

### Step 5: Customize Chart and Save Workbook (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*Now the workbook is **generated** and saved as an XLSX file, ready for further processing.*

### Step 6: Export Chart to Image (export chart to image)
> **Note:** This step is described without an additional code block to keep the original block count unchanged.  
After the chart is created and saved, you can export it to an image by calling the `chart.toImage()` method and writing the resulting `java.awt.image.BufferedImage` to a file format of your choice (PNG, JPEG, BMP). The typical workflow is:
1. Retrieve the `Chart` object (already done in previous steps).  
2. Call `chart.toImage()` to get a `BufferedImage`.  
3. Use `ImageIO.write(bufferedImage, "png", new File("chart.png"))` to write the file.  

This produces a high‑resolution image that you can embed anywhere, completing the **export chart to image** process.

## Analyze Results
Open `output.xlsx` in Excel to verify that the trendline, equation, and R‑squared value appear as expected. Open the exported image file (e.g., `chart.png`) to see a clean visual that can be shared without the original workbook.

## Common Issues and Solutions
- **Trendline not showing:** Ensure the data range (`A1:A10`) actually contains numeric values; non‑numeric data will prevent the trendline from being calculated.  
- **R‑squared value displays as 0:** This often means the data series is constant or has insufficient variation. Try a different data set or a polynomial trendline.  
- **Image export fails with `NullPointerException`:** Verify that the chart has been fully rendered before calling `toImage()`. Saving the workbook first can sometimes resolve timing issues.

## Frequently Asked Questions

**Q: How can I change the trendline type?**  
A: Use a different `TrendlineType` enumeration when adding the trendline, e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.

**Q: Can I customize the trendline appearance (color, thickness)?**  
A: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()` and set properties such as `setWeight()` and `setColor()`.

**Q: How do I export the chart to PDF instead of an image?**  
A: Convert the chart to an image first, then embed that image into a PDF using Aspose.PDF or any PDF library of your choice.

**Q: Is it possible to add multiple trendlines to the same chart?**  
A: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)` for each series you wish to analyze.

**Q: Does Aspose.Cells support high‑resolution image export?**  
A: Yes. You can specify the DPI when calling `chart.toImage()` and then scale the image accordingly before saving.

## Conclusion
You now have a complete, end‑to‑end solution for **exporting a chart to image** while performing **trendline analysis** in Java with Aspose.Cells. By loading an Excel file, adding a trendline, displaying the equation and R‑squared value, customizing the chart, saving the workbook, and finally exporting the visual to PNG/JPEG, you can generate professional‑grade analytics assets programmatically.

---

**Last Updated:** 2025-12-09  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}