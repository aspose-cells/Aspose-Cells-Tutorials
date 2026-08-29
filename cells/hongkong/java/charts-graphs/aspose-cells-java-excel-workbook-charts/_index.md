---
date: '2026-04-11'
description: 學習使用 Aspose.Cells 進行 Excel 自動化（Java）。本教學示範如何以 Java 建立 Excel 工作簿、填入 Excel
  資料，並以圖表儲存 Excel 檔案。
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: Excel 自動化 Java：使用 Aspose 建立工作簿與圖表
url: /zh-hant/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel Automation Java：使用 Aspose 建立活頁簿與圖表

## 介紹

使用 Java 自動化 Excel 任務可以節省大量手動工作時間，特別是當您需要即時產生報告、儀表板或資料驅動的圖表時。**Excel automation java** 搭配 Aspose.Cells 提供乾淨且高效能的 API，能處理從活頁簿建立到精緻圖表樣式的所有工作。在本教學中，您將學會如何設定 Aspose.Cells、**建立 Excel workbook java**、填入資料、加入圖表、套用 3‑D 格式，最後 **儲存 Excel file java**。

### 快速回答
- **哪個函式庫簡化了 Java 中的 Excel 自動化？** Aspose.Cells for Java。  
- **我可以以程式方式加入 3‑D 圖表嗎？** 是 – API 支援 3‑D 格式化與光照效果。  
- **開發時需要授權嗎？** 可使用免費試用授權；正式上線需購買商業授權。  
- **支援哪些 Java 建置工具？** Maven 與 Gradle 均完整支援。  
- **可以匯出哪些檔案格式？** XLS、XLSX、CSV、PDF 等多種格式。

## 什麼是 Excel 自動化 Java？

Excel 自動化 Java 指的是使用 Java 程式碼以程式方式產生、修改與儲存 Excel 活頁簿的過程。它可省去手動編輯試算表的工作，確保一致性，並能與資料庫或 Web 服務等其他系統整合。

## 為什麼使用 Aspose.Cells for Java？

- **功能豐富** – 從簡單的儲存格值到複雜的圖表、樞紐分析表與條件格式化。  
- **無需 Microsoft Office 依賴** – 可在任何伺服器端環境執行。  
- **高效能** – 為大型資料集與多執行緒情境進行最佳化。  
- **支援多種格式** – 可讀寫 XLS、XLSX、ODS、CSV、PDF、HTML 等。

## 前置條件

- **Java Development Kit (JDK) 8+**  
- **Maven 或 Gradle** 用於相依性管理  
- **Aspose.Cells for Java 25.3 或更新版本**（試用或授權）  

## 設定 Aspose.Cells for Java

使用以下任一設定方式將函式庫加入您的專案。

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### 取得授權

向 Aspose 官方網站申請免費試用授權，或購買正式授權以供生產環境使用。將授權檔放置於專案中，並於執行時載入。

## 基本初始化與設定

相依性解決後，即可開始撰寫程式碼。

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## 步驟說明

### 步驟 1：如何建立 Excel 活頁簿 Java

建立一個全新的活頁簿實例，用於容納所有工作表。

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### 步驟 2：新增工作表（含圖表工作表）

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### 步驟 3：如何填入 Excel 資料 Java

插入圖表將參考的範例資料。

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### 步驟 4：在活頁簿中加入直條圖

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### 步驟 5：套用顏色格式至圖表區域

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### 步驟 6：設定圖例與資料系列

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### 步驟 7：為系列套用 3D 格式

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### 步驟 8：設定系列顏色以提升視覺辨識度

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### 步驟 9：如何儲存 Excel 檔案 Java

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## 實務應用

- **財務報告** – 產生含動態圖表的季報表。  
- **資料分析儀表板** – 建立可自動刷新之互動式儀表板。  
- **庫存管理** – 匯出庫存水平與趨勢至 Excel，供利害關係人審閱。  
- **專案規劃** – 從基於 Java 的排程系統直接產生甘特圖式圖表。  

## Excel 自動化 Java 效能技巧

- **重複使用 Workbook 物件** 在處理多個工作表時以減少記憶體佔用。  
- **批次儲存格更新** 使用 `Cells.importArray` 處理大型資料集，避免逐一呼叫 `putValue`。  
- **釋放資源** 在儲存大型檔案後呼叫 `book.dispose()`。  

## 常見問題

**Q: 我可以產生 XLSX 而非 XLS 嗎？**  
A: 可以 – 只需將 `book.save("output.xlsx")` 的副檔名改為 .xlsx；Aspose 會自動選擇正確的格式。

**Q: 開發時需要授權嗎？**  
A: 免費試用授權可用於開發與測試。正式上線則需購買授權。

**Q: 我要如何加入其他圖表類型？**  
A: 在呼叫 `charts.add(...)` 時使用 `ChartType` 列舉（例如 `ChartType.PIE`、`ChartType.LINE`）。

**Q: 如果需要保護活頁簿該怎麼做？**  
A: 在儲存前呼叫 `book.getSettings().setPassword("yourPassword")`。

**Q: Aspose.Cells 是否支援含巨集的檔案？**  
A: 支援 – 您可以在 XLSM 活頁簿中建立或保留 VBA 巨集。

---

**最後更新：** 2026-04-11  
**測試環境：** Aspose.Cells 25.3 (Java)  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}