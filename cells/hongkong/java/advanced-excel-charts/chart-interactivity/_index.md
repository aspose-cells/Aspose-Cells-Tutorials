---
date: 2025-12-05
description: 學習如何使用 Aspose.Cells 在 Java 中加入資料標籤圖表並建立互動圖表。加入工具提示、資料標籤及下鑽功能。
language: zh-hant
linktitle: Add Data Labels Chart with Interactivity
second_title: Aspose.Cells Java Excel Processing API
title: 在 Aspose.Cells Java 中新增具互動性的資料標籤圖表
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.Cells Java 中加入資料標籤圖表與互動功能

互動圖表讓使用者能即時探索資料。在本教學中，您將使用 Aspose.Cells for Java **add data labels chart** 功能——工具提示、資料標籤與下鑽動作。完成後，您將擁有一個精緻的互動圖表，讓複雜資料即刻易於理解。

## 快速解答
- **我需要哪個函式庫？** Aspose.Cells for Java  
- **我可以在 Excel 圖表中加入工具提示嗎？** 是 – 使用 API 的資料標籤設定。  
- **哪些圖表類型支援互動功能？** 大多數內建類型（柱狀圖、折線圖、圓餅圖等）。  
- **正式環境需要授權嗎？** 需要有效的 Aspose.Cells 授權。  
- **實作大約需要多久？** 基本圖表大約需要 10–15 分鐘。

## 什麼是「add data labels chart」？
一個 *add data labels chart* 是指每個資料點直接在圖形上顯示標籤（數值、名稱或自訂文字）的圖表。這讓觀眾能在不懸停或參照其他圖例的情況下，直接讀取精確數值。

## 為什麼要建立 Java 互動圖表解決方案？
嵌入互動功能——工具提示、可點擊點、下鑽連結——可將靜態試算表轉變為探索式儀表板。使用者可以：
- 快速辨識異常值。
- 只需點擊一次即可存取更深入的資料層級。
- 透過減少額外報告的需求，提高決策速度。

## 前置條件

在開始之前，請確保您已具備：

- Java 開發環境（建議使用 JDK 8 以上）。  
- Aspose.Cells for Java 函式庫（從 [here](https://releases.aspose.com/cells/java/) 下載）。

## 步驟 1：設定 Java 專案

1. 在您喜愛的 IDE（IntelliJ、Eclipse、VS Code 等）中建立新 Java 專案。  
2. 將 Aspose.Cells for Java JAR 加入專案的 classpath。

## 步驟 2：載入資料

要建立互動圖表，首先需要在工作表中有資料。以下程式碼片段會載入名為 **data.xlsx** 的現有活頁簿。

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 步驟 3：建立圖表

現在我們建立一個柱狀圖並將其放置於工作表上。如有需要，可自行將 `ChartType.COLUMN` 替換為其他類型。

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 步驟 4：加入互動功能 – 「add data labels chart」的核心

### 4.1. 加入工具提示 (add tooltips excel chart)

當使用者將滑鼠懸停於資料點時，會顯示工具提示。以下程式碼透過啟用資料標籤並顯示數值來開啟此功能。

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. 加入資料標籤 (add data labels chart)

資料標籤是顯示在每個點旁的文字。此程式碼片段將圖表設定為顯示呼叫框標籤，而非純數值。

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. 實作下鑽 (create interactive chart java)

下鑽允許使用者點擊資料點後跳轉至詳細視圖。此處我們為第一個資料點附加超連結；您可以依需求為其他點重複此操作。

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 步驟 5：儲存活頁簿

設定完圖表後，將活頁簿保存為新檔案，以便在 Excel 中開啟並測試互動功能。

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 常見問題與技巧

| 問題 | 解決方案 |
|-------|----------|
| **工具提示未顯示** | 確保在設定 `ShowValue` 之前先呼叫 `setHasDataLabels(true)`。 |
| **超連結無法點擊** | 確認 URL 格式正確，且 Excel 的安全設定允許外部連結。 |
| **圖表類型不相容** | 某些圖表類型（例如雷達圖）標籤支援有限——請選擇相容的類型，如柱狀圖或折線圖。 |
| **大量資料時效能延遲** | 限制帶資料標籤的點數量；對於不太重要的系列，可考慮使用 `setShowValue(false)`。 |

## 常見問答

**Q: 如何變更圖表類型？**  
A: 在建立圖表的程式碼行中修改 `ChartType` 列舉（例如使用 `ChartType.LINE` 以建立折線圖）。

**Q: 我可以自訂工具提示的外觀嗎？**  
A: 可以——使用 `DataLabel` 物件的字型、背景色與邊框屬性來樣式化工具提示。

**Q: 如何在 Web 應用程式中處理使用者互動？**  
A: 將活頁簿匯出為 HTML 頁面或使用 Aspose.Cells Cloud 來呈現圖表，然後使用 JavaScript 捕捉點擊事件。

**Q: 我在哪裡可以找到更多範例與文件？**  
A: 前往 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) 查看完整的圖表相關類別與方法清單。

## 結論

本指南示範了如何使用 Aspose.Cells 於 **add data labels chart** 功能，並建立 **interactive chart Java** 解決方案。透過加入工具提示、資料呼叫框與下鑽超連結，您可以將靜態的 Excel 圖表轉變為動態的資料探索工具，提升洞察力與可用性。

---

**最後更新：** 2025-12-05  
**測試環境：** Aspose.Cells for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}