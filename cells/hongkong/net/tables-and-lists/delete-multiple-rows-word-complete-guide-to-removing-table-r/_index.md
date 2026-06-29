---
category: general
date: 2026-06-27
description: 使用 C# 刪除 Word 中的多行。學習如何刪除表格行、移除表格行以及高效編輯 Word 文件中的表格。
draft: false
keywords:
- delete multiple rows word
- how to delete table rows
- how to remove table rows
- delete rows from word table
- word document table editing
language: zh-hant
og_description: 即時刪除 Word 中的多行。本教學示範如何刪除表格行、從 Word 表格中移除行，以及精通 Word 文件的表格編輯。
og_title: 在 Word 中刪除多列 – 步驟式表格編輯
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Delete multiple rows word using C#. Learn how to delete table rows,
    remove table rows and edit Word document tables efficiently.
  headline: Delete Multiple Rows Word – Complete Guide to Removing Table Rows
  type: TechArticle
tags:
- Aspose.Words
- C#
- Word Automation
title: 刪除 Word 中的多列 – 完整指南：移除表格列
url: /zh-hant/net/tables-and-lists/delete-multiple-rows-word-complete-guide-to-removing-table-r/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 刪除多行 Word – 完整的表格列移除指南

是否曾經需要在 **delete multiple rows word** 文件中刪除多行卻不確定該使用哪個 API 呼叫？您並不孤單——大多數開發人員在嘗試縮減表格同時保留標題時，都會遇到相同的困擾。  

在本教學中，我們將示範一個簡潔、端對端的解決方案，說明 *如何以程式方式刪除表格列*、*如何安全地移除表格列*，以及為何此方法能適用於每一個 **delete rows from word table** 情境。

完成後，您將擁有一段可重複使用的程式碼片段，能直接放入任何 C# 專案，並附帶一些針對更廣泛 **word document table editing** 任務的技巧。

## 前置條件

- .NET 6.0 或更新版本（程式碼亦可在 .NET Framework 4.6+ 上執行）
- 已安裝 Aspose.Words for .NET（`dotnet add package Aspose.Words`）
- 具備 C# 語法的基本認識
- 一個包含至少一個帶有標題列的表格的 `.docx` 輸入檔案

> **Pro tip:** 若您尚未取得授權，Aspose.Words 提供免費的評估模式，非常適合測試使用。

## 步驟 1：設定專案並載入 Word 文件

首先，建立一個 console 應用程式（或整合至現有服務），加入必要的 `using` 指示詞，然後載入來源文件。

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // Load the Word document (replace YOUR_DIRECTORY with your actual path)
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded successfully.");
```

**為什麼這很重要：**  
`Document` 是每個 Aspose.Words 操作的入口點。一次載入檔案即可降低記憶體使用，並讓您取得後續所有表格編輯呼叫的操作句柄。

## 步驟 2：定位第一個表格（或任何您需要的表格）

如果文件中包含多個表格，您可以依索引或關鍵字搜尋來挑選目標表格。為了簡化示範，我們直接取得第一個表格，通常它就是我們想要裁剪的資料所在。

```csharp
        // Retrieve the first table in the document
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found in the document.");
            return;
        }
        Console.WriteLine($"Table with {firstTable.Rows.Count} rows found.");
```

**說明：**  
`GetChild(NodeType.Table, 0, true)` 以深度優先方式遍歷文件樹，回傳第一個遇到的 `Table` 節點。`as Table` 的型別轉換安全地將節點轉為 `Table`，讓我們稍後能操作 `Rows`。

## 步驟 3：在保留標題的同時刪除多行

現在進入重點：**delete multiple rows word** 文件。假設標題位於第 0 列，您想刪除接下來的兩列（索引 1 與 2），`DeleteRows` 方法正好能做到這點。

```csharp
        // Delete two rows starting from the second row (index 1)
        // This keeps the header row untouched while removing the following rows
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Specified rows deleted.");
```

### 如何刪除表格列 – 變體

- **刪除單一列：** `firstTable?.DeleteRows(rowIndex, 1);`
- **刪除除標題外的所有列：** `firstTable?.DeleteRows(1, firstTable.Rows.Count - 1);`
- **根據條件刪除列：** 迭代 `firstTable.Rows`，當儲存格符合您的條件時呼叫 `DeleteRows`。

這些程式碼片段以彈性的方式回答了常見的 **how to remove table rows** 問題。

## 步驟 4：儲存已修改的文件

列刪除完成後，只需將文件寫回磁碟。您可以覆寫原始檔案，或另存為新檔案。

```csharp
        // Save the modified document
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Document saved as output.docx");
    }
}
```

**您將看到：**  
如果原始表格有五列（標題 + 四筆資料），儲存的 `output.docx` 現在只會剩下三列（標題 + 兩筆剩餘資料）。在 Word 中開啟檔案，即可驗證不需要的列已消失，且其他內容未受影響。

![delete multiple rows word – Word 表格的前後截圖](delete-multiple-rows-word.png)

*Image alt text: delete multiple rows word – Word 表格的前後截圖.*

## 完整、可直接執行的範例

將前面的步驟整合起來，以下是您可以直接複製貼上的完整程式：

```csharp
using System;
using Aspose.Words;
using Aspose.Words.Tables;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the Word document
        Document doc = new Document(@"YOUR_DIRECTORY\input.docx");
        Console.WriteLine("Document loaded.");

        // 2️⃣ Retrieve the first table
        Table firstTable = doc.GetChild(NodeType.Table, 0, true) as Table;
        if (firstTable == null)
        {
            Console.WriteLine("No table found.");
            return;
        }
        Console.WriteLine($"Found table with {firstTable.Rows.Count} rows.");

        // 3️⃣ Delete rows – this is the core of delete rows from word table
        //    Starting at index 1 (second row), delete the next two rows.
        firstTable?.DeleteRows(1, 2);
        Console.WriteLine("Rows deleted.");

        // 4️⃣ Save the result
        doc.Save(@"YOUR_DIRECTORY\output.docx");
        Console.WriteLine("Saved output.docx");
    }
}
```

執行程式、開啟 `output.docx`，您會看到標題仍在，而選取的列已消失。這就是 **delete multiple rows word** 的實際運作。

## 常見陷阱與避免方法

| 問題 | 為何會發生 | 解決方法 |
|-------|----------------|-----|
| **NullReferenceException** 當 `firstTable` 為 `null` 時 | 文件中沒有表格或索引錯誤 | 在呼叫 `DeleteRows` 前，務必檢查 `firstTable != null`。 |
| **列未被刪除** | 使用了錯誤的起始索引（Word 表格是從 0 開始） | 請記住標題是第 0 列；若要保留標題，請從第 1 列開始。 |
| **覆寫唯讀檔案** | 檔案權限阻止覆寫 | 儲存至不同路徑或調整檔案屬性。 |
| **意外的版面變化** | 刪除包含合併儲存格的列可能會損壞表格 | 確保先處理合併儲存格——先取消合併或謹慎刪除整列。 |

## 擴充解決方案 – 更多 Word 文件表格編輯

如果您對更廣泛的 **word document table editing** 有興趣，請考慮以下進階步驟：

- **插入新列**：`firstTable?.Rows.Add(new Row(doc));`
- **更新儲存格文字**：`firstTable.Rows[rowIndex].Cells[colIndex].Paragraphs[0].AppendText("New value");`
- **套用樣式**：使用 `CellFormat` 或 `RowFormat` 設定底色、邊框或字型屬性。
- **匯出為 PDF**：`doc.Save("output.pdf", SaveFormat.Pdf);`

所有這些操作皆建立在我們用於刪除列的相同物件模型上，讓程式碼基礎保持一致。

## 結論

我們剛剛示範了如何使用少量 C# 程式碼 **delete multiple rows word** 文件。此方法涵蓋 *如何刪除表格列*、*如何移除表格列*，以及更廣泛的 **word document table editing** 主題。

現在您擁有一套穩固、可重複使用的模式：載入文件、定位表格、以正確的索引呼叫 `DeleteRows`，最後儲存。之後您可以調整列範圍、遍歷多個表格，或結合其他編輯功能，以符合任何自動化需求。

想更進一步嗎？試著自動產生發票、清理報告範本，或打造一次處理數十個 Word 檔的批次更新工具。只要有 API，工作就能變得輕鬆無痛。

如有任何問題，歡迎在下方留言——祝編程愉快！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能進一步深化您對 API 功能的掌握，並提供在實務專案中可替代的實作方式。

- [如何在 Excel 中使用 Aspose.Cells for .NET 插入與刪除列：完整指南](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [在 Excel 中使用 Aspose.Cells .NET 刪除多列：資料操作完整指南](/cells/english/net/data-manipulation/delete-rows-excel-aspose-cells-net/)
- [在 Aspose.Cells .NET 中刪除多列](/cells/english/net/row-and-column-management/delete-multiple-rows-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}