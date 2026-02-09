---
date: 2026-02-09
description: 學習如何使用 Aspose.Cells for Java 為 Excel 圖表添加資料標籤、變更圖表類型，以及加入工具提示與下鑽互動功能。
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells Java 為 Excel 圖表新增資料標籤
url: /zh-hant/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 為 Excel 圖表新增資料標籤並變更圖表類型 – Aspose.Cells Java

互動圖表為您的 Excel 報表帶來全新層次的洞見，**在 Excel 圖表中新增資料標籤** 能讓資訊即時可讀。於本教學中，您將學會 **在 Excel 圖表中新增資料標籤**、變更圖表類型，並使用 Aspose.Cells 建立互動式 Java 解決方案。我們亦會示範如何加入工具提示以及簡易的下鑽超連結，讓讀者能深入探索資料。

## 快速解答
- **使用哪個函式庫？** Aspose.Cells for Java  
- **可以變更圖表類型嗎？** 可以 – 只要在建立圖表時修改 `ChartType` 列舉即可。  
- **如何為圖表加入工具提示？** 使用資料標籤 API (`setHasDataLabels(true)`) 並啟用顯示數值。  
- **支援下鑽功能嗎？** 您可以為資料點附加超連結，以實現基本的下鑽行為。  
- **前置條件？** Java IDE、Aspose.Cells JAR，以及含有範例資料的 Excel 檔案。

## 前置條件

在開始之前，請確保您已具備以下項目：

- Java 開發環境（建議 JDK 8 以上）  
- Aspose.Cells for Java 函式庫（可從 [here](https://releases.aspose.com/cells/java/) 下載）  
- 包含欲視覺化資料的範例活頁簿（`data.xlsx`）

## 第一步：設定 Java 專案

1. 在您喜愛的 IDE（IntelliJ IDEA、Eclipse 等）中建立新 Java 專案。  
2. 將 Aspose.Cells JAR 加入專案的建置路徑或 Maven/Gradle 相依性中。

## 第二步：載入資料

要操作圖表，首先需要將活頁簿載入記憶體。

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 第三步：建立圖表（並變更其類型）

您可以選擇任何符合分析需求的圖表類型。以下範例建立 **直條圖**，但只要更改 `ChartType` 列舉，即可輕鬆切換為折線圖、圓餅圖或長條圖。

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **專業提示：** 若要 **變更 Excel 圖表類型**，請將 `ChartType.COLUMN` 替換為 `ChartType.LINE`、`ChartType.PIE` 等。

## 第四步：加入互動功能

### 4.1. 加入工具提示（Add Tooltips to Chart）

當使用者將滑鼠懸停於資料點時會顯示工具提示。以下程式碼啟用資料標籤並將數值作為工具提示顯示。

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. 加入資料標籤 – **add data labels to excel chart**

資料標籤在圖表本身提供永久的視覺提示。您可以將其顯示為標註，以提升可讀性。

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **為何要加入資料標籤？** 直接在圖表上顯示資料標籤，可免除使用者必須懸停或猜測數值的需求，提升報表的清晰度。

### 4.3. 實作下鑽（資料點上的超連結）

加入下鑽功能的簡易方式是為特定資料點附加超連結。點擊該點即會開啟包含詳細資訊的網頁。

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## 第五步：儲存活頁簿

完成圖表設定後，將活頁簿寫入檔案，以確保互動功能被儲存於輸出檔案中。

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 常見問題與解決方案

| 問題 | 解決方案 |
|------|----------|
| **工具提示未顯示** | 確認在設定 `setShowValue(true)` 之前已呼叫 `setHasDataLabels(true)`。 |
| **超連結無法點擊** | 檢查輸出格式是否支援超連結（例如 XLSX，而非 CSV）。 |
| **圖表類型未變更** | 再次確認在新增圖表時已修改正確的 `ChartType` 列舉。 |

## 常見問答

**Q: 如何在圖表建立後變更圖表類型？**  
A: 必須以目標 `ChartType` 重新建立新圖表。Aspose.Cells 不提供即時類型轉換，請先移除舊圖表再新增新圖表。

**Q: 可以自訂工具提示的外觀嗎？**  
A: 可以。使用 `DataLabel` 的屬性，如 `setFontSize`、`setFontColor`、`setBackgroundColor` 來樣式化工具提示文字。

**Q: 在 Web 應用程式中如何處理使用者互動？**  
A: 將活頁簿匯出為 HTML 或 XLSX，並在客戶端使用 JavaScript 捕捉圖表元素的點擊事件。

**Q: 哪裡可以找到更多範例與文件？**  
A: 前往 [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) 查看完整的圖表相關類別與方法清單。

## 結論

現在您已掌握 **在 Excel 圖表中新增資料標籤**、**變更 Excel 圖表類型**、**使用 Java 建立互動圖表** 的技巧，並能透過 Aspose.Cells for Java 為圖表加入工具提示、資料標籤與下鑽超連結。這些強化功能可讓您的 Excel 報表對最終使用者更具吸引力與洞見。

---

**最後更新：** 2026-02-09  
**測試環境：** Aspose.Cells for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}