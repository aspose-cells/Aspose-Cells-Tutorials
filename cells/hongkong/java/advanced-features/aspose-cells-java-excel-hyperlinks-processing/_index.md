---
date: '2026-02-24'
description: 學習如何使用 Aspose.Cells for Java 從 Excel 中提取超連結，包括載入工作簿、讀取 Excel 超連結以及批量處理
  Excel 檔案。
keywords:
- Aspose.Cells Java
- Excel Hyperlink Management
- Aspose.Cells for Java setup
title: 從 Excel 中提取超連結 – Aspose Cells 工作簿載入
url: /zh-hant/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 中提取超連結 – 進階 Excel 超連結管理

在當今以資料為驅動的世界，**extracting hyperlinks from excel** 能快速且可靠地完成，是所有自動化 Excel 報表的使用者的核心需求。無論您是要建立財務儀表板、資料遷移工具，或是文件產生服務，處理充斥超連結的活頁簿都是常見的挑戰。在本教學中，您將學會如何載入 Excel 活頁簿、存取工作表，並使用 Aspose.Cells for Java **retrieve hyperlinks from excel**。完成後，您即可將超連結處理整合到自己的應用程式，甚至 **batch process excel files** 以因應大規模情境。

## 快速解答
- **開啟活頁簿的主要類別是什麼？** `Workbook`
- **哪個方法會回傳範圍內的所有超連結？** `Range.getHyperlinks()`
- **基本的超連結擷取需要授權嗎？** 免費試用版可使用，但授權會移除評估限制。
- **能有效率地處理大型檔案嗎？** 可以——只聚焦特定工作表或範圍。
- **支援哪些 Java 版本？** Java 8 及更新版本。

## 什麼是 “extract hyperlinks from excel”？
從 Excel 中提取超連結是指讀取儲存格內的連結資訊，例如 URL、檔案路徑、電子郵件地址或內部儲存格參照。Aspose.Cells 提供簡易的 API，讓您在不開啟 Excel 的情況下列舉這些連結。

## 為什麼要從 Excel 取得超連結？
超連結常指向外部資料來源、文件或內部參照。提取它們可以讓您：
- 自動驗證連結的可用性。
- 在資料遷移期間重新寫入或遷移 URL。
- 產生所有連結資源的彙總報表。
- 建立可搜尋的索引，以整合知識庫。

## 前置需求

- **Aspose.Cells for Java** 函式庫（25.3 版或更新）
- Java 8 + 以及 IDE（IntelliJ IDEA、Eclipse 等）
- Maven 或 Gradle 進行相依管理
- 有效的 Aspose.Cells 授權（試用版為選用）

### 設定 Aspose.Cells for Java

使用 Maven 或 Gradle 將函式庫加入專案。

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

> **專業提示：** 保持函式庫版本為最新，可獲得效能提升與新超連結處理功能。

#### 基本初始化

相依加入後，建立簡易的 Java 類別，以驗證活頁簿能正確載入。

```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        // License license = new License();
        // license.setLicense("path/to/license/file");

        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

### 步驟實作

以下示範三個核心功能：載入活頁簿、存取工作表與範圍，最後取得並處理超連結。

## 如何從 Excel 中提取超連結 – 載入活頁簿

### 載入活頁簿（功能 1）

```java
import com.aspose.cells.Workbook;

public class FeatureLoadWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## 如何從 Excel 中提取超連結 – 存取工作表與範圍

### 存取工作表與範圍（功能 2）

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Range;

public class FeatureAccessWorksheetAndRange {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");

        // Access the first worksheet in the workbook (index 0).
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Create a range from cell A1 to A7 within the worksheet.
        Range range = worksheet.getCells().createRange("A1", "A7");
        
        System.out.println("Range created successfully!");
    }
}
```

## 如何從 Excel 中提取超連結 – 取得與處理超連結

### 取得與處理超連結（功能 3）

```java
import com.aspose.cells.Range;
import com.aspose.cells.Hyperlink;
import com.aspose.cells.TargetModeType;

public class FeatureRetrieveAndProcessHyperlinks {
    public static void main(String[] args) throws Exception {
        // Assume 'range' is obtained as shown in previous examples.
        Range range = null;  // Placeholder, replace with actual range initialization

        // Retrieve all hyperlinks within the specified range.
        Hyperlink[] hyperlinks = range.getHyperlinks();

        // Iterate over each hyperlink and process it to determine its type.
        for (Hyperlink link : hyperlinks) {
            String displayText = link.getTextToDisplay();
            int linkType = link.getLinkType();
            System.out.println(displayText + ": " + getLinkTypeName(linkType));
        }
    }

    // Helper method to convert hyperlink type integer to a human‑readable string.
    private static String getLinkTypeName(int linkType) {
        switch (linkType) {
            case TargetModeType.EXTERNAL:
                return "EXTERNAL";
            case TargetModeType.FILE_PATH:
                return "FILE_PATH";
            case TargetModeType.EMAIL:
                return "EMAIL";
            default:
                return "CELL_REFERENCE";
        }
    }
}
```

### 實務應用

| 使用情境 | 好處 |
|----------|------|
| **資料驗證** | 在發佈報表前，自動驗證每個超連結是否可達。 |
| **自動化** | 在遷移至新資料倉儲時，提取連結並即時更新參照。 |
| **報表** | 建立彙總工作表，列出活頁簿中所有外部資源。 |

### 效能考量

- **僅處理必要的範圍** – 限制範圍可減少記憶體使用。
- **釋放物件** – 使用完畢後將 `workbook = null;`，讓 JVM 垃圾回收機制回收記憶體。
- **批次處理** – 處理多個檔案時，盡可能重複使用單一 `Workbook` 實例，以提升 **batch process excel files** 效率。

## 常見問題與解決方案

| 問題 | 解決方案 |
|------|----------|
| **`range` 為 null** | 確認在呼叫 `getHyperlinks()` 前已正確建立範圍。 |
| **缺少授權** | 試用版可用於開發，授權版會移除評估限制並提升效能。 |
| **不支援的超連結類型** | 使用 `TargetModeType` 常數，隨 Aspose 更新處理新類型。 |

## 常見問答

**Q: Aspose.Cells 支援哪些 Java 版本？**  
A: Aspose.Cells for Java 支援 Java 8 及更新版本，請確保您的 JDK 符合此需求。

**Q: 能否在不耗盡記憶體的情況下，從極大型 Excel 檔案提取超連結？**  
A: 可以。僅載入所需的工作表或範圍，避免一次載入整本活頁簿。

**Q: 生產環境是否必須購買授權才能提取超連結？**  
A: 試用版可供實驗使用，商業授權則會移除評估限制並提供完整支援。

**Q: 如何處理指向電子郵件地址的超連結？**  
A: `TargetModeType.EMAIL` 常數可辨識電子郵件連結，您可依需求單獨處理。

**Q: Aspose.Cells 在儲存時會保留超連結的格式嗎？**  
A: 會的。所有超連結屬性（顯示文字、提示文字、位址）在儲存活頁簿時皆會被保留。

**Q: 我可以在批次工作中使用 Aspose.Cells **read excel hyperlinks** 嗎？**  
A: 可以——將 API 與檔案迴圈結合，即可在多本活頁簿中批次讀取 Excel 超連結。

**Q: 在高吞吐量情境下，最佳的 **load excel workbook java** 方法是什麼？**  
A: 盡可能重複使用單一 `Workbook` 實例，並即時關閉串流以釋放資源。

---

**最後更新：** 2026-02-24  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

如有其他問題，歡迎造訪 [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}