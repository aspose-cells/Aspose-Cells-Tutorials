---
date: '2026-09-27'
description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step guide
  to customize Excel pie chart, set up Maven dependency, and generate professional
  charts.
images:
- /java/charts-graphs/create-customize-aspose-cells-pie-chart-java/og-image.png
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Create pie chart java using Aspose.Cells for Java. Learn to customize
  Excel pie chart, add Maven dependency, and generate professional charts in minutes.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Create pie chart java with Aspose.Cells – Full Java Guide
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: How to create pie chart java with Aspose.Cells
url: /java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create pie chart java with Aspose.Cells

## Introduction
Creating a **pie chart** programmatically often feels like a puzzle, especially when you need fine‑grained control over colors, legends, and titles. In this guide you’ll learn how to **create pie chart java** using Aspose.Cells, then customize the Excel pie chart to match your brand or reporting style. We’ll walk through environment setup, data population, chart generation, and visual tweaks—all without leaving your Java IDE.

**What you'll learn**
- Add the **Maven dependency Aspose.Cells** to your project.
- Build a workbook, fill cells with data, and generate a pie chart.
- Apply custom colors, titles, and legends to the chart.
- Export the workbook to an XLSX file ready for sharing.

Before you start, you should be comfortable with basic Java syntax and have Maven or Gradle installed.

## Quick answers
- **Which library creates pie charts in Java?** Aspose.Cells for Java.
- **Do I need a license?** A free trial works for development; a paid license is required for production.
- **What Maven coordinates are required?** `com.aspose:aspose-cells:24.10`.
- **Can I change slice colors?** Yes, via the `setAreaColor` method on each series.
- **Is the chart exportable to XLSX?** Absolutely—just call `workbook.save("output.xlsx")`.

## What is a pie chart in Excel?
A pie chart visualizes a single data series as proportional slices of a circle, making it easy to compare parts of a whole. Each slice’s angle corresponds to its value relative to the total, allowing quick insight into distribution across categories such as market share, budget allocation, or demographic percentages.

## Why use Aspose.Cells to create a pie chart java?
Aspose.Cells supports over 50 chart types and can handle worksheets with up to one million rows without loading the entire file into memory. This performance edge lets you generate large reports on modest hardware, while offering fine‑grained control over chart appearance, data binding, and export formats, making it a superior choice over many open‑source libraries.

## Prerequisites
- **Java Development Kit (JDK)** 8 or newer.
- **IDE** such as IntelliJ IDEA or Eclipse.
- **Maven** or **Gradle** for dependency management.
- A **trial or purchased Aspose.Cells license**.

### Required libraries and dependencies
Add the Aspose.Cells Maven artifact to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Or the Gradle equivalent:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### License acquisition steps
Aspose.Cells for Java is commercial, but you can start with a free trial. Visit the [purchase page](https://purchase.aspose.com/buy) to obtain a temporary license key.

## Setting up Aspose.Cells for Java
First, make sure the library is on your classpath. After adding the dependency, you can initialize the API as shown below.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Implementation guide

### Create and configure a workbook
The `Workbook` class represents an entire Excel file in memory.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Step 1: instantiate a workbook
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
This creates a new, empty workbook that you can immediately start populating.

### Access or modify worksheet cells
A `Worksheet` represents a single sheet within the workbook, containing cells, rows, and columns.  
You’ll write the data that drives the pie chart into a worksheet.

#### Step 2: get the first worksheet and its cells
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Populate the cells with category names and values that the chart will consume.

### Create a pie chart
`Chart` objects visualize data in a worksheet and support various types such as pie, column, and line.

#### Step 3: add a pie chart to the worksheet
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Configure pie chart series and data
`Series` defines the data range and formatting for a chart, linking worksheet cells to visual elements.

#### Step 4: set the series for the chart
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Configure chart legend and title appearance
A chart `Legend` displays the series names and colors, helping readers identify each slice.

#### Step 5: customize chart legend and title
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Customize chart series colors
`setAreaColor` sets the fill color of a chart series slice using an RGB value.

#### Step 6: change pie segment colors
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Autofit columns and save workbook
`autoFitColumns` automatically adjusts column widths to fit the cell contents.

#### Step 7: adjust column widths and save the file
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Common use cases
- **Demographic analysis:** Show population distribution across regions.
- **Market‑share reporting:** Visualize each competitor’s share in a single glance.
- **Budget allocation:** Highlight how funds are split among departments.

## Performance considerations
- Release objects (`workbook.dispose()`) when they’re no longer needed to free native memory.
- For massive data sets, use `WorkbookDesigner` to stream data instead of loading everything at once.
- Profile with Java Flight Recorder to spot any bottlenecks in chart generation.

## Frequently asked questions

**Q: Can I generate multiple pie charts in the same workbook?**  
A: Yes, repeat the chart‑creation steps for each data range; each chart is independent.

**Q: Does Aspose.Cells support 3‑D pie charts?**  
A: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.

**Q: How do I apply a custom theme to all charts?**  
A: Use the `Workbook.setDefaultTheme` method before creating any charts.

**Q: What file formats can I export the workbook to?**  
A: Over 30 formats, including XLSX, CSV, PDF, and HTML.

**Q: Is a license required for commercial deployment?**  
A: Yes, a valid license removes evaluation watermarks and unlocks full functionality.

## Conclusion
You now have a complete, end‑to‑end recipe for **create pie chart java** with Aspose.Cells. By following the steps above you can generate polished Excel pie charts, tailor colors and titles, and embed them into any reporting pipeline. Explore other chart types—column, line, radar—to broaden your data‑visualization toolkit.

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## Related Tutorials

- [Customize Excel Chart Data Labels Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Create Dynamic Excel Charts with Aspose.Cells Java&#58; A Comprehensive Guide for Developers](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Create and Customize Excel Workbooks Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}