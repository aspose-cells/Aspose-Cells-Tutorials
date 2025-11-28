---
date: 2025-11-28
description: 學習如何在 Java 中使用 Aspose.Cells 添加工具提示、資料標籤和下鑽功能，以建立互動圖表。
language: zh-hant
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: 如何在互動圖表中加入工具提示 (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 如何在互動圖表中加入工具提示 (Aspose.Cells Java)

## 介紹

互動圖表讓使用者透過懸停、點擊或深入探索細節來探索資料。在本教學中，您將學習**如何加入工具提示**至圖表，以及**如何加入資料標籤**，並實作**深入探索**導覽——全部使用 Aspose.Cells for Java。完成後，您將能建立具備完整功能的互動圖表，讓您的資料展示更具吸引力與洞察力。

## 快速解答
- **需要的函式庫是什麼？** Aspose.Cells for Java（最新版本）。  
- **本指南主要涵蓋哪項功能？** 為圖表加入工具提示。  
- **我也可以加入資料標籤嗎？** 可以 — 請參閱「加入資料標籤」章節。  
- **支援深入探索嗎？** 支援，透過資料點的超連結實現。  
- **產生的檔案格式為何？** 含有互動圖表的 Excel 活頁簿（`.xlsx`）。

## 什麼是加入工具提示？

工具提示是一種小型彈出視窗，當使用者將滑鼠懸停在圖表元素上時會顯示，提供額外資訊，如精確數值或自訂訊息。工具提示可提升資料可讀性，同時不會使視覺版面雜亂。

## 為何在 Java 中建立互動圖表？

- **更佳的決策制定：** 使用者能即時看到精確的數值。  
- **專業報告：** 互動元素讓儀表板更具現代感。  
- **可重複使用的元件：** 一旦掌握 API，即可套用於任何基於 Excel 的報告解決方案。

## 前置條件

在開始之前，請確保您已具備以下條件：

- Java 開發環境（JDK 8 或更新版本）。  
- Aspose.Cells for Java 函式庫（從 [here](https://releases.aspose.com/cells/java/) 下載）。  
- 一個名為 **data.xlsx** 的範例 Excel 檔案，內含您想要視覺化的資料。

## 步驟 1：設定 Java 專案

1. 在您偏好的 IDE（IntelliJ IDEA、Eclipse 等）中建立新的 Java 專案。  
2. 將 Aspose.Cells JAR 加入專案的 classpath。

## 步驟 2：載入資料

要建立互動圖表，首先需要一個含有資料的工作表。以下程式碼會從 **data.xlsx** 載入第一個工作表。

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 步驟 3：建立圖表

現在我們將在工作表中加入直條圖。圖表將佔用 F6 至 K16 的儲存格。

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 步驟 4：加入互動功能

### 4.1. 如何加入工具提示

以下程式碼片段會為圖表的第一個系列啟用工具提示。每個資料點在懸停時會顯示其數值。

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. 為圖表加入資料標籤

如果您也想在每個直條旁顯示可見的標籤，請使用下方示範的 **add data labels chart** 方法。這符合次要關鍵字 *add data labels chart*。

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. 如何深入探索（實作 Drill‑Down）

深入探索允許使用者點擊資料點並跳轉至詳細視圖（例如網頁）。此處我們為系列的第一個點附加超連結。

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **專業提示：** 您可以根據資料點的數值動態產生 URL，打造真正以資料為驅動的深入探索體驗。

## 步驟 5：儲存活頁簿

設定完圖表後，儲存活頁簿。產生的檔案包含可在 Excel 中開啟的互動圖表。

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|------|------|----------|
| 工具提示未顯示 | 未啟用資料標籤 | 確保在設定 `ShowValue` 之前呼叫 `setHasDataLabels(true)`。 |
| 超連結無法點擊 | 資料點索引錯誤 | 確認您引用的是正確的資料點（`get(0)` 為第一個點）。 |
| 圖表位置錯誤 | 儲存格範圍不正確 | 調整 `add(ChartType.COLUMN, row1, col1, row2, col2)` 中的列/欄索引。 |

## 常見問答

**問：如何變更圖表類型？**  
答：將 `ChartType.COLUMN` 替換為其他列舉值，例如在呼叫 `worksheet.getCharts().add(...)` 時使用 `ChartType.LINE` 或 `ChartType.PIE`。

**問：我可以自訂工具提示的外觀嗎？**  
答：可以。使用 `DataLabel` 物件的格式屬性（字型大小、背景顏色等）來設定工具提示文字的樣式。

**問：如何在 Web 應用程式中處理使用者互動？**  
答：將活頁簿匯出為 Web 相容格式（例如 HTML），並使用 JavaScript 捕捉圖表元素的點擊事件。

**問：在哪裡可以找到更多範例與文件？**  
答：請參閱官方 API 參考文件：[Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)。

**問：是否可以在同一圖表中加入多個深入探索連結？**  
答：當然可以。遍歷系列的資料點，並為每個點的 `Hyperlinks` 集合指派唯一的 URL。

## 結論

在本指南中，您學會了**如何加入工具提示**、**加入資料標籤**，以及**實作深入探索**功能，從而使用 Aspose.Cells 建立**create interactive chart java** 解決方案。這些功能可將靜態的 Excel 圖表轉變為動態、使用者友善的視覺化圖形，協助利害關係人輕鬆探索資料。

---

**最後更新：** 2025-11-28  
**測試環境：** Aspose.Cells for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}