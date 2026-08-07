---
date: '2026-04-02'
description: 學習如何使用 Aspose.Cells for Java 建立圖表及產生 Excel 泡泡圖。此指南將逐步說明設定、資料與儲存圖表的流程。
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 如何創建圖表：使用 Aspose.Cells Java 的 Excel 氣泡圖
url: /zh-hant/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 如何建立圖表：使用 Aspose.Cells for Java 的 Excel 氣泡圖

使用 Aspose.Cells for Java 為您的 Excel 報表增添動態氣泡圖。本教學將教您 **如何建立圖表** 物件，以氣泡圖方式視覺化資料，讓您的簡報更具洞察力與互動性。我們將逐步說明——從設定開發環境、配置圖表資料，到最終儲存活頁簿的完整流程。

## 快速答覆
- **哪個程式庫最適合在 Java 中製作 Excel 圖表？** Aspose.Cells for Java。  
- **我可以以程式方式產生 Excel 氣泡圖嗎？** 可以，使用下方示範的圖表 API。  
- **執行程式碼是否需要授權？** 免費試用版可執行，但完整授權可解鎖全部功能。  
- **支援哪些 Java 建置工具？** Maven 與 Gradle 皆受支援。  
- **設定氣泡圖資料的主要方法是什麼？** 在系列上使用 `setBubbleSizes`、`setXValues` 與 `setValues`。

## 什麼是氣泡圖？
氣泡圖是散佈圖的變形，每個資料點以氣泡呈現。X 軸與 Y 軸決定位置，氣泡大小則傳遞第三維度資訊——非常適合視覺化財務、銷售或科學資料。

## 為何使用 Aspose.Cells for Java？
- **零安裝 Excel 引擎** ─ 伺服器上不需安裝 Microsoft Office。  
- **豐富的圖表 API** ─ 支援所有現代圖表類型，包括氣泡圖。  
- **跨平台** ─ 可在 Windows、Linux 與 macOS 上執行。  
- **高效能** ─ 為大型資料集與大量報表產生進行最佳化。

## 前置條件
若要使用 Aspose.Cells for Java 建立氣泡圖，請確保符合以下前置條件：

### 必要的程式庫與相依性
- **Aspose.Cells for Java**：安裝最新版本（例如 25.3）。

### 環境設定需求
- 已安裝相容的 Java Development Kit (JDK)。  
- 專案已設定為使用 Maven 或 Gradle。

### 知識前提
- 具備基本的 Java 程式設計概念。  
- 熟悉 Excel 檔案結構與圖表類型。

## 設定 Aspose.Cells for Java
正確的環境設定至關重要，以下說明如何開始：

### 透過 Maven 安裝
在 `pom.xml` 中加入以下相依性：
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### 透過 Gradle 安裝
使用 Gradle 的使用者，將下列內容加入 `build.gradle`：
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 授權取得
Aspose.Cells 提供功能受限的免費試用版。若需完整功能，請：
- **購買**：前往 [purchase page](https://purchase.aspose.com/buy) 了解授權方案。  
- **臨時授權**：從 [here](https://purchase.aspose.com/temporary-license/) 取得臨時授權，以完整測試。

### 基本初始化
在 Java 專案中使用 Aspose.Cells 前，先進行初始化：
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## 實作指南
以下分步說明如何使用 Aspose.Cells 建立與設定氣泡圖。

### 如何建立圖表：初始化 Workbook 物件
`Workbook` 代表整個 Excel 檔案，可操作工作表、儲存格等。如下初始化：
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### 如何設定氣泡圖資料：存取與操作工作表
準備供氣泡圖使用的資料：
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### 如何產生 Excel 氣泡圖：建立與設定圖表
將氣泡圖加入工作表並設定資料來源：
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### 如何儲存圖表：儲存活頁簿
將活頁簿（含內嵌圖表）寫入磁碟：
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## 實務應用
- **財務報表** ─ 在單一視圖中呈現營收、利潤與市場佔有率。  
- **銷售資料分析** ─ 以氣泡大小顯示銷售量，突顯各區域表現。  
- **科學研究** ─ 同時展示三個變數的實驗結果。

## 效能考量
- 及時釋放不再使用的物件以節省記憶體。  
- 盡量縮小資料範圍；過大的不必要範圍會降低渲染速度。  
- 處理大量資料時，遵循 Java 記憶體管理的最佳實踐。

## 常見問題與解決方案
| 問題 | 原因 | 解決方案 |
|------|------|----------|
| **圖表為空** | 資料範圍未正確對應系列 | 確認 `setBubbleSizes`、`setXValues` 與 `setValues` 指向正確的儲存格。 |
| **氣泡大小不正確** | 範圍長度不一致 | 確保三個範圍的資料點數相同。 |
| **授權例外** | 未使用有效授權執行 | 在建立活頁簿前套用臨時或正式授權。 |

## 常見問答

**Q: 需要的最低 Aspose.Cells 版本為何？**  
A: 建議使用 25.3 版，以確保所有示範功能相容。

**Q: 如何自訂氣泡圖的顏色？**  
A: 使用系列的格式化方法，例如 `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`。

**Q: 這段程式碼能在 Linux 伺服器上執行嗎？**  
A: 能，Aspose.Cells for Java 完全跨平台，任何具相容 JDK 的作業系統皆可執行。

**Q: 若出現「Data source size mismatch」錯誤該怎麼辦？**  
A: 再次確認氣泡大小、X 值與 Y 值的範圍包含相同數量的儲存格。

**Q: 從哪裡取得測試用的臨時授權？**  
A: 前往 [Aspose's temporary license page](https://purchase.aspose.com/temporary-license/) 申請試用授權。

## 資源
- **文件說明**：欲取得更詳細資訊，請參考 [official documentation](https://reference.aspose.com/cells/java/)。  
- **下載**：從 [the release page](https://releases.aspose.com/cells/java/) 取得最新版本。  
- **購買**：在 [this page](https://purchase.aspose.com/buy) 探索授權選項。  
- **免費試用**：前往 [Aspose's releases section](https://releases.aspose.com/cells/java/) 開始免費試用。  
- **支援論壇**：如有任何疑問，可至 [support forum](https://forum.aspose.com/c/cells/9) 交流。

---

**最後更新：** 2026-04-02  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}