---
date: '2026-07-07'
description: 學習 Aspose Cells 圖表範例，使用 Java 在 Excel 中建立動態樞紐圖表。遵循逐步說明，實現流暢的資料分析。
keywords:
- aspose cells chart example
- how to create pivot chart
- dynamic pivot chart excel
- export pivot chart excel
- add pivot chart workbook
og_description: 學習 Aspose Cells 圖表範例，使用 Java 在 Excel 中建立動態樞紐圖表。遵循逐步說明，實現流暢的資料分析。
og_title: Aspose Cells 圖表範例：精通 Java 中的樞紐圖表
schemas:
- author: Aspose
  dateModified: '2026-07-07'
  description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  headline: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  type: TechArticle
- description: Learn the Aspose Cells chart example to create dynamic pivot charts
    in Excel using Java. Follow step‑by‑step instructions for seamless data analysis.
  name: 'Aspose Cells Chart Example: Mastering Pivot Charts in Java'
  steps:
  - name: Load the Source Workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory.
  - name: Add a Worksheet for the Pivot Chart
    text: Create a dedicated chart sheet to keep the visual separate from raw data.
  - name: Insert a Pivot Table
    text: First, define the data range for the pivot table, then add it to the chart
      sheet. The `PivotTable` class represents a pivot table in a worksheet and provides
      methods to define its data source, layout, and calculations.
  - name: Create and Configure the Pivot Chart
    text: The `Chart` class represents any Excel chart. Here we create a column chart
      linked to the pivot table.
  - name: Export the Workbook
    text: Save the workbook with the new pivot chart to an `.xlsx` file, or directly
      to PDF if you need a static report.
  type: HowTo
- questions:
  - answer: Yes, call `chart.toImage("chart.png", ImageFormat.PNG)` after configuring
      the chart.
    question: Can I export a pivot chart directly to an image file?
  - answer: The library can preserve existing VBA macros, but it does not create or
      modify them programmatically.
    question: Does Aspose.Cells support Excel macros in pivot charts?
  - answer: Absolutely—invoke `pivotTable.refreshData()` and then `chart.refresh()`
      to reflect the latest values.
    question: Is it possible to update the pivot chart after changing the source data?
  - answer: Over 40 types, including column, line, area, pie, radar, and stacked bar,
      all fully supported for pivot data.
    question: Which chart types are available for pivot charts?
  - answer: Yes, a purchased license removes evaluation limits and enables full feature
      set.
    question: Do I need a license to use the Maven/Gradle setup in production?
  type: FAQPage
title: Aspose Cells 圖表範例：精通 Java 中的樞紐圖表
url: /zh-hant/java/charts-graphs/aspose-cells-java-pivot-charts-excel-tutorial/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose Cells 圖表範例：精通 Java 中的樞紐圖表

在當今以數據為驅動的世界，將原始數字轉化為清晰的視覺洞察至關重要。本教程向您展示建立動態樞紐圖表所需的 **aspose cells chart example**，使用 Java 在 Excel 中操作。完成本指南後，您將能夠載入工作簿、添加專用圖表工作表、綁定樞紐表，並匯出結果——只需幾行程式碼。

## 快速解答
- **什麼是處理 Excel 檔案的主要類別？** `Workbook` 代表記憶體中的整個 Excel 檔案。  
- **哪個 Maven 套件可將 Aspose.Cells 加入專案？** `com.aspose:aspose-cells`（版本 25.3 或更新）。  
- **我可以在沒有授權的情況下建立樞紐圖表嗎？** 可以，免費試用可用於開發，但授權會移除評估限制。  
- **Aspose.Cells 支援多少種圖表類型？** 超過 40 種圖表類型，包括折線圖、柱狀圖、圓餅圖和雷達圖。  
- **將樞紐圖表匯出為 PDF 的最快方法是什麼？** 在設定圖表資料來源後，呼叫 `chart.toPdf("output.pdf")`。

## 什麼是 Excel 中的樞紐圖表？
**樞紐圖表** 是樞紐表的互動式視覺呈現，允許使用者動態探索彙總資料。使用 Aspose.Cells，您可以在不開啟 Excel 的情況下以程式方式產生這些圖表。當底層樞紐表變更時，它會自動更新，支援篩選，且可透過各種圖表類型、標題與圖例進行自訂，成為資料分析的強大工具。

## 為何使用 Aspose.Cells for Java 來建立樞紐圖表？
Aspose.Cells 處理 **50 多種輸入與輸出格式**，且能在記憶體使用量低於 200 MB 的情況下處理包含 **數百個工作表** 的工作簿。其 API 能在 **2 秒以下** 為典型 10 KB 資料集建立、修改與渲染圖表，使其成為伺服器端報表的理想選擇。

## 前置條件

- **Aspose.Cells for Java** 版本 25.3 或更新。  
- Maven 或 Gradle 建置系統。  
- JDK 8 或更新，並使用 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE。  
- 基本的 Java 知識；熟悉 Excel 有助於學習，但非必需。

### 必要的函式庫與相依性
- **Maven:** 新增 Aspose.Cells 相依性（請參閱下方 *aspose cells maven setup* 章節）。  
- **Gradle:** 在 `build.gradle` 中加入相同的套件。

### 取得授權步驟
- **Free Trial:** 先使用免費試用以探索 aspose cells chart example。  
- **Temporary License:** 取得臨時金鑰以延長測試時間。  
- **Purchase:** 從 [Aspose’s official website](https://purchase.aspose.com/buy) 購買完整授權。

## 如何設定 Aspose.Cells for Java

### Maven 相依性（aspose cells maven setup）
將以下程式碼片段加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```

### Gradle 相依性
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 基本初始化
加入相依性後，請如下初始化函式庫：

```java
// Initialize license (optional for trial)
License license = new License();
license.setLicense("Aspose.Cells.lic");

// Create a Workbook object – this loads or creates an Excel file.
Workbook workbook = new Workbook();
```

## 如何使用 Aspose.Cells for Java 建立樞紐圖表？

載入來源資料、產生樞紐表，並將其綁定至圖表——只需幾個簡單步驟。此流程包括載入包含來源資料的工作簿、建立樞紐表以彙總資料、添加專用圖表工作表、將樞紐表綁定至圖表、客製化圖表外觀，最後將工作簿儲存為所需格式。

### 步驟 1：載入來源工作簿
`Workbook` 類別是 Aspose.Cells 的頂層物件，代表記憶體中的單一 Excel 檔案。

```java
Workbook workbook = new Workbook("data.xlsx");
```

### 步驟 2：為樞紐圖表新增工作表
建立專用的圖表工作表，以將視覺效果與原始資料分離。

```java
int chartSheetIndex = workbook.getWorksheets().addChart("PivotChartSheet");
Worksheet chartSheet = workbook.getWorksheets().get(chartSheetIndex);
```

### 步驟 3：插入樞紐表
首先，定義樞紐表的資料範圍，然後將其加入圖表工作表。`PivotTable` 類別代表工作表中的樞紐表，提供設定資料來源、版面配置與計算的方法。

```java
int pivotTableIndex = chartSheet.getPivotTables().add("A1:D100", "PivotTable1", 0, 0);
PivotTable pivotTable = chartSheet.getPivotTables().get(pivotTableIndex);
pivotTable.addFieldToArea(PivotFieldType.ROW, 0);   // Category
pivotTable.addFieldToArea(PivotFieldType.DATA, 1);  // Values
```

### 步驟 4：建立與設定樞紐圖表
`Chart` 類別代表任何 Excel 圖表。此處我們建立與樞紐表連結的柱狀圖。

```java
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 5, 0, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
chart.getNSeries().add("=PivotTable1!$B$2:$B$5", true);
chart.setTitle("Sales by Region");
```

### 步驟 5：匯出工作簿
將包含新樞紐圖表的工作簿儲存為 `.xlsx` 檔案，或在需要靜態報告時直接匯出為 PDF。

```java
workbook.save("PivotChartResult.xlsx", SaveFormat.XLSX);
// Optional PDF export
workbook.save("PivotChartResult.pdf", SaveFormat.PDF);
```

## 動態樞紐圖表的實務應用

- **Financial Reporting:** 自動產生隨新資料匯入即更新的季度儀表板。  
- **Sales Analysis:** 只需一次 API 呼叫即可視覺化區域銷售趨勢。  
- **Inventory Management:** 即時追蹤庫存水平與再訂貨點。  
- **Customer Insights:** 結合人口統計資料與購買歷史，製作互動式圖表。  
- **Project Management:** 使用樞紐圖表顯示資源分配與時間線差異。

## 大型資料集的效能技巧

- **Memory Management:** 儲存後呼叫 `workbook.dispose()` 以釋放本機資源。  
- **Batch Operations:** 使用 `CellsHelper.copyRange` 移動大型資料區塊，避免逐格迴圈。  
- **Lazy Loading:** 處理超過 100 MB 的檔案時，啟用 `LoadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 以降低記憶體使用量。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **樞紐表未反映新資料** | 在建立圖表前，使用 `pivotTable.refreshData()` 重新整理樞紐表。 |
| **圖表顯示空白** | 確保圖表的資料來源範圍與樞紐表的結果範圍相符。 |
| **大型檔案的記憶體不足錯誤** | 使用 `LoadOptions` 搭配 `MemorySetting.MEMORY_PREFERENCE`，並關閉不再需要的工作表。 |

## 常見問答

**Q: 我可以直接將樞紐圖表匯出為影像檔案嗎？**  
A: 可以，在設定圖表後呼叫 `chart.toImage("chart.png", ImageFormat.PNG)`。

**Q: Aspose.Cells 是否支援 Excel 宏在樞紐圖表中的使用？**  
A: 此函式庫可保留現有的 VBA 宏，但無法以程式方式建立或修改宏。

**Q: 在變更來源資料後，是否可以更新樞紐圖表？**  
A: 當然可以——呼叫 `pivotTable.refreshData()`，然後 `chart.refresh()` 以反映最新數值。

**Q: 樞紐圖表支援哪些圖表類型？**  
A: 超過 40 種，包括柱狀圖、折線圖、區域圖、圓餅圖、雷達圖與堆疊條形圖，皆完整支援樞紐資料。

**Q: 在正式環境使用 Maven/Gradle 設定是否需要授權？**  
A: 需要，購買授權可移除評估限制並啟用完整功能。

---

**最後更新：** 2026-07-07  
**測試版本：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

## 資源

- [Aspose.Cells 文件說明](https://reference.aspose.com/cells/java/)
- [下載 Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [購買授權](https://purchase.aspose.com/buy)
- [免費試用與臨時授權](https://releases.aspose.com/cells/java/)
- [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

```java
import com.aspose.cells.Workbook;

// Load an existing workbook
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
```

```java
   import com.aspose.cells.Workbook;
   ```

```java
   String dataDir = "YOUR_DATA_DIRECTORY";
   Workbook workbook = new Workbook(dataDir + "/pivotTable_test.xls");
   ```

```java
   import com.aspose.cells.SheetType;
   import com.aspose.cells.Worksheet;
   ```

```java
   int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
   Worksheet sheet3 = workbook.getWorksheets().get(sheetIndex);
   sheet3.setName("PivotChart");
   ```

```java
   import com.aspose.cells.Chart;
   import com.aspose.cells.ChartType;
   ```

```java
   int chartIndex = sheet3.getCharts().add(ChartType.COLUMN, 0, 5, 28, 16);
   Chart chart = sheet3.getCharts().get(chartIndex);
   ```

```java
   chart.setPivotSource("PivotTable!PivotTable1");
   chart.setHidePivotFieldButtons(false);
   ```

```java
   String outDir = "YOUR_OUTPUT_DIRECTORY";
   workbook.save(outDir + "/CPCBasedOnPTable_out.xls");
   ```

## 相關教學

- [精通 Excel 樞紐表（使用 Aspose.Cells for Java）：資料分析完整指南](/cells/java/data-analysis/excel-pivot-tables-aspose-cells-java-tutorial/)
- [使用 Aspose.Cells for Java 建立工作簿與圖表：完整指南](/cells/java/charts-graphs/create-workbook-add-charts-aspose-cells-java/)
- [Java 中的 Excel 圖表自訂：精通 Aspose.Cells 以實現無縫資料視覺化](/cells/java/charts-graphs/excel-chart-customization-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}