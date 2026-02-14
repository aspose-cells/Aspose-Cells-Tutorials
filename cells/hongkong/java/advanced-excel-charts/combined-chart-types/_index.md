---
date: 2026-02-14
description: 學習如何使用 Aspose.Cells for Java 將圖表匯出為 PNG、添加資料系列、結合折線與柱狀圖、將活頁簿另存為 XLSX，並為圖表添加圖例。
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: 匯出圖表為 PNG 並為合併圖表新增資料系列
url: /zh-hant/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 匯出圖表為 PNG 並為組合圖表新增資料系列

在本教學中，您將 **新增資料系列** 到 Excel 活頁簿，**結合折線圖與柱狀圖** 元素，並學習如何使用 Aspose.Cells for Java **匯出圖表為 PNG**。我們將逐步說明每個步驟——從設定活頁簿、將圖表加入工作表、客製化圖例，到 **將活頁簿另存為 xlsx** 並產生圖表的 PNG 圖片。完成後，您將擁有一個可直接使用的組合圖表，可嵌入報告或儀表板中。

## 快速解答
- **哪個函式庫可建立組合圖表？** Aspose.Cells for Java  
- **如何新增資料系列？** 使用 `chart.getNSeries().add(...)`  
- **如何將圖表匯出為 png？** 呼叫 `chart.toImage("file.png", ImageFormat.getPng())`  
- **活頁簿可以儲存為什麼檔案格式？** 標準 `.xlsx`（save workbook as xlsx）  
- **生產環境是否需要授權？** 需要有效的 Aspose.Cells 授權  

## 什麼是 Aspose.Cells 中的 **export chart to PNG**？
將圖表匯出為 PNG 會產生 Excel 圖表的點陣圖像，可在網頁、報告或電子郵件中顯示，且不需要 Excel 應用程式。

## 為什麼要建立 **combined line column chart**？
組合圖表讓您在同一視圖中以不同的視覺呈現方式（例如折線系列疊加於柱狀系列）顯示不同資料集。這非常適合比較趨勢與總量、突顯相關性，或在緊湊的版面中提供更豐富的洞見。

## 前置條件
- Java Development Kit (JDK) 8 或以上  
- Aspose.Cells for Java 函式庫（從以下連結下載）  
- 具備 Java 語法與 Excel 概念的基本熟悉度  

## 開始使用

首先，從官方網站下載 Aspose.Cells for Java 函式庫：

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

將 JAR 加入專案的 classpath 後，即可開始建立圖表。

### 步驟 1：匯入 Aspose.Cells 類別
```java
import com.aspose.cells.*;
```

### 步驟 2：建立新活頁簿
```java
Workbook workbook = new Workbook();
```

### 步驟 3：存取第一個工作表
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 步驟 4：在工作表中新增組合圖表物件  
我們將先建立折線圖，之後再加入柱狀系列，以實現 **combined line column chart** 效果。
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## 為圖表新增資料

既然圖表容器已建立，我們需要為其提供資料。

### 步驟 5：定義資料範圍並 **add data series**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **小技巧：** 第一個參數 (`"A1:A5"`) 為第一個系列的範圍，第二個參數 (`"B1:B5"`) 會建立第二個系列，將與第一個系列結合。

### 步驟 6：設定類別（X 軸）資料
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## 客製化圖表

好的圖表能說故事。讓我們為它加入標題、軸標籤與清晰的圖例。

### 步驟 7：**Set chart axis labels** 與標題
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

客製化完成後，您會想要 **save workbook as xlsx** 並產生圖像。

### 步驟 9：將活頁簿儲存為 Excel 檔案（xlsx）
```java
workbook.save("CombinedChart.xlsx");
```

### 步驟 10：**Export chart to PNG**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` 方法 **產生 Excel 圖表** 圖像，可用於網頁、報告或電子郵件。

## 常見問題與故障排除

| 問題 | 解決方案 |
|-------|----------|
| **沒有資料顯示** | 確認儲存格範圍 (`A1:A5`, `B1:B5`, `C1:C5`) 在建立圖表前確實包含資料。 |
| **圖例覆蓋圖表** | 設定 `chart.getLegend().setOverlay(false)`，或將圖例移至其他位置（例如 `RIGHT`）。 |
| **影像檔案為空白** | 確保圖表至少有一個系列，且在完成所有客製化後才呼叫 `chart.toImage`。 |
| **儲存時拋出例外** | 檢查您對目標目錄是否有寫入權限，且檔案未在 Excel 中開啟。 |

## 常見問答

**問：如何安裝 Aspose.Cells for Java？**  
**答：** 從官方網站下載 JAR，並將其加入專案的 classpath。下載連結為：[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

**問：除了折線圖和柱狀圖，我可以建立其他類型的圖表嗎？**  
**答：** 可以，Aspose.Cells 支援長條圖、圓餅圖、散佈圖、區域圖等多種圖表類型。請參閱 API 文件取得完整清單。

**問：生產環境是否需要授權？**  
**答：** 在生產部署時需要有效的 Aspose.Cells 授權。可使用免費試用版進行評估。

**問：如何變更每個系列的顏色？**  
**答：** 在新增系列後，使用 `chart.getNSeries().get(i).setAreaColor(Color.getRed())`（或類似方法）設定顏色。

**問：在哪裡可以找到更多程式碼範例？**  
**答：** 完整文件與其他範例可於 Aspose 參考網站取得：[here](https://reference.aspose.com/cells/java/)

---

**最後更新：** 2026-02-14  
**測試環境：** Aspose.Cells for Java 最新版本  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}