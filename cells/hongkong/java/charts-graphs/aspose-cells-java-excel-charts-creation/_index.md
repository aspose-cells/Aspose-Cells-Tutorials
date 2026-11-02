---
date: '2026-04-08'
description: 學習如何使用 Aspose.Cells for Java 建立帶有標記的折線圖、將圖表加入工作表，並自訂 Excel 圖表以實現自動化報告。
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: 使用 Aspose.Cells for Java 建立帶標記的折線圖
url: /zh-hant/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells Java 建立與樣式化 Excel 圖表

## 簡介

在當今以數據為驅動的世界，**line chart with markers** 是視覺化趨勢與異常值的最有效方法之一。無論您是建立自動化報告或每日更新的儀表板，能以程式方式在工作表中加入帶標記的折線圖，可節省無數手動步驟。本教學將指導您如何使用 Aspose.Cells for Java 來建立、樣式化及匯出此類圖表，讓您專注於洞察，而非繁瑣的 Excel 操作。

**您將學習**
- 使用 Aspose.Cells 初始化工作簿並填充資料。  
- **如何在工作表中加入帶標記的折線圖** 並設定其外觀。  
- 自訂系列顏色、標記及其他樣式選項。  
- 將工作簿儲存為包含已樣式化圖表的 Excel 檔案。

## 快速答案

- **開始時的主要類別是什麼？** `Workbook` 初始化一個新的 Excel 檔案。  
- **哪種圖表類型會產生帶標記的折線圖？** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **如何為系列點設定自訂顏色？** 使用 `chart.getNSeries().setColorVaried(true)` 並設定標記區域顏色。  
- **完整功能是否需要授權？** 是的，付費或臨時的 Aspose.Cells 授權可移除評估限制。  
- **我可以將結果匯出為 XLSX 嗎？** 當然 — `workbook.save("StyledChart.xlsx")` 會建立 XLSX 檔案。

## 先決條件

在使用 Aspose.Cells for Java 建立與樣式化圖表之前，請確保您已完成以下設定：

### 必要的函式庫

在您的專案中將 Aspose.Cells 作為相依性加入。以下提供 Maven 與 Gradle 使用者的說明：

**Maven:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 環境設定需求
- 已在系統上安裝 Java Development Kit (JDK)。  
- 使用如 IntelliJ IDEA 或 Eclipse 等整合開發環境 (IDE) 進行程式編寫與測試。

### 知識先備條件
需要具備 Java 程式設計的基本概念，並熟悉 Excel 工作簿與圖表相關概念。 

### 取得授權
Aspose.Cells 為商業產品，完整功能需取得授權。您可下載免費試用版以評估功能，申請臨時授權以延長測試，或購買正式授權以長期使用。

- **免費試用：** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **臨時授權：** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **購買：** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## 設定 Aspose.Cells for Java

安裝必要的相依性後，設定開發環境以使用 Aspose.Cells。首先在 Java 應用程式中匯入函式庫並初始化 `Workbook` 物件：

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## 實作指南

本節將把實作分解為以下功能：工作簿初始化與資料填充、圖表建立與設定、系列自訂以及工作簿儲存。

### 功能 1：工作簿初始化與資料填充

**概觀：** 此功能著重於建立新工作簿、存取第一個工作表，並填入圖表建立所需的資料。

#### 步驟 1：初始化工作簿
先建立 `Workbook` 物件：

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### 步驟 2：設定欄位標題並填充資料
定義欄位標題，並以範例資料填充列：

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### 功能 2：圖表建立與設定

**概觀：** 此功能示範如何在工作簿的工作表中加入圖表、設定樣式，並配置基本屬性。

#### 步驟 3：在工作表中加入圖表
加入帶資料標記的折線圖：

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### 功能 3：系列設定與自訂

**概觀：** 透過自訂系列設定（如多樣顏色與標記樣式），提升圖表的視覺效果。

#### 步驟 4：自訂系列設定
設定系列資料，套用自訂格式，並調整標記：

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### 功能 4：工作簿儲存

**概觀：** 最後，儲存工作簿以保留變更，並確保圖表已包含於 Excel 檔案中。

#### 步驟 5：儲存工作簿
將工作簿儲存，包含新建立的圖表：

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### 常見問題與故障排除

- **圖表顯示為空白：** 請確認在 `setXValues` 與 `setValues` 中使用的儲存格範圍正確指向已填充資料的儲存格。  
- **顏色未套用：** 請確保在自訂各系列之前已呼叫 `chart.getNSeries().setColorVaried(true)`。  
- **授權錯誤：** 試用授權可能限制圖表數量；安裝正式授權即可移除限制。

## 常見問題

**問：我可以使用 Aspose.Cells 建立其他圖表類型（例如長條圖、圓餅圖）嗎？**  
答：可以，Aspose.Cells 支援多種圖表類型，只需將 `ChartType.LINE_WITH_DATA_MARKERS` 替換為所需的列舉值即可。

**問：需要關閉工作簿或釋放資源嗎？**  
答：`Workbook` 類別會自動管理資源，但在長時間執行的應用程式中，您可以呼叫 `workbook.dispose()` 以釋放記憶體。

**問：可以在同一工作表中加入多個圖表嗎？**  
答：當然可以 — 為每個欲插入的圖表呼叫 `worksheet.getCharts().add(...)`。

**問：如何將檔案匯出為較舊的 Excel 格式（XLS）？**  
答：使用 `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);`。

**問：在 Microsoft Excel 中開啟時，圖表會保留其樣式嗎？**  
答：會，Aspose.Cells 會寫入原生的 Excel 圖表物件，所有樣式、顏色與標記皆會如同定義時那樣呈現。

---

**最後更新：** 2026-04-08  
**測試版本：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}