---
category: general
date: 2026-11-22
description: 學習如何使用 Aspose.Cells for Java 將 Excel 轉換為 PowerPoint，並包含在單一工作流程中將 Excel
  圖表匯出至 PowerPoint 的步驟。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- export excel chart to powerpoint
- Aspose.Cells Java
- Excel to PPTX conversion
- Java file format conversion
language: zh-hant
lastmod: 2026-11-22
og_description: 使用 Aspose.Cells for Java 將 Excel 轉換為 PowerPoint。按照此完整的逐步教學，還可將 Excel
  圖表匯出至 PowerPoint。
og_image_alt: Diagram showing conversion of Excel to PowerPoint using Aspose.Cells
og_title: 使用 Aspose.Cells 將 Excel 轉換為 PowerPoint – Java 指南
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  headline: How to convert Excel to PowerPoint with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  name: How to convert Excel to PowerPoint with Aspose.Cells for Java
  steps:
  - name: Open `withShapes.pptx` in PowerPoint.
    text: Open `withShapes.pptx` in PowerPoint.
  - name: Confirm that each Excel sheet appears as a separate slide.
    text: Confirm that each Excel sheet appears as a separate slide.
  - name: Check that charts retain their colors, legends, and data labels.
    text: Check that charts retain their colors, legends, and data labels.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: 如何使用 Aspose.Cells for Java 將 Excel 轉換為 PowerPoint
url: /zh-hant/java/integration-interoperability/how-to-convert-excel-to-powerpoint-with-aspose-cells-for-jav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells for Java 將 Excel 轉換為 PowerPoint

如果您需要 **convert Excel to PowerPoint**，本指南將示範使用 Aspose.Cells for Java 的簡易方法。您亦會看到如何在同一流程中 **export Excel chart to PowerPoint**，讓您可以直接將圖表嵌入簡報，而不必手動複製貼上。

將試算表轉換為投影片是想向非技術觀眾分享資料驅動洞見的常見需求。您不必在 PowerPoint 中重新製作圖表，只要自動化整個管線，即可保持格式完整，節省大量時間。

在本教學中您將會：

* 在 Maven 或 Gradle 專案中設定 Aspose.Cells。  
* 載入包含資料與圖表的現有活頁簿。  
* 設定 `ImageOrPrintOptions` 以目標 PPTX 格式。  
* 將活頁簿儲存為 PowerPoint 簡報。  
* 驗證結果並處理常見的例外情況。

> **Prerequisite** – 您需要一份有效的 Aspose.Cells for Java 授權（或使用評估版）。此程式碼相容於 Java 8+ 以及任何支援 Maven/Gradle 的 IDE。

![Diagram showing conversion of Excel to PowerPoint using Aspose.Cells](convert_excel_to_powerpoint.png)

## 您需要的項目

| 項目 | 原因 |
|------|------|
| **Java Development Kit (JDK) 8 或更新版本** | 必須編譯與執行範例程式。 |
| **Maven 或 Gradle** | 簡化 Aspose.Cells 的相依管理。 |
| **Aspose.Cells for Java** | 提供用於轉換的 `Workbook` 與 `ImageOrPrintOptions` API。 |
| **一個包含至少一個圖表的 Excel 檔案 (`shapes.xlsx`)** | 用於示範 *export Excel chart to PowerPoint* 情境。 |

## 第一步：將 Aspose.Cells 加入您的專案

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-cells:24.10' // latest version as of 2026
```

> **Why this step matters** – Adding the library makes the `Workbook`, `ImageOrPrintOptions`, and `SaveFormat` classes available. Without the correct dependency the code will not compile.

## 第二步：載入包含圖表的活頁簿

```java
import com.aspose.cells.Workbook;

// Load the Excel file. Replace the path with your actual location.
Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
```

**Explanation:**  
`Workbook` is the entry point for all Excel operations. By loading `shapes.xlsx` you bring both the data tables and any embedded charts into memory, enabling the subsequent conversion.

## 第三步：建立轉換選項並將目標格式設定為 PPTX

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

// Configure options for image/print conversion.
ImageOrPrintOptions options = new ImageOrPrintOptions();
// The SaveFormat.PPTX constant tells Aspose.Cells to generate a PowerPoint file.
options.setSaveFormat(SaveFormat.PPTX);
```

**Why use `ImageOrPrintOptions`?**  
These options control how each worksheet or chart is rendered. Setting `SaveFormat.PPTX` instructs the library to place each sheet (or chart) on its own slide, preserving visual fidelity.

## 第四步：將活頁簿儲存為 PowerPoint 簡報

```java
// The second argument is the options object we just configured.
workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);
```

**What happens here?**  
Aspose.Cells iterates over the workbook’s worksheets and charts, rasterizes them into slide‑compatible graphics, and writes a `.pptx` package to the specified location. The resulting file can be opened in Microsoft PowerPoint, Google Slides, or any PPTX‑compatible viewer.

## 第五步：驗證轉換結果

1. 在 PowerPoint 中開啟 `withShapes.pptx`。  
2. 確認每個 Excel 工作表皆以獨立投影片顯示。  
3. 檢查圖表是否保留顏色、圖例與資料標籤。  

如果圖表顯示失真，您可能需要調整 `ImageOrPrintOptions` 的 DPI：

```java
options.setResolution(300); // 300 DPI gives higher quality for complex charts
```

## Export Excel chart to PowerPoint – a focused variation

Sometimes you only need to move a single chart rather than the whole workbook. You can achieve this by converting the chart to an image first and then inserting it into a PowerPoint slide manually, but Aspose.Cells simplifies the process:

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;
import com.aspose.cells.SaveOptions;

// Assume the chart is on the first worksheet, first chart object.
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

// Create options for converting the chart to an image.
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
chartOptions.setImageFormat(ImageFormat.PNG);
chartOptions.setSaveFormat(SaveFormat.PPTX);

// Save only the chart as a PPTX slide.
chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOptions);
```

**Why this matters:**  
The snippet isolates a single chart, reduces file size, and gives you finer control over which visuals become slides. It’s the most direct way to **export Excel chart to PowerPoint** when you don’t need the full workbook.

## 常見陷阱與避免方式

| Issue | Cause | Fix |
|-------|-------|-----|
| **Blank slides** | Worksheet contains no visible data or the chart is hidden. | Ensure the chart is visible and the worksheet has data before saving. |
| **Low‑resolution images** | Default DPI is 96, which may be insufficient for printed slides. | Call `options.setResolution(200‑300)` before `workbook.save`. |
| **Unsupported chart types** | Very new or custom chart types may not render perfectly. | Export the chart as an image (`ImageFormat.PNG`) then insert it manually. |
| **File‑path errors** | Incorrect relative path on different OS. | Use `Paths.get("YOUR_DIRECTORY", "file.xlsx").toString()` for platform‑independent paths. |

## 生產環境級別的進階技巧

* **Batch processing:** Loop through a directory of Excel files and call the same conversion logic.  
* **Memory management:** For large workbooks, invoke `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` to reduce heap usage.  
* **License activation:** Place your license file (`Aspose.Cells.lic`) in the classpath and call `License license = new License(); license.setLicense("Aspose.Cells.lic");` before any Aspose API usage.  
* **Thread safety:** Each thread should work with its own `Workbook` instance; Aspose.Cells objects are not thread‑safe.

## 完整範例程式碼

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) throws Exception {
        // 1. Optional: activate your Aspose.Cells license.
        // License license = new License();
        // license.setLicense("Aspose.Cells.lic");

        // 2. Load the workbook that contains charts.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // 3. Set conversion options – target PPTX format.
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
        // Increase resolution for sharper charts (optional).
        options.setResolution(300);

        // 4. Save the workbook as a PowerPoint presentation.
        workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);

        // 5. (Optional) Export only the first chart to its own PPTX.
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        ImageOrPrintOptions chartOpts = new ImageOrPrintOptions();
        chartOpts.setSaveFormat(SaveFormat.PPTX);
        chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOpts);

        System.out.println("Conversion completed successfully.");
    }
}
```

**Expected output:**  

Running the program prints `Conversion completed successfully.` and creates two files:

* `withShapes.pptx` – a slide deck where each worksheet (and its charts) appears on a separate slide.  
* `singleChart.pptx` – a single‑slide presentation containing only the first chart from the workbook.

Open these files in PowerPoint to verify that the charts retain their original styling and data labels.

## 結論

You now know how to **convert Excel to PowerPoint** using Aspose.Cells for Java, and you also saw the most efficient way to **export Excel chart to PowerPoint** when only a specific visual is needed. By configuring `ImageOrPrintOptions` and setting the `SaveFormat` to `PPTX`, the library handles the heavy lifting of rendering worksheets and charts into slide‑compatible graphics.

From here you can:

* Automate batch conversions for reporting pipelines.  
* Combine the generated PPTX with other slide assets using the Apache POI `XSLF` API.  
* Explore additional export formats such as PDF or HTML for multi‑channel distribution.

Feel free to experiment with DPI settings, custom slide layouts, or embedding the generated PPTX into email workflows. Happy coding!


## 接下來該學什麼？

以下教學與本指南的技術緊密相關，提供完整範例程式碼與逐步說明，協助您掌握更多 API 功能並探索其他實作方式：

- [How to export Excel sheet to PowerPoint with Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step‑by‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to export chart to docx from Excel using Aspose.Cells for Java](/cells/english/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}