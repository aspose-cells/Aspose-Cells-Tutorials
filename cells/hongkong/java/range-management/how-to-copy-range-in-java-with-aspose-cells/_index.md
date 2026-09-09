---
category: general
date: 2026-09-08
description: 如何在 Java 中使用 Aspose.Cells 複製範圍 – 學習複製樞紐分析表、製作樞紐分析表副本，以及在匯出樞紐分析表時保留格式。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: zh-hant
lastmod: 2026-09-08
og_description: 如何在 Java 中使用 Aspose.Cells 複製範圍。本教程將示範如何複製樞紐分析表、建立樞紐分析表的副本，以及在保留格式的前提下匯出樞紐分析表。
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: 在 Java 中如何複製範圍 – 完整 Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 複製範圍
url: /zh-hant/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 複製範圍

如果您需要 **how to copy range**，Aspose.Cells 讓此任務變得簡單。無論是搬移一般的儲存格區塊或是完整功能的 pivot table，該函式庫都會在保留公式、樣式與 pivot cache 的同時處理複製操作。在本指南中，您將學會 **copy pivot table**、**duplicate pivot table**，以及甚至 **export pivot table** 到新活頁簿，且保留完整格式。

本教學涵蓋從專案設定到最終驗證的所有步驟，讓您在閱讀完畢後即可立即執行程式碼。除了 Aspose.Cells for Java 的 JAR，無需其他外部工具。

## 前置條件

- 安裝並在 IDE 中設定 Java 17（或任何受支援的 JDK）。
- 使用 Maven 或 Gradle 進行相依性管理（範例使用 Maven）。
- 一個包含 pivot table 於 `A1:H20` 範圍的來源 Excel 檔案（`source.xlsx`）。
- 具備基本的 Java 程式設計知識。

## 步驟 1：將 Aspose.Cells 加入您的專案

Aspose.Cells 為商業函式庫，但提供免費評估版。將相依性加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **小技巧:** 如果您偏好使用 Gradle，等效的條目如下：
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

加入 JAR 後，您即可使用本指南中所使用的 `Workbook`、`Worksheet`、`Range` 與 `CopyOptions` 類別。

## 步驟 2：載入來源活頁簿並選取第一個工作表

**how to copy range** 的第一步是開啟包含您欲搬移資料的活頁簿。

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **為什麼重要：** 開啟活頁簿會在記憶體中建立一個表示，讓 API 能在不觸碰磁碟上原始檔案的情況下進行操作。

## 步驟 3：定義包含 pivot table 的範圍

pivot table 位於矩形區塊內。您必須指定該區塊，讓 Aspose.Cells 知道要複製什麼。

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **注意：** `createRange` 方法尚未執行任何複製；它僅建立指向您欲複製儲存格的 `Range` 物件。

## 步驟 4：建立新活頁簿並取得其第一個工作表

現在建立目的地活頁簿，讓複製的範圍存放於其中。

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **為什麼要使用新活頁簿？** 使用全新的檔案可確保沒有隱藏樣式或命名範圍會干擾複製操作，這在您 **export pivot table** 到另一個檔案時尤為重要。

## 步驟 5：將範圍（含 pivot table）複製至目的工作表

這是 **how to copy range with formatting** 的核心。`CopyOptions` 物件告訴 Aspose.Cells 保留所有內容：數值、公式、樣式與 pivot cache。

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **複製 pivot table：** 由於來源範圍包含 pivot table，API 會自動複製 pivot cache，讓新工作表擁有與原始完全相同且可正常運作的 pivot table。

## 步驟 6：儲存目的活頁簿

最後，將結果寫入磁碟。

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

當您開啟 `dest.xlsx` 時，會看到與原始 pivot table 完全相同的副本，包含其格式、切片器與計算欄位。

## 預期輸出

- `dest.xlsx` 包含名為 **Sheet1** 的工作表。
- 儲存格 `A1:H20` 含有與來源相同的資料與 pivot table。
- 所有儲存格樣式（字型、顏色、邊框）均被保留。
- pivot table 具備完整的互動功能；重新整理時會反映複製範圍內的基礎資料。

## 如何在保留格式的情況下複製範圍 – 深入探討

前述範例示範最簡單的情況，但您可能會遇到需要稍作調整的變化情形。

### 複製 pivot table 至現有活頁簿

如果您需要在已有資料的活頁簿內 **duplicate pivot table**，可使用相同的 `copyRange` 呼叫，只是將目的位址指向不同的位置：

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### 僅匯出 pivot table（不含周圍資料）

有時您只想取得 pivot table 本身，而非來源資料。可透過 `getPivotTable` 方法取得 pivot table 的顯示範圍：

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### 保留條件格式

條件格式規則屬於樣式集合的一部份。`PasteType.ALL` 旗標已會複製它們，但您也可以明確指定：

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### 邊緣情況與疑難排解

| Situation | What to watch for | Recommended fix |
|-----------|-------------------|-----------------|
| 來源與目的活頁簿使用不同的 Excel 版本 | 某些較新的 pivot 功能（例如資料模型）可能無法正確呈現 | 使用最新的 Aspose.Cells 版本，並為兩個活頁簿設定 `Workbook.setFileFormatType(FileFormatType.XLSX)` |
| 非常大的 pivot 分析表（> 10 000 列）會造成記憶體壓力 | 複製過程中發生記憶體不足錯誤 | 在載入前啟用 `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` |
| 目的工作表已包含與來源相同名稱的命名範圍 | 名稱衝突導致 `CopyOptions` 失敗 | 呼叫 `copyOptions.setIgnoreNameConflicts(true)` |

## 完整、可執行的範例

以下是完整的程式碼，您可以直接複製貼上至 Java 類別中。它包含所有匯入、錯誤處理與註解。

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

執行程式後，開啟 `dest.xlsx` 以驗證 pivot table 是否與原始完全相同。

## 結論

您現在已了解如何在 Java 中使用 Aspose.Cells **how to copy range**，包括如何 **copy pivot table**、**duplicate pivot table** 與 **export pivot table**，同時保留所有格式。此函式庫抽象化了 Excel XML 結構的底層細節，讓您專注於業務邏輯。

### 後續步驟

- 探索圖表與圖片的 **copy range with formatting**（使用 `PasteType.PICTURES`）。
- 自動化批次處理：迴圈處理多個來源檔案，並將它們的 pivot 分析表彙總至一個摘要活頁簿。
- 結合此技巧與 Aspose.Slides，產生嵌入已複製的 pivot 分析表的 PowerPoint 報告。

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [How to Update Excel Pivot Table Source with Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Optimize Pivot Table Loading in Java using Aspose.Cells – A Comprehensive Guide](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}