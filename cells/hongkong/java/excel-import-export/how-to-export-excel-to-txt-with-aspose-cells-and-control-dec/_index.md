---
category: general
date: 2026-08-20
description: 學習如何使用 Java 將 Excel 匯出為 TXT，限制小數位數、保留有效位數，並將工作簿儲存為 TXT。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: zh-hant
lastmod: 2026-08-20
og_description: 使用 Aspose.Cells 將 Excel 匯出為 TXT。本指南說明如何限制小數位數、保留有效位數，並在 Java 中將工作簿儲存為
  TXT。
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: 在 Java 中將 Excel 匯出為 TXT — 控制小數位與有效位數
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: 如何使用 Aspose.Cells 將 Excel 匯出為 TXT 並控制小數位數
url: /zh-hant/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 將 Excel 匯出為 TXT 並控制小數位精度

如果您需要 **將 Excel 匯出為 TXT**，且必須確保輸出符合特定的小數位數，本教學提供完整解決方案。您將學會如何限制小數位、保留有效位數，並使用 Aspose.Cells for Java **將活頁簿儲存為 TXT**。

本教學將逐步說明建立活頁簿、插入高精度數值、設定 TXT 儲存選項，最後寫入檔案。完成後，您即可產生一個文字檔，內容精確到您所要求的位數，無需額外的後處理。

## 需求條件

- Java 17（或任何受支援的 JDK）
- Aspose.Cells for Java 23.10 或更新版本
- IDE 或建置工具（Maven / Gradle）以管理相依性
- 對輸出目錄具有寫入權限

## 第一步：建立活頁簿並存取第一個工作表

在 **將 Excel 匯出為 TXT** 前，第一步必須建立活頁簿。`Workbook` 類別代表整個 Excel 檔案，`Worksheet` 則讓您存取儲存格。

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*為什麼這很重要*：活頁簿物件包含所有資料、樣式與中繼資料。從全新活頁簿開始，可確保沒有隱藏的格式會影響文字匯出。

## 第二步：加入數值並限制小數位

插入一個具有多個小數位的數字，以示範在匯出時如何 **限制小數位**。

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*為什麼這很重要*：Excel 會儲存完整精度，但在匯出時您可能需要截斷或四捨五入。`limit decimal places` 設定會自動處理此需求。

## 第三步：設定 TXT 儲存選項以保留有效位數

Aspose.Cells 提供 `TxtSaveOptions`。設定 `significantDigits` 可指示匯出器只保留所需的有效位數，忽略前導零。

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*為什麼這很重要*：**保留有效位數** 的選項確保輸出檔案的精度可預測，對於需要固定寬度數值格式的下游系統尤為重要。

## 第四步：將活頁簿儲存為 TXT

最後，將活頁簿寫入文字檔。`save` 方法會遵循先前設定的選項，產生限制小數位的檔案。

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*為什麼這很重要*：使用 **save workbook as txt** 搭配事先設定好的 `TxtSaveOptions`，可保證匯出檔案符合前一步所設定的精度限制。

### `SignificantDigits.txt` 的預期內容

```
0.00012346
```

此值在四捨五入後保留五個有效位數（`12346`），且前導零依照 TXT 格式得以保留。

## 變體與例外情況

| 情境 | 調整方式 |
|------|----------|
| **不同的有效位數** | 呼叫 `txtOptions.setSignificantDigits(n)`，其中 `n` 為 1‑15。 |
| **匯出特定範圍而非整張工作表** | 在儲存前使用 `txtOptions.setExportRange("A1:B10")`。 |
| **保留欄位分隔符** | 設定 `txtOptions.setSeparator('\t')` 以產生 Tab 分隔的輸出。 |
| **大型工作表** | 增加 `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)`，以避免 `OutOfMemoryError`。 |

## 常見陷阱與專業提示

- **不要混淆有效位數與小數位**。前導零不算在有效位數內；若需要固定小數點後位數，請使用 `setSignificantDigits` 取得有意義的精度，或使用 `setDecimalPlaces` 取得固定的小數位數。
- **執行於 IDE 時務必指定絕對輸出路徑**，以免發生權限錯誤。
- **使用 `java.nio.file.Files.readAllLines(Paths.get(outputPath))`** 讀取產生的檔案，驗證內容是否符合預期，再交給下游流程。

## 完整原始碼供參考

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

執行程式後會產生 `SignificantDigits.txt`，內容為單行 `0.00012346`，證明 **export excel to txt** 流程同時滿足 **limit decimal places** 與 **keep significant digits** 兩項需求。

## 結論

現在您已掌握如何使用 Aspose.Cells for Java **將 Excel 匯出為 TXT**，同時控制數值精度。透過設定 `TxtSaveOptions`，您可以 **限制小數位**、**保留有效位數**，並可靠地 **save workbook as txt**，無需額外的後處理。

接下來，您可以探索：

- 將多個工作表分別匯出為不同的 TXT 檔（每張工作表 **save workbook as txt**）
- 使用 `setSeparator` 產生相容 CSV 的輸出
- 為大型資料集自動化批次轉換

歡迎嘗試不同的位數與分隔符，以符合專案的精確需求。祝您開發順利！

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步擴展您在實務專案中的應用技巧。每篇資源皆提供完整可執行的程式碼範例與步驟說明，協助您掌握更多 API 功能與替代實作方式。

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}