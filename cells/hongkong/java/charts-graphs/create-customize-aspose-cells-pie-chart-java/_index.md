---
"date": "2025-04-08"
"description": "學習使用 Aspose.Cells for Java 建立和自訂餅圖。為開發人員提供帶有程式碼範例的逐步指南。"
"title": "掌握 Aspose.Cells'使用 Java 建立和自訂餅圖"
"url": "/zh-hant/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 掌握 Aspose.Cells：使用 Java 建立和自訂餅圖

## 介紹
在 Excel 中處理資料視覺化時，建立視覺上吸引人的圖表是一項常見要求。無論您是展示人口統計資訊還是分析市場趨勢，圓餅圖都能提供一種清晰的方式來表示比例數據。但是，以程式設計方式設定這些圖表可能很複雜。本教學將指導您使用 Java 建立和自訂 Aspose.Cells 圓餅圖，簡化開發人員的流程。

**您將學到什麼：**
- 使用 Aspose.Cells for Java 設定您的環境。
- 建立新工作簿並存取工作表儲存格。
- 將資料填入特定單元格以準備建立圖表。
- 根據該數據產生餅圖。
- 自訂餅圖的外觀，包括顏色、標題和圖例。

在深入研究之前，請確保您對 Java 程式設計和 Maven 或 Gradle 依賴管理有一些基本的了解。讓我們設定我們的環境！

## 先決條件
要學習本教程，您需要：
- **Java 開發工具包 (JDK)**：版本 8 或更高版本。
- **整合開發環境 (IDE)**：例如 IntelliJ IDEA 或 Eclipse。
- **依賴管理**：使用 Maven 或 Gradle 來管理您的依賴項。

### 所需的庫和依賴項
確保使用 Maven 或 Gradle 將 Aspose.Cells for Java 包含在您的專案中。

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 許可證取得步驟
Aspose.Cells for Java 是一個商業庫，但您可以先免費試用或申請臨時許可證。訪問 [購買頁面](https://purchase.aspose.com/buy) 探索許可證選項。

## 設定 Aspose.Cells for Java
首先，確保您的專案環境包含必要的程式庫，方法是透過 Maven 或 Gradle 新增它們，如上所示。一旦包含，您就可以初始化 Aspose.Cells：

```java
import com.aspose.cells.Workbook;

// 初始化新的工作簿實例
Workbook workbook = new Workbook();
```

## 實施指南

### 建立和配置工作簿
建立工作簿是您設定資料的初始步驟。

#### 導入庫
確保這些導入包含在文件頂部：

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

#### 步驟 1：建立工作簿實例
```java
// 建立一個空的工作簿實例以供使用。
Workbook workbook = new Workbook();
```
此步驟以程式設計方式初始化您的 Excel 文件，讓您可以使用 Aspose.Cells 功能對其進行操作。

### 存取或修改工作表單元格
接下來，將資料填入將用於餅圖的工作表儲存格中。

#### 步驟 2：存取工作表及其儲存格
```java
// 存取工作簿中的第一個工作表。
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// 將圓餅圖使用的樣本值放入特定儲存格。
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// 將圓餅圖的百分比值放入特定的儲存格中。
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
在這裡，您可以用代表餅圖不同部分的資料填入工作表。

### 創建圓餅圖

#### 步驟 3：在工作表上新增圓餅圖
```java
// 在工作表中建立餅圖。
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
此步驟將新的圓餅圖依指定位置和尺寸新增至工作表。

### 配置圓餅圖系列和數據

#### 步驟 4：設定圖表的系列
```java
// 配置圖表的系列資料範圍。
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// 將餅圖標題連結到包含標題文字的儲存格。
pie.getTitle().setLinkedSource("D2");
```
此程式碼連結您的資料範圍並設定餅圖的系列。

### 配置圖表圖例和標題外觀

#### 步驟 5：自訂圖表圖例與標題
```java
// 設定圖表底部的圖例位置。
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// 設定圖表標題的字體屬性。
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
自訂外觀可增強可讀性和視覺吸引力。

### 自訂圖表系列顏色

#### 步驟 6：更改圓餅圖各部分的顏色
```java
import com.aspose.cells.Color;

// 存取並自訂各個餅圖部分的顏色。
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
這些設定可個性化您的圖表以適應特定的配色方案。

### 自動調整列並儲存工作簿

#### 步驟 7：調整列寬並儲存文件
```java
// 自動調整所有列。
worksheet.autoFitColumns();

// 定義用於保存工作簿的輸出目錄佔位符路徑。
String outDir = "YOUR_OUTPUT_DIRECTORY";

// 將修改後的工作簿儲存為指定目錄中的 Excel 檔案。
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
最後，自動調整列並儲存您的工作簿。

## 實際應用
1. **人口統計分析**：使用圓餅圖顯示不同國家或地區的人口分佈。
2. **市佔率報告**：說明某一產業內不同公司的市佔率。
3. **預算分配**：直觀地了解組織內各部門之間的預算分配。

這些應用程式展示了 Aspose.Cells 在現實場景中的多功能性和實用性。

## 性能考慮
為了優化使用 Aspose.Cells 時的效能：
- 透過處理不再需要的物件來最大限度地減少記憶體使用。
- 使用高效的資料結構來處理大型資料集。
- 分析您的應用程式以識別瓶頸。

遵循最佳實務可確保應用程式順暢且反應迅速。

## 結論
本教學將引導您完成使用 Java 中的 Aspose.Cells 建立和自訂餅圖的步驟。有了這些知識，您現在可以將這些技術應用到專案中的各種資料視覺化任務中。為了進一步探索，請考慮深入了解 Aspose.Cells 提供的其他圖表類型和進階自訂選項。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}