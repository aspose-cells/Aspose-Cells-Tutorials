---
"date": "2025-04-08"
"description": "Aspose.Words Java 程式碼教程"
"title": "Aspose.Cells Java&#58;建立和自訂圖表"
"url": "/zh-hant/java/charts-graphs/aspose-cells-java-create-customize-charts/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 掌握使用 Aspose.Cells Java 建立和客製化圖表

在當今數據驅動的世界中，視覺化複雜數據集對於做出明智的決策至關重要。無論您是經驗豐富的開發人員還是剛起步，在應用程式中建立引人注目的圖表都可以顯著增強使用者體驗。本教學將引導您使用 Aspose.Cells for Java 輕鬆建立和自訂圖表的過程。

## 您將學到什麼

- 如何設定 Aspose.Cells for Java
- 建立和命名工作表
- 用資料填充儲存格
- 新增圖表表並建立長條圖
- 使用圖像、標題和系列配置自訂圖表
- 儲存工作簿

透過這些步驟，您將能夠立即製作出具有視覺吸引力的圖表。

## 先決條件

在深入研究 Aspose.Cells for Java 之前，請確保您已：

- **Java 開發工具包 (JDK) 8 或更高版本** 安裝在您的機器上。
- 對Java程式設計有基本的了解，熟悉Excel操作。
  
### 所需庫

若要開始使用 Aspose.Cells，請在專案管理工具中包含下列相依性。

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

### 許可證獲取

Aspose 提供免費試用，讓您在購買之前測試該庫的全部功能。您還可以獲得臨時許可證以進行廣泛的測試。

- **免費試用**： [免費下載](https://releases.aspose.com/cells/java/)
- **臨時執照**： [在此請求](https://purchase.aspose.com/temporary-license/)

## 設定 Aspose.Cells for Java

準備好環境後，透過創建新的 `Workbook` 實例。這將作為我們圖表創建之旅的基礎。

```java
import com.aspose.cells.Workbook;

// 初始化新的工作簿
Workbook workbook = new Workbook();
```

## 實施指南

### 1. 建立並命名工作表

#### 概述
首先設定數據表，它將保存圖表所需的所有數據。

#### 步驟：

**建立新工作簿**
```java
import com.aspose.cells.Worksheet;

// 建立新的工作簿實例
Workbook workbook = new Workbook();
```

**命名工作表**

```java
// 存取第一個工作表並將其名稱設為“資料”
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. 用資料填充儲存格

#### 概述
在工作表中填寫資料對於創建有意義的圖表至關重要。

#### 步驟：

**訪問細胞集合**

```java
import com.aspose.cells.Cells;

// 從「資料」表中取得儲存格集合
Cells cells = sheet.getCells();
```

**插入數據**

```java
// 插入地區名稱和銷售數字
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. 新增圖表表

#### 概述
新增專用圖表表以將資料和視覺化分開。

#### 步驟：

**建立圖表表**

```java
import com.aspose.cells.SheetType;

// 新增圖表表
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// 將工作表命名為“圖表”
chartSheet.setName("Chart");
```

### 4.創建圖表

#### 概述
產生長條圖來按地區直觀顯示銷售數據。

#### 步驟：

**建立長條圖**

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// 在「圖表」表中新增新的長條圖
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. 設定圖片作為圖表繪圖區的背景填充

#### 概述
透過添加背景圖像來增強圖表的視覺吸引力。

#### 步驟：

**設定影像數據**

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

### 6.配置圖表標題和系列

#### 概述
使用標題、系列資料和圖例定位自訂圖表。

#### 步驟：

**設定圖表標題**

```java
// 配置圖表的標題屬性
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

**配置系列數據**

```java
// 設定圖表的系列和類別數據
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// 將圖例放置在圖表頂部
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 7.保存工作簿

#### 概述
透過匯出工作簿確保您的所有辛勤工作都得到保存。

#### 步驟：

**儲存工作簿**

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## 實際應用

- **商業報告**：建立動態銷售和績效報告。
- **數據分析工具**：增強分析軟體中的資料視覺化。
- **儀表板集成**：將圖表整合到儀表板中以進行即時更新。

## 性能考慮

- 透過最小化對大型資料集的操作次數來進行最佳化。
- 透過及時處理未使用的物件來有效地管理記憶體。

## 結論

現在，您已經掌握了使用 Java 中的 Aspose.Cells 建立和自訂圖表。若要繼續您的旅程，請探索更多功能，例如動態資料範圍或不同圖表類型。 

## 常見問題部分

1. **如何為圖表新增多個系列？**
   - 使用 `add` 方法 `NSeries` 具有多個範圍。

2. **我可以自訂圖表的軸標籤嗎？**
   - 是的，使用存取和配置軸 `chart.getCateg或者yAxis()` or `chart。getValueAxis()`.

3. **如果我的圖像檔案沒有在繪圖區域正確顯示怎麼辦？**
   - 確保檔案路徑正確且影像格式受 Aspose.Cells 支援。

4. **如何有效處理大型資料集？**
   - 考慮分塊讀取資料並逐步更新儲存格。

5. **是否可以將圖表匯出為 PDF 或 PNG 等其他格式？**
   - 是的，使用 `workbook.save()` 針對不同的格式使用適當的檔案副檔名。

## 資源

- [Aspose.Cells文檔](https://reference.aspose.com/cells/java/)
- [下載 Aspose.Cells](https://releases.aspose.com/cells/java/)
- [購買許可證](https://purchase.aspose.com/buy)
- [免費試用](https://releases.aspose.com/cells/java/)
- [臨時許可證申請](https://purchase.aspose.com/temporary-license/)
- [支援論壇](https://forum.aspose.com/c/cells/9)

透過遵循本指南，您將能夠輕鬆地使用 Aspose.Cells 在 Java 應用程式中建立和自訂圖表。編碼愉快！

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}