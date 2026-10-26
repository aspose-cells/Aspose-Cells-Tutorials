---
category: general
date: 2026-10-26
description: 學習如何使用 Java 複製樞紐分析表至新工作簿，同時保留格式與樞紐分析定義，並透過 Aspose.Cells 複製帶格式的 Excel
  範圍。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: zh-hant
lastmod: 2026-10-26
og_description: 在 Java 中使用 Aspose.Cells 將樞紐分析表複製到新活頁簿。本指南說明如何複製 Excel 範圍、保留格式，並高效建立空白活頁簿。
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: 在 Java 中將樞紐分析表複製到新工作簿 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中將樞紐分析表複製到新活頁簿
url: /zh-hant/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中將樞紐分析表複製到新活頁簿

如果您需要將 **copy pivot table** 從一個 Excel 檔案複製到另一個，本文指南會提供完整且可執行的解決方案。您將看到如何保留樞紐分析表的定義、保持所有格式，並避免在複製 Excel 範圍時常見的陷阱。

複製樞紐分析表時常會出現如 *how to copy pivot* 之類的問題，擔心會破壞資料來源或失去樣式。完成本教學後，您將擁有一個自包含的 Java 程式，能建立空白活頁簿、複製所需範圍，並將結果儲存且樞紐分析表保持完整。

## 您將達成的目標

* 載入包含樞紐分析表的來源活頁簿。  
* **Create empty workbook** 以接收複製的資料。  
* **Copy excel range** 包含樞紐分析表的範圍，使用能保留樞紐與格式的選項。  
* 儲存目標檔案，並驗證樞紐分析表的功能與原始檔案完全相同。

### 前置條件

* Java 17 或更新版本。  
* Aspose.Cells for Java（版本 23.10 或更新）。  
* 具備基本的 Java IDE（IntelliJ IDEA、Eclipse 等）使用經驗。  

> **專業提示：** 使用免費的 Aspose.Cells 評估授權進行快速測試；在正式上線前請換成正式授權。

## 將樞紐分析表複製到新活頁簿

第一步是設定來源與目標活頁簿。目標活頁簿以 **create empty workbook** 呼叫開始，會得到只有單一工作表的乾淨檔案。

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### 為什麼這樣可行

* `new Workbook()` **creates empty workbook** 並帶有預設工作表，避免必須刪除既有資料。  
* `CopyOptions` 告訴 Aspose.Cells 複製 **pivot table** 的中繼資料，而不只是原始值。`PASTE_ALL` 模式同時攜帶儲存格樣式、數字格式與條件格式——滿足 **copy range with formatting** 的需求。  
* `copyRange` 執行 **copy excel range** 操作，尊重來源的內部結構，使得樞紐分析表在複製後仍可正常運作。

## 如何在不失去格式的情況下複製樞紐分析表

如果僅使用預設的 `CopyOptions`，在較舊的 Aspose.Cells 版本中可能會遺漏部分樣式資訊。明確設定貼上類型可保證 **copy range with formatting** 被正確保留。

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

加入 `setPasteSpecialType` 可確保欄寬、列高，甚至資料驗證規則都會隨範圍一起傳遞。當樞紐分析表跨越多個自訂欄寬的欄位時，這特別有用。

## 複製前先建立空白活頁簿

有時開發者會嘗試將資料複製到已包含資料的現有活頁簿，這可能導致範圍重疊或意外覆寫。以 **create empty workbook** 呼叫作為起點，可將操作隔離開來：

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

如果目標需要多於一個工作表，可在複製完成後再加入它們：

```java
destWb.getWorksheets().add("Summary");
```

## 使用 CopyOptions 複製 Excel 範圍並保留格式

除了樞紐分析表外，同樣的模式也適用於任何需要保留格式的 **copy excel range**——例如圖表、表格或條件格式。

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

`CopyOptions` 例項保持不變，因而在不同範圍間能獲得一致的行為。

### 需留意的邊緣情況

| 情況                                   | 建議處理方式 |
|----------------------------------------|--------------|
| 來源活頁簿有多個樞紐分析表               | 分別複製每個樞紐分析表的範圍，或直接複製整個工作表。 |
| 目標活頁簿已包含資料                     | 在呼叫 `copyRange` 時選擇不衝突的起始儲存格（例如 "H1"）。 |
| 樞紐分析表的資料來源為外部（例如資料庫） | 確保目標活頁簿指向相同的外部資料來源，或在複製後重新整理樞紐分析表。 |
| 大型活頁簿（> 10 MB）                   | 增加 Java 堆積大小（`-Xmx2g`）以避免 `OutOfMemoryError`。 |

## 驗證結果

執行程式後，開啟 `destination.xlsx`。您應該會看到：

* 與 `source.xlsx` 中相同的樞紐分析表版面配置。  
* 所有儲存格顏色、數字格式與欄寬皆被保留。  
* 樞紐分析表的資料來源仍指向新檔案內的原始資料範圍，刷新樞紐分析表即可正確更新數值。

如果樞紐分析表顯示為靜態表格，請再次確認已設定 `CopyOptions.setPasteType(PasteType.PASTE_ALL)`。若未使用此選項，Aspose.Cells 會將樞紐分析表視為普通資料。

## 結論

現在您已了解如何在 Java 中 **copy pivot table** 到新活頁簿，同時保留格式、資料連結與工作表版面。完整的解決方案示範了載入來源檔案、**create empty workbook**、設定 **copy excel range** 選項，並儲存結果。

接下來您可以探索相關主題，例如在不同工作表之間 **how to copy pivot**、將圖表與樞紐分析表一起嵌入，或自動批次處理多個活頁簿。試驗 `CopyOptions` 設定以符合您的自動化需求，您將擁有一套強大的 Excel 操作工具箱。

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在已示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [在 Java 中建立新活頁簿 – 完整的 Copy Pivot Table 指南](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [在活頁簿之間 Copy Pivot Table – 步驟式 Java 指南](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [如何在 Java 中複製範圍並保留樞紐分析表](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}