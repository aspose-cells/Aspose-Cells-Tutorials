---
date: 2026-02-16
description: 學習如何在 Java 中使用 Aspose.Cells 設定圖表資料範圍並建立瀑布圖。一步一步的指南，教您新增資料系列圖表、客製化圖表，並匯出為
  XLSX。
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: 設定圖表資料範圍 – Aspose.Cells for Java 瀑布圖
url: /zh-hant/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 瀑布圖表

## 使用 Aspose.Cells for Java 的瀑布圖表簡介

在本教學中，您將學習如何使用 Aspose.Cells for Java **設定圖表資料範圍** 並建立 **瀑布圖表**。瀑布圖表是資料視覺化的重要工具，因為它能讓您看到一系列正負值的累積效果。無論您是要編製財務報表、銷售績效報告，或任何其他以資料為驅動的分析，瀑布圖表都能將原始數字轉化為清晰、可行的洞見。

## 快速答案
- **What is a waterfall chart?** 什麼是瀑布圖表？ 一種視覺化方式，顯示初始值如何透過一系列中間值的增加與減少，最終得到總計。  
- **Which library is used?** 使用哪個函式庫？ Aspose.Cells for Java。  
- **Do I need a license?** 我需要授權嗎？ 免費試用可用於開發；正式環境需購買商業授權。  
- **Can I save the file as XLSX?** 我可以將檔案儲存為 XLSX 嗎？ 可以 – 使用 `workbook.save("FileName.xlsx")`。  
- **Is it suitable for Java data visualization?** 它適合用於 Java 資料視覺化嗎？ 絕對適合；Aspose.Cells 提供豐富的圖表功能，且不需安裝 Office。

## 什麼是瀑布圖表？

瀑布圖表顯示對起始值的連續正向與負向貢獻，協助您了解每個組成部分如何影響最終結果。

## 為什麼使用 Aspose.Cells for Java 來新增瀑布圖表？

- **No Microsoft Excel required** – 不需要 Microsoft Excel – 可在任何伺服器或 CI 流程中產生圖表。  
- **Full control over formatting** – 完全掌控格式設定 – 顏色、資料標籤與座標軸皆可透過程式碼自訂。  
- **Supports multiple output formats** – 支援多種輸出格式 – XLSX、PDF、HTML 等。  
- **High performance** – 高效能 – 適用於大型活頁簿與自動化報告。

## 先決條件

在深入程式碼之前，請確保已具備以下先決條件：

- Aspose.Cells for Java: 您需要安裝 Aspose.Cells for Java。可從 [此處](https://releases.aspose.com/cells/java/) 下載。

- Java 開發環境：確保系統已安裝 Java。

現在，讓我們一步一步開始建立瀑布圖表。

## 如何在 Java 中設定瀑布圖表的圖表資料範圍

### 步驟 1：匯入 Aspose.Cells

```java
import com.aspose.cells.*;
```

首先，您需要將 Aspose.Cells 函式庫匯入您的 Java 專案。此函式庫提供廣泛的功能，以處理 Excel 檔案，包括圖表建立。

### 步驟 2：初始化 Workbook 與 Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

建立一個新的 workbook 並新增一個 worksheet。我们將使用此 worksheet 輸入資料並 **add chart to worksheet**。

### 步驟 3：輸入資料

現在，讓我們將要在瀑布圖表中呈現的資料填入 worksheet。

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

在此範例中，我們在 A 欄有類別，B 欄有相對應的數值。您可以將此資料替換為自己的資料集。

### 步驟 4：建立瀑布圖表

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

我們已在 worksheet 中加入瀑布圖表，並指定資料系列與類別資料。這是 **adds waterfall chart** 到工作表的核心步驟。請注意 `add` 方法使用的範圍 "B2:B6" – 這就是我們為系列 **set chart data range** 的位置。您可以使用 `Chart` 物件的屬性進一步自訂圖表外觀（顏色、資料標籤等）。

### 步驟 5：儲存 Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

將 workbook 儲存為檔案。此範例使用 XLSX 格式，但 Aspose.Cells 亦允許您 **export excel pdf java** 相容的檔案，例如 PDF、CSV 以及其他多種格式。這符合 **save workbook xlsx** 的需求。

## 常見問題與解決方案

- **Chart appears blank** – 確認資料範圍參照 (`B2:B6` 與 `A2:A6`) 與實際包含數值與類別的儲存格相符。  
- **Negative values not displayed correctly** – 確保系列類型設定為 `ChartType.WATERFALL`；其他圖表類型會以不同方式處理負值。  
- **File not opening in Excel** – 確認您使用的是最新版本的 Aspose.Cells（最新發行版），且檔案副檔名與格式相符（Excel 使用 `.xlsx`）。

## 常見問題

### 如何自訂我的瀑布圖表外觀？

您可以透過修改顏色、資料標籤與座標軸標籤等屬性來自訂瀑布圖表的外觀。請參考 Aspose.Cells 文件以取得詳細說明。

### 我可以在同一個 worksheet 中建立多個瀑布圖表嗎？

可以，您只要使用不同的資料範圍，依照相同步驟即可在同一 worksheet 中建立多個瀑布圖表。

### Aspose.Cells 是否相容於不同的 Java 開發環境？

是的，Aspose.Cells for Java 相容於多種 Java 開發環境，包括 Eclipse、IntelliJ IDEA 與 NetBeans。

### 我可以為我的瀑布圖表加入額外的資料系列嗎？

當然可以，您可以為瀑布圖表加入更多資料系列，以有效呈現複雜的資料情境。以下示範如何以程式方式 **add data series chart**。

### 哪裡可以找到更多 Aspose.Cells for Java 的資源與範例？

您可於 [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) 探索 Aspose.Cells for Java 的文件，取得深入資訊與程式碼範例。

## 常見問答

**Q: 如何為財務瀑布圖表設定圖表資料範圍？**  
A: 使用圖表系列的 `add` 方法，傳入包含數值的儲存格範圍，例如 `"B2:B6"`。

**Q: 我可以將 workbook 匯出為 PDF 而非 XLSX 嗎？**  
A: 可以，呼叫 `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` 以產生 **export excel pdf java** 相容的輸出。

**Q: 若需建立具有更多類別的財務瀑布圖表該怎麼辦？**  
A: 同時擴展數值欄與類別欄的資料範圍，然後相應更新 `add` 與 `setCategoryData` 的呼叫。

**Q: 有沒有方法自動格式化正負柱狀？**  
A: 您可以遍歷 `Series` 集合，根據每個數值的正負設定 `FillFormat` 顏色。

**Q: Aspose.Cells 是否支援圖表的動態資料更新？**  
A: 支援，您可以在圖表建立後修改儲存格數值；儲存 workbook 時圖表會反映變更。

---

**最後更新：** 2026-02-16  
**測試環境：** Aspose.Cells for Java（最新）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}