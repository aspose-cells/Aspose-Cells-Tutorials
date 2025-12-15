---
date: 2025-12-10
description: 學習如何使用 Aspose.Cells 在 Java 中建立瀑布圖。一步一步的指南，教您將圖表加入工作表、進行自訂，並將活頁簿儲存為 XLSX。
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: 如何使用 Aspose.Cells for Java 建立瀑布圖
url: /zh-hant/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 瀑布圖表

## 使用 Aspose.Cells for Java 介紹瀑布圖表

在本教學中，您將學習如何使用 Aspose.Cells for Java **建立瀑布圖表**。瀑布圖表是資料視覺化的重要工具，因為它能讓您看到一系列正負值的累積效果。無論您是在編製財務報表、銷售績效報告，或任何其他以資料為驅動的分析，瀑布圖表都能將原始數字轉化為清晰、可行的洞見。

## 快速回答
- **什麼是瀑布圖表？** 一種視覺化圖表，顯示初始值如何透過一系列中間值的增加與減少，最終得到總計。  
- **使用哪個函式庫？** Aspose.Cells for Java。  
- **我需要授權嗎？** 免費試用可用於開發；正式上線需購買商業授權。  
- **可以將檔案儲存為 XLSX 嗎？** 可以 – 使用 `workbook.save("FileName.xlsx")`。  
- **適合用於 Java 資料視覺化嗎？** 當然；Aspose.Cells 提供豐富的圖表功能，且不需要安裝 Office。

## 什麼是瀑布圖表？

瀑布圖表顯示對起始值的連續正向與負向貢獻，協助您了解每個組成部分如何影響最終結果。

## 為什麼使用 Aspose.Cells for Java 來新增瀑布圖表？

- **不需要 Microsoft Excel** – 可在任何伺服器或 CI 流程中產生圖表。  
- **完整的格式控制** – 顏色、資料標籤與座標軸皆可透過程式碼自訂。  
- **支援多種輸出格式** – 包括 XLSX、PDF、HTML 等。  
- **高效能** – 適用於大型活頁簿與自動化報表。

## 前置條件

在深入程式碼之前，請確保已具備以下前置條件：

- Aspose.Cells for Java：您需要安裝 Aspose.Cells for Java。可從 [here](https://releases.aspose.com/cells/java/) 下載。  
- Java 開發環境：請確認系統已安裝 Java。  

現在，讓我們一步一步開始建立瀑布圖表。

## 如何在 Java 中建立瀑布圖表

### 步驟 1：匯入 Aspose.Cells

```java
import com.aspose.cells.*;
```

首先，您需要將 Aspose.Cells 函式庫匯入 Java 專案。此函式庫提供廣泛的 Excel 檔案操作功能，包含圖表建立。

### 步驟 2：初始化 Workbook 與 Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

建立一個新的 Workbook，並在其中新增 Worksheet。我們將使用此工作表輸入資料，並 **將圖表加入工作表**。

### 步驟 3：輸入資料

現在，讓我們在工作表中填入欲在瀑布圖表中呈現的資料。

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

在此範例中，我們在 A 欄放置類別，B 欄放置相對應的數值。您可以自行替換為自己的資料集。

### 步驟 4：建立瀑布圖表

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

我們已在工作表中加入瀑布圖表，並指定資料系列與類別資料。這是 **將瀑布圖表加入工作表** 的核心步驟。您可使用 `Chart` 物件的屬性進一步自訂圖表外觀（顏色、資料標籤等）。

### 步驟 5：儲存 Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

將 Workbook 儲存為檔案。範例使用 XLSX 格式，但 Aspose.Cells 亦支援匯出為 PDF、CSV 等多種格式。這符合 **save workbook xlsx** 的需求。

## 常見問題與解決方案

- **圖表顯示空白** – 請確認資料範圍參照 (`B2:B6` 與 `A2:A6`) 與實際包含數值與類別的儲存格相符。  
- **負值未正確顯示** – 請確保系列類型設定為 `ChartType.WATERFALL`；其他圖表類型會以不同方式處理負值。  
- **檔案無法在 Excel 開啟** – 請確認使用的是最新版本的 Aspose.Cells（最新發行版），且檔案副檔名與格式相符（Excel 使用 `.xlsx`）。

## 常見問答

### 如何自訂我的瀑布圖表外觀？

您可以透過修改顏色、資料標籤與座標軸標籤等屬性，自訂瀑布圖表的外觀。請參考 Aspose.Cells 文件以取得詳細說明。

### 我可以在同一工作表中建立多個瀑布圖表嗎？

可以，您只要對範圍重複相同步驟，即可在同一工作表中建立多個瀑布圖表。

### Aspose.Cells 是否相容於不同的 Java 開發環境？

是的，Aspose.Cells for Java 相容於多種 Java 開發環境，包括 Eclipse、IntelliJ IDEA 與 NetBeans。

### 我可以為我的瀑布圖表加入額外的資料系列嗎？

當然，您可以加入更多資料系列，以有效呈現複雜的資料情境。

### 我可以在哪裡找到更多 Aspose.Cells for Java 的資源與範例？

您可前往 [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) 探索 Aspose.Cells for Java 的文件，取得深入資訊與程式碼範例。

---

**最後更新：** 2025-12-10  
**測試環境：** Aspose.Cells for Java 24.12（最新）  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}