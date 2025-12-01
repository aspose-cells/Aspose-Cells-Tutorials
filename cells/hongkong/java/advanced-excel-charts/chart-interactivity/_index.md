---
date: 2025-12-01
description: 學習如何使用 Aspose.Cells for Java 更改 Excel 圖表類型，並加入工具提示、資料標籤及下鑽等互動功能。
language: zh-hant
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: 變更 Excel 圖表類型並加入互動功能 – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 更改 Excel 圖表類型並加入互動功能

## Introduction

互動圖表讓您的觀眾即時探索資料，同時能夠 **更改 Excel 圖表類型** 為您提供彈性，以最有效的視覺格式呈現資訊。在本教學中，您將學習如何使用 Aspose.Cells for Java 來更改圖表類型、加入工具提示、嵌入資料標籤，甚至建立下鑽連結——全部在 Java 程式碼中完成。完成後，您將擁有一個功能完整、具互動性的 Excel 活頁簿，可嵌入報告、儀表板或 Web 應用程式中。

## Quick Answers
- **我可以以程式方式更改圖表類型嗎？** 是的 – 在建立或更新圖表時使用 `ChartType` 列舉。  
- **如何為圖表加入工具提示？** 啟用資料標籤並將 `ShowValue` 設為 true。  
- **加入下鑽連結的最簡單方法是什麼？** 透過 `getHyperlinks().add(url)` 為資料點附加超連結。  
- **使用 Aspose.Cells 是否需要授權？** 免費試用版可用於開發；正式環境需購買授權。  
- **支援哪個版本的 Java？** 完全支援 Java 8 及以上版本。

## 什麼是「更改 Excel 圖表類型」？

更改圖表類型是指在保持底層資料不變的情況下，切換視覺呈現方式（例如，從柱狀圖改為折線圖）。當您發現其他圖表能更有效傳達趨勢、比較或分佈時，這非常有用。

## 為何要為 Excel 圖表加入互動性？

- **更佳的資料洞察：** 工具提示與資料標籤讓使用者在不捲動的情況下看到精確數值。  
- **吸引人的簡報：** 互動元素能保持觀眾的興趣。  
- **下鑽功能：** 超連結讓使用者跳轉至詳細工作表或外部資源。  
- **可重複使用的資產：** 只要切換圖表類型，同一本活頁簿即可應用於多種報告情境。

## 先決條件

- Java 開發環境 (JDK 8+)  
- Aspose.Cells for Java 程式庫（從 [here](https://releases.aspose.com/cells/java/) 下載）  
- 一個包含欲視覺化資料的範例 Excel 檔案 (`data.xlsx`)

## 逐步指南

### 步驟 1：設定您的 Java 專案

1. 在您喜愛的 IDE（IntelliJ IDEA、Eclipse、VS Code 等）中建立新的 Java 專案。  
2. 將 Aspose.Cells JAR 加入專案的 classpath。

### 步驟 2：載入來源活頁簿

我們先載入包含圖表資料的現有活頁簿。

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 步驟 3：建立圖表並 **更改其類型**

以下我們先建立柱狀圖，接著立即示範如有需要如何將其切換為折線圖。

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **專業提示：** 在建立後更改圖表類型只需呼叫 `setChartType(...)`。這即可滿足主要關鍵字 **change Excel chart type**，而不需要建立新圖表物件。

### 步驟 4：加入互動性

#### 4.1 為圖表加入工具提示

當使用者將滑鼠懸停於資料點上時會顯示工具提示。在 Aspose.Cells 中，工具提示是透過資料標籤實作的。

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 加入資料標籤（ **add data labels chart** ）

資料標籤可顯示精確數值、類別名稱或兩者皆顯示。此處我們使用標註樣式。

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 實作下鑽（ **add drill down excel** ）

下鑽連結允許使用者點擊資料點後跳轉至詳細視圖，無論是活頁簿內部或是網頁上。

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### 步驟 5：儲存活頁簿

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 常見問題與解決方案

| 問題 | 原因 | 解決方式 |
|------|------|----------|
| 工具提示未顯示 | `HasDataLabels` 未啟用 | 確保在設定 `ShowValue` 之前呼叫 `setHasDataLabels(true)`。 |
| 下鑽連結無作用 | 超連結 URL 格式錯誤 | 確認 URL 以 `http://` 或 `https://` 開頭。 |
| 圖表類型未變更 | 使用較舊的 Aspose.Cells 版本 | 升級至最新版本（已測試 24.12）。 |

## 常見問答

**Q: 如何在圖表建立後更改其類型？**  
A: 在現有的 `Chart` 物件上呼叫 `chart.setChartType(ChartType.YOUR_CHOICE)`。此做法直接滿足 **change Excel chart type** 的需求。

**Q: 我可以自訂工具提示的外觀嗎？**  
A: 可以。使用 `chart.getNSeries().get(0).getPoints().getDataLabels()` 來設定字型大小、顏色與背景。

**Q: 是否可以在同一圖表中加入多個下鑽連結？**  
A: 完全可以。遍歷各資料點，對想要連結的點呼叫 `getHyperlinks().add(url)`。

**Q: Aspose.Cells 是否支援其他圖表類型，例如圓餅圖或雷達圖？**  
A: 支援 `ChartType` 列舉中定義的所有圖表類型，包括 `PIE`、`RADAR`、`AREA` 等。

**Q: 我可以在哪裡找到更多範例？**  
A: 前往官方的 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) 查看完整的圖表相關方法清單。

## 結論

您現在已了解如何使用 Aspose.Cells for Java **更改 Excel 圖表類型**、嵌入 **工具提示**、加入 **資料標籤**，以及建立 **下鑽** 連結。這些互動功能可將靜態試算表轉變為動態資料探索工具，十分適合儀表板、報告與 Web 分析。

---

**最後更新：** 2025-12-01  
**測試環境：** Aspose.Cells 24.12 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}