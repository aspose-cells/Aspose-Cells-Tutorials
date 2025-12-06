---
date: 2025-12-06
description: 學習如何使用 Aspose.Cells 於 Java 中變更 Excel 圖表類型並建立互動圖表。為圖表新增工具提示、資料標籤及下鑽功能，以實現更豐富的資料視覺化。
language: zh-hant
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells Java 更改 Excel 圖表類型
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 更改 Excel 圖表類型並加入互動功能

## 介紹

互動圖表為您的 Excel 報表帶來全新層次的洞察，讓使用者可以滑過、點擊，直接探索資料點。在本教學中，您將 **更改 Excel 圖表類型**，並使用 Aspose.Cells for Java 建立 **互動圖表 Java** 解決方案。我們將示範如何為圖表加入工具提示、資料標籤，以及簡易的下鑽超連結，讓讀者能更深入了解數據。

## 快速解答
- **使用的函式庫是什麼？** Aspose.Cells for Java  
- **我可以變更圖表類型嗎？** 可以 – 只要在建立圖表時修改 `ChartType` 列舉即可。  
- **如何為圖表加入工具提示？** 使用資料標籤 API（`setHasDataLabels(true)`）並啟用顯示值。  
- **支援下鑽功能嗎？** 您可以為資料點附加超連結，以實作基本的下鑽行為。  
- **前置條件？** Java IDE、Aspose.Cells JAR，以及一個含範例資料的 Excel 檔案。

## 前置條件

在開始之前，請確保您已具備以下項目：

- Java 開發環境（建議使用 JDK 8 以上）  
- Aspose.Cells for Java 函式庫（從 [here](https://releases.aspose.com/cells/java/) 下載）  
- 一個包含欲視覺化資料的範例活頁簿（`data.xlsx`）  

## 步驟 1：設定 Java 專案

1. 在您喜愛的 IDE（IntelliJ IDEA、Eclipse 等）中建立新 Java 專案。  
2. 將 Aspose.Cells JAR 加入專案的建置路徑，或於 Maven/Gradle 相依性中加入。

## 步驟 2：載入資料

要操作圖表，首先必須將活頁簿載入記憶體。

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 步驟 3：建立圖表（並變更其類型）

您可以選擇任何符合分析需求的圖表類型。以下範例建立 **直條圖**，但只要更改 `ChartType` 列舉，即可輕鬆切換為折線圖、圓餅圖或長條圖。

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **專業提示：** 若要 **更改 Excel 圖表類型**，請將 `ChartType.COLUMN` 替換為 `ChartType.LINE`、`ChartType.PIE` 等。

## 步驟 4：加入互動功能

### 4.1. 加入工具提示（Add Tooltips to Chart）

工具提示會在使用者滑過資料點時顯示。以下程式碼啟用資料標籤並將值作為工具提示顯示。

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. 加入資料標籤

資料標籤在圖表本身提供永久的視覺提示。您可以將其顯示為呼叫框，以提升可讀性。

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. 實作下鑽（Hyperlink on a Data Point）

為特定資料點附加超連結，即可實作簡易的下鑽功能。點擊該點會開啟包含詳細資訊的網頁。

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 步驟 5：儲存活頁簿

完成圖表設定後，將活頁簿儲存，以確保互動功能寫入輸出檔案。

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **工具提示未顯示** | 確認在設定 `setShowValue(true)` 前已呼叫 `setHasDataLabels(true)`。 |
| **超連結無法點擊** | 檢查輸出格式是否支援超連結（例如 XLSX，而非 CSV）。 |
| **圖表類型未變更** | 再次確認在新增圖表時已修改正確的 `ChartType` 列舉。 |

## 常見問答

**問：建立後如何變更圖表類型？**  
答：必須以目標 `ChartType` 重新建立圖表。Aspose.Cells 不提供即時類型轉換，請先移除舊圖表，再新增新圖表。

**問：我可以自訂工具提示的外觀嗎？**  
答：可以。使用 `DataLabel` 的屬性，如 `setFontSize`、`setFontColor`、`setBackgroundColor` 來樣式化工具提示文字。

**問：如何在 Web 應用程式中處理使用者互動？**  
答：將活頁簿匯出為 HTML 或 XLSX，並在客戶端使用 JavaScript 捕捉圖表元素的點擊事件。

**問：在哪裡可以找到更多範例與文件？**  
答：請造訪 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) 取得完整的圖表相關類別與方法清單。

## 結論

現在您已了解如何 **更改 Excel 圖表類型**、**建立互動圖表 Java** 解決方案，並使用 Aspose.Cells for Java 為圖表加入工具提示、資料標籤與下鑽超連結。這些強化功能能讓您的 Excel 報表對最終使用者更具吸引力與洞察力。

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.Cells for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}