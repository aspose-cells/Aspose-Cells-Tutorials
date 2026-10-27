---
category: general
date: 2026-07-16
description: 使用 Aspose.Cells 匯出 Excel 表格為 TXT 時設定自訂儲存格分隔符號。了解如何將 Excel 公式匯出為文字並將工作表儲存為
  txt 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: zh-hant
lastmod: 2026-07-16
og_description: 在 Aspose.Cells 中設定自訂儲存格分隔符號，可讓您將 Excel 表格匯出為具有精確格式的 TXT。輕鬆將 Excel
  公式匯出為文字，並將工作表儲存為 txt 檔案。
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: 設定自訂儲存格分隔符 – 將 Excel 表格匯出為 TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: 設定自訂儲存格分隔符 – 匯出 Excel 表格為 TXT
url: /zh-hant/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 設定自訂儲存格分隔符 – 匯出 Excel 表格為 TXT

設定自訂儲存格分隔符是當你想從 Excel 工作表取得整潔文字匯出的祕密武器。是否曾想過如何 **export excel table to txt** 而不會得到一團亂七八糟的逗號與換行？在本教學中，我們將使用 Aspose.Cells for Java，從載入活頁簿到 **save worksheet as txt file**，一步步說明整個流程，讓你自行選擇分隔符。

## 你將學會

- 如何 **set custom cell separator** 以匯出文字。
- **export excel formulas to text** 的完整步驟，讓計算後的值一起輸出。
- 如何 **export excel data as plain text** 同時保留版面配置。
- 完整、可直接執行的程式碼範例，讓你可以直接 copy‑paste 到專案中。

閱讀完本指南後，你將能夠對任何 Excel 活頁簿，選擇管道符號 (`|`)、製表符 (`\t`) 或任何你喜歡的字元，產生乾淨且分隔明確的文字檔，讓下游系統輕鬆使用。

### 前置條件

- 已安裝 Java 8 或更新版本。
- 使用 Maven（或任何建置工具）取得 Aspose.Cells for Java 套件。
- 一個包含公式的示範活頁簿 (`TableDemo.xlsx`)。

如果你已具備上述條件，讓我們直接開始——不囉嗦，只提供實作步驟。

## 步驟 1：將 Aspose.Cells 加入專案

在你能 **set custom cell separator** 之前，需要先把 Aspose.Cells 的 JAR 放入 classpath。最簡單的方式是使用 Maven：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

如果你偏好 Gradle，只需將上述 XML 改為等效的 `implementation 'com.aspose:aspose-cells:24.10'`。當相依性解決後，即可撰寫與 Excel 檔案互動的 Java 程式碼。

## 步驟 2：載入活頁簿 – 準備匯出 Excel 表格為 TXT

第一行實作程式碼永遠相同：開啟包含欲匯出表格的活頁簿。

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

此處取得第一個工作表 (`get(0)`)。若資料位於其他工作表，只需更改索引或使用 `get("SheetName")`。此步驟對於 **export excel table to txt** 至關重要，因為匯出器是以工作表層級運作的。

## 步驟 3：設定自訂儲存格分隔符 – 匯出的核心

現在重頭戲上場：設定 `ExportTableOptions`。此物件讓你精確決定每個儲存格在最終文字檔中的呈現方式。

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

為什麼要 **set custom cell separator**？預設的分隔符是製表符，若資料本身已包含製表符就會衝突。改用管道符號 (`|`) 或分號，可確保下游解析器讀取檔案時，各欄位保持分離。

### 匯出 Excel 公式為文字

`setFormulaValueInCell(true)` 這行指示 Aspose.Cells 將 **export excel formulas to text** 寫入公式的 *結果*，而非公式字串本身。若省略此設定，包含 `=SUM(A1:A5)` 的儲存格會在 TXT 中顯示為 `=SUM(A1:A5)`，這通常不是你想要的結果。

## 步驟 4：將匯出選項附加至 TXT 儲存選項

現在我們將這些表格選項綁定到整體的 TXT 匯出設定。

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` 是控制整個工作表輸出的總管物件。將 `exportTableOptions` 插入其中，即可確保工作表上所有表格皆遵循 **set custom cell separator** 的規則。

## 步驟 5：將工作表儲存為 TXT 檔案 – 完成匯出

最後，我們將檔案寫入磁碟。

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

執行此程式會產生 `TableExported.txt`。原始 Excel 表格的每一列現在會以管道分隔的值呈現在一行，例如：

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

請注意 **Total** 欄位的公式在寫入前已被計算——感謝 `setFormulaValueInCell(true)`。這正是 **export excel data as plain text** 同時保留計算結果的核心。

## 步驟 6：驗證輸出 – 看起來正確嗎？

使用任意文字編輯器開啟產生的 `TableExported.txt`。你應該會看到：

- 每個 Excel 列對應一行文字。
- 欄位以你使用 `setCellValueSeparator` 設定的管道符號分隔。
- 除非原始儲存格值本身包含，否則不會出現多餘的逗號或製表符。
- 只寫入公式結果，而非公式字串本身。

若發現任何非預期的字元，請再次確認你所選的分隔符。某些字元（如管道符號）對大多數 CSV 風格的解析器而言是安全的，但若資料已包含管道符號，請考慮改用其他分隔符，例如 `~` 或製表符 (`\t`)。

## 小技巧、邊緣案例與最佳實踐 – 匯出 Excel 資料為純文字

| 情況 | 處理方式 |
|-----------|------------|
| **資料已包含所選的分隔符** | 改用較不常見的字元（`^`、`~` 或 Unicode 非印刷字元）。 |
| **需要 UTF‑8 編碼** |  |

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並在此基礎上深入。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [使用 Aspose.Cells 儲存 Excel 為自訂分隔符的文字檔](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [使用 Aspose Cells Net 儲存 Excel 文字自訂分隔符](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [使用 Aspose Cells Net 儲存 Excel 文字自訂分隔符](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}