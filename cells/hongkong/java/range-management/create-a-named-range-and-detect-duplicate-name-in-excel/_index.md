---
category: general
date: 2026-09-27
description: 使用 Aspose.Cells 在 Excel 中建立命名範圍、設定表格名稱、加入命名範圍、建立 Excel 表格，並偵測重複名稱錯誤。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create named range
- set table name
- create excel table
- add named range
- detect duplicate name
language: zh-hant
lastmod: 2026-09-27
og_description: 使用 Aspose.Cells 在 Excel 中建立命名範圍，然後設定表格名稱、加入命名範圍、建立 Excel 表格，並偵測重複名稱錯誤。
og_image_alt: Screenshot showing how to create a named range in Excel with Aspose.Cells
og_title: 在 Excel 中建立命名範圍並偵測重複名稱
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create a named range in Excel using Aspose.Cells, set table name, add
    named range, create Excel table, and detect duplicate name errors.
  headline: Create a named range and detect duplicate name in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: 在 Excel 中建立命名範圍並偵測重複名稱
url: /zh-hant/java/range-management/create-a-named-range-and-detect-duplicate-name-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中建立命名範圍並偵測重複名稱

如果您需要在 Excel 活頁簿中 **建立命名範圍**，且想避免名稱衝突，本指南將示範如何使用 Aspose.Cells for Java 完成此操作。您將學會 **新增命名範圍**、**建立 Excel 表格**、**設定表格名稱**，以及 **偵測重複名稱** 錯誤，全部在一個完整且獨立的範例中。

在建立報表工具、資料驗證工作表或動態儀表板時，使用命名範圍是常見需求。完成本教學後，您將擁有一個可執行的程式，能安全地建立命名範圍、建立表格，並優雅地處理任何名稱衝突例外。

## Prerequisites

- 安裝 Java 17 或更新版本
- 使用 Maven 或 Gradle 進行相依管理
- Aspose.Cells for Java（最新版本；撰寫時的 Maven 坐標為 `com.aspose:aspose-cells:23.9`）
- 具備 Excel 基本概念，如工作表、範圍與表格

## Step 1: Create a named range in the workbook

在活頁簿中建立命名範圍

第一步是實例化一個 `Workbook` 物件，並新增一個指向特定儲存格區塊的命名範圍。

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the default first worksheet (named "Sheet1")
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Define a named range called "MyRange" that covers A1:C5
        // This demonstrates the "add named range" operation.
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");
```

**為什麼這很重要：**  
命名範圍充當可重複使用的參照，公式與表格皆可指向它。提前加入可確保後續步驟能在不硬編碼儲存格位址的情況下重複使用相同的識別碼。

## Step 2: Create Excel table that uses the named range

建立使用命名範圍的 Excel 表格

接下來，我們建立一個結構化表格（ListObject），其佔用的區域與命名範圍相同。這說明了 **create excel table** 概念。

```java
        // Create an Excel table (ListObject) that spans the same area as the named range.
        // The parameters (0,0,4,2) represent the top‑left cell (A1) and bottom‑right cell (C5).
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);
```

**為什麼這很重要：**  
表格提供內建的排序、篩選與樣式功能。將表格與命名範圍對齊，可保持資料模型的一致性。

## Step 3: Set table name and handle a possible conflict

設定表格名稱並處理可能的衝突

現在我們嘗試將表格命名為先前建立的命名範圍名稱。此步驟示範 **set table name**，並刻意觸發名稱衝突。

```java
        try {
            // Attempt to set the table name to "MyRange".
            // Because a named range with the same identifier already exists,
            // Aspose.Cells will throw an exception.
            table.setName("MyRange"); // <-- conflict expected
        } catch (Exception e) {
            // Step 4: Detect duplicate name and respond appropriately
            System.out.println("Name conflict detected: " + e.getMessage());
        }
```

**為什麼這很重要：**  
Excel 不允許表格與命名範圍使用相同的識別碼。提前偵測衝突可防止活頁簿損毀，並讓除錯更容易。

## Step 4: Detect duplicate name and resolve it

偵測重複名稱並解決

當捕獲例外時，您可以重新命名表格或移除衝突的命名範圍。以下示範一個簡單的解決策略，使用字尾重新命名表格。

```java
            // Resolve the conflict by appending a numeric suffix
            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the workbook to verify the result
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**解決方案的重點：**

- **detect duplicate name** – `catch` 區塊確認衝突。  
- 迴圈會檢查活頁簿的名稱集合，以確保新識別碼唯一。  
- 最後，將活頁簿儲存，您即可在 Excel 中開啟，驗證表格擁有不同的名稱，而原始命名範圍仍保持不變。

## Full, runnable example

完整、可執行的範例

將所有部件組合起來，完整程式如下：

```java
import com.aspose.cells.*;

public class NamedRangeDemo {
    public static void main(String[] args) throws Exception {
        // Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Add a named range called "MyRange" covering A1:C5
        workbook.getNames().add("MyRange", "'Sheet1'!$A$1:$C$5");

        // Create an Excel table that occupies the same cells
        ListObject table = sheet.getListObjects().add(0, 0, 4, 2, true);

        try {
            // Try to set the table name to the same identifier
            table.setName("MyRange");
        } catch (Exception e) {
            // Detect duplicate name and resolve it
            System.out.println("Name conflict detected: " + e.getMessage());

            String baseName = "MyRange";
            int suffix = 1;
            String newName;
            do {
                newName = baseName + "_" + suffix;
                suffix++;
            } while (workbook.getNames().get(newName) != null);

            table.setName(newName);
            System.out.println("Table renamed to: " + newName);
        }

        // Save the file for inspection
        workbook.save("NamedRangeDemo.xlsx");
    }
}
```

**執行程式時的預期輸出：**

```
Name conflict detected: A name with the specified identifier already exists.
Table renamed to: MyRange_1
```

在 Excel 中開啟 `NamedRangeDemo.xlsx` 後會看到：

- 一個命名範圍 **MyRange**，指向儲存格 A1:C5。  
- 一個名稱為 **MyRange_1** 的表格，覆蓋相同儲存格。  
- 當您嘗試加入參照 `MyRange` 的公式時，不會出現命名錯誤。

## Common pitfalls and best practices

常見陷阱與最佳實務

- **不要重複使用識別碼**：在將名稱指派給表格前，務必確認該名稱尚未存在。  
- **偏好明確檢查**：`workbook.getNames().get("Name")` 若名稱可用會回傳 `null`，比捕獲一般例外更安全。  
- **保持命名慣例一致**：為表格使用 `tbl_` 前綴、為範圍使用 `rng_` 前綴，可降低衝突機率。  
- **版本相容性**：此程式碼適用於 Aspose.Cells 23.9 及之後版本；較早版本的例外訊息可能不同。

## Conclusion

結論

您現在已了解如何使用 Aspose.Cells for Java **建立命名範圍**、**新增命名範圍**、**建立 Excel 表格**、**設定表格名稱**，以及 **偵測重複名稱** 衝突。透過主動處理命名衝突，您可以保持活頁簿整潔，並讓自動化腳本更具韌性。

**下一步**

- 深入探索 **set table name** API，以套用樣式選項。  
- 在程式化產生多個表格時，使用 **detect duplicate name** 模式。  
- 將命名範圍與公式或資料驗證結合，以實現動態報表。

祝開發順利！

## What Should You Learn Next?

接下來您應該學習什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [Create Style Named Range Excel Aspose Cells Java](/cells/hindi/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Create Style Named Range Excel Aspose Cells Java](/cells/german/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)
- [Create Style Named Range Excel Aspose Cells Java](/cells/french/java/tables-structured-references/create-style-named-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}