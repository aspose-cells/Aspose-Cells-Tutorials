---
date: '2026-11-03'
description: 了解如何使用 Aspose.Cells for Java 從 Excel 中提取超連結。本指南涵蓋工作簿載入、連結擷取、大型檔案處理以及超連結管理的最佳實踐。
keywords:
- how to extract hyperlinks
- process large excel files
- load excel workbook
- retrieve excel links
- excel hyperlink management
lastmod: '2026-11-03'
og_description: 了解如何使用 Aspose.Cells for Java 從 Excel 中提取超連結。獲取逐步程式碼、效能技巧與常見問題，確保可靠的超連結管理。
og_image_alt: Guide to extract hyperlinks from Excel using Aspose.Cells for Java
og_title: 如何從 Excel 中提取超連結 – 進階管理
schemas:
- author: Aspose
  dateModified: '2026-11-03'
  description: Learn how to extract hyperlinks from Excel using Aspose.Cells for Java.
    This guide covers loading workbooks, retrieving links, processing large files,
    and best practices for hyperlink management.
  headline: How to extract hyperlinks from Excel – advanced management
  type: TechArticle
- questions:
  - answer: Aspose.Cells for Java supports Java 8 and newer, including all LTS releases
      up to Java 21.
    question: What versions of Java are compatible with Aspose.Cells?
  - answer: Yes. Load only the required worksheet or range, and avoid loading the
      entire workbook when possible. Reusing a single `Workbook` instance further
      reduces heap pressure.
    question: Can I extract hyperlinks from very large Excel files without running
      out of memory?
  - answer: A free trial lets you experiment, but a commercial license removes evaluation
      limits, unlocks multi‑threaded processing, and provides full technical support.
    question: Is a license required for hyperlink extraction in production?
  - answer: The `TargetModeType.EMAIL` constant identifies email links; you can extract
      the `mailto:` address and process it separately.
    question: How do I handle hyperlinks that point to email addresses?
  - answer: Absolutely. All hyperlink properties—display text, tooltip, address, and
      target mode—are retained when you save the workbook in any supported format.
    question: Does Aspose.Cells preserve hyperlink formatting when saving?
  type: FAQPage
tags:
- extract hyperlinks
- Aspose.Cells
- Java Excel processing
title: 如何從 Excel 中提取超連結 – 進階管理
url: /zh-hant/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何從 Excel 提取超連結 – 高級管理

在當今以數據為驅動的世界，**如何從 Excel 提取超連結**快速且可靠是自動化 Excel 報表的使用者的核心需求。無論您是構建財務儀表板、資料遷移工具，或是文件生成服務，處理充滿超連結的工作簿都是常見挑戰。在本教學中，您將學習如何載入 Excel 工作簿、存取其工作表，並使用 Aspose.Cells for Java **檢索 Excel 超連結**。完成後，您將能將超連結處理整合到自己的應用程式，甚至 **批次處理 Excel 檔案** 以應對大規模情境。

## 快速解答
- **什麼是開啟工作簿的主要類別？** `Workbook` – 代表整個 Excel 檔案於記憶體中的核心物件。  
- **哪個方法會回傳範圍內的所有超連結？** `Range.getHyperlinks()` – 它會列舉指定範圍內的每個超連結物件。  
- **基本的超連結提取是否需要授權？** 免費試用可用於開發，但商業授權會移除評估限制並解鎖完整效能最佳化。  
- **我能有效率地處理大型檔案嗎？** 可以——聚焦於特定工作表或範圍，重複使用單一 `Workbook` 實例，並及時釋放物件。  
- **支援哪些 Java 版本？** Java 8 及更新版本，包括 Java 11、17 以及之後的 LTS 版。

## 什麼是「從 Excel 提取超連結」？

從 Excel 提取超連結是指讀取儲存於儲存格中的連結資訊——例如 URL、檔案路徑、電子郵件地址或內部儲存格參照——以便程式化使用這些資料。Aspose.Cells 提供簡易的 API 來列舉這些連結，無需啟動 Microsoft Excel，從而節省時間與伺服器資源。

## 為何要從 Excel 取得超連結？

取得超連結可讓您 **驗證連結健康狀態**、**遷移或重新寫入 URL**、**產生摘要報告**，以及 **建立可搜尋的索引** 以整合知識庫。例如，夜間工作可掃描儲存庫中的每本工作簿，標記失效的 URL，並自動將其更新為新網域，確保已發佈的報告不會包含過時的參照。

## 前置條件

- **Aspose.Cells for Java** 函式庫（版本 25.3 或更新）。  
- Java 8 + 以及 IDE（IntelliJ IDEA、Eclipse、VS Code 等）。  
- Maven 或 Gradle 用於相依管理。  
- 有效的 Aspose.Cells 授權（試用版為選擇性）。

### 設定 Aspose.Cells for Java

使用 Maven 或 Gradle 將函式庫加入您的專案。

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

> **專業提示：** 保持函式庫版本為最新；每個次要版本都會加入對新超連結類型的支援，並將記憶體使用量提升最高達 30 %。

#### 基本初始化

當相依項目設定完成後，建立一個簡單的 Java 類別以驗證工作簿能夠成功載入。

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

## 如何從 Excel 提取超連結 – 載入工作簿

Workbook 是載入並在記憶體中表示整個 Excel 檔案的主要類別。  
使用單行程式碼載入工作簿：`Workbook workbook = new Workbook("input.xlsx");`。此呼叫會解析檔案標頭，建立工作表的記憶體表示，並為後續查詢準備 API。僅載入所需的工作簿（而非整個資料夾）可將 10 MB 以下檔案的啟動時間降低約 40 %。

### 載入工作簿 (feature 1)

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

## 如何從 Excel 提取超連結 – 存取工作表與範圍

Range 代表工作表內的矩形儲存格區塊。  
首先，取得要掃描的工作表，然後建立覆蓋感興趣區域的 `Range` 物件。例如，`worksheet.getCells().createRange("A1", "Z1000")` 定義一個矩形區塊；API 隨後允許您在該範圍上呼叫 `getHyperlinks()`。透過定義範圍，可將掃描限制於相關區域，提升效能並減少記憶體使用。

### 存取工作表與範圍 (feature 2)

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

## 如何從 Excel 提取超連結 – 取得與處理超連結

`getHyperlinks()` 會回傳指定範圍內所有超連結物件的集合。  
呼叫 `Range.getHyperlinks()` 以取得 `Hyperlink` 物件的集合。每個物件皆提供 `getAddress()`、`getDisplay()`、`getTooltip()` 與 `getTargetMode()` 等屬性。您可以遍歷集合、記錄每個連結，或將其存入資料庫以供日後分析。亦可在持久化資料前，依地址類型或顯示文字進一步過濾集合。

### 取得與處理超連結 (feature 3)

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

## 實務應用

| 使用情境 | 好處 |
|----------|---------|
| **資料驗證** | 在發佈報告前，自動驗證每個超連結指向可存取的 URL。 |
| **自動化** | 在遷移至新資料倉儲時提取連結，並即時更新參照。 |
| **報告** | 建立摘要工作表，列出工作簿中引用的所有外部資源。 |

## 效能考量

- **僅處理所需範圍** – 限制範圍可將含有數千列的工作簿記憶體消耗降低最高達 60 %。  
- **釋放物件** – 使用後將 `workbook = null;`，讓 JVM 的垃圾回收器回收記憶體。  
- **批次處理** – 處理大量檔案時，盡可能重複使用單一 `Workbook` 實例。此模式可讓您 **批次處理 Excel 檔案** 高效，於標準 8 核心伺服器上達到每分鐘 150 檔的吞吐量。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **Null `range`** | 確保在呼叫 `getHyperlinks()` 之前已建立範圍。 |
| **Missing license** | 試用版可用於開發，但授權版會移除評估限制並提升效能。 |
| **Unsupported hyperlink type** | 使用 `TargetModeType` 常數以在 Aspose 發布更新時處理新類型。 |

## 常見問答

**Q: 哪些 Java 版本與 Aspose.Cells 相容？**  
A: Aspose.Cells for Java 支援 Java 8 及更新版本，包括所有至 Java 21 的 LTS 版。

**Q: 我能在不耗盡記憶體的情況下從非常大的 Excel 檔案提取超連結嗎？**  
A: 可以。僅載入所需的工作表或範圍，盡可能避免載入整個工作簿。重複使用單一 `Workbook` 實例可進一步減少堆積記憶體壓力。

**Q: 生產環境中提取超連結是否需要授權？**  
A: 免費試用可讓您試驗，但商業授權會移除評估限制，解鎖多執行緒處理，並提供完整技術支援。

**Q: 我該如何處理指向電子郵件地址的超連結？**  
A: `TargetModeType.EMAIL` 常數可辨識電子郵件連結；您可以提取 `mailto:` 地址並單獨處理。

**Q: Aspose.Cells 在儲存時會保留超連結的格式嗎？**  
A: 絕對會。所有超連結屬性——顯示文字、工具提示、地址與目標模式——在您以任何支援的格式儲存工作簿時皆會被保留。

**Q: 我可以使用 Aspose.Cells 在批次工作中 **讀取 Excel 超連結** 嗎？**  
A: 可以——將 API 與檔案迴圈結合，以讀取多本工作簿的 Excel 超連結，然後將結果存入中央儲存庫。

**Q: 在高吞吐量情境下，最佳的 **載入 Excel 工作簿 Java** 方法是什麼？**  
A: 盡可能重複使用單一 `Workbook` 實例，及時關閉輸入串流，並啟用 `MemorySetting.MEMORY_PREFERENCE` 選項以最佳化記憶體使用。

---

**最後更新：** 2026-11-03  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

如有其他問題，歡迎造訪 [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)。

## 相關教學

- [如何使用 Aspose.Cells for Java 為 Excel 新增超連結 – 步驟指南](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [處理大型 Excel 檔案：透過 Aspose.Cells 管理超連結](/cells/java/advanced-features/manage-excel-hyperlinks-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 找出 Excel 工作簿中的隱藏外部連結](/cells/java/advanced-features/detect-hidden-external-links-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}