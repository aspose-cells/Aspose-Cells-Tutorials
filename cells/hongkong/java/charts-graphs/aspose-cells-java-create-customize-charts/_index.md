---
date: '2026-04-08'
description: 學習如何在 Java 中使用 Aspose.Cells 產生直條圖，涵蓋建立圖表、加入圖表工作表以及匯出 Excel 工作簿。
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: 使用 Aspose.Cells Java 教程生成柱狀圖
url: /zh-hant/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells Java 產生直條圖

在當今以數據為驅動的應用程式中，**快速且程式化產生直條圖** 能將原始數字轉化為清晰的視覺洞見。無論您是構建報告儀表板、分析工具，或是簡單的匯出功能，Aspose.Cells for Java 為您提供流暢的 API，讓您在不使用 Excel 介面的情況下 **建立 chart java** 專案。在本教學中，您將學習如何設定函式庫、**填充 Excel 儲存格**、新增 **圖表工作表**、自訂 **圖表標題**，以及最終 **匯出 workbook excel** 為檔案。

## 快速解答
- **「generate column chart」是什麼意思？** 它會從表格資料產生垂直條形的視覺化圖表。  
- **需要哪個函式庫？** Aspose.Cells for Java（提供免費試用）。  
- **是否需要安裝 Excel？** 不需要，該函式庫可獨立於 Microsoft Excel 運作。  
- **可以匯出成除 XLS 之外的格式嗎？** 可以 – 例如 PDF、PNG、SVG 等，透過 `workbook.save()`。  
- **在正式環境中是否必須擁有授權？** 必須，需購買授權或使用臨時授權。

## 什麼是 generate column chart？
直條圖會以垂直條形顯示資料系列，讓您能輕鬆比較不同類別（如區域、月份或產品線）的數值。Aspose.Cells 允許您完全以程式碼建立此圖表，讓您對資料、樣式與輸出格式擁有完整控制。

## 為何使用 Aspose.Cells 來建立 chart java？
- **無 COM 互操作** – 可在任何具 JVM 的作業系統上執行。  
- **豐富的樣式選項** – 圖片、漸層、圖例與自訂字型。  
- **高效能** – 適用於大型資料集。  
- **多種匯出格式** – XLS、XLSX、PDF、PNG 等。

## 前置條件
- **Java Development Kit (JDK) 8+** 已安裝。  
- 具備基本的 Java 知識並熟悉 Excel 概念。  

### 必要函式庫
使用以下任一程式碼片段將 Aspose.Cells 加入您的專案。

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### 授權取得
Aspose 提供免費試用與臨時授權，以供廣泛測試。

- **免費試用**: [Download Free](https://releases.aspose.com/cells/java/)  
- **臨時授權**: [Request Here](https://purchase.aspose.com/temporary-license/)

## 設定 Aspose.Cells for Java

首先，建立一個 `Workbook` 實例 – 它將作為我們資料與圖表的畫布。

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## 步驟說明

### 1. 建立並命名工作表
我們將把原始資料儲存在名為 **Data** 的工作表中。

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. 填充 Excel 儲存格
插入區域名稱與銷售數字，供直條圖視覺化。

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. 新增圖表工作表
將圖表與原始資料分離，可保持活頁簿整潔。

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. 建立直條圖
現在我們實際 **generate column chart** 物件。

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. 在繪圖區設定圖片作為背景填充
背景圖片能讓圖表更為突出。

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. 設定圖表標題
自訂 **set chart title** 可提升可讀性。

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. 設定系列資料與圖例
將資料範圍連結至圖表，並設定圖例位置。

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. 匯出 Workbook Excel
最後，將 **export workbook excel** 匯出為 XLS 檔（或任何支援的格式）。

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## 實務應用
- **商業報告** – 自動產生每月 PDF 的銷售圖表。  
- **資料分析工具** – 在自訂分析儀表板中嵌入動態圖表。  
- **企業儀表板** – 即時刷新圖表影像以進行即時監控。  

## 效能考量
- 在處理大型資料集時，批次更新儲存格以減少開銷。  
- 若在迴圈中處理大量活頁簿，請釋放資源（`workbook.dispose()`）。  

## 常見問題與解決方案
- **圖片未顯示** – 請確認檔案路徑且圖片格式（PNG、JPEG）受支援。  
- **圖表顯示空白** – 確認資料範圍參照（`Data!B2:B8`）與已填充的儲存格相符。  
- **記憶體不足錯誤** – 將資料分批處理，並在大型儲存後呼叫 `System.gc()`。  

## 常見問答

**Q: 如何在直條圖中加入多個系列？**  
A: 反覆呼叫 `chart.getNSeries().add()`，並使用不同的資料範圍，例如第二個系列使用 `"Data!C2:C8"`。

**Q: 可以更改座標軸標籤嗎？**  
A: 可以。使用 `chart.getCategoryAxis().setTitle("Regions")` 與 `chart.getValueAxis().setTitle("Sales")`。

**Q: 除了 XLS，還能匯出哪些格式？**  
A: 使用 `workbook.save("chart.pdf")`、`workbook.save("chart.png")` 或 `workbook.save("chart.xlsx")` 分別匯出為 PDF、PNG 與 XLSX。

**Q: 開發版是否需要授權？**  
A: 免費試用可用於評估，但正式部署時需購買永久授權或使用臨時授權。

**Q: 如何提升數千列的渲染速度？**  
A: 使用 `cells.importArray()` 填充儲存格，並在所有資料載入後才建立圖表，以減少圖表重繪次數。

---

**最後更新：** 2026-04-08  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

## 資源

- [Aspose.Cells 文件](https://reference.aspose.com/cells/java/)
- [下載 Aspose.Cells](https://releases.aspose.com/cells/java/)
- [購買授權](https://purchase.aspose.com/buy)
- [免費試用](https://releases.aspose.com/cells/java/)
- [臨時授權申請](https://purchase.aspose.com/temporary-license/)
- [支援論壇](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}