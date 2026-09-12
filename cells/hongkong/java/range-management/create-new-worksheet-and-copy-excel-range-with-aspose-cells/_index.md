---
category: general
date: 2026-09-11
description: 使用 Aspose.Cells 建立新工作表並複製 Excel 範圍。了解如何在工作表之間複製範圍，同時保留樞紐分析表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new worksheet
- copy excel range
- copy range between sheets
- copy range aspose.cells
language: zh-hant
lastmod: 2026-09-11
og_description: 使用 Aspose.Cells 建立新工作表並複製 Excel 範圍。本教學示範了在工作表之間複製範圍且保持樞紐分析表完整的具體步驟。
og_image_alt: Screenshot of a Java IDE showing code that creates a new worksheet and
  copies an Excel range
og_title: 建立新工作表並複製 Excel 範圍 – Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Create new worksheet and copy Excel range using Aspose.Cells. Learn
    how to copy range between sheets while preserving pivot tables.
  headline: Create new worksheet and copy Excel range with Aspose.Cells
  type: TechArticle
- questions:
  - answer: The `copy` method also copies merge information, so merged cells appear
      unchanged on the destination sheet.
    question: What if the source range contains merged cells?
  - answer: Yes. Load a second `Workbook` instance, create a destination range in
      that workbook, and call `sourceRange.copy(destinationRange)`. The method handles
      cross‑workbook copying automatically.
    question: Can I copy to a different workbook?
  - answer: The copy operation overwrites any existing cells that intersect the destination
      range. To avoid data loss, ensure the destination area is empty or use a different
      start cell (e.g., `"B2"`).
    question: What if the destination sheet already has data?
  - answer: Aspose.Cells reuses the original pivot cache, which means the new pivot
      table remains linked to the same source data. If you need an independent cache,
      you must recreate the pivot table after copying.
    question: Is the pivot cache duplicated?
  type: FAQPage
tags:
- Aspose.Cells
- Excel automation
- Java
title: 使用 Aspose.Cells 建立新工作表並複製 Excel 範圍
url: /zh-hant/java/range-management/create-new-worksheet-and-copy-excel-range-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立新工作表並使用 Aspose.Cells 複製 Excel 範圍

如果您需要 **create new worksheet** 並在 Excel 檔案中移動資料，Aspose.Cells 讓這個過程變得簡單。本指南會精確說明如何將 Excel 範圍從一個工作表複製到另一個工作表，同時保留範圍內的樞紐分析表。  
您將學習如何 **copy excel range**、如何 **copy range between sheets**，以及為何 Aspose.Cells 的 `copy` 方法能保持樞紐分析表的定義不變。無需任何外部工具—只需一個使用 Aspose.Cells 函式庫的 Java 專案。

## 前置條件

- 已安裝 Java 17 或更新版本
- 已將 Aspose.Cells for Java（版本 23.12 或更新）加入專案的 classpath
- 一個來源活頁簿（`input.xlsx`），其中在您想要複製的範圍內包含樞紐分析表
- 具備 Java 語法以及 Maven/Gradle 相依性管理的基本認識

## 步驟 1：設定專案並匯入 Aspose.Cells

建立一個簡單的 Maven 專案（或您偏好的 Gradle），並加入 Aspose.Cells 相依性：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

接著在 Java 原始檔中匯入所需的類別：

```java
import com.aspose.cells.*;
import java.io.IOException;
```

*Why this step matters*：匯入正確的類別可讓您使用 `Workbook`、`Worksheet`、`Range` 以及負責範圍傳輸的 `copy` 方法。

## 步驟 2：載入來源活頁簿

開啟包含您想要複製資料的活頁簿。以下程式碼會從您指定的目錄載入 `input.xlsx`：

```java
public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Explanation*：`Workbook` 代表整個 Excel 檔案。載入一次即可對所有工作表與儲存格集合取得讀寫權限。

## 步驟 3：識別包含樞紐分析表的來源範圍

選取包含樞紐分析表的工作表，並定義您想要複製的精確儲存格區塊。在此範例中，我們複製 A1 至 D20 的儲存格：

```java
        // Get the first worksheet (index 0) that contains the pivot table
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the source range – this range includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");
```

*Why this matters*：透過建立 `Range` 物件，您告訴 Aspose.Cells 哪些儲存格（包括任何嵌入的物件，如樞紐分析表）需要被複製。

## 步驟 4：**Create new worksheet** 以接收複製的資料

現在我們在同一個活頁簿中新增一個全新的工作表。這裡正是主要關鍵字出現的地方：

```java
        // Create a new worksheet named "Copy"
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // Define the top‑left cell of the destination range
        Range destinationRange = destinationSheet.getCells().createRange("A1");
```

*Explanation*：新增工作表可將複製的資料隔離，讓您輕鬆驗證 **copy excel range** 操作是否成功，同時不影響原始工作表。

## 步驟 5：複製範圍 – 樞紐分析表會自動保留

使用 `copy` 方法將範圍從來源工作表移至目標工作表。Aspose.Cells 會複製公式、格式以及樞紐分析表的定義：

```java
        // Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);
```

*Why this works*：`copy` 方法會對來源儲存格執行深層複製。它不僅僅複製值，還會複製整個儲存格結構，包括樞紐快取。因此您可以 **copy range aspose.cells**，且在新工作表上仍能看到可運作的樞紐分析表。

## 步驟 6：儲存包含新工作表的活頁簿

最後，將修改過的活頁簿寫入磁碟：

```java
        // Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

*Result*：`output.xlsx` 現在包含原始工作表以及名為 **Copy** 的新工作表，該工作表保有完全相同的範圍，且包含樞紐分析表。

## 完整範例程式

將所有步驟組合起來，以下是完整且可執行的程式：

```java
import com.aspose.cells.*;
import java.io.IOException;

public class ExcelRangeCopy {
    public static void main(String[] args) throws IOException {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table and define the source range
        Worksheet sourceSheet = workbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:D20");

        // Step 3: Create a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
        Range destinationRange = destinationSheet.getCells().createRange("A1");

        // Step 4: Copy the range – the pivot table inside the range is preserved
        sourceRange.copy(destinationRange);

        // Step 5: Save the workbook with the copied data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Expected output**：在 Excel 中開啟 `output.xlsx`。您會看到名為 **Copy** 的工作表，其 A1:D20 儲存格包含相同的資料、格式，且有一個與原始相同的可用樞紐分析表。

## 常見問題與邊緣情況

- **What if the source range contains merged cells?**  
  `copy` 方法也會複製合併資訊，因此合併儲存格在目標工作表上保持不變。

- **Can I copy to a different workbook?**  
  可以。載入第二個 `Workbook` 實例，在該活頁簿中建立目標範圍，然後呼叫 `sourceRange.copy(destinationRange)`。此方法會自動處理跨活頁簿的複製。

- **What if the destination sheet already has data?**  
  複製操作會覆寫與目標範圍相交的任何現有儲存格。為避免資料遺失，請確保目標區域為空，或使用不同的起始儲存格（例如 `"B2"`）。

- **Is the pivot cache duplicated?**  
  Aspose.Cells 會重用原始的樞紐快取，這表示新樞紐分析表仍連結至相同的來源資料。若需要獨立的快取，必須在複製後重新建立樞紐分析表。

## 提示與最佳實踐

- **Pro tip**：若您的範圍包含依賴於複製區塊外資料的公式，請在儲存前使用 `Workbook.setForceFormulaRecalculation(true)`。
- **Watch out for** 大範圍：複製大型工作表可能會佔用大量記憶體。如果遇到 `OutOfMemoryError`，請考慮分段複製。
- **Performance tip**：在處理非常大的檔案時，停用螢幕更新 (`workbook.getSettings().setCalculateFormulaOnOpen(false)`) 可加速複製過程。

## 結論

您現在已了解如何使用 Aspose.Cells **create new worksheet** 並 **copy excel range** 於工作表之間，保留樞紐分析表與所有儲存格屬性。此技巧讓您能以程式方式複製資料區塊、建立報表範本，或在不需手動複製貼上的情況下重新組織活頁簿。  
接下來，您可以探索相關主題，例如 **copy range aspose.cells** 用於跨活頁簿操作、自動化樞紐分析表重新整理，或將複製的工作表匯出為 PDF。嘗試不同的來源範圍與工作表名稱，以符合您的特定自動化情境。祝開發順利！

## 接下來您應該學習什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [Copy Shapes Between Excel Sheets Using Aspose.Cells for .NET&#58; A Complete Guide](/cells/english/net/images-shapes/copy-shapes-between-sheets-aspose-cells-dotnet/)
- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/hindi/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}