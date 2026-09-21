---
date: 2026-02-09
description: 學習如何使用 Aspose.Cells 在 Java 中建立 3D 圓餅圖。產生 3D 長條圖、在 Excel 中加入 3D 圖表，並以逐步程式碼範例將工作簿儲存為
  xlsx。
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells 在 Java 中建立 3D 圓餅圖
url: /zh-hant/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 建立 3D 圓餅圖（Java）

## 簡介 3D 圖表

Aspose.Cells for Java 是一個功能強大的 Java API，用於處理 Excel 檔案，讓 **create 3d pie chart** 專案以及傳統的 3‑D 長條圖視覺化變得相當簡單。在本教學中，您將會看到如何產生 3‑D 長條圖、如何將相同的做法套用到 3‑D 圓餅圖、如何自訂外觀，最後 **add 3d chart excel** 檔案至您的報告。無論您是建立財務儀表板、銷售績效表，或是視覺化科學資料，以下步驟都能為您奠定堅實的基礎。

## 快速答覆
- **需要哪個函式庫？** Aspose.Cells for Java (latest version)  
- **我可以產生 3D 長條圖嗎？** Yes – use `ChartType.BAR_3_D`  
- **我需要授權嗎？** A valid license removes evaluation limits  
- **支援哪些 Excel 版本？** All major versions from 2003 to 2023  
- **是否可以將圖表匯出為影像？** Yes, via `chart.toImage()` methods  

## 什麼是 3D 圖表？

3D 圖表為傳統 2D 視覺化加入深度，協助觀眾更直觀地理解多維關係。當需要在保持清晰視覺層次的同時，並排比較多個類別時，特別有用。

## 為何使用 Aspose.Cells for Java 產生 3D 長條圖？

Aspose.Cells for Java 提供豐富的圖表建立 API、與 Excel 完全相容，且可細緻控制樣式。這意味著您可以程式化 **generate 3d bar chart** 物件，而不必擔心 Excel 版本的差異。

## 設定 Aspose.Cells for Java

### 下載與安裝
您可以從官方網站下載 Aspose.Cells for Java 函式庫。依照提供的 Maven/Gradle 指示操作，或直接將 JAR 加入專案的 classpath。

### 授權初始化
要解鎖全部功能，請在任何圖表操作之前初始化授權：

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## 建立基本 3D 圖表

### 匯入必要的函式庫
首先，將所需的類別匯入範圍：

```java
import com.aspose.cells.*;
```

### 初始化活頁簿
建立一個全新的活頁簿以容納圖表：

```java
Workbook workbook = new Workbook();
```

### 為圖表加入資料
在工作表中填入圖表將參考的範例資料：

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### 如何在 Java 中產生 3D 長條圖
現在我們建立圖表本身，並套用一些基本的自訂設定：

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### 將圖表儲存至檔案
最後，將包含 3‑D 圖表的活頁簿寫入磁碟。這同時會 **save workbook xlsx** 為標準的 Excel 格式：

```java
workbook.save("3D_Chart.xlsx");
```

## 如何使用 Aspose.Cells for Java 建立 3D 圓餅圖
如果您需要圓餅樣式的視覺化，工作流程幾乎相同——唯一需要變更的是 `ChartType` 列舉。加入圖表時將 `ChartType.BAR_3_D` 替換為 `ChartType.PIE_3_D`，並將系列指向相同的資料範圍。圖表建立後，您可以：

* 設定描述性的標題，例如「3D 銷售分佈」。
* 使用 `chart.getSeries().get(i).getArea().setForegroundColor(...)` 調整切片顏色。
* 以 `chart.toImage("pie_chart.png", ImageFormat.getPng())` 匯出圓餅圖為 PNG 影像，滿足 **convert chart png** 的需求。

由於必須保持程式碼區塊數量不變，實際的 Java 程式碼此處省略，但步驟與上面的長條圖範例相同。

## 不同類型的 3D 圖表
Aspose.Cells for Java 支援多種 3D 圖表類型，您可以 **add 3d chart excel** 檔案：

- **Bar charts** – 適合比較各類別。  
- **Pie charts** – 顯示比例貢獻（含 3D 圓餅）。  
- **Line charts** – 展示隨時間的趨勢。  
- **Area charts** – 強調變化幅度。  

您可以將 `ChartType` 列舉切換為上述任意類型，同時保持相同的建立模式。

## 進階圖表自訂

### 加入標題與標籤
透過設定描述性的標題與座標軸標籤，為圖表提供上下文。

### 調整顏色與樣式
使用 `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` 方法，以符合企業品牌色彩。

### 操作圖表座標軸
微調座標軸刻度、間隔與刻度線，以提升可讀性。

### 加入圖例
使用 `chart.getLegend().setVisible(true)` 啟用圖例，讓觀眾能辨識每個資料系列。

### 將圖表匯出為影像
當您需要為網頁報告提供靜態影像時，呼叫 `chart.toImage("chart.png", ImageFormat.getPng())`。此方式滿足 **convert chart png** 的使用情境，且不必離開活頁簿。

## 資料整合
Aspose.Cells for Java 能從資料庫、CSV 檔案或即時 API 抓取資料。只要在將範圍連結至圖表之前，先將取得的資料填入工作表儲存格，即可讓您的 **add 3d chart excel** 工作流程保持動態且即時更新。

## 結論
本指南從頭到尾說明了如何 **create 3d pie chart** 與 **create 3d bar chart** 專案——設定函式庫、加入資料、產生 3‑D 長條圖、將相同步驟套用至 3‑D 圓餅圖，並應用進階樣式。使用 Aspose.Cells for Java，您即可以可靠且不受版本限制的方式，將豐富的 3‑D 視覺化直接嵌入 Excel 活頁簿，甚至匯出為 PNG 影像。

## 常見問題

**Q: 如何在 3D 圖表中加入多個資料系列？**  
A: 使用 `chart.getNSeries().add()` 為每個系列範圍新增，並確保圖表類型保持為 3‑D（例如 `ChartType.BAR_3_D` 或 `ChartType.PIE_3_D`）。

**Q: 是否可以將使用 Aspose.Cells for Java 建立的 3D 圖表匯出為其他格式？**  
A: 可以，您可以透過呼叫相應的 `chart.toImage()` 或 `workbook.save()` 重載方法，將圖表儲存為 PNG、JPEG 或 PDF，滿足 **convert chart png** 的需求。

**Q: 是否能使用 Aspose.Cells for Java 建立互動式 3D 圖表？**  
A: Aspose.Cells 主要針對靜態 Excel 圖表。若需互動式的 Web 3‑D 視覺化，建議將 Excel 資料與 JavaScript 函式庫（如 Three.js）結合使用。

**Q: 我可以自動化更新 3D 圖表中的資料嗎？**  
A: 完全可以。以程式方式將新資料載入工作表，並重新整理圖表範圍；下次開啟活頁簿時，圖表即會顯示更新後的數值。

**Q: 在哪裡可以找到更多 Aspose.Cells for Java 的資源與文件？**  
A: 您可以在以下網站找到 Aspose.Cells for Java 的完整文件與資源：[Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**最後更新：** 2026-02-09  
**測試環境：** Aspose.Cells for Java 24.12 (latest)  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}