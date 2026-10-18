---
category: general
date: 2026-07-06
description: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表 – 程式化複製 Excel 樞紐分析表的逐步指南
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: zh-hant
lastmod: 2026-07-06
og_description: 使用 Aspose.Cells 在 Java 中複製樞紐分析表，可讓您快速且可靠地複製 Excel 樞紐分析表。
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: 如何在 Java 中複製樞紐分析表 – 完整的 Aspose.Cells 指南
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: 如何在 Java 中使用 Aspose.Cells 複製樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 使用 Aspose.Cells 複製樞紐分析表

有沒有想過 **如何在不手動開啟工作簿的情況下** 複製 Excel 檔案中的樞紐分析表？你並不是唯一有此需求的人。在許多報告流程中，你需要即時 **複製 Excel 樞紐分析表**——可能是為了建立快照、移到新工作表，或為下游使用者產生範本。

本教學將逐步示範一個完整、可執行的範例，正好說明上述需求。透過 Aspose.Cells for Java 函式庫，我們會載入工作簿、定位來源樞紐分析表範圍、將其複製到新位置，並儲存結果。沒有模糊的說明，只有你今天就能直接套用到專案的具體解決方案。

---

## 前置條件

* **Java Development Kit (JDK) 8+** – 程式碼可在任何較新的 JDK 上編譯。  
* **Aspose.Cells for Java** 版本 25.11 或更新 – 支援樞紐分析表的 `Range.copy` 方法即在此版本加入。  
* 一個已包含樞紐分析表的 **input.xlsx** 檔案（可在 Excel 中自行建立以作測試）。  
* 你選擇的建置工具（Maven、Gradle，或純 `javac`）。我們將示範 Maven 依賴以快速開始。

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## 步驟 1：載入來源工作簿

首先，我們會開啟包含原始樞紐分析表的 Excel 檔案。Aspose.Cells 將工作簿視為記憶體中的物件，讓你無需啟動 Excel 即可操作。

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **為何重要：** 載入工作簿後，我們即可存取工作表、儲存格，以及最關鍵的支援樞紐分析表的快取。若未執行此步驟，函式庫將無法進行複製。

---

## 步驟 2：取得包含樞紐分析表的工作表

如果工作簿有多個工作表，你需要指向正確的那一張。此處我們直接取得第一張工作表，但也可以使用 `get("SheetName")` 依名稱查找。

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **專業提示：** 處理大量工作表時，建議將索引或名稱快取於設定檔中，以免硬編碼數字。

---

## 步驟 3：定義包含樞紐分析表的來源範圍

自 25.11 版起，Aspose.Cells 允許將樞紐分析表視為普通儲存格範圍。指定左上角與右下角儲存格，即可包住整個樞紐分析表。

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **邊緣情況：** 若樞紐分析表會動態擴展（例如之後新增列），可考慮使用 `worksheet.getPivotTables().get(0).getDataRange()` 以程式方式取得精確範圍。

---

## 步驟 4：定義樞紐分析表要複製到的目標範圍

選擇任意空白儲存格作為複製後樞紐分析表的起始位置。本示範中我們從 **F1** 開始，讓原始與複製之間保留間距。

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **為何不使用新工作表？** 你也可以建立全新工作表（`workbook.getWorksheets().add("Copy")`），並使用其儲存格作為目標。相同的 `copy` 方法在工作表之間亦可使用。

---

## 步驟 5：將樞紐分析表複製到新位置

現在魔法發生了。`copy` 方法會複製樞紐分析表、其快取、格式，甚至任何相關的切片器（以最新版本為準）。

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **重要提示：** 複製操作是*深層*的；它**不會**建立回原始樞紐分析表的參照。你可以獨立修改新樞紐分析表，而不會影響來源。

---

## 步驟 6：儲存含有複製樞紐分析表的工作簿

最後，將修改過的工作簿寫回磁碟。你可以覆寫原始檔案或建立新檔；此處我們選擇後者，以免觸動來源檔案。

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

當你在 Excel 中開啟 **output.xlsx** 時，會看到原始樞紐分析表位於 A‑D 欄，且在 F 欄開始有完整的複製。兩個樞紐分析表可分別重新整理。

---

## 完整範例程式

將上述步驟整合起來，以下是可直接編譯執行的完整 Java 類別：

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**預期結果：** 開啟 `output.xlsx` 後會看到原始樞紐分析表 (A1:D20) 與在 F1 開始的相同樞紐分析表。兩個表格皆保留其篩選條件、樣式與計算欄位。

---

## 處理常見變化情況

| 情況 | 調整方式 |
|-----------|----------------|
| **同一工作表上有多個樞紐分析表** | 遍歷 `worksheet.getPivotTables()`，為每個樞紐分析表使用各自的目標範圍進行複製。 |
| **動態資料範圍** | 使用 `worksheet.getPivotTables().get(0).getDataRange()` 自動偵測來源區域。 |
| **複製到另一個工作簿** | 載入第二個 `Workbook` 實例，建立目標工作表，然後呼叫 `sourceRange.copy(destWorksheet.getCells().createRange("A1"))`。 |
| **保留切片器** | 自 25.12 版起，若範圍包含切片器，會自動複製。儲存後請在 Excel 中驗證。 |

---

## 專業提示與常見陷阱

* **版本檢查：** 支援樞紐分析表的 `copy` 方法於 **Aspose.Cells 25.11** 版加入。若使用較舊版本會拋出例外。請務必在 `pom.xml` 中確認 `aspose-cells` 版本。  
* **效能考量：** 複製大型樞紐分析表可能佔用大量記憶體。若僅需資料，可考慮將樞紐分析表匯出為平面表格，而非完整克隆。  
* **重新整理行為：** 複製的樞紐分析表保有自己的快取。若修改底層資料，請對新樞紐分析表呼叫 `pivotTable.refresh()` 重新計算。  
* **格式差異：** 某些自訂數字格式在非常舊的 Excel 版本（<2007）可能無法保留。請以目標使用者的 Excel 版本進行測試。  

---

## 結論

現在你已掌握使用 Aspose.Cells for Java **複製樞紐分析表** 的完整解決方案，並且看到只需幾行程式碼即可 **複製 Excel 樞紐分析表**。此方法適用於單一或多個樞紐分析表，跨工作表，甚至跨工作簿。

接下來的步驟可以包括：

* 在批次作業中自動為每個樞紐分析表執行複製。  
* 加入程式碼為複製的樞紐分析表重新命名（例如 `pivotTable.setName("Copy_of_Sales")`）。  
* 將此例程整合至更大的報告服務，產生 PDF 或 CSV 匯出。  

試試看，依實際資料調整範圍，讓函式庫處理繁重工作。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎延伸。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [使用 Aspose.Cells Java 操作 Excel 樞紐分析表：完整指南](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 樞紐分析表來源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}