---
"date": "2025-04-07"
"description": "了解如何使用 Aspose.Cells for Java 在 Excel 中建立和自訂圓餅圖。請按照本逐步指南來增強您的資料視覺化技能。"
"title": "使用 Aspose.Cells for Java 在 Excel 中建立餅圖&#58;綜合指南"
"url": "/zh-hant/java/charts-graphs/master-pie-chart-creation-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for Java 在 Excel 中建立圓餅圖
## 介紹
在 Excel 中創建引人入勝且資訊豐富的餅圖可以將原始數據轉化為強大的見解，使您能夠迅速做出明智的業務決策。您是否在使用 Microsoft Excel 的內建功能時遇到困難，或者尋求與您的 Java 應用程式無縫整合的可擴展解決方案？ Aspose.Cells for Java 可以為您提供協助。

本教學將指導您使用 Aspose.Cells for Java 在 Excel 檔案中建立和自訂圓餅圖。了解如何有效率地新增資料、配置圖表元素以及完成工作簿—所有操作都輕鬆且精確。

**您將學到什麼：**
- 設定並使用 Aspose.Cells for Java
- 建立新工作簿並用範例資料填充
- 在 Excel 工作表中新增和自訂圓餅圖
- 圖表配置和優化的最佳實踐

讓我們先介紹一下先決條件。
## 先決條件
在開始之前，請確保您已具備以下條件：
### 所需的函式庫、版本和相依性
請確保使用 Maven 或 Gradle 的專案中包含 Aspose.Cells for Java 版本 25.3 或更高版本。
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
- 整合開發環境 (IDE)，例如 IntelliJ IDEA、Eclipse 或 NetBeans。
### 知識前提
對 Java 程式設計有基本的了解並且熟悉 Excel 文件結構將會很有幫助。
## 設定 Aspose.Cells for Java
Aspose.Cells 是一個功能強大的函式庫，可讓開發人員在 Java 應用程式中建立、修改和呈現 Excel 電子表格。設定方法如下：
1. **安裝**：如上所示新增 Maven 或 Gradle 相依性。
2. **許可證獲取**：
   - 取得免費試用許可證，用於初步測試 [Aspose 免費試用](https://releases。aspose.com/cells/java/).
   - 申請臨時許可證，以無限制測試全部功能 [臨時執照](https://purchase。aspose.com/temporary-license/).
3. **基本初始化**：先創建一個 `Workbook` 類，代表您的 Excel 文件。
```java
import com.aspose.cells.Workbook;
// 建立並初始化新工作簿
String dataDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook();
```
## 實施指南
現在，讓我們逐步實現每個功能來建立具有圓餅圖的 Excel 工作簿。
### 1. 建立並初始化工作簿
**概述**：我們首先初始化我們的 `Workbook` 物件並存取其第一個工作表，我們將在其中添加資料和圖表。
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY";
// 建立新的工作簿實例
Workbook workbook = new Workbook();
// 訪問工作簿中的第一個工作表
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
```
### 2.向單元格添加範例數據
**概述**：使用將在餅圖中顯示的範例資料填入您的工作表。
```java
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

Cells cells = sheet.getCells();
// 在 A 欄位中新增國家名稱
Cell cell = cells.get("A1");
cell.setValue("Italy");
cell = cells.get("A2");
cell.setValue("Germany");
// 繼續前往其他國家...
// 在B列中新增對應的銷售數據
cell = cells.get("B1");
cell.setValue(10000);
cell = cells.get("B2");
cell.setValue(20000);
// 繼續取得其餘數據...
```
### 3. 在工作表上新增圓餅圖
**概述**：使用預先定義的資料範圍將餅圖插入工作表。
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

ChartCollection charts = sheet.getCharts();
// 在指定位置和大小添加圓餅圖
int chartIndex = charts.add(ChartType.PIE, 15, 4, 40, 15);
Chart chart = charts.get(chartIndex);
```
### 4.配置圖表系列
**概述**：定義銷售和類別資料（國家名稱）的資料範圍，以確保餅圖準確地代表您的資料集。
```java
import com.aspose.cells.SeriesCollection;

SeriesCollection serieses = chart.getNSeries();
// 將銷售數據設定為圖表的資料來源
serieses.add("B1:B8", true);
// 指定類別資料（國家名稱）
serieses.setCategoryData("A1:A8");
// 為每個圓餅圖切片啟用不同的顏色
serieses.setColorVaried(true);

// 為了清晰起見，在圖表上顯示數據表
chart.setShowDataTable(true);
```
### 5.設定圖表標題和樣式
**概述**：自訂圖表的標題以增強可讀性和簡報效果。
```java
import com.aspose.cells.Color;

// 使用樣式選項設定圖表標題
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```
### 6. 配置圖表系列的資料標籤
**概述**：為每個圓餅圖切片加上資料標籤，提供清晰的數值細分。
```java
import com.aspose.cells.DataLabels;
import com.aspose.cells.LabelPositionType;

for (int i = 0; i < serieses.getCount(); i++) {
    DataLabels datalabels = serieses.get(i).getDataLabels();
    // 將標籤放置在每個圓餅圖切片的底部
    datalabels.setPosition(LabelPositionType.INSIDE_BASE);
    // 配置標籤顯示選項
    datalabels.setShowCategoryName(true);
    datalabels.setShowValue(true);
    datalabels.setShowPercentage(false);
    datalabels.setShowLegendKey(true);
}
```
### 7.保存工作簿
**概述**：完成 Excel 文件，將所有資料和圖表儲存到磁碟。
```java
import com.aspose.cells.SaveFormat;

String outDir = "YOUR_OUTPUT_DIRECTORY";
// 將工作簿儲存為 Excel 文件
workbook.save(outDir + "/HTCPChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
## 實際應用
- **商業分析**：在銷售報告中使用圓餅圖來直觀地顯示各地區的市場份額或收入分佈。
- **教育工具**：建立顯示統計資料分佈的互動式學習模組。
- **專案管理**：向利害關係人直觀地展示資源分配和預算利用。
## 性能考慮
為了優化性能：
- 透過有效管理工作簿大小來最大限度地減少記憶體使用量。
- 如果處理大量資料集，請利用 Aspose.Cells 的功能，例如串流大檔案。
- 遵循 Java 的記憶體管理最佳實踐，確保資源在使用後得到適當釋放。
## 結論
透過遵循本指南，您學會了使用 Aspose.Cells for Java 在 Excel 中建立、配置和自訂圓餅圖。這個強大的程式庫使開發人員能夠將高級電子表格功能無縫地整合到他們的 Java 應用程式中。
為了進一步探索，請考慮研究其他圖表類型或使用 Aspose.Cells 提供的附加功能來擴展您的資料處理能力。
## 常見問題部分
1. **我可以免費使用 Aspose.Cells 嗎？**
   - 是的，可以免費試用。為了不受限制地存取全部功能，您可以申請臨時許可證。
2. **是否可以使用 Aspose.Cells 建立其他圖表類型？**
   - 絕對地！您可以透過調整 `ChartType`。
3. **如何使用 Java 處理 Excel 中的大型資料集？**
   - 使用高效的資料載入技術並考慮對非常大的檔案進行串流傳輸。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}