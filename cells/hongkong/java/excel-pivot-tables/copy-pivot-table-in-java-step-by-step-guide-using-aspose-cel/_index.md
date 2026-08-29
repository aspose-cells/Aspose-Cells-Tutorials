---
category: general
date: 2026-08-04
description: 使用 Aspose.Cells for Java 複製樞紐分析表。了解如何複製 Excel 範圍、複製樞紐分析表，以及僅用幾行代碼即可複製包含樞紐分析表的工作表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: zh-hant
lastmod: 2026-08-04
og_description: 使用 Aspose.Cells for Java 複製樞紐分析表。本教學將指導您如何複製 Excel 範圍、複製樞紐分析表，並在新工作表中保留所有資料。
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: 在 Java 中複製樞紐分析表 – 完整 Aspose.Cells 教程
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: 在 Java 中複製樞紐分析表 – 使用 Aspose.Cells 的逐步指南
url: /zh-hant/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中複製樞紐分析表 – 使用 Aspose.Cells 的逐步指南

如果您需要在 Java 中將 **樞紐分析表** 從一個工作表複製到另一個工作表，本指南將向您展示如何使用 Aspose.Cells 完成此操作。無論您是以程式方式產生報表，或是構建資料遷移工具，您都會看到一個完整且可執行的範例，能保留樞紐分析表的定義與資料。

複製樞紐分析表不僅僅是複製儲存格範圍；底層的快取與資料來源必須保持完整。在本教學中，我們還會說明如何 **copy excel range**、如何在工作表之間 **duplicate pivot table**，以及如何使用相同的 API **copy worksheet with pivot**。

## 前置條件

* Java Development Kit (JDK) 8 或更新版本。
* Maven 或 Gradle 用於管理相依性。
* Aspose.Cells for Java（最新版本，例如 23.12）。將以下 Maven 坐標加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* 包含第一個工作表上樞紐分析表的來源活頁簿（`Source.xlsx`）。

## 如何使用 Aspose.Cells 在 Java 中複製樞紐分析表

核心概念是複製包含樞紐分析表的 *source range*，然後貼到新的工作表中。Aspose.Cells 會自動複製樞紐快取，因而產生的工作表會包含一個完整可用的 **duplicate pivot table**。

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### 為什麼這樣可行

* **Range copy includes the pivot cache** – Aspose.Cells 將樞紐分析表視為嵌入於儲存格範圍的特殊物件。當您呼叫 `Range.copy` 時，函式庫會同時複製可見儲存格與驅動樞紐的隱藏快取。  
* **No manual recreation needed** – 您不需要重新建立樞紐欄位或資料來源；複製出的樞紐分析表即可立即重新整理。  
* **Works with any Excel version** – 產生的檔案遵循 Office Open XML（XLSX）標準，Excel 2007 以上版本皆可無警告開啟。

## 複製 Excel 範圍 – 於非樞紐資料重複使用相同程式碼

如果您只需要 **copy excel range** 而不涉及樞紐分析表，則可套用相同的模式。只要將範圍位址調整為您想要複製的區域即可。

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

`copy` 方法會保留公式、格式與註解，使其成為任何 Excel 資料區塊的通用解決方案。

## 在多個工作表間複製樞紐分析表

有時您需要將 **duplicate pivot table** 多次複製，例如每個部門一個。遍歷目標工作表，並重複使用相同的 `sourceRange.copy` 呼叫：

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

每個新工作表都包含一個可獨立重新整理的樞紐分析表。快取已被複製，因此在其中一張工作表的變更不會影響其他工作表。

## 複製含樞紐分析表的工作表 – 保留工作表層級設定

如果您想 **copy worksheet with pivot**，同時保留頁面設定、欄寬與命名範圍，可使用 `Worksheet.copy` 取代手動複製範圍。此方法會複製整個工作表，包括樞紐分析表。

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

當工作表內含圖表、圖片或自訂樣式必須與樞紐分析表一併搬移時，`addCopy` 非常方便。

## 常見陷阱與避免方法

| Issue | 發生原因 | 解決方法 |
|-------|----------|----------|
| **Pivot cache lost after copy** | 在個別儲存格上使用 `Cell.copy`（而非範圍）會丟棄隱藏的快取。 | 必須始終複製 *整個* 範圍，包住樞紐分析表，如 Step 2 所示。 |
| **Source range too small** | 範圍未包含樞紐的資料區域，導致新工作表僅顯示靜態值。 | 將位址擴展（例如 `A1:G20`）以涵蓋完整的樞紐分析表及任何切片器或篩選條件。 |
| **Destination workbook version mismatch** | 儲存為 XLS（舊版）會失去現代樞紐功能。 | 儲存為 XLSX（預設）或明確設定 `SaveFormat.XLSX`。 |
| **External data source broken** | 樞紐指向工作簿外的資料來源，複製時未嵌入該來源。 | 在複製後使用 `PivotTable.refreshData()`，或將來源資料嵌入同一工作簿。 |

## 預期輸出

執行程式後：

1. `CopyWithPivot.xlsx` 會出現在 `YOUR_DIRECTORY` 中。  
2. 在 Excel 中開啟該檔案會看到一個名為 **CopySheet** 的新工作表。  
3. **CopySheet** 包含一個功能完整、與原始樞紐分析表相同的樞紐分析表，隨時可重新整理。  
4. 所有格式、篩選與計算欄位皆被保留。

若開啟 `FullCopy.xlsx`，您會看到原始工作表的完整副本，包含來源工作表上的所有圖表與圖片。

## 重點回顧

* 您已學會如何在 Java 中使用 Aspose.Cells **copy pivot table**。  
* 相同的方法也適用於純粹的 **copy excel range** 或 **copy range java** 情境。  
* 若需大量操作，您可以在多張工作表上 **duplicate pivot table**。  
* 當需要整張工作表時，可使用 `addCopy` **copy worksheet with pivot**。

## 往後步驟

* 探索 **PivotTable.refreshData()** 以在複製後以程式方式更新快取。  
* 將複製邏輯與 **Excel file streaming** 結合，以在不將整本活頁簿載入記憶體的情況下處理大型活頁簿。  
* 若您的報表依賴互動式篩選，請查看 Aspose.Cells 對 **pivot slicers** 的支援。

歡迎將程式碼套用到您自己的專案結構、嘗試不同的範圍大小，或整合至更大型的資料處理流程。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 更新 Excel 樞紐分析表來源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel 樞紐分析表操作 Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [建立新 Excel 活頁簿 – 複製與重複樞紐分析表](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}