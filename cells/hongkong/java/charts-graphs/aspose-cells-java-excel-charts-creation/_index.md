---
"date": "2025-04-07"
"description": "了解如何使用 Aspose.Cells for Java 在 Excel 中建立和自訂圖表。透過本詳細指南，可以自動建立圖表、增強資料視覺化並節省時間。"
"title": "使用 Aspose.Cells Java&#58; 建立和設定 Excel 圖表樣式綜合指南"
"url": "/zh-hant/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells Java 建立和設定 Excel 圖表樣式

## 介紹

在當今數據驅動的世界中，有效的資訊視覺化對於分析和決策至關重要。通常，需要以程式設計方式在 Excel 工作簿中建立動態圖表 - 尤其是在處理大型資料集或自動報告系統時。本教學課程示範如何使用 Aspose.Cells for Java 在 Excel 中無縫建立和自訂圖表。透過將 Aspose.Cells 整合到您的 Java 應用程式中，您可以自動建立圖表、增強資料呈現並節省時間。

**您將學到什麼：**
- 使用 Aspose.Cells 初始化工作簿並用資料填滿它。
- 使用資料標記建立和配置折線圖。
- 自訂系列外觀和顏色以實現更好的視覺化。
- 以 Excel 格式儲存包含新建立的圖表的工作簿。

讓我們先討論一下開始所需的先決條件。

## 先決條件

在使用 Aspose.Cells for Java 建立和設計圖表之前，請確保您已完成以下設定：

### 所需庫
將 Aspose.Cells 作為相依性包含在您的專案中。以下是針對 Maven 和 Gradle 使用者的說明：

**Maven：**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle：**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 環境設定要求
- 您的系統上安裝了 Java 開發工具包 (JDK)。
- 用於編碼和測試的整合開發環境 (IDE)，例如 IntelliJ IDEA 或 Eclipse。

### 知識前提
需要對 Java 程式設計有基本的了解，並且熟悉 Excel 工作簿和圖表概念。 

### 許可證獲取
Aspose.Cells 是一款商業產品，需要許可證才能使用全部功能。您可以獲得免費試用版來評估其功能，申請臨時許可證以進行擴展測試，或購買產品以供長期使用。

- **免費試用：** [下載免費試用版](https://releases.aspose.com/cells/java/)
- **臨時執照：** [申請臨時許可證](https://purchase.aspose.com/temporary-license/)
- **購買：** [購買 Aspose.Cells](https://purchase.aspose.com/buy)

## 設定 Aspose.Cells for Java

安裝必要的依賴項後，設定開發環境以使用 Aspose.Cells。首先在 Java 應用程式中匯入庫並初始化 Workbook 物件：

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // 初始化新的工作簿實例
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## 實施指南

在本節中，我們將把實作分解為不同的功能：工作簿初始化和資料填充、圖表建立和配置、系列自訂和工作簿保存。

### 功能 1：工作簿初始化和資料填充

**概述：** 此功能主要用於建立新工作簿、存取其第一個工作表以及向其中填入用於建立圖表的資料。

#### 步驟 1：初始化工作簿
首先實例化一個 `Workbook` 目的：

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // 實例化工作簿
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### 步驟 2：設定列標題並填入數據
定義列標題並使用範例資料填充行：

```java
        // 設定列標題 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // 為系列 1 建立隨機數據
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // 為系列 2 建立隨機數據
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### 功能2：圖表建立與配置

**概述：** 此功能示範如何在工作簿的工作表中新增圖表、設定其樣式以及配置基本屬性。

#### 步驟 3：在工作表中新增圖表
新增帶有資料標記的折線圖：

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // 實例化工作簿
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // 將圖表新增至工作表
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // 存取和配置圖表
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // 設定預定義樣式
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### 特點3：系列配置和客製化

**概述：** 透過自訂系列設定（例如不同的顏色和標記樣式）來增強圖表的視覺吸引力。

#### 步驟 4：自訂系列設置
配置系列資料、套用自訂格式並調整標記：

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // 實例化工作簿
        Workbook workbook = new Workbook();
        
        // 訪問第一個工作表
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // 在圖表中新增系列
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // 為系列點啟用多種顏色
        chart.getNSeries().setColorVaried(true);

        // 自訂第一個系列標記樣式和顏色
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // 設定第一個系列的 X 和 Y 值
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // 自訂第二個系列標記樣式和顏色
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // 設定第二個系列的 X 和 Y 值
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### 功能4：工作簿保存

**概述：** 最後，儲存工作簿以保留您的變更並確保圖表包含在 Excel 檔案中。

#### 步驟 5：儲存工作簿
使用新建立的圖表儲存您的工作簿：

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // 實例化工作簿
        Workbook workbook = new Workbook();
        
        // 存取第一個工作表並按照前面的步驟新增資料、圖表配置...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // （添加數據和配置圖表的實現將在這裡）

        // 將工作簿儲存為 Excel 文件
        workbook.save("StyledChart.xlsx");
    }
}
```

**關鍵字建議：**
- “Aspose.Cells for Java”
- 《用 Java 建立 Excel 圖表》
- 《Java 程式設計實現 Excel 自動化》

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}