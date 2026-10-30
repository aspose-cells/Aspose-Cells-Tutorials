---
category: general
date: 2026-08-08
description: 如何在 Aspose.Cells 中使用 Java 複製樞紐分析表並將範圍複製到工作簿。了解使用 CopyOptions 複製樞紐分析表的具體步驟。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range to workbook
- aspose.cells copy range
language: zh-hant
lastmod: 2026-08-08
og_description: 如何在 Aspose.Cells 中複製樞紐分析表，並使用 Java 將範圍複製到工作簿。請參考本完整指南，使用 CopyOptions
  複製樞紐分析表。
og_image_alt: Diagram showing how to copy pivot in Aspose.Cells
og_title: 如何在 Aspose.Cells 中複製樞紐分析表 – 複製範圍至工作簿
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  headline: How to copy pivot in Aspose.Cells – copy range to workbook
  type: TechArticle
- description: How to copy pivot in Aspose.Cells and copy range to workbook using
    Java. Learn the exact steps to duplicate a pivot table with CopyOptions.
  name: How to copy pivot in Aspose.Cells – copy range to workbook
  steps:
  - name: Add Aspose.Cells to your project
    text: 'If you use Maven, add the following dependency to your `pom.xml`:'
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Configure copy options to include the pivot table
    text: '```java // Define copy options to include the pivot table in the copied
      range CopyOptions copyOptions = new CopyOptions() .setCopyPivotTable(true);
      ```'
  - name: Copy the desired range with the pivot table
    text: '```java // Copy the range A1:H20, preserving the pivot table workbook.getWorksheets().get(0).getCells()
      .copyRange("A1:H20", copyOptions); ```'
  - name: Save the modified workbook
    text: '```java // Save the workbook with the copied pivot table workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected result
    text: '* `output.xlsx` contains the same data as `input.xlsx`. * The pivot table
      that originally occupied the source range appears in the destination cells,
      fully functional (filters, refresh capability, etc.). * All cell formatting,
      formulas, and column widths are preserved because `copyRange` copies the '
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- CopyRange
title: 如何在 Aspose.Cells 中複製樞紐分析表 – 複製範圍至工作簿
url: /zh-hant/java/excel-pivot-tables/how-to-copy-pivot-in-aspose-cells-copy-range-to-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Aspose.Cells 中複製樞紐分析表 – 複製範圍至工作簿

如果您需要在 Excel 檔案中使用 Aspose.Cells **複製樞紐分析表**，本指南將向您展示完整的操作流程。完成本教學後，您將能夠 **將範圍複製至工作簿**，同時保留樞紐分析表的定義。

本範例使用 Java，但相同概念同樣適用於任何使用 Aspose.Cells 的 .NET 語言。無需額外工具——只需 Aspose.Cells for Java 程式庫以及基本的開發環境。

## 前置條件

在開始之前，請確保您已具備：

* Java Development Kit（JDK）8 或更新版本。
* Maven 或 Gradle 以管理相依性（本範例使用 Maven）。
* 已在專案中加入 Aspose.Cells for Java 23.9（或最新版本）。
* 一個包含至少一個樞紐分析表於第一個工作表的輸入工作簿（`input.xlsx`）。

事先準備好上述項目，可避免程式在存取工作簿時發生執行時錯誤。

## 如何使用 Aspose.Cells 複製樞紐分析表

本節將逐步說明使用 `CopyOptions` 類別，將工作表中的某一區域 **複製樞紐分析表** 至另一處所需的每個步驟。

### 步驟 1：將 Aspose.Cells 加入專案

如果您使用 Maven，請將以下相依性加入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust JDK version as needed -->
</dependency>
```

*此步驟的重要性*：此程式庫提供 `Workbook`、`CopyOptions` 以及其他執行 **aspose.cells copy range** 操作所需的類別。若未加入相依性，編譯器將無法解析這些類型。

### 步驟 2：載入來源工作簿

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

載入檔案會在記憶體中建立試算表的表示。`Workbook` 物件讓您可以存取工作表、儲存格與樞紐分析表。

### 步驟 3：設定複製選項以包含樞紐分析表

```java
        // Define copy options to include the pivot table in the copied range
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);
```

`CopyOptions.setCopyPivotTable(true)` 告訴 Aspose.Cells 此操作應保留樞紐分析表的中繼資料。若省略此旗標，樞紐分析表將會變成靜態資料，失去互動性。

### 步驟 4：連同樞紐分析表一起複製指定範圍

```java
        // Copy the range A1:H20, preserving the pivot table
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);
```

`copyRange` 方法會複製儲存格、格式，且因為先前步驟已設定相關選項，還會複製與該範圍相交的任何樞紐分析表。這就是 **copy range to workbook** 功能的核心。

### 步驟 5：儲存已修改的工作簿

```java
        // Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

儲存會將變更寫入新檔案（`output.xlsx`）。現在您可以在 Excel 中開啟此檔案，看到樞紐分析表已在複製的範圍位置完整複製。

## 完整、可執行的範例

將所有步驟整合起來，以下是您可以編譯並執行的完整程式碼：

```java
import com.aspose.cells.*;

public class CopyPivotTableRange {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Define copy options to include the pivot table
        CopyOptions copyOptions = new CopyOptions()
                .setCopyPivotTable(true);

        // 3. Copy the range A1:H20 with the specified options
        workbook.getWorksheets().get(0).getCells()
                .copyRange("A1:H20", copyOptions);

        // 4. Save the modified workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### 預期結果

* `output.xlsx` 包含與 `input.xlsx` 相同的資料。
* 原本位於來源範圍的樞紐分析表會出現在目標儲存格中，且功能完整（篩選、重新整理等）。
* 所有儲存格格式、公式與欄寬皆被保留，因為 `copyRange` 會複製整個儲存格區塊。

## 常見問題與邊緣情況

**如果目標範圍與現有的樞紐分析表重疊會怎樣？**  
Aspose.Cells 會覆寫目標儲存格。為避免資料遺失，請確保目標區域為空，或先搬移現有的樞紐分析表。

**我可以跨工作表複製樞紐分析表嗎？**  
可以。使用 `workbook.getWorksheets().get(targetSheetIndex).getCells().copyRange(sourceRange, copyOptions);`，其中 `targetSheetIndex` 為目標工作表的索引。

**`setCopyPivotTable(true)` 會複製底層資料來源嗎？**  
此方法僅複製樞紐快取的參考。若來源資料位於同一工作簿，目的地的樞紐分析表會指向相同的快取。若要複製快取，必須手動建立新的樞紐快取。

**如何有效率地複製大型範圍？**  
在複製極大範圍時，僅在必要時使用 `CopyOptions.setCopyFormula(true)` 與 `setCopyDataValidation(true)`。減少選項數量可提升效能。

## 使用 **aspose.cells copy range** 的可靠技巧

* **專業提示：** 若複製的範圍包含依賴樞紐快取的公式，請在複製後務必呼叫 `workbook.calculateFormula()`。
* **注意：** 隱藏的工作表。`copyRange` 僅在可見工作表上運作，除非您以索引明確指定隱藏工作表。
* **版本檢查：** `setCopyPivotTable` 旗標自 Aspose.Cells 20.9 起提供。請確認您的程式庫版本支援此功能。

## 結論

您現在已了解如何在 Aspose.Cells 中 **複製樞紐分析表**，以及如何在保留完整樞紐功能的前提下 **將範圍複製至工作簿**。這些步驟——加入程式庫、載入工作簿、設定 `CopyOptions`、執行複製以及儲存——構成可重複使用的模式，您可將其套用於其他複製貼上情境。

接下來，您可以探索相關主題，例如針對圖表、條件格式與資料驗證的 **aspose.cells copy range**。嘗試在不同檔案格式之間（XLSX → XLS）進行複製，以擴展自動化能力。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 樞紐分析表來源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在樞紐分析表中實作切片器：完整指南](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}