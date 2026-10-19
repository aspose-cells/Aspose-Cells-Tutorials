---
date: 2026-09-02
description: 了解如何使用 Aspose.Cells for Java 將圖表匯出為 PNG、加入資料系列、合併折線與柱狀圖、將活頁簿儲存為 XLSX，並新增圖例。
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: 將圖表匯出為 PNG 並為合併圖表新增資料系列
og_description: 使用 Aspose.Cells for Java 將圖表匯出為 PNG、合併折線與柱狀圖、加入資料系列，並在單一教學中將活頁簿儲存為
  XLSX。
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: 將圖表匯出為 PNG 並為合併圖表新增資料系列
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: 將圖表匯出為 PNG 並為合併圖表新增資料系列
url: /zh-hant/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 匯出圖表為 PNG 並為合併圖表新增資料系列

在本教學中，您將 **新增資料系列** 到 Excel 活頁簿，**結合折線圖與長條圖** 元素，並學習如何使用 Aspose.Cells for Java **將圖表匯出為 PNG**。我們將逐步說明——從設定活頁簿、將圖表加入工作表、客製化圖例，到 **將活頁簿另存為 XLSX** 並產生圖表的 PNG 圖像。完成後，您將擁有可直接嵌入報告或儀表板的合併圖表。

## 快速解答
- **哪個函式庫可建立合併圖表？** Aspose.Cells for Java。  
- **如何新增資料系列？** 呼叫 `chart.getNSeries().add(...)` 並傳入適當的範圍。  
- **如何將圖表匯出為 PNG？** 使用 `chart.toImage("chart.png", ImageFormat.getPng())`。  
- **活頁簿可以儲存為哪種檔案格式？** 標準的 `.xlsx`（將活頁簿另存為 XLSX）。  
- **生產環境是否需要授權？** 需要——必須擁有有效的 Aspose.Cells 授權才能在生產環境部署。

## 在 Aspose.Cells 中什麼是匯出圖表為 PNG？
將圖表匯出為 PNG 會產生 Excel 圖表的點陣圖像，可在網頁、報告或電子郵件中顯示，且無需安裝 Excel 應用程式。此方法會完整捕捉圖表的視覺佈局、顏色與資料標記，產生可攜帶的圖像檔案。

## 為何要建立合併折線與長條圖？
合併折線與長條圖可讓您在同一視圖中以不同的視覺呈現方式（例如在長條圖上疊加折線系列）顯示多組資料。此方式非常適合比較趨勢與總量、突顯相關性，或在保持視覺佔用空間小的同時提供更豐富的洞見。

## 前置條件
- Java Development Kit (JDK) 8 或更新版本  
- Aspose.Cells for Java 函式庫（從以下連結下載）  
- 具備基本的 Java 語法與 Excel 概念的熟悉度  

## 開始使用

首先，從官方網站下載 Aspose.Cells for Java 函式庫：

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

將 JAR 加入專案的 classpath 後，即可開始建立圖表。

### 步驟 1：匯入 aspose.cells 類別
`Workbook` 是 Aspose.Cells 的核心物件，代表記憶體中的整個 Excel 檔案。  
```java
import com.aspose.cells.*;
```

### 步驟 2：建立新活頁簿
`Worksheet` 代表 `Workbook` 中的單一工作表，提供對儲存格、列與圖表的存取。  
```java
Workbook workbook = new Workbook();
```

### 步驟 3：存取第一個工作表
`Chart` 是保存所有圖表相關設定、系列與渲染選項的物件。  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 步驟 4：將合併圖表物件加入工作表
我們將先建立折線圖，之後再加入長條系列，以達成 **合併折線與長條圖** 的效果。  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 為圖表新增資料

現在圖表容器已建立，我們需要為其提供資料。

### 步驟 5：定義資料範圍並新增資料系列
`NSeries` 是儲存圖表每個資料系列的集合。新增系列會將儲存格範圍連結至圖表。  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **小技巧：** 第一個參數（`"A1:A5"`）是第一個系列的範圍，第二個參數（`"B1:B5"`）則建立第二個系列，將與第一個系列合併。

### 步驟 6：設定類別（X 軸）資料
`CategoryAxis` 代表圖表的水平軸，控制 X 軸上顯示的標籤。  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## 客製化圖表

好的圖表能說明故事。讓我們為它加上標題、軸標籤與清晰的圖例。

### 步驟 7：設定圖表軸標籤與標題
`Title` 設定圖表的主標題，`Axis` 物件則代表 X 與 Y 軸。  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 步驟 8：新增圖例並調整其位置
`Legend` 控制圖表中系列圖例的放置位置與外觀。  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## 儲存與匯出圖表

客製化完成後，您會想要 **將活頁簿另存為 XLSX** 並產生圖像。

### 步驟 9：將活頁簿儲存為 Excel 檔案（XLSX）
`Workbook.save` 將記憶體中的活頁簿寫入指定格式的檔案。  
```java
workbook.save("CombinedChart.xlsx");
```

### 步驟 10：將圖表匯出為 PNG
`Chart.toImage` 會將圖表渲染為所選格式的圖像檔案。  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 方法 **產生 Excel 圖表** 圖像，可用於網頁、報告或電子郵件。

## 常見問題與故障排除

| 問題 | 解決方案 |
|-------|----------|
| **沒有資料顯示** | 確認儲存格範圍（`A1:A5`、`B1:B5`、`C1:C5`）在建立圖表前確實包含資料。 |
| **圖例覆蓋圖表** | 設定 `chart.getLegend().setOverlay(false)`，或將圖例移至其他位置（例如 `RIGHT`）。 |
| **圖像檔案為空白** | 確保圖表至少有一個系列，且在完成所有客製化後才呼叫 `chart.toImage`。 |
| **儲存時拋出例外** | 檢查您是否對目標目錄具有寫入權限，且檔案未在 Excel 中開啟。 |

## 常見問答

**Q:** 如何安裝 Aspose.Cells for Java？  
**A:** 從官方網站下載 JAR 並將其加入專案的 classpath。下載連結為：[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)。  

**Q:** 我可以建立除折線與長條圖之外的其他圖表類型嗎？  
**A:** 可以，Aspose.Cells 支援長條圖、圓餅圖、散佈圖、區域圖等多種圖表類型。請參閱 API 文件取得完整清單。  

**Q:** 生產環境是否需要授權？  
**A:** 在生產部署時必須擁有有效的 Aspose.Cells 授權。亦提供免費試用供評估使用。  

**Q:** 如何變更每個系列的顏色？  
**A:** 在新增系列後，使用 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`（或類似方法）來變更顏色。  

**Q:** 在哪裡可以找到更多程式碼範例？  
**A:** 完整文件與其他範例可於 Aspose 參考網站取得：[Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/)。  

---

**最後更新：** 2026-09-02  
**測試環境：** Aspose.Cells for Java latest version  
**作者：** Aspose

## 相關教學

- [如何使用 Aspose.Cells for Java 為 Excel 圖表新增標籤](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [如何使用 Aspose.Cells for Java 建立帶趨勢線的 Excel 圖表並匯出為圖像](/cells/java/advanced-excel-charts/trendline-analysis/)
- [使用 Aspose.Cells for Java 將 Excel 圖表匯出為 PDF：自訂頁面尺寸指南](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}