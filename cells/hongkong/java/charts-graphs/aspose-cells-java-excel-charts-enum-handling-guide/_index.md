---
date: '2026-04-11'
description: 學習如何顯示 Aspose Cells 版本、在 Java 中載入 Excel 工作簿，以及使用 Aspose.Cells 處理圖表列舉。跟隨一步一步的範例。
keywords:
- display aspose cells version
- load excel workbook java
- excel chart manipulation
title: 在 Java 中顯示 Aspose Cells 版本與圖表列舉處理
url: /zh-hant/java/charts-graphs/aspose-cells-java-excel-charts-enum-handling-guide/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 顯示 Aspose Cells 版本與圖表 Enum 處理於 Java

## 簡介

如果您需要 **顯示 Aspose Cells 版本**、在 Java 中載入 Excel 活頁簿，並處理圖表 Enum，您來對地方了。在本教學中，我們將逐步說明將 Aspose.Cells for Java 整合至您的專案、擷取圖表資料，以及將基於整數的 Enum 轉換為可讀的字串。完成後，您將擁有一個穩固、可直接投入程式碼庫的生產就緒解決方案。

**您將學會**
- 如何顯示 Aspose.Cells 版本。
- 如何 **在 Java 中載入 Excel 活頁簿** 並存取圖表資料。
- 如何將整數 Enum 值轉換為其字串等價物。
- 如何取得圖表點的 X 與 Y 值類型。

讓我們開始吧！

## 快速解答
- **如何檢查 Aspose.Cells 版本？** 呼叫 `CellsHelper.getVersion()` 並印出結果。  
- **哪個 Maven 坐標可加入 Aspose.Cells？** `com.aspose:aspose-cells:25.3`。  
- **我可以在 Java 中載入 Excel 活頁簿嗎？** 可以——使用 `new Workbook(filePath)`。  
- **Enum 值如何轉換？** 將 `HashMap<Integer, String>` 儲存起來，並以整數鍵查詢。  
- **哪個方法可印出 X/Y 值類型？** `pnt.getXValueType()` 與 `pnt.getYValueType()`。

## 何謂「顯示 Aspose Cells 版本」？
此詞語指的是取得函式庫的執行時版本字串。了解確切的版本有助於除錯、確保相容性，並確認您的授權已套用至目標版本。

## 為何要顯示版本並在 Java 中載入 Excel 活頁簿？
- **除錯** – 確認正確的函式庫已在 classpath 上。  
- **合規** – 輕鬆驗證您使用的是授權版本。  
- **自動化** – 讓腳本能依不同函式庫版本自動調整，無需手動變更。  

## 前置條件

### 必要的函式庫與相依性
- **Aspose.Cells for Java** – 用於 Excel 操作的核心函式庫。  
- **Java Development Kit (JDK)** – 版本 8 或以上。

### 環境設定
- 您偏好的 IDE（IntelliJ IDEA、Eclipse、NetBeans）。  
- 建置工具：Maven **或** Gradle（以下說明）。

### 所需知識
- 基本的 Java 程式設計。  
- 熟悉 Excel 概念（工作表、圖表）雖有幫助，但非必須。

## 設定 Aspose.Cells for Java

### Using Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Using Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 取得授權步驟
- **免費試用**：從 [Aspose's Release Page](https://releases.aspose.com/cells/java/) 下載。  
- **臨時授權**：於 [Aspose's Temporary License Page](https://purchase.aspose.com/temporary-license/) 取得短期授權。  
- **購買**：對於長期專案，透過 [Aspose Purchase Page](https://purchase.aspose.com/buy) 購買授權。

### 基本初始化與設定
```java
import com.aspose.cells.*;

public class InitializeAsposeCells {
    public static void main(String[] args) {
        // Set the license if available
        License license = new License();
        try {
            license.setLicense("Path_to_License_File");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Print Aspose.Cells version to confirm setup
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

## 實作指南

### 如何顯示 Aspose Cells 版本
**概述** – 快速在執行時驗證函式庫版本。

#### 步驟 1：匯入必要的套件
```java
import com.aspose.cells.*;
```

#### 步驟 2：建立類別與 main 方法
```java
public class DisplayAsposeCellsVersion {
    public static void main(String[] args) throws Exception {
        // This prints the Aspose.Cells version
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

#### 說明
- `CellsHelper.getVersion()` 會回傳您應用程式所使用的 Aspose.Cells DLL 的確切版本字串。

### 如何將整數 Enum 轉換為字串 Enum
**概述** – 將數值型 Enum（例如 `CellValueType.IS_NUMERIC`）轉換為可讀的文字。

#### 步驟 1：設定 HashMap 以進行轉換
```java
import java.util.HashMap;

HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### 步驟 2：轉換並印出 Enum 值
```java
public class EnumConversion {
    public static void main(String[] args) {
        int exampleEnumValue = CellValueType.IS_NUMERIC;
        System.out.println("Converted Enum Value: " + cvTypes.get(exampleEnumValue));
    }
}
```

#### 說明
- `cvTypes` 映射將數值常數與人類可讀的標籤對應起來。

### 如何在 Java 中載入 Excel 活頁簿並存取圖表資料
**概述** – 開啟現有活頁簿、定位圖表，並確保其資料為最新。

#### 步驟 1：匯入必要的套件
```java
import com.aspose.cells.*;
```

#### 步驟 2：載入活頁簿並存取工作表
```java
public class LoadExcelAndAccessChart {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();
    }
}
```

#### 說明
- `new Workbook(filePath)` 會將檔案載入記憶體。  
- `ch.calculate()` 會強制圖表重新計算任何公式，確保讀取的資料為最新。

### 如何取得並印出圖表點的 X 與 Y 值類型
**概述** – 取得特定點的 X 與 Y 值的資料類型。

#### 步驟 1：設定 Enum 轉換 HashMap（重複使用先前的設定）
```java
HashMap<Integer, String> cvTypes = new HashMap<>();
cvTypes.put(CellValueType.IS_NUMERIC, "IsNumeric");
cvTypes.put(CellValueType.IS_STRING, "IsString");
```

#### 步驟 2：存取圖表點並印出值類型
```java
public class RetrieveChartPointTypes {
    static String dataDir = "YOUR_DATA_DIRECTORY";

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook(dataDir + "/sampleFindTypeOfXandYValuesOfPointsInChartSeries.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Chart ch = ws.getCharts().get(0);
        ch.calculate();

        ChartPoint pnt = ch.getNSeries().get(0).getPoints().get(0);

        System.out.println("X Value Type: " + cvTypes.get(pnt.getXValueType()));
        System.out.println("Y Value Type: " + cvTypes.get(pnt.getYValueType()));
    }
}
```

#### 說明
- `pnt.getXValueType()` / `pnt.getYValueType()` 會回傳整數常數，指示該值是數字、字串、日期等。  
- `cvTypes` 映射將這些整數轉換為可讀的文字。

## 實務應用
1. **財務報告** – 自動產生具備驗證資料類型的圖表，以供稽核追蹤。  
2. **資料視覺化儀表板** – 將圖表點拉入自訂 UI 元件。  
3. **自動化測試** – 驗證圖表系列包含預期的資料類型。  
4. **商業智慧** – 將圖表中介資料輸入下游分析管線。  
5. **自訂報告工具** – 建構需要精確 Enum 處理的客製化報告引擎。

## 效能考量
- **僅載入必要工作表** – 處理大型檔案時，使用 `Workbook.getWorksheets().get(index)` 而非載入所有工作表。  
- **及時釋放物件** – 處理完畢後將活頁簿參考設為 `null`，協助垃圾回收。  
- **批次處理檔案** – 當處理大量活頁簿時，分批執行以保持記憶體使用可預測。

## 常見問題與解決方案
- **找不到授權** – 確認授權檔案路徑正確且已包含於建置輸出中。  
- **圖表未計算** – 在讀取點值前務必呼叫 `chart.calculate()`。  
- **Enum 映射錯誤** – 確認已將所有相關的 `CellValueType` 常數加入 `HashMap`。

## 常見問答

**Q: 我可以在 Aspose.Cells 24.x 上使用此程式碼嗎？**  
A: 可以，取得版本、載入活頁簿及存取圖表點的 API 在近期版本中保持穩定。

**Q: 如果我的圖表包含日期值該怎麼辦？**  
A: 將 `CellValueType.IS_DATE_TIME` 加入 `cvTypes` 映射，並對應為 `"IsDateTime"`。

**Q: 試用期間需要授權嗎？**  
A: 完整功能需要試用授權；若未使用授權，產生的檔案會出現浮水印。

**Q: 如何處理多個工作表？**  
A: 迭代 `wb.getWorksheets()`，對每個遇到的 `Chart` 物件進行處理。

**Q: 有辦法將圖表資料匯出為 CSV 嗎？**  
A: 有，透過 `chart.getNSeries().get(i).getValues()` 取得系列值，並使用標準 Java I/O 寫入檔案。

---

**Last Updated:** 2026-04-11  
**測試於:** Aspose.Cells 25.3 for Java  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}