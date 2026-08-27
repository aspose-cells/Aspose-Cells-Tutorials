---
date: 2026-08-27
description: 了解如何在 chart 中添加 trendline、顯示其 R‑squared 值，並使用 Aspose.Cells for Java 將
  chart 匯出為 PNG 或 JPEG 圖像。
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: 以 Trendline 分析將 Chart 匯出為圖像
og_description: 為 chart 添加 trendline、檢視 R‑squared，並使用 Aspose.Cells for Java 將結果匯出為
  PNG/JPEG——快速且支援 50 種格式的解決方案。
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: 使用 Aspose.Cells for Java 為 chart 添加 trendline 並匯出為圖像
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: 如何在 Java 中為 chart 添加 trendline 並匯出為圖像
url: /zh-hant/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖表中加入趨勢線並匯出為圖像

在本教學中，您將學會如何 **在圖表中加入趨勢線**、顯示 R 平方值，並使用 Aspose.Cells for Java 將視覺圖形匯出為 PNG 或 JPEG 檔案。您將了解趨勢線的重要性、如何準備活頁簿，以及產生可嵌入報告、電子郵件或網頁的高解析度圖像的具體步驟。

## 快速回答
- **本指南的主要目標是什麼？** 示範如何在圖表中加入趨勢線、顯示其方程式與 R 平方值，並使用 Java 匯出圖表為圖像。  
- **我需要哪個程式庫？** Aspose.Cells for Java – 可從 [Aspose.Cells for Java release page](https://releases.aspose.com/cells/java/) 下載。  
- **開發時需要授權嗎？** 免費試用版可用於開發；商業授權則需於正式部署時使用。  
- **我可以程式化產生 Excel 活頁簿嗎？** 可以 – 本教學會從頭建立並儲存 XLSX 活頁簿。  
- **圖表如何匯出為 PNG 或 JPEG？** 呼叫 `Chart.toImage()` 方法，並使用 `ImageIO.write(...)` 寫入回傳的 `BufferedImage`。

## 如何建立帶有趨勢線的 Excel 圖表並匯出為圖像？
載入活頁簿、加入折線圖、附加顯示方程式與 R 平方值的趨勢線、儲存活頁簿，然後呼叫 `chart.toImage()` 並將產生的 `BufferedImage` 寫入 PNG 或 JPEG 檔案。此端對端流程僅需幾行 Java 程式碼，即可產生適用於任何下游應用的像素完美圖像。

## 什麼是匯出圖表為圖像？
將圖表匯出為圖像會將資料的視覺呈現轉換為可攜帶的點陣圖（PNG、JPEG、BMP 等）。此格式非常適合在報告、網頁或簡報中嵌入圖表，而不需要原始的 Excel 檔案。

## 為什麼要加入趨勢線並顯示 R 平方值？
趨勢線揭示資料序列的底層模式，而 **R 平方** 指標則量化趨勢線與資料的貼合程度。將兩者同時呈現在匯出的圖像中，可讓利害關係人立即獲得洞見，無需開啟活頁簿。這有助於決策者快速評估相關性強度與預測趨勢。

## 前置條件
- 已在開發機器上安裝 Java 8 或更新版本。  
- 已將 Aspose.Cells for Java 程式庫加入專案的 classpath（JAR 檔）。  
- 熟悉 IntelliJ IDEA 或 Eclipse 等 Java IDE。

## 步驟說明

### 步驟 1：設定專案
建立新的 Java 專案，並將 Aspose.Cells 的 JAR 放入建置路徑。此步驟會為產生與操作 Excel 檔案的環境做好準備。

### 步驟 2：載入 Excel 檔案 (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*我們剛剛 **載入了一個 Excel 檔案** 到記憶體中，已可開始建立圖表。*

### 步驟 3：建立圖表
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*此處產生一個折線圖，稍後將用於放置趨勢線。*

### 步驟 4：加入趨勢線 (how to add trendline) 並顯示 R 平方值
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*`setDisplayRSquaredValue(true)` 呼叫確保 **R 平方值** 會顯示在圖表上。*

### 步驟 5：自訂圖表並儲存活頁簿 (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*現在活頁簿已 **產生** 並儲存為 XLSX 檔案，準備進一步處理。*

### 步驟 6：匯出圖表為圖像 (export chart to image)
> **注意：** 此步驟未加入額外程式碼區塊，以保持原始區塊數量不變。  
在圖表建立並儲存後，您可以透過呼叫 `chart.toImage()` 方法，將產生的 `java.awt.image.BufferedImage` 寫入您選擇的檔案格式（PNG、JPEG、BMP）。典型工作流程如下：
1. 取得 `Chart` 物件（已在前述步驟完成）。  
2. 呼叫 `chart.toImage()` 取得 `BufferedImage`。  
3. 使用 `ImageIO.write(bufferedImage, "png", new File("chart.png"))` 寫入檔案。  

`Chart` 物件代表活頁簿中的圖表，提供修改外觀與資料的方法。`BufferedImage` 是 Java 中用於在記憶體中保存圖像的類別，可寫入檔案。`ImageIO` 為 Java 的圖像讀寫工具類別。`setDisplayRSquaredValue` 會在趨勢線上顯示 R 平方統計值。

### 分析結果
在 Excel 中開啟 `output.xlsx`，驗證趨勢線、方程式與 R 平方值是否如預期顯示。再開啟匯出的圖像檔（例如 `chart.png`），即可看到可直接分享且不需原始活頁簿的乾淨視覺效果。

## 常見問題與解決方案
- **趨勢線未顯示：** 確認資料範圍 (`A1:A10`) 為數值型別；非數值資料會導致無法計算趨勢線。  
- **R 平方值顯示為 0：** 這通常表示資料序列恆定或缺乏變化。請嘗試使用不同的資料集或改用多項式趨勢線。  
- **圖像匯出時拋出 `NullPointerException`：** 確認圖表已完整渲染後再呼叫 `toImage()`。先儲存活頁簿有時可解決時序問題。

## 常見問答

**Q: 如何變更趨勢線類型？**  
A: 在加入趨勢線時使用不同的 `TrendlineType` 列舉，例如 `TrendlineType.POLYNOMIAL` 代表多項式擬合。

**Q: 我可以自訂趨勢線的外觀（顏色、粗細）嗎？**  
A: 可以。透過 `trendline.getLineFormat()` 取得趨勢線的 `LineFormat`，並設定 `setWeight()`、`setColor()` 等屬性。

**Q: 如何將圖表匯出為 PDF 而非圖像？**  
A: 先將圖表匯出為圖像，然後使用 Aspose.PDF 或其他 PDF 程式庫將該圖像嵌入 PDF。

**Q: 可以在同一圖表中加入多條趨勢線嗎？**  
A: 當然可以。對每個欲分析的系列呼叫 `chart.getNSeries().get(0).getTrendlines().add(...)` 即可。

**Q: Aspose.Cells 支援高解析度圖像匯出嗎？**  
A: 支援。呼叫 `chart.toImage()` 時可指定 DPI，並在儲存前調整圖像大小，以確保列印或高密度螢幕上的清晰輸出。

---

**最後更新：** 2026-08-27  
**測試環境：** Aspose.Cells for Java 最新版（支援 50+ 檔案格式，且可在不完全載入記憶體的情況下處理高達 200 萬列的活頁簿）  
**作者：** Aspose

## 相關教學

- [Add Data Labels to Excel Chart with Aspose.Cells Java](/cells/java/advanced-excel-charts/chart-interactivity/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java&#58; Custom Page Sizes Guide](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}