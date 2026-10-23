---
category: general
date: 2026-10-23
description: 學習如何在 Java 中複製 Excel 工作表，同時保留樞紐分析表。本指南亦示範如何複製樞紐分析表、複製 Excel 範圍，以及複製含有樞紐資料的工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: zh-hant
lastmod: 2026-10-23
og_description: 在 Java 中複製 Excel 工作表，同時保留樞紐分析表。跟隨本完整教學，學習如何複製樞紐分析表、複製 Excel 範圍，以及複製含有樞紐資料的工作表。
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: 在 Java 中複製含樞紐分析表的 Excel 工作表 – 一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: 如何在 Java 中複製 Excel 工作表並保持樞紐分析表完整
url: /zh-hant/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中複製 Excel 工作表並保持樞紐分析表完整

如果您需要 **duplicate Excel sheet** 同時保持每個樞紐分析表仍然有效，本指南將精確說明操作步驟。您將看到一個簡潔的解決方案，能複製工作表、複製特定範圍，甚至將樞紐分析表複製到另一個活頁簿——全部使用純 Java 及 Aspose.Cells。

在從範本產生每月報告或需要測試用的沙箱副本時，複製 Excel 工作表是一項常見任務。以下程式碼適用於 Aspose.Cells 25.11 及更新版本，該版本引入了 `setCopyPivotTable(true)` 選項。

## 您需要的條件

- 已安裝 Java 17（或任何較新的 JDK）
- 專案中已加入 Aspose.Cells for Java 25.11 或更新版本（Maven 坐標 `com.aspose:aspose-cells:25.11`）
- 一個已包含樞紐分析表的來源活頁簿（`SourceWithPivot.xlsx`）
- 您慣用的 IDE 或建置工具（IntelliJ IDEA、Eclipse、Maven、Gradle 等）

## 步驟 1：載入包含樞紐分析表的來源活頁簿

第一步是開啟保存您想保留之樞紐分析表的活頁簿。

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **此步驟的重要性：** 載入來源活頁簿可讓您存取工作表物件、儲存格以及內嵌的樞紐分析表。若未載入，您將無法參照欲複製的樞紐資料。

## 步驟 2：建立空的目標活頁簿（或載入現有活頁簿）

您可以從空白活頁簿開始，或開啟一個將接收複製工作表的既有檔案。

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **提示：** 若您已有報告活頁簿，請將上述程式碼改為 `new Workbook("ExistingReport.xlsx")`，即可將複製的工作表加入其中。

## 步驟 3：複製整個工作表 – 樞紐分析表會自動保留

複製整個工作表是最簡單的 **copy sheet with pivot** 方法。Aspose.Cells 會自動複製樞紐分析表的定義與快取。

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **為什麼有效：** `addCopy` 會複製工作表結構、儲存格值、樣式以及任何內嵌的樞紐分析表。`dstWb` 中的新工作表將與原始工作表完全相同，包含樞紐快取。

## 步驟 4：（可選）僅複製包含樞紐分析表的特定範圍

有時您不需要整張工作表——可能只需要包含樞紐分析表的某個區段。這時可使用 **copy Excel range**，並明確要求同時複製樞紐分析表。

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **它的作用：** `setCopyPivotTable(true)` 會強制引擎在複製受限範圍時仍複製樞紐分析表的定義。若未設定此旗標，僅會複製原始資料，樞紐分析表將遺失。

## 步驟 5：儲存目標活頁簿

最後，將複製的內容寫入新檔案。

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### 預期輸出

執行程式後會在目標目錄產生 `DuplicatedWithPivot.xlsx`。在 Excel 中開啟該檔案，您會看到：

- 一個名為 `Sheet1 (Copy)` 的新工作表（或在原名稱後加上 “Copy”）
- 樞紐分析表與來源工作表完全相同，且功能完整
- 若使用了可選的範圍複製，僅會保留 A1:G30 的儲存格，但樞紐分析表仍可運作，因為其快取已被複製

## 常見問題與邊緣情況

### 如何在不複製整張工作表的情況下將樞紐分析表複製到另一個活頁簿？

若您只需要樞紐分析表及其底層資料，請複製同時包含來源資料與樞紐的範圍，然後使用 `setCopyPivotTable(true)`。與 **步驟 4** 相同的程式碼即可，只需確保範圍涵蓋資料來源。

### 如果來源活頁簿有多個包含樞紐分析表的工作表該怎麼辦？

對每個想要複製的工作表，重複 **步驟 3**：

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### 受保護的工作表是否也能使用此方法？

Aspose.Cells 能夠複製受保護的工作表，但若在複製後需修改樞紐分析表，必須先解除保護：

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### 能否將樞紐分析表複製到已包含同名工作表的現有活頁簿？

可以。使用 `addCopy` 並指定唯一名稱：

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## 專業提示：驗證樞紐快取

複製完成後，您可以透過程式驗證樞紐快取是否存在：

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

> 若快取 ID 輸出為非負數，表示樞紐分析表已成功複製。

## 結論

現在您已了解如何在 Java 中 **duplicate Excel sheet** 並保留所有樞紐分析表，如何直接 **copy pivot** 表格，如何 **copy Excel range** 包含樞紐，以及如何使用 Aspose.Cells 25.11+ **copy sheet with pivot** 或 **copy pivot to workbook**。將這些模式套用於自動化報告產生、建立範本副本，或建構需要相同樞紐分析功能的測試環境。

準備好深入探索了嗎？試著將複製的活頁簿匯出為 PDF，或在複製後以程式方式重新整理樞紐快取，確保顯示最新資料。祝開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南技術密切相關的主題。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何在 Java 中複製工作表並保留樞紐分析表](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [如何在 Java 中複製樞紐分析表 – 完整 Aspose.Cells 指南](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [如何在 Java 中複製範圍並保留樞紐分析表](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}