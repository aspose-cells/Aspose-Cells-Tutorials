---
date: 2026-09-02
description: 了解如何在 Java 中使用 Aspose.Cells 建立 Excel 瀑布圖，設定圖表資料範圍、客製化標籤並匯出為 XLSX。
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: 瀑布圖表
og_description: 使用 Aspose.Cells for Java 建立 Excel 瀑布圖 – 設定圖表資料範圍、加入資料標籤，並在幾個步驟內匯出為
  XLSX。
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: 使用 Aspose.Cells for Java 建立 Excel 瀑布圖
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: 使用 Aspose.Cells for Java 建立 Excel 瀑布圖
url: /zh-hant/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 瀑布圖表

## 使用 Aspose.Cells for Java 的瀑布圖表簡介

在本教學中，您將學習如何使用 Aspose.Cells for Java **建立 Excel 瀑布圖** 以及 **設定圖表資料範圍**。瀑布圖將一系列正負數字轉化為清晰的視覺敘事，非常適合財務報表、銷售績效檢視，以及任何需要了解各項目對總額貢獻的情境。

## 快速答案
- **什麼是瀑布圖表？** 一種視覺化方式，顯示初始值如何透過一系列中間值的增加與減少，最終得到最終總計。  
- **使用哪個函式庫？** Aspose.Cells for Java。  
- **我需要授權嗎？** 免費試用版可用於開發；商業授權則需於正式環境使用。  
- **我可以將檔案儲存為 XLSX 嗎？** 可以 – 使用 `workbook.save("FileName.xlsx")`。  
- **它適合用於 Java 資料視覺化嗎？** 絕對適合；Aspose.Cells 在未安裝 Office 的情況下亦提供豐富的圖表功能。

## 什麼是瀑布圖表？
瀑布圖顯示對起始值的連續正向與負向貢獻，協助您了解每個組成部分如何影響最終結果。透過將盈餘與損失並排視覺化，使複雜的財務流動一目了然。

## 為何使用 Aspose.Cells for Java 來新增瀑布圖表？
Aspose.Cells 讓您在任何伺服器、CI 流程或桌面上產生 Excel 圖表，無需安裝 Microsoft Excel。它支援 **15+ 輸出格式**（XLSX、PDF、HTML、CSV 等），在不到一秒的時間內處理含有 **500+ 列** 的活頁簿，並提供對每個圖表元素的程式化控制——從顏色到資料標籤皆可自訂。

## 前置條件
在深入程式碼之前，請確保已具備以下前置條件：

- Aspose.Cells for Java：您需要安裝 Aspose.Cells for Java。您可從 Aspose.Cells for Java 發行頁面下載：[Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/)。
- Java 開發環境：確保您的系統已安裝 Java，且具備可使用的建置工具（Maven/Gradle）。

現在，讓我們一步一步開始建立瀑布圖表。

## 如何在 Java 中設定瀑布圖表的資料範圍
載入新的活頁簿，填入資料，加入 `Chart` 物件，定義系列範圍，最後儲存檔案。此流程相當簡單：您建立活頁簿，於儲存格填入類別與數值，建立圖表，綁定資料範圍，然後匯出活頁簿。最終會得到一個完整功能的瀑布圖表，可用於報告或儀表板。

### 步驟 1：匯入 Aspose.Cells
`com.aspose.cells` 套件包含所有 Excel 操作所需的類別，包括活頁簿建立、工作表處理與圖表產生。

### 步驟 2：初始化活頁簿與工作表
**Workbook** 代表一個 Excel 檔案，而 **Worksheet** 則是該檔案中的單一工作表。建立這些物件即提供放置原始資料與圖表的畫布。

### 步驟 3：輸入資料
A 欄保存類別標籤，B 欄則包含瀑布圖的數值。此佈局符合財務分析中常見的損益流程。

### 步驟 4：建立瀑布圖表
**Chart** 物件產生視覺化表示；將其類型設定為 `ChartType.WATERFALL` 即可配置為瀑布圖。使用 `add` 方法設定系列的圖表資料範圍（`"B2:B6"`），並將類別軸連結至 `"A2:A6"`。

### 步驟 5：儲存活頁簿
儲存活頁簿會將圖表與資料寫入指定的檔案格式。呼叫 `workbook.save("WaterfallChart.xlsx")` 以產生 XLSX 檔，或變更格式參數以匯出為 PDF、CSV 或 HTML。

## 常見問題與解決方案

- **圖表顯示為空白** – 請確認資料範圍參照（`B2:B6` 與 `A2:A6`）與實際包含數值與類別的儲存格相符。  
- **負值未正確顯示** – 請確保系列類型設定為 `ChartType.WATERFALL`；其他圖表類型對負值的處理方式不同。  
- **檔案無法在 Excel 中開啟** – 使用最新的 Aspose.Cells 版本，並確認檔案副檔名與格式相符（Excel 為 `.xlsx`）。

## 常見問答

### 如何自訂我的瀑布圖表外觀？
您可以修改屬性，例如 `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` 以變更條形顏色，使用 `setShowDataLabels(true)` 開啟資料標籤，並透過 `getCategoryAxis().setTitle("Stage")` 調整軸標題。Aspose.Cells API 參考文件提供完整的可自訂選項清單。

### 我可以在同一工作表中建立多個瀑布圖表嗎？
可以。加入第一個圖表後，使用不同的資料範圍與新的 `Chart` 物件重複圖表建立步驟。每個圖表皆獨立，且可放置於工作表的任意位置。

### Aspose.Cells 與不同的 Java 開發環境相容嗎？
絕對相容。此函式庫可在 Eclipse、IntelliJ IDEA、NetBeans 以及任何支援 Maven 或 Gradle 的建置系統中使用，無需額外插件。

### 我可以為我的瀑布圖表新增額外的資料系列嗎？
您可以透過呼叫 `chart.getNSeries().add("C2:C6", true)` 並分別設定每個系列來新增更多系列。這讓您能夠並排比較多個情境。

### 我可以在哪裡找到更多 Aspose.Cells for Java 的資源與範例？
請參閱 Aspose.Cells Java API 參考文件取得完整說明：https://reference.aspose.com/cells/java/（[Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/)）。

## 常見問答

**Q: 如何設定財務瀑布圖的圖表資料範圍？**  
A: 使用圖表系列的 `add` 方法，傳入包含數值的儲存格範圍，例如 `"B2:B6"`。

**Q: 我可以將活頁簿匯出為 PDF 而非 XLSX 嗎？**  
A: 可以，呼叫 `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` 以產生 PDF 版本。

**Q: 如果需要建立包含更多類別的瀑布圖該怎麼辦？**  
A: 同時擴展數值欄與類別欄的資料範圍，然後相應更新 `add` 與 `setCategoryData` 呼叫。

**Q: 有沒有辦法自動格式化正負條形？**  
A: 迭代 `Series` 集合，根據每個數值的正負設定 `FillFormat` 顏色；Aspose.Cells 允許以程式方式套用條件格式。

**Q: Aspose.Cells 支援圖表的動態資料更新嗎？**  
A: 支援。修改儲存格數值後，只需重新儲存活頁簿——圖表會自動反映新資料。

---

**最後更新：** 2026-09-02  
**測試環境：** Aspose.Cells for Java (latest)  
**作者：** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## 相關教學

- [使用 Aspose.Cells for Java 自訂 Excel 圖表資料標籤：逐步指南](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [使用 Aspose.Cells Java 為 Excel 圖表新增資料標籤](/cells/java/advanced-excel-charts/chart-interactivity/)
- [如何使用 Aspose.Cells 在 Java 中建立與匯出圖表：完整指南](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}