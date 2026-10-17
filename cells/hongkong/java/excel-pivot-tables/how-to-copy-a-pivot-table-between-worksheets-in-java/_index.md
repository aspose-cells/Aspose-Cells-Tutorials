---
category: general
date: 2026-10-16
description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表 – 學習將範圍複製到其他工作表以及在工作表之間高效複製範圍。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: zh-hant
lastmod: 2026-10-16
og_description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表。本教學示範如何將範圍複製到另一工作表，以及在工作表之間複製範圍，並提供完整程式碼。
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: 如何在 Java 中於工作表之間複製樞紐分析表 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: 如何在 Java 中於工作表之間複製樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中於工作表之間複製樞紐分析表

如果您需要在同一本工作簿中將 **how to copy pivot table** 從一個工作表複製到另一個工作表，本指南提供完整、可直接執行的解決方案。您將看到如何複製包含樞紐分析表的來源範圍、保留其功能，並驗證結果——全部使用 Aspose.Cells for Java。

在程式化產生報表時，複製樞紐分析表是一項常見任務，正確執行可避免遺失樞紐快取或破壞公式。完成本教學後，您將能夠 **copy range to another sheet** 與 **copy range between worksheets**，且無需任何手動步驟。

## 您將學習到

* 載入包含樞紐分析表的現有 Excel 檔案。
* 定義保存樞紐分析表的來源範圍。
* 在不同的工作表上定義目的地範圍。
* 使用 `CopyOptions` 以保持樞紐分析表完整。
* 驗證複製的樞紐分析表如預期般運作。

**先決條件**

* Java 17 或更新版本。
* Aspose.Cells for Java（版本 23.12 或更新）。
* 一個在第一個工作表上包含樞紐分析表的 Excel 檔案（`input.xlsx`）。

---

## 使用 Aspose.Cells 複製樞紐分析表

此操作的核心是一個四步驟流程：載入活頁簿、定位來源範圍、設定目的地範圍，然後執行複製。以下將詳細說明每個步驟。

### 步驟 1：載入活頁簿

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*為什麼需要這一步？*  
載入活頁簿會將整個檔案載入記憶體，讓您可以存取工作表、儲存格以及樞紐快取。Aspose.Cells 會自動讀取檔案格式，您無需擔心 `.xls` 與 `.xlsx` 的差異。

### 步驟 2：定位包含樞紐分析表的來源範圍

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*為什麼需要這一步？*  
樞紐分析表儲存在同時參照隱藏快取的儲存格區塊中。透過選取精確的範圍（本例中的 `A1:G20`），可確保在複製範圍時快取仍保持連結。

### 步驟 3：在另一個工作表上定義目的地範圍

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*為什麼需要這一步？*  
在不同工作表上選擇目的地可讓您 **copy range to another sheet**。左上角儲存格（`A1`）是常見的起始點，但您可以透過變更地址將其放置於任意位置。

### 步驟 4：在保留樞紐分析表的同時複製來源範圍

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*為什麼需要這一步？*  
`CopyOptions` 控制會傳輸什麼內容。使用 `PasteType.PASTE_ALL` 可保證樞紐分析表、其格式以及底層公式都會被複製。若未使用這些選項，可能只會複製原始值，導致樞紐功能受損。

### 步驟 5：儲存活頁簿並驗證結果

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

在 Excel 中開啟 `output.xlsx`，並確認：

* 第二個工作表包含與原始表格完全相同且功能完整的樞紐分析表。
* 重新整理樞紐分析表會更新資料，證明快取仍然完整。

---

## 使用 Java 複製範圍至另一個工作表

如果您的目標僅是 **copy range to another sheet** 而不涉及樞紐分析表，相同的程式碼也適用於一般儲存格範圍。唯一的變更是來源地址。`CopyOptions` 設定保持不變，確保公式與格式得以保留。

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

此程式碼片段展示了 API 在樞紐與非樞紐情境下的彈性。

---

## 複製範圍於工作表之間而不遺失公式

當您 **copy range between worksheets** 時，若相對參照發生變化，引用其他工作表的公式可能會斷裂。為避免此情況：

1. 若僅需公式，使用 `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)`。
2. 將目的地工作表保留在同一本活頁簿中，以確保內部參照仍有效。
3. 複製完成後，呼叫 `workbook.calculateFormula();` 以強制重新計算。

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

這些額外步驟可確保複製的範圍即使跨越多個工作表，也能完全如原始範圍般運作。

---

## 專業提示與常見陷阱

| Situation | Tip |
|-----------|-----|
| **樞紐快取未更新** | 複製後，呼叫 `destSheet.getPivotTables().get(0).refresh();` 以重新整理快取。 |
| **複製至不同活頁簿** | 使用 `Workbook destWorkbook = new Workbook();`，然後執行 `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`。如有需要，請記得另行複製樞紐快取。 |
| **大型樞紐分析表** | 將 Java 堆積大小提升至 (`-Xmx2g`) 以避免在複製過程中發生 `OutOfMemoryError`。 |
| **保留樣式** | 設定 `copyOptions.setPasteType(PasteType.PASTE_ALL)`；否則僅會複製值。 |

---

## 預期輸出

執行完整程式會產生 `output.xlsx`。在 Excel 中開啟時：

* **Sheet2!A1:G20** 顯示與 **Sheet1!A1:G20** 相同的樞紐分析表。
* 樞紐欄位清單、列/欄標籤以及資料值皆與來源相符。
* 重新整理樞紐分析表會更新數字，證實快取功能正常。

主控台將列印：

```
Pivot table copied successfully.
```

---

## 結論

在本教學中，您學會了使用 Aspose.Cells for Java 從一個工作表複製 **how to copy pivot table** 到另一個工作表。透過載入活頁簿、選取正確的來源範圍、定義目的地，並設定 `CopyOptions`，您即可可靠地 **copy range to another sheet** 與 **copy range between worksheets**，同時保留所有樞紐功能。  

接下來，您可以探索：

* 將複製的樞紐分析表匯出為 PDF 或 HTML。
* 在多本活頁簿間自動化樞紐分析表的重新整理。
* 使用 `CopyOptions` 僅複製特定元素（例如值、格式）。

歡迎嘗試不同的範圍地址、活頁簿結構，甚至跨活頁簿的複製。祝編程愉快！

## 接下來您應該學習什麼？

以下教學涵蓋與本指南密切相關的主題，並在此基礎上進一步擴展。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能並探索在專案中的替代實作方式。

- [如何在 Java 中複製範圍 – 使用 Aspose.Cells 複製樞紐分析表](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [如何在 Java 中複製樞紐分析表 – 完整 Aspose.Cells 指南](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [複製 Excel 樞紐分析表 – 使用 Java 的逐步指南](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}