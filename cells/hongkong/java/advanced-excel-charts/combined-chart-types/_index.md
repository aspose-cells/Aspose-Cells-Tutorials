---
date: 2025-12-06
description: 學習如何新增資料系列、建立組合圖表類型、將工作簿儲存為 Excel，並使用 Aspose.Cells for Java 將圖表匯出為 PNG。
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells 添加資料系列以建立組合圖表
url: /zh-hant/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.Cells 中加入資料序列以建立組合圖表

在本教學中，您將 **加入資料序列** 到 Excel 活頁簿，並學習如何使用 Aspose.Cells for Java **建立組合圖表** 類型。我們會逐步說明——從設定活頁簿、加入序列、客製化圖例，到 **儲存 Excel 活頁簿** 檔案以及匯出 **圖表為 PNG**。完成後，您將擁有一個可直接使用的組合圖表，能嵌入報告或儀表板中。

## 快速解答
- **哪個函式庫可建立組合圖表？** Aspose.Cells for Java  
- **如何加入資料序列？** 使用 `chart.getNSeries().add(...)`  
- **可以將圖表匯出為圖片嗎？** 可以，使用 `chart.toImage(...)`（PNG）  
- **活頁簿可以儲存為什麼檔案格式？** 標準 `.xlsx`（Excel）  
- **生產環境需要授權嗎？** 需要有效的 Aspose.Cells 授權  

## 在 Aspose.Cells 中什麼是 **add data series**
加入資料序列可告訴圖表哪些儲存格包含您想要繪製的數值。每個序列可以代表折線、柱狀或其他任何圖表類型，您亦可將它們混合，以建立 **combined chart**。

## 為什麼要建立 **combined chart**？
組合圖表可讓您在同一視圖中，以不同的視覺呈現方式（例如，折線序列疊加於柱狀序列上）顯示不同資料集。這非常適合比較趨勢與總量、突顯相關性，或在緊湊的版面中提供更豐富的洞見。

## 前置條件
- Java Development Kit (JDK) 8 或以上  
- Aspose.Cells for Java 函式庫（從以下連結下載）  
- 具備 Java 語法與 Excel 概念的基本知識  

## 開始使用

首先，從官方網站下載 Aspose.Cells for Java 函式庫：

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

將 JAR 加入專案的 classpath 後，即可開始建立圖表。

### 步驟 1：匯入 Aspose.Cells 類別
```java
import com.aspose.cells.*;
```

### 步驟 2：建立新的活頁簿
```java
Workbook workbook = new Workbook();
```

### 步驟 3：存取第一個工作表
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 步驟 4：新增組合圖表物件  
我們將先建立折線圖，之後再加入其他序列，以產生 **combined chart** 效果。
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 為圖表加入資料

既然圖表容器已建立，我們需要為其提供資料。

### 步驟 5：定義資料範圍並 **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **小技巧：** 第一個參數 (`"A1:A5"`) 為第一個序列的範圍，第二個參數 (`"B1:B5"`) 則建立第二個將與第一個合併的序列。

### 步驟 6：設定類別（X 軸）資料
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## 客製化圖表

好的圖表能說明故事。讓我們為它加上標題、軸標籤與清晰的圖例。

### 步驟 7：設定圖表標題與軸標籤
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### 步驟 8：**Add legend chart** 並調整其位置
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## 儲存與匯出圖表

客製化完成後，您會想要 **save workbook Excel** 並產生圖像。

### 步驟 9：將活頁簿儲存為 Excel 檔案
```java
workbook.save("CombinedChart.xlsx");
```

### 步驟 10：匯出 **chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 方法 **generates excel chart** 圖像，可用於網頁、報告或電子郵件。

## 常見問題與故障排除

| 問題 | 解決方案 |
|-------|----------|
| **沒有資料顯示** | 確認儲存格範圍 (`A1:A5`, `B1:B5`, `C1:C5`) 在建立圖表前確實包含資料。 |
| **圖例覆蓋圖表** | 設定 `chart.getLegend().setOverlay(false)`，或將圖例移至其他位置（例如 `RIGHT`）。 |
| **影像檔為空白** | 確保圖表至少有一個序列，且在完成所有客製化後才呼叫 `chart.toImage`。 |
| **儲存時拋出例外** | 檢查您是否對目標目錄具有寫入權限，且檔案未在 Excel 中開啟。 |

## 常見問答

**Q: 如何安裝 Aspose.Cells for Java？**  
A: 從官方網站下載 JAR 並加入專案的 classpath。下載連結為：[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).

**Q: 除了折線與柱狀，我可以建立其他圖表類型嗎？**  
A: 可以，Aspose.Cells 支援長條圖、圓餅圖、散佈圖、區域圖等多種圖表類型。請參考 API 文件取得完整清單。

**Q: 生產環境需要授權嗎？**  
A: 生產部署需要有效的 Aspose.Cells 授權。可使用免費試用版進行評估。

**Q: 如何變更每個序列的顏色？**  
A: 在加入序列後使用 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`（或類似方法）即可。

**Q: 在哪裡可以找到更多程式碼範例？**  
A: 完整文件與其他範例可於 Aspose 參考網站取得：[here](https://reference.aspose.com/cells/java/).

---

**最後更新：** 2025-12-06  
**測試於：** Aspose.Cells for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
