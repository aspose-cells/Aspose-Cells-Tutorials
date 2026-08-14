---
category: general
date: 2026-08-14
description: 如何使用 Aspose.Cells 設定分隔符並儲存為 CSV、限制位數、匯出 CSV 字串，以及在 Java 中重新計算公式
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: zh-hant
lastmod: 2026-08-14
og_description: 如何使用 Aspose.Cells 設定分隔符並儲存為 CSV、限制位數、匯出 CSV 字串，以及在 Java 中重新計算公式。
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: 如何設定分隔符並另存為 CSV – Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: 如何設定分隔符並以 Aspose.Cells 儲存為 CSV
url: /zh-hant/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何設定分隔符並以 CSV 儲存（使用 Aspose.Cells）

如果您需要在將 Excel 活頁簿匯出資料時 **設定分隔符**，本指南將示範如何使用 Aspose.Cells for Java 完整、端對端的解決方案。您將學習如何設定 CSV 分隔符、限制有效位數、匯出 CSV 字串，以及在載入活頁簿後重新整理動態陣列公式。

本教學涵蓋在本機執行程式碼所需的一切，包括處理如日本天皇年號等特殊曆法。完成後，您將能產生正確的 CSV 檔案、控制數值精度，並確保公式為最新狀態。

## 前置條件

- Java 17 或更新版本（程式碼亦可在 JDK 11+ 上編譯）
- Aspose.Cells for Java 23.9 或更新版本 – 從 [Aspose 官方網站](https://products.aspose.com/cells/java/) 下載
- 具備 Maven 或 Gradle 依賴管理的基本認識
- 開發環境（IntelliJ IDEA、Eclipse、VS Code）或簡易文字編輯器加指令列

> **專業提示：** 建議使用專屬的 `libs` 資料夾或 Maven Central 來放置 Aspose.Cells JAR，確保其在 classpath 中。以下範例假設為 Maven 專案。

## 步驟 1：設定 Maven 專案

建立包含 Aspose.Cells 相依性的 `pom.xml`：

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

執行 `mvn clean compile` 以下載函式庫並確認建置成功。

## 步驟 2：設定分隔符並儲存為 CSV

主要目標是在將 Excel 活頁簿儲存為 CSV 時，將預設的逗號分隔符改為自訂字元（例如分號）。Aspose.Cells 提供 `CsvSaveOptions` 以達成此目的。

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### 為什麼這樣可行

- `CsvSaveOptions.setDelimiter(char)` 告訴 Aspose.Cells 使用哪個字元作為欄位分隔符。預設為逗號，但任何字元（如 Tab `'\t'`、管線符 `'|'` 等）皆可使用。
- `setSignificantDigits(int)` 限制數值精度，滿足 **如何限制位數** 的需求，無需手動格式化每個儲存格。

#### 預期輸出

`output.csv` 檔案將包含如下列：

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

請注意，數字會四捨五入至五個有效位數（例如 `123.45678` → `123.46`）。

## 步驟 3：儲存 CSV 時限制位數

若需更精細的數值格式控制，也可以使用 `CsvSaveOptions` 例項來指定自訂的數字格式字串。

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` 採用 .NET 風格的模式，Aspose.Cells 會遵循此格式。
- 同時使用 `setNumberFormat` 與 `setSignificantDigits`，即可在不同語系間獲得可預測的四捨五入結果。

## 步驟 4：使用自訂分隔符將 CSV 匯出為字串

有時您不需要實體檔案，而是需要將 CSV 資料保存在記憶體中（例如作為 HTTP 回應傳送）。`ExportTableOptions` 類別可讓您將範圍匯出為字串。

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### 何時使用此方式

- 從 REST 端點回傳 CSV（Spring 中的 `@RestController`）
- 將 CSV 資料嵌入電子郵件附件，無需寫入磁碟
- 在單元測試期間快速執行資料檢查

## 步驟 5：載入活頁簿後重新計算公式

如果活頁簿內含公式——尤其是近期 Excel 版本引入的 **動態陣列公式**——必須在載入檔案後重新計算。Aspose.Cells 會自動重新整理動態陣列的結果，但對於一般公式仍需呼叫 `calculateFormula()`。

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### 為什麼需要重新計算？

- 公式可能參照外部資料或易變函數（`NOW()`、`RAND()`），需要取得最新值。
- 動態陣列公式（例如 `=SORT(A1:A10)`）會自動評估，但呼叫 `calculateFormula()` 可確保所有工作表的一致性。

## 步驟 6：完整端對端範例

以下是一個單一類別，示範 **如何設定分隔符**、**儲存為 CSV**、**限制位數**、**匯出 CSV 字串**、**載入含特殊曆法的活頁簿**，以及 **重新計算公式**。此程式碼可直接複製貼上至您的專案中。

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### 驗證結果

1. 在文字編輯器中開啟 `output.csv` – 您應該會看到每欄位以分號 (`;`) 分隔。
2. 確認數值欄位最多顯示五個有效位數。
3. 主控台輸出會列印第 4 步產生的 CSV 字串。
4. 在 Excel 中開啟 `japan_updated.xlsx` – 先前顯示 `#REF!` 或過時值的公式現在會顯示正確結果。

## 常見陷阱與避免方法

| 問題 | 原因 | 解決方案 |
|-------|-------|-----|
| CSV 顯示額外的引號 | 儲存格內含逗號，而分隔符也是逗號 | 使用不同的分隔符（`;` 或 `\t`），透過 `setDelimiter` 設定 |
| 數字四捨五入不正確 | `setSignificantDigits` 在自訂數字格式之後套用 | 先套用 `setNumberFormat`，再套用 `setSignificantDigits` |

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，提供完整的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 載入與儲存 Excel 為 CSV：完整指南](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [如何使用 Aspose.Cells for Java 載入 CSV 檔案：完整指南](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [如何在 Java 中使用自訂解析器載入 CSV 檔案（搭配 Aspose.Cells）](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}