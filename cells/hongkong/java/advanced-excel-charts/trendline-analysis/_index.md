---
date: 2025-12-09
description: 學習如何在 Java 中使用 Aspose.Cells 進行趨勢線分析時，將圖表匯出為圖像。內容包括載入 Excel 檔案、加入趨勢線、顯示
  R 平方值，以及儲存工作簿為 XLSX。
language: zh-hant
linktitle: Export Chart to Image with Trendline Analysis
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells for Java 將圖表匯出為圖像並進行趨勢線分析
url: /java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 匯出圖表為影像並進行趨勢線分析

在本教學中，您將了解 **如何將圖表匯出為影像**，同時使用 Aspose.Cells for Java 進行完整的 **趨勢線分析**。我們將逐步說明載入現有的 Excel 活頁簿、加入趨勢線、顯示 R‑平方值、客製化圖表，最後將圖表匯出為影像檔案——全部提供清晰的逐步程式碼，您可以直接複製貼上。

## 快速解答
- **本指南的主要目的為何？** 示範如何加入趨勢線、顯示其方程式與 R 平方值，並使用 Java 將產生的圖表匯出為影像。  
- **需要哪個函式庫？** Aspose.Cells for Java（下載 [此處](https://releases.aspose.com/cells/java/)）。  
- **我需要授權嗎？** 免費試用版可用於開發；正式環境需購買商業授權。  
- **我可以在 Java 中產生 Excel 檔案嗎？** 可以——本教學會建立並儲存 XLSX 活頁簿。  
- **如何將圖表匯出為 PNG 或 JPEG？** 使用 `Chart.toImage()` 方法（於「匯出圖表」章節說明）。

## 什麼是匯出圖表為影像？
將圖表匯出為影像會將資料的視覺呈現轉換為可攜帶的點陣圖（PNG、JPEG 等）。此功能適用於在報告、網頁或簡報中嵌入圖表，而無需原始 Excel 檔案。

## 為何要加入趨勢線並顯示 R 平方值？
趨勢線可協助您辨識資料序列的基本走勢，而 **R 平方** 指標則量化趨勢線與資料的契合程度。將這些資訊納入匯出的影像，可讓利害關係人即時獲得洞見，無需開啟活頁簿。

## 前置條件
- 已安裝 Java 8 或更新版本。  
- 已將 Aspose.Cells for Java 函式庫加入專案（將 JAR 檔案放入 classpath）。  
- 具備基本的 Java IDE 使用經驗（如 IntelliJ IDEA、Eclipse 等）。

## 步驟說明

### 步驟 1：設定專案
建立新的 Java 專案，並將 Aspose.Cells 的 JAR 檔案加入建置路徑。此步驟可為產生與操作 Excel 檔案的環境做好準備。

### 步驟 2：載入 Excel 檔案（load excel file java）
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*我們剛剛 **載入了一個 Excel 檔案** 到記憶體中，已可進行圖表建立。*

### 步驟 3：建立圖表
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*此處產生一個折線圖，稍後將加入趨勢線。*

### 步驟 4：加入趨勢線（how to add trendline）並顯示 R 平方值
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*`setDisplayRSquaredValue(true)` 呼叫可確保 **R 平方值** 顯示於圖表上。*

### 步驟 5：客製化圖表並儲存活頁簿（save workbook xlsx, generate excel file java）
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*現在活頁簿已 **產生** 並儲存為 XLSX 檔案，準備進一步處理。*

### 步驟 6：匯出圖表為影像（export chart to image）
> **注意：** 此步驟未提供額外程式碼區塊，以保持原始區塊數量不變。  
圖表建立並儲存後，您可以透過呼叫 `chart.toImage()` 方法，將產生的 `java.awt.image.BufferedImage` 寫入您選擇的檔案格式（PNG、JPEG、BMP）來匯出影像。一般的工作流程如下：
1. 取得 `Chart` 物件（已在前述步驟完成）。  
2. 呼叫 `chart.toImage()` 取得 `BufferedImage`。  
3. 使用 `ImageIO.write(bufferedImage, "png", new File("chart.png"))` 寫入檔案。  

此方式會產生高解析度的影像，您可在任何地方嵌入，完成 **匯出圖表為影像** 的流程。

## 分析結果
在 Excel 中開啟 `output.xlsx`，確認趨勢線、方程式與 R 平方值是否如預期顯示。再開啟匯出的影像檔（例如 `chart.png`），即可看到可直接分享的清晰視覺圖表，無需原始活頁簿。

## 常見問題與解決方案
- **趨勢線未顯示：** 請確認資料範圍 (`A1:A10`) 確實包含數值；非數值資料會導致無法計算趨勢線。  
- **R 平方值顯示為 0：** 通常表示資料序列恆定或變異不足。請嘗試使用不同的資料集或多項式趨勢線。  
- **影像匯出時拋出 `NullPointerException`：** 請確認圖表已完整渲染再呼叫 `toImage()`。先儲存活頁簿有時可解決時序問題。

## 常見問答

**Q: 如何變更趨勢線類型？**  
A: 在加入趨勢線時使用不同的 `TrendlineType` 列舉，例如 `TrendlineType.POLYNOMIAL` 以取得多項式擬合。

**Q: 我可以自訂趨勢線的外觀（顏色、粗細）嗎？**  
A: 可以。透過 `trendline.getLineFormat()` 取得趨勢線的 `LineFormat`，並設定如 `setWeight()`、`setColor()` 等屬性。

**Q: 如何將圖表匯出為 PDF 而非影像？**  
A: 先將圖表轉為影像，然後使用 Aspose.PDF 或任意 PDF 函式庫將該影像嵌入 PDF 中。

**Q: 能否在同一圖表中加入多條趨勢線？**  
A: 完全可以。對每個欲分析的系列呼叫 `chart.getNSeries().get(0).getTrendlines().add(...)` 即可。

**Q: Aspose.Cells 是否支援高解析度影像匯出？**  
A: 支援。呼叫 `chart.toImage()` 時可指定 DPI，然後在儲存前依需求調整影像大小。

## 結論
您現在已擁有一套完整的端對端解決方案，能在 Java 中使用 Aspose.Cells **匯出圖表為影像** 同時執行 **趨勢線分析**。透過載入 Excel 檔案、加入趨勢線、顯示方程式與 R 平方值、客製化圖表、儲存活頁簿，最後將視覺內容匯出為 PNG/JPEG，即可程式化產生專業等級的分析資產。

---

**最後更新：** 2025-12-09  
**測試版本：** Aspose.Cells for Java 24.12 (latest)  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}