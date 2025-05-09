---
"date": "2025-04-07"
"description": "了解如何使用 Aspose.Cells for Java 建立 Excel 工作簿並使用自訂資料填入工作簿。有效簡化您的工作流程。"
"title": "使用 Java 中的 Aspose.Cells 建立 Excel 工作簿&#58;逐步指南"
"url": "/zh-hant/java/getting-started/create-excel-workbook-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Java 中的 Aspose.Cells 建立 Excel 工作簿
## 逐步指南

### 介紹
您是否希望使用 Java 自動建立複雜的 Excel 工作簿？管理自訂資料和公式可能具有挑戰性，但藉助強大的 Aspose.Cells for Java 函式庫，這項任務變得簡單。本教學將指導您設定環境並實施使用 Aspose.Cells 建立填滿自訂資料項目的 Excel 工作簿的解決方案。

**您將學到什麼：**
- 在 Java 中定義和實例化使用者定義的類別。
- 使用自訂資料類別的實例填入 ArrayList。
- 使用 Aspose.Cells for Java 將這些資料匯入 Excel 工作簿，設定公式並儲存檔案。
- 處理大型資料集時優化效能的最佳實務。

在開始編碼之前，讓我們先回顧一下先決條件！

### 先決條件

#### 所需的庫和依賴項
為了繼續操作，您需要：
- **Java 開發工具包 (JDK)**：版本 8 或更高版本。
- **Aspose.Cells for Java**：請確保您已透過 Maven 或 Gradle 安裝了 25.3 版本。

#### 環境設定要求
確保您的 IDE 已設定必要的依賴項。使用以下任一建置工具來包含 Aspose.Cells：

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
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### 知識前提
您應該具備以下基本知識：
- Java 程式設計。
- 物件導向的概念，例如類別和物件。

### 設定 Aspose.Cells for Java
Aspose.Cells 提供了強大的 API 來操作 Excel 檔案。您可以按照以下方式開始：

1. **安裝 Aspose.Cells**：使用 Maven 或 Gradle（如上所示）將庫包含在您的專案中。
2. **許可證獲取**：
   - 從 [免費試用](https://releases。aspose.com/cells/java/).
   - 如需長期使用，請考慮購買 [臨時執照](https://purchase.aspose.com/temporary-license/) 或直接從 [Aspose 網站](https://purchase。aspose.com/buy).
3. **基本初始化**：首先建立一個新的 `Workbook` 物件並存取其第一個工作表：

```java
import com.aspose.cells.*;

public class WorkbookSetup {
    public static void main(String[] args) throws Exception {
        // 初始化工作簿
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        
        // 繼續資料填充和公式設定...
    }
}
```

### 實施指南

#### 建立和填入自訂資料項列表
要管理自訂數據，定義 `DataItems` 班級。該類別將把數值和公式儲存為字串。

```java
import java.util.ArrayList;

class DataItems {
    private int m_Number1;
    private int m_Number2;
    private String m_Formula1;
    private String m_Formula2;

    public DataItems(int num1, int num2, String form1, String form2) {
        this.m_Number1 = num1;
        this.m_Number2 = num2;
        this.m_Formula1 = form1;
        this.m_Formula2 = form2;
    }

    public int getNumber1() { return m_Number1; }
    public int getNumber2() { return m_Number2; }
    public String getFormula1() { return m_Formula1; }
    public String getFormula2() { return m_Formula2; }
}
```

##### 建立一個 ArrayList 來保存資料項
使用以下實例填充列表 `DataItems`。

```java
ArrayList<DataItems> dataItemList = new ArrayList<>();
dataItemList.add(new DataItems(2002, 3502, 
"=SUM(A2,B2)", "=HYPERLINK(\"https://www.aspose.com\"，\"Aspose 網站\")"));
dataItemList.add(new DataItems(2003, 3503,
 "=SUM(A3,B3)", 
"=HYPERLINK(\"https://www.aspose.com\"，\"Aspose 網站\")"));
// 根據需要添加更多項目...
```

#### 使用 Aspose.Cells 建立和操作 Excel 工作簿
現在您已經準備好數據，請使用 Aspose.Cells 將其匯入 Excel 工作簿。

##### 導入自訂對象
設定 `ImportTableOptions` 指定哪些列包含公式。然後，將清單匯入工作表：

```java
import com.aspose.cells.*;

String outDir = "YOUR_OUTPUT_DIRECTORY";

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
ImportTableOptions opts = new ImportTableOptions();

opts.setFormulas(new boolean[] {false, false, true, true }); // 指定公式列
ws.getCells().importCustomObjects(dataItemList, 0, 0, opts); 
wb.calculateFormula(); // 計算公式
ws.autoFitColumns(); // 調整列寬
```

##### 儲存工作簿
創建一個 `FileSaver` 處理保存的類別：

```java
class FileSaver {
    public void saveWorkbook(Workbook wb) throws Exception {
        wb.save(outDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
    }
}

// 用法
FileSaver saver = new FileSaver();
saver.saveWorkbook(wb);
```

### 實際應用
1. **財務報告**：透過將計算資料直接匯入Excel來自動產生財務報表。
2. **庫存管理**：使用自訂公式進行即時庫存追蹤和管理。
3. **專案規劃**：使用動態公式填入具有依賴關係的專案時間表。

Aspose.Cells 與其他系統順利集成，使您能夠自動化需要在 Java 應用程式和 Excel 檔案之間交換資料的工作流程。

### 性能考慮
- **優化數據處理**：對於大型資料集，透過管理物件生命週期確保高效的記憶體使用。
- **批次處理**：分批處理數據而不是一次處理所有數據，以減少記憶體負載。
- **公式計算**： 使用 `wb.calculateFormula()` 明智地；僅計算必要的公式。

### 結論
透過遵循本指南，您現在可以使用 Aspose.Cells for Java 建立並使用自訂資料填入 Excel 工作簿的強大解決方案。這種設定不僅提高了生產力，而且還提供了以程式設計方式管理複雜資料集的靈活性。

**後續步驟**：深入探索 Aspose.Cells 的更多進階功能 [文件](https://reference.aspose.com/cells/java/)。嘗試不同的資料結構和公式來客製化滿足您特定需求的解決方案。

### 常見問題部分
1. **如何自訂輸出 Excel 檔案的格式？**
   - 使用 `wb.getWorksheets().get(0).setSheetName("Custom Name")` 透過 Aspose.Cells API 更改工作表名稱或調整樣式。
2. **如果我的公式計算不正確怎麼辦？**
   - 確保您的 `ImportTableOptions` 正確配置了 `opts.setFormulas()`。驗證資料項中的公式語法。
3. **我可以使用此設定進行大規模資料處理嗎？**
   - 是的，但請考慮優化記憶體使用並利用批次技術來提高效率。
4. **是否可以為工作簿新增圖表？**
   - 絕對地！ Aspose.Cells 支援建立和管理圖表。檢查他們的 [API 文件](https://reference.aspose.com/cells/java/) 有關圖表集成的指導。
5. **儲存工作簿時有哪些常見問題？**
   - 確保您的 `outDir` 路徑正確且您對該目錄具有寫入權限。在保存邏輯中正確處理異常。

### 資源
- [文件](https://reference.aspose.com/cells/java/)
- [下載 Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [購買選項](https://purchase.aspose.com/buy)
- [免費試用](https://releases.aspose.com/cells/java/)
- [臨時執照](https://purchase.aspose.com/temporary-license/)
- [支援論壇](https://forum.aspose.com/c/cells)

### 關鍵字推薦
- “Aspose.Cells for Java”
- “Excel 工作簿自動化”
- “Java Excel 整合”


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}