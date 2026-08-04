---
title: Export chart to PNG and add data series for combined chart
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
description: Learn how to export chart to png, add data series, combine line column chart, save workbook as xlsx and add legend chart using Aspose.Cells for Java.
weight: 12
url: /java/advanced-excel-charts/combined-chart-types/
date: 2026-02-14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Export chart to PNG and add data series for combined chart

In this tutorial you’ll **add data series** to an Excel workbook, **combine line and column chart** elements, and learn how to **export chart to PNG** using Aspose.Cells for Java. We'll walk through every step—from setting up the workbook, adding the chart to a worksheet, customizing the legend, to **save workbook as xlsx** and generate a PNG image of the chart. By the end, you’ll have a ready‑to‑use combined chart that you can embed in reports or dashboards.

## Quick Answers
- **Which library creates combined charts?** Aspose.Cells for Java  
- **How do I add a data series?** Use `chart.getNSeries().add(...)`  
- **How can I export chart to png?** Call `chart.toImage("file.png", ImageFormat.getPng())`  
- **What file format can I save the workbook as?** Standard `.xlsx` (save workbook as xlsx)  
- **Do I need a license for production?** A valid Aspose.Cells license is required  

## What is **export chart to PNG** in Aspose.Cells?
Exporting a chart to PNG creates a raster image of the Excel chart that can be displayed in web pages, reports, or emails without requiring the Excel application.

## Why create a **combined line column chart**?
A combined chart lets you display different data sets with distinct visual representations (e.g., a line series over a column series) in a single view. This is perfect for comparing trends against totals, highlighting correlations, or delivering richer insights in a compact format.

## Prerequisites
- Java Development Kit (JDK) 8 or higher  
- Aspose.Cells for Java library (download from the link below)  
- Basic familiarity with Java syntax and Excel concepts  

## Getting Started

First, download the Aspose.Cells for Java library from the official site:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

Once the JAR is added to your project’s classpath, you can start building the chart.

### Step 1: Import Aspose.Cells classes
```java
import com.aspose.cells.*;
```

### Step 2: Create a new workbook
```java
Workbook workbook = new Workbook();
```

### Step 3: Access the first worksheet
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Step 4: Add a combined chart object to the worksheet  
We’ll start with a line chart and later add a column series to achieve a **combined line column chart** effect.
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adding Data to the Chart

Now that the chart container exists, we need to feed it with data.

### Step 5: Define the data ranges and **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** The first parameter (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates a second series that will be combined with the first.

### Step 6: Set the category (X‑axis) data
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## Customizing the Chart

A good chart tells a story. Let’s give it titles, axis labels, and a clear legend.

### Step 7: **Set chart axis labels** and title
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### Step 8: **Add legend chart** and adjust its position
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## Saving and Exporting the Chart

After customizing, you’ll want to **save workbook as xlsx** and also generate an image.

### Step 9: Save the workbook as an Excel file (xlsx)
```java
workbook.save("CombinedChart.xlsx");
```

### Step 10: **Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> The `chart.toImage` method **generates excel chart** images that can be used in web pages, reports, or emails.

## Common Issues & Troubleshooting

| Issue | Solution |
|-------|----------|
| **No data appears** | Verify that the cell ranges (`A1:A5`, `B1:B5`, `C1:C5`) actually contain data before creating the chart. |
| **Legend overlaps chart** | Set `chart.getLegend().setOverlay(false)` or move the legend to a different position (e.g., `RIGHT`). |
| **Image file is blank** | Ensure the chart has at least one series and that `chart.toImage` is called after all customizations. |
| **Saving throws an exception** | Check that you have write permissions to the target directory and that the file isn’t open in Excel. |

## Frequently Asked Questions

**Q: How do I install Aspose.Cells for Java?**  
A: Download the JAR from the official site and add it to your project’s classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: Can I create other chart types besides line and column?**  
A: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart types. Refer to the API documentation for the full list.

**Q: Is a license required for production use?**  
A: A valid Aspose.Cells license is required for production deployments. A free trial is available for evaluation.

**Q: How can I change the colors of each series?**  
A: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar) after adding the series.

**Q: Where can I find more code examples?**  
A: Comprehensive documentation and additional samples are available at the Aspose reference site: [here](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2026-02-14  
**Tested With:** Aspose.Cells for Java latest version  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}