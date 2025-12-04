---
date: 2025-12-04
description: 學習如何使用 Aspose.Cells 在 Java 中建立互動圖表、為圖表添加工具提示，並加入下鑽圖表，以實現更豐富的資料視覺化。
language: zh-hant
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells 在 Java 中建立互動圖表
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 建立互動式圖表 Java

## 介紹

互動式圖表讓使用者能夠探索資料點、在懸停時查看詳細資訊，甚至深入更深層的資料集——全部不必離開試算表。在本教學中，您將學習 **如何使用 Aspose.Cells 建立互動式圖表 Java** 應用程式。我們將逐步說明如何加入工具提示、資料標籤，以及實作下鑽（drill‑down）體驗，讓您的圖表更具吸引力與資訊性。

## 快速回答
- **使用哪個函式庫？** Aspose.Cells for Java  
- **可以為圖表加入工具提示嗎？** 可以，使用 NSeries 資料標籤 API  
- **支援下鑽功能嗎？** 可以，透過為資料點附加超連結實現  
- **產生的檔案格式為何？** 含嵌入圖表的標準 XLSX 活頁簿  
- **需要授權嗎？** 評估可使用免費試用版；正式上線需購買商業授權  

## 前置條件

在開始之前，請確保您已具備：

- Java 開發環境（建議 JDK 8 以上）  
- Aspose.Cells for Java 函式庫（可從官方 [Aspose 釋出頁面](https://releases.aspose.com/cells/java/) 下載）  
- 一個名為 **data.xlsx** 的範例 Excel 檔案，內含您想要視覺化的資料  

## 步驟 1：設定 Java 專案

1. 在您喜愛的 IDE（IntelliJ IDEA、Eclipse、VS Code 等）建立新 Java 專案。  
2. 將 Aspose.Cells JAR 加入專案的 classpath——可以將 JAR 放在 `libs` 資料夾，或是使用 Maven/Gradle 依賴方式。

## 步驟 2：載入資料

要建立互動式圖表，首先需要一個含資料的工作表。以下程式碼片段會開啟既有活頁簿並取得第一張工作表。

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **小技巧：** 確保您要繪製的資料範圍是連續的；Aspose.Cells 會在綁定序列時自動偵測範圍。

## 步驟 3：建立圖表

現在我們建立一個柱狀圖並將其放置於工作表上。若想使用其他圖表類型（例如 `ChartType.LINE`），只要將 `ChartType.COLUMN` 改成相應的列舉即可。

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **為何重要：** 以程式方式加入圖表可完整掌控其大小、位置與資料來源，這對打造互動體驗相當關鍵。

## 步驟 4：加入互動功能

### 如何為圖表加入工具提示

工具提示（或顯示數值的資料標籤）讓使用者能即時看到每根柱狀背後的精確數字。以下程式碼會啟用資料標籤並設定顯示數值。

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 如何加入資料標籤（呼叫框）

若希望標籤以呼叫框（callout）形式呈現，而非純文字，可切換 `ShowLabelAsDataCallout` 屬性。

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 如何加入下鑽圖表

下鑽讓使用者點擊資料點後跳轉至相關的詳細檢視——通常透過超連結實作。以下範例將 URL 附加到序列的第一個資料點。

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **常見陷阱：** 記得將超連結目標設定為能呈現詳細資料的頁面（例如網頁報表或另一張 Excel 工作表），否則點擊後會變成死鏈結。

## 步驟 5：儲存活頁簿

完成圖表設定後，將活頁簿寫入檔案。產生的檔案內含可在 Excel 或任何相容檢視器中開啟的互動式圖表。

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## 結論

本指南教會您 **如何使用 Aspose.Cells 建立互動式圖表 Java** 解決方案，涵蓋：

- 從既有活頁簿載入資料  
- 以程式方式建立柱狀圖  
- 加入工具提示與呼叫框資料標籤  
- 透過超連結實作下鑽功能  
- 儲存最終活頁簿  

這些技巧可將靜態試算表轉變為動態、使用者友善的儀表板，提升資料理解與決策效率。

## 常見問答

**Q: 如何變更圖表類型？**  
A: 在 `add` 方法中修改 `ChartType` 列舉（例如改成 `ChartType.LINE` 以建立折線圖）。

**Q: 可以自訂工具提示的外觀嗎？**  
A: 可以，透過 `DataLabels` 物件調整字型大小、顏色、背景等樣式屬性。

**Q: 如何在 Web 應用程式中處理圖表互動性？**  
A: 可將活頁簿匯出為 XLSX，然後使用 JavaScript 圖表函式庫（如 Highcharts）在客戶端渲染資料，或將 Excel 檔案嵌入支援超連結的 Office Web Viewer。

**Q: 哪裡可以找到更多範例？**  
A: 前往官方 [Aspose.Cells Java API 參考文件](https://reference.aspose.com/cells/java/) 查看完整的圖表相關類別與方法清單。

**Q: 正式上線需要授權嗎？**  
A: 需要，商業授權才能部署；測試階段可使用免費評估授權。

---

**最後更新：** 2025-12-04  
**測試環境：** Aspose.Cells for Java 24.12（撰寫時的最新版本）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}