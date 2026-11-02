---
date: 2026-08-21
description: 了解如何在 Excel 圖表中使用 Aspose.Cells for Java 新增 tooltips、data labels，並變更 chart
  type – 逐步指南，附有互動範例。
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: 變更 Excel Chart Type
og_description: 了解如何在 Excel 圖表中使用 Aspose.Cells for Java 新增 tooltips、data labels，並變更
  chart type – 逐步指南，附有互動範例。
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: 如何在 Java 中為 Excel 圖表新增 tooltips 與 data labels
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: 如何在 Java 中為 Excel 圖表新增 tooltips 與 data labels
url: /zh-hant/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 圖表中新增資料標籤並變更圖表類型 – Aspose.Cells Java

互動圖表為您的 Excel 報告帶來全新的洞察層次，而 **如何新增工具提示** 讓資訊即時可讀。在本教學中，您將學習如何 **在 Excel 圖表中新增資料標籤**、**變更圖表類型**，以及使用 Aspose.Cells 建立互動式 Java 解決方案。我們亦會示範如何新增工具提示以及簡單的下鑽超連結，讓您的觀眾深入探索資料。

## 快速解答
- **使用的函式庫是什麼？** Aspose.Cells for Java  
- **我可以變更圖表類型嗎？** 可以 – 只要在建立圖表時修改 `ChartType` 列舉即可。  
- **如何在圖表中新增工具提示？** 使用資料標籤 API（`setHasDataLabels(true)`）並啟用顯示數值。  
- **支援下鑽嗎？** 您可以將超連結附加到資料點，以實現基本的下鑽功能。  
- **前置條件？** Java IDE、Aspose.Cells JAR，以及含有範例資料的 Excel 檔案。

## 什麼是「新增工具提示」？
**「新增工具提示」** 指的是在 Excel 圖表上啟用滑鼠懸停文字，以顯示資料點的數值或自訂資訊的過程。在 Aspose.Cells 中，這透過圖表的資料標籤設定來實現。工具提示可協助使用者快速了解資料，同時不會使圖表雜亂，且可自訂字型、顏色與格式。

## 為什麼要使用 Aspose.Cells 的互動圖表？
Aspose.Cells 支援 **超過 50 種輸入與輸出格式**——包括 XLSX、CSV、PDF 與 HTML，且能在不將整個檔案載入記憶體的情況下處理 **超過 1 000 張工作表** 的活頁簿，提供快速的伺服器端圖表產生，適用於企業報告。互動圖表亦允許嵌入超連結、動態資料更新，並匯出為網頁友善的格式，因而非常適合儀表板與報告入口網站。

## 前置條件

在開始之前，請確保您已具備以下項目：

- Java 開發環境（建議使用 JDK 8 以上）  
- Aspose.Cells for Java 函式庫（從 [Aspose.Cells for Java 下載頁面](https://releases.aspose.com/cells/java/) 下載）  
- 含有您想要視覺化資料的範例活頁簿（`data.xlsx`）

## 步驟 1：設定您的 Java 專案

1. 在您喜愛的 IDE（IntelliJ IDEA、Eclipse 等）中建立新的 Java 專案。  
2. 將 Aspose.Cells JAR 加入專案的建置路徑或 Maven/Gradle 相依性。

## 步驟 2：載入資料

要使用圖表，您首先需要將活頁簿載入記憶體。

`Workbook` 類別代表一個 Excel 檔案，`Worksheet` 代表該檔案中的單一工作表。

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 如何在 Aspose.Cells 中變更圖表類型？

使用所需的 `ChartType` 列舉建立新圖表；Aspose.Cells 不會直接在原圖表上修改類型，因此您必須新增一個正確類型的圖表，並視需要移除舊圖表。此做法可確保所有系列與座標軸皆正確重建，以呈現新的視覺效果。

## 步驟 3：建立圖表（並變更其類型）

您可以選擇任何符合分析需求的圖表類型。以下我們建立一個 **柱狀圖**，但只要更改 `ChartType` 列舉，即可輕鬆切換為折線圖、圓餅圖或長條圖。

`Chart` 物件提供方法，以設定工作表中資料的視覺呈現方式。

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **專業提示：** 若要 **變更 Excel 圖表類型**，請將 `ChartType.COLUMN` 替換為 `ChartType.LINE`、`ChartType.PIE` 等。

## 如何在 Excel 圖表中新增工具提示？

載入圖表後，啟用資料標籤，並設定 `showValue` 旗標。如此一來，當使用者在已渲染的 Excel 檔案或 HTML 檢視中將滑鼠懸停於資料點時，工具提示會顯示該儲存格的值。您亦可自訂工具提示的字型、顏色與背景，以符合報告風格。

`DataLabel` 類別控制資料標籤的外觀與內容，亦同時充當工具提示。

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## 步驟 4：加入互動性

### 4.1. 新增工具提示（在圖表中新增工具提示）

當使用者將滑鼠懸停於資料點時會顯示工具提示。以下程式碼啟用資料標籤並將數值顯示為工具提示。

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. 新增資料標籤 – **在 Excel 圖表中新增資料標籤**

資料標籤在圖表本身提供永久的視覺提示。您可以將其顯示為說明框，以提升可讀性。

`DataLabel` 類別控制每個系列標籤的外觀。透過呼叫 `setHasDataLabels(true)` 並設定如 `setShowValue(true)` 等屬性，即可將數值直接嵌入圖表，使其在未互動的情況下即時可見。其他選項允許顯示系列名稱、百分比或自訂文字，以提供更豐富的資訊。

> **為什麼要新增資料標籤？** 直接在圖表上加入資料標籤可免除使用者懸停或猜測數值的需求，提升報告的清晰度。

### 4.3. 實作下鑽（在資料點上加入超連結）

加入下鑽功能的簡易方法是將超連結附加至特定資料點。點擊該點即會開啟包含詳細資訊的網頁。

`Hyperlink` 類別將可點擊的連結附加至圖表元素，實現下鑽導覽。

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 如何在 Excel 圖表中新增資料標籤？

`DataLabel` 類別控制每個系列標籤的外觀。透過呼叫 `setHasDataLabels(true)` 並設定如 `setShowValue(true)` 等屬性，即可將數值直接嵌入圖表，使其在未互動的情況下即時可見。其他選項允許顯示系列名稱、百分比或自訂文字，以提供更豐富的資訊。

## 步驟 5：儲存活頁簿

設定完圖表後，請將活頁簿持久化，以便將互動功能儲存至輸出檔案。

呼叫 `workbook.save` 會將修改後的活頁簿寫入指定格式的檔案。

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **工具提示未顯示** | 確保在設定 `setShowValue(true)` 之前已呼叫 `setHasDataLabels(true)`。 |
| **超連結無法點擊** | 確認輸出格式支援超連結（例如 XLSX，而非 CSV）。 |
| **圖表類型未變更** | 再次檢查在新增圖表時是否修改了正確的 `ChartType` 列舉。 |

## 常見問答

**Q: 如何在圖表建立後變更其類型？**  
A: 您需要使用所需的 `ChartType` 建立新圖表。Aspose.Cells 不支援即時類型轉換，請移除舊圖表並新增一個新圖表。

**Q: 我可以自訂工具提示的外觀嗎？**  
A: 可以。使用 `DataLabel` 的屬性，如 `setFontSize`、`setFontColor` 與 `setBackgroundColor` 來樣式化工具提示文字。

**Q: 如何在 Web 應用程式中處理使用者互動？**  
A: 將活頁簿匯出為 HTML 或 XLSX 檔案，並在客戶端使用 JavaScript 捕捉圖表元素的點擊事件。

**Q: 我可以在哪裡找到更多範例與文件？**  
A: 前往 [Aspose.Cells Java API 參考文件](https://reference.aspose.com/cells/java/) 查看完整的圖表相關類別與方法清單。

## 結論

現在您已了解如何 **在 Excel 圖表中新增資料標籤**、**變更 Excel 圖表類型**、**建立互動式 Java 圖表** 解決方案，並使用 Aspose.Cells for Java 為其加入工具提示、資料標籤與下鑽超連結。這些強化功能讓您的 Excel 報告對最終使用者而言更加引人入勝且富有洞察力。

---

**最後更新：** 2026-08-21  
**測試環境：** Aspose.Cells for Java 24.12  
**作者：** Aspose

## 相關教學

- [如何使用 Aspose.Cells for Java 修改 Excel 圖表與資料標籤](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [使用 Aspose.Cells Java 提取 Excel 圖表軸標籤：完整指南](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [使用 Aspose.Cells for Java 在 Excel 中建立氣泡圖：逐步指南](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}