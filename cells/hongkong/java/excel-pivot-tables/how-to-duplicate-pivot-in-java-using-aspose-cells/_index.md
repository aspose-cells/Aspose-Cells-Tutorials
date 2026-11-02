---
category: general
date: 2026-09-18
description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表 – 快速且可靠地在工作簿之間複製樞紐分析表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: zh-hant
lastmod: 2026-09-18
og_description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表。跟隨本完整教學，使用簡潔的 Java 程式碼在工作簿之間複製樞紐分析表。
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: 在 Java 中複製樞紐分析表 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表

如果您需要在 Java 應用程式中 **how to duplicate pivot**，本指南將向您展示具體步驟。透過載入 Excel 活頁簿、定義樞紐分析表的儲存格區域，並將該範圍複製到新活頁簿，您可以在不遺失其定義或資料的情況下移動樞紐分析表。

在產生報告、歸檔分析或將大型活頁簿拆分為模組化檔案時，複製樞紐分析表是一項常見需求。在本教學中，您將學習如何 **copy range between workbooks**、如何 **load Excel workbook Java**，以及安全 **how to copy pivot** 的細節。

您將完成一個可直接執行的 Java 程式，使用 Aspose.Cells for Java 將 `Source.xlsx` 中的樞紐分析表複製到 `PivotCopied.xlsx`。

## 前置條件

* JDK 8 或更新版本已安裝。
* Maven（或其他建置工具）用於管理相依性。
* Aspose.Cells for Java 版本 23.10 或更新。將以下 Maven 相依性加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* 包含樞紐分析表且範圍為 **A1:H30** 的來源活頁簿（`Source.xlsx`）。

## 如何在 Java 中複製樞紐分析表

核心概念相當簡單：

1. **Load the source workbook** – 這會讓您取得包含樞紐分析表的工作表。
2. **Define the cell area** – 定義包住樞紐分析表的儲存格區域。
3. **Create a destination workbook** – 建立一個空的活頁簿，用於接收複製的範圍。
4. **Copy the range** – Aspose.Cells 會自動複製樞紐分析表的定義。
5. **Save the destination workbook** – 您現在擁有一個包含相同樞紐分析表的獨立檔案。

以下是一個完整且可執行的 Java 程式，遵循上述步驟。

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### 為什麼這樣可行

* **Aspose.Cells** 將樞紐分析表視為工作表儲存格集合的一部份。當您呼叫 `copyRange` 時，函式庫不僅會複製儲存格值，還會複製底層的樞紐快取與定義，因而新活頁簿會包含完整可用的複本。
* `CopyOptions` 物件預設會保留公式、格式與嵌入式物件。若需要額外控制，可自行客製化（例如 `setCopyColumnWidths(true)`）。

## 複製範圍於活頁簿之間 – 更深入的探討

雖然上述範例僅複製單一連續區塊，`copyRange` 仍能處理任何矩形區域。若您的樞紐分析表跨越非相鄰的範圍，可多次呼叫 `copyRange`，或使用 `Worksheet.copy` 來複製整個工作表。

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**提示：** 複製大型活頁簿時，啟用 `CopyOptions.setPreserveCellStyle(true)` 可避免不必要的樣式重複，從而提升效能。

## 如何將樞紐分析表複製至活頁簿 – 處理多個樞紐分析表

如果來源工作表包含多個樞紐分析表，您可以遍歷工作表的樞紐分析表集合，逐一複製每個樞紐分析表：

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

此方法可確保每個樞紐分析表保留其原始名稱與資料來源。

## 載入 Excel 活頁簿 Java – 常見陷阱

* **File path separators:** 使用正斜線 (`/`) 或 `File.separator` 以保持程式碼跨平台相容。
* **Missing license:** Aspose.Cells 在評估模式下仍可使用，但輸出會帶有浮水印。於載入活頁簿前以 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` 註冊授權，以移除浮水印。
* **Large files:** 若活頁簿大於 100 MB，建議使用 `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` 搭配串流選項，以降低記憶體使用量。

## 完整端對端範例回顧

將所有步驟整合起來，以下是您可以直接複製貼上至 IDE 的最終程式碼：

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**預期輸出：** 執行後，`PivotCopied.xlsx` 會出現在指定目錄中。於 Excel 開啟時，會顯示與 `Source.xlsx` 相同的樞紐分析表版面、篩選條件與資料，所有計算欄位與格式皆被保留。

## 常見問題

* **這在較舊的 Excel 格式（.xls）下也能運作嗎？**  
  是的。Aspose.Cells 會自動偵測格式。使用 `new Workbook("file.xls")`，相同的複製邏輯仍適用。

* **如果樞紐分析表參考外部資料來源會怎樣？**  
  複製後仍保留原始資料來源的參照。若目標環境無法存取該來源，樞紐分析表會顯示 `#REF!` 錯誤。為避免此情況，可在複製後重新整理樞紐分析表，或透過 `PivotTable.setDataSource(...)` 更改其資料來源。

* **我可以將樞紐分析表複製到指定的工作表名稱嗎？**  
  當然可以。建立目的工作表後，重新命名即可：

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## 結論

您現在已了解如何在 Java 中使用 Aspose.Cells **how to duplicate pivot** 表格、如何 **copy range between workbooks**，以及 **load Excel workbook Java** 的最佳實踐。遵循載入、定義、建立目的地、複製與儲存這五個步驟，即可自動化報告產生、歸檔分析或將複雜活頁簿拆分，而不會失去樞紐分析表功能。

接下來，您可以探索相關主題，例如具有多個工作表的 **copy pivot to workbook**，或在非 Aspose 情境下使用 Apache POI 將複製的樞紐分析表整合至更大的資料處理流程。嘗試不同的 `CopyOptions` 設定，以微調大型活頁簿的效能。

祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表&#58; 完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 樞紐分析表來源&#58; 完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [使用 Aspose.Cells for Java 在 Excel 活頁簿中分組樞紐分析欄位 - 完整指南](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}