---
date: '2026-09-27'
description: 了解如何使用 Aspose.Cells 在 Java 中建立 pie chart。一步一步的指南，教您自訂 Excel pie chart、設定
  Maven 相依性，並產生專業圖表。
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: 使用 Aspose.Cells for Java 建立 pie chart。了解如何自訂 Excel pie chart、加入 Maven
  相依性，並在數分鐘內產生專業圖表。
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: 使用 Aspose.Cells 建立 pie chart Java – 完整 Java 指南
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: 如何使用 Aspose.Cells 在 Java 中建立 pie chart
url: /zh-hant/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 建立 Java 圓餅圖

## 介紹
以程式方式建立 **pie chart** 往往像解謎，特別是當你需要對顏色、圖例與標題進行細緻控制時。在本指南中，你將學習如何使用 Aspose.Cells **create pie chart java**，並自訂 Excel 圓餅圖以符合你的品牌或報告風格。我們將一步步說明環境設定、資料填充、圖表產生與視覺調整——全部在你的 Java IDE 中完成。

**您將學習**
- 將 **Maven 依賴 Aspose.Cells** 加入您的專案。
- 建立工作簿、填入資料至儲存格，並產生圓餅圖。
- 為圖表套用自訂顏色、標題與圖例。
- 將工作簿匯出為可分享的 XLSX 檔案。

在開始之前，你應該熟悉基本的 Java 語法，並已安裝 Maven 或 Gradle。

## 快速問答
- **Which library creates pie charts in Java?** Aspose.Cells for Java.  
- **Do I need a license?** 免費試用可用於開發；正式環境需購買授權。  
- **What Maven coordinates are required?** `com.aspose:aspose-cells:24.10`.  
- **Can I change slice colors?** 可以，透過每個 series 的 `setAreaColor` 方法。  
- **Is the chart exportable to XLSX?** 當然，只要呼叫 `workbook.save("output.xlsx")` 即可。

## 什麼是 Excel 圓餅圖？
圓餅圖將單一資料系列以圓形的比例切片方式呈現，讓人輕鬆比較整體中的各部分。每一切片的角度對應其相對於總和的數值，便於快速洞察如市場佔有率、預算分配或人口比例等分類的分布情況。

## 為什麼使用 Aspose.Cells 建立 Java 圓餅圖？
Aspose.Cells 支援超過 50 種圖表類型，且可在不將整個檔案載入記憶體的情況下處理高達百萬列的工作表。此效能優勢讓你在一般硬體上產生大型報表，同時提供對圖表外觀、資料綁定與匯出格式的細緻控制，遠勝許多開源函式庫。

## 前置條件
- **Java Development Kit (JDK)** 8 或更新版本。
- **IDE** 如 IntelliJ IDEA 或 Eclipse。
- **Maven** 或 **Gradle** 用於相依管理。
- 一份 **試用或已購買的 Aspose.Cells 授權**。

### 必要的函式庫與相依性
將 Aspose.Cells Maven 套件加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

或使用 Gradle 等價設定：

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 取得授權步驟
Aspose.Cells for Java 為商業授權，但你可以先使用免費試用版。前往 [purchase page](https://purchase.aspose.com/buy) 取得暫時授權金鑰。

## 設定 Aspose.Cells for Java
首先，確保程式庫已在 classpath 中。加入相依後，你可以如以下範例初始化 API。

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## 實作指南

### 建立與設定工作簿
`Workbook` 類別在記憶體中代表整個 Excel 檔案。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### 步驟 1：實例化工作簿
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
此程式碼會建立一個全新的空白工作簿，讓你立即開始填充資料。

### 存取或修改工作表儲存格
`Worksheet` 代表工作簿中的單一工作表，包含儲存格、列與欄。  
你將把驅動圓餅圖的資料寫入工作表。

#### 步驟 2：取得第一個工作表及其儲存格
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
將類別名稱與數值填入儲存格，供圖表使用。

### 建立圓餅圖
`Chart` 物件可視覺化工作表中的資料，支援圓餅圖、柱狀圖、折線圖等多種類型。

#### 步驟 3：在工作表中加入圓餅圖
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### 設定圓餅圖系列與資料
`Series` 定義圖表的資料範圍與格式，將工作表儲存格連結至視覺元素。

#### 步驟 4：設定圖表的系列
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### 設定圖表圖例與標題外觀
圖表的 `Legend` 會顯示系列名稱與顏色，協助讀者辨識每一切片。

#### 步驟 5：自訂圖例與標題
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### 自訂圖表系列顏色
`setAreaColor` 使用 RGB 值設定圖表系列切片的填色。

#### 步驟 6：變更圓餅切片顏色
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### 自動調整欄寬並儲存工作簿
`autoFitColumns` 會自動調整欄寬以符合儲存格內容。

#### 步驟 7：調整欄寬並儲存檔案
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## 常見使用情境
- **人口統計分析：** 顯示各區域的人口分布。  
- **市場佔有率報告：** 一目了然地視覺化每個競爭者的佔比。  
- **預算分配：** 突顯資金在各部門之間的分配情況。

## 效能考量
- 在不再需要時釋放物件（`workbook.dispose()`），以釋放本機記憶體。  
- 面對大量資料時，使用 `WorkbookDesigner` 以串流方式處理資料，而非一次載入全部。  
- 使用 Java Flight Recorder 進行效能分析，找出圖表產生的瓶頸。

## 常見問答

**Q: Can I generate multiple pie charts in the same workbook?**  
A: 可以，對每個資料範圍重複圖表建立步驟；每個圖表彼此獨立。

**Q: Does Aspose.Cells support 3‑D pie charts?**  
A: 支援；在加入圖表時將圖表類型設為 `ChartType.PIE_3D`。

**Q: How do I apply a custom theme to all charts?**  
A: 在建立任何圖表之前，呼叫 `Workbook.setDefaultTheme` 方法即可套用自訂主題。

**Q: What file formats can I export the workbook to?**  
A: 超過 30 種格式，包括 XLSX、CSV、PDF 與 HTML。

**Q: Is a license required for commercial deployment?**  
A: 必須，合法授權可移除評估水印並解鎖全部功能。

## 結論
現在你已掌握使用 Aspose.Cells **create pie chart java** 的完整端對端流程。依照上述步驟，你可以產生精緻的 Excel 圓餅圖、客製化顏色與標題，並將其嵌入任何報告管線。也可探索其他圖表類型——柱狀圖、折線圖、雷達圖——以擴充你的資料視覺化工具箱。

---

**Last Updated:** 2026-09-27  
**Tested with:** Aspose.Cells 24.10 for Java  
**Author:** Aspose

## 相關教學

- [使用 Aspose.Cells for Java 自訂 Excel 圖表資料標籤：一步步指南](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [使用 Aspose.Cells Java 建立動態 Excel 圖表：開發者完整指南](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [使用 Aspose.Cells Java 建立與自訂 Excel 工作簿：一步步指南](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}