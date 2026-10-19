---
category: general
date: 2026-08-17
description: 匯出 Excel 為 TXT 同時限制有效位數 – 學習如何設定位數並在 Java 中將 Excel 轉換為文字，完整的 Aspose.Cells
  範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: zh-hant
lastmod: 2026-08-17
og_description: 匯出 Excel 為 TXT 並限制有效位數。此教學示範如何設定位數以及使用 Aspose.Cells for Java 將 Excel
  轉換為文字。
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: 將 Excel 匯出為 TXT 並限制有效位數 – Java 指南
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: 如何使用 Java 將 Excel 匯出為 TXT 並限制有效位數
url: /zh-hant/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Java 匯出 Excel 為 TXT 並限制有效位數

如果您需要在**匯出 Excel 為 TXT**的同時控制有效位數，本指南提供即用的解決方案。您將了解如何設定位數、將 Excel 轉換為文字，並透過一次設定即可保持輸出整潔。

本範例使用 Aspose.Cells for Java 25.10，該版本加入了 `setSignificantDigits` 選項。完成本教學後，您即可產生僅包含所需位數的 TXT 檔案，無需額外的四捨五入程式碼。

## 您將能夠

- 以程式方式建立工作簿。
- 在儲存格中插入數值。
- 設定 TXT 儲存選項以限制有效位數。
- 將工作簿儲存為純文字檔。
- 了解 `significantDigits` 設定的運作原理，並學會在其他情境下加以調整。

### 前置條件

- Java 17 或更新版本（程式碼亦可在 Java 8 編譯）。
- Aspose.Cells for Java 25.10 或更新版本。從 [Aspose website](https://products.aspose.com/cells/java) 下載 JAR，並加入專案的 classpath。
- IDE 或簡易文字編輯器，搭配指令列建置工具（Maven/Gradle）。

## 步驟 1：設定專案並匯入 Aspose.Cells

建立新的 Java 專案，並將 Aspose.Cells JAR 加入建置路徑。若使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **小技巧：** 使用 `jdk17` classifier 以取得最新的 Java 執行環境；可降低相容性警告的風險。

## 步驟 2：建立工作簿並寫入數值

工作簿在記憶體中代表一個 Excel 檔案。您可以使用 `putValue` 方法將資料寫入任意儲存格。

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

數值 `123.456789` 將作為我們 TXT 匯出的來源。預設情況下，Aspose.Cells 會寫入所有小數位，往往會產生雜訊較多的文字檔。

## 步驟 3：設定 TXT 儲存選項以限制有效位數

Aspose.Cells 提供 `TxtSaveOptions` 以精細控制純文字輸出。`setSignificantDigits` 方法告訴匯出器要保留多少位**總體**的數字，而不僅是小數點之後的位數。

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

當 `significantDigits` 設為 `4` 時，匯出器會將數值 `123.456789` 四捨五入為 `123.5`。此行為符合有效數字的數學定義：保留前四個非零位數。

### 設定與「限制小數位」的差異

- **限制小數位** (`setDecimalPlaces`) 只會裁剪小數點*之後*的位數，與整數部分無關。
- **有效位數** (`setSignificantDigits`) 從第一個非零位開始計算，適用於數值大小差異較大的情況。

若您需要固定的小數位數，請將上述程式碼改為以下內容：

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## 步驟 4：將工作簿儲存為 TXT 檔案

現在使用先前設定的選項將工作簿寫入磁碟。

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

執行程式後會在工作目錄產生 `significant_digits.txt`，檔案內只有一行內容：

```
123.5
```

### 預期輸出

| 儲存格 | 原始值 | 匯出（4 有效位數） |
|------|--------|-------------------|
| A1   | 123.456789 | 123.5 |

若將 `setSignificantDigits(4)` 改為 `6`，輸出會變成 `123.457`。可自行嘗試不同的設定值，觀察四捨五入的變化。

## 步驟 5：常見變形與邊緣情況

### 匯出整個範圍

若要匯出多於一個儲存格，只需在儲存前填滿該範圍：

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

相同的 `significantDigits` 設定會套用至每個數值儲存格，確保檔案內的精度一致。

### 處理特定語系的小數分隔符號

Aspose.Cells 在寫入文字時會遵循系統語系。若要強制使用點 (`.`) 作為小數分隔符，請設定 `TxtSaveOptions` 的 culture：

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

當目標應用程式需要特定格式（例如僅接受 `.` 的 CSV 解析器）時，此設定相當有用。

### 覆寫已存在的檔案

`save` 方法預設會覆寫目標檔案。若需避免意外遺失資料，請先檢查檔案是否已存在：

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### 大型工作簿與記憶體使用量

匯出極大型工作表時，建議使用串流輸出：

```java
saveOptions.setEnableMemorySaving(true);
```

此選項透過逐行寫入，降低堆積記憶體的使用量。

## 完整範例程式

以下提供完整程式碼，您可直接複製、貼上並執行：

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

執行此程式會產生 `significant_digits.txt`，內容如下（以 Tab 分隔欄位）：

```
123.5	0.001235	98770
```

每個數字皆遵守 **4 有效位數** 的規則，證明此設定在不同量級的數值上皆能正常運作。

## 結論

現在您已掌握在 **匯出 Excel 為 TXT** 時控制有效位數的方法。透過 `TxtSaveOptions.setSignificantDigits`，您可以在單一且易於維護的程式碼行中 **設定位數**、**限制小數位**，以及 **限制有效位數**。此方式同樣適用於單一儲存格、完整範圍以及大型工作簿。

### 往後步驟

- 探索其他 `TxtSaveOptions` 屬性，例如使用 `setDelimiter('\t')` 來自訂欄位分隔符。
- 若需逗號分隔值，可將匯出器與 `CsvSaveOptions` 結合使用。
- 將此流程整合至 Web 服務，接受上傳的 Excel 檔案並即時回傳裁切過的 TXT 輸出。

歡迎自行嘗試不同的位數限制與語系設定。若遇到內建選項無法滿足的特殊需求，亦可使用標準的 Java I/O 工具對產生的 TXT 檔案進行後處理。

祝程式開發愉快！

## 接下來您可以學習什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上延伸技術。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 將文字轉換為 Excel 數字](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 建立並匯出 Excel 為 HTML | 工作簿操作指南](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [如何使用 Aspose.Cells for Java 匯出自訂 Excel 屬性為 PDF](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}