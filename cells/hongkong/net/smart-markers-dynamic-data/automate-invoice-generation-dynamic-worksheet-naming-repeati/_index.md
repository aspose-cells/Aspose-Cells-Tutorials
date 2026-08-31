---
category: general
date: 2026-02-14
description: 使用 SmartMarker 自動化發票生成：學習如何重複工作表、動態命名工作表，並在數分鐘內掌握動態工作表命名。
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: zh-hant
og_description: 使用 SmartMarker 自動化發票生成。本指南說明如何重複工作表、動態命名工作表，以及掌握動態工作表命名。
og_title: 自動化發票生成 – 動態工作表命名與重複
tags:
- C#
- SmartMarker
- Excel Automation
title: 自動化發票產生 – C# 中的動態工作表命名與重複
url: /zh-hant/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

there are bullet lists.

We must keep the same structure.

Let's produce translation.

First shortcodes lines unchanged.

Then heading "# Automate Invoice Generation – Dynamic Worksheet Naming & Repeating in C#" translate to Traditional Chinese (Hong Kong). Something like "# 自動化發票產生 – 動態工作表命名與重複 (C#)". Keep the rest.

Proceed.

Will translate each paragraph.

Make sure not to translate code block placeholders.

Also keep markdown formatting.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 自動化發票產生 – 動態工作表命名與重複 (C#)

有沒有想過 **自動化發票產生**，而不需要為每筆訂單手動複製工作表？你並不孤單。許多開發者在需要為每張發票建立獨立工作表，同時希望工作表名稱能反映訂單編號時，常會卡關。本文將使用 SmartMarker 的 `SmartMarkerProcessor` 來解決這個問題，示範 **如何動態命名工作表**，並說明 **如何為每筆記錄重複工作表**。完成後，你將得到一個可直接執行的 C# 範例，產生的活頁簿中每張發票都位於各自命名良好的分頁。

我們會一步一步說明——從從資料來源取得訂單、設定 `SmartMarkerOptions` 以實現動態工作表命名。全部內容都在此，不需要額外文件。只要具備基本的 C# 知識，並參考 Aspose.Cells 函式庫（或任何支援 SmartMarker 的引擎）即可。

---

## 你將建立的功能

- 取得一系列訂單物件。
- 設定 SmartMarker 以 **為每筆訂單重複工作表**。
- 使用 `{OrderId}` 佔位符 **動態命名工作表**。
- 產生 Excel 檔案，分頁名稱分別為 `Invoice_12345`、`Invoice_67890` 等。
- 開啟活頁簿驗證輸出結果。

---

## 前置條件

- .NET 6.0 或更新版本（程式碼亦可在 .NET 5+ 編譯）。
- Aspose.Cells for .NET（或任何實作 SmartMarker 的函式庫）。透過 NuGet 安裝：

```bash
dotnet add package Aspose.Cells
```

- 一個基本的 `Order` 類別（可自行替換為自己的 DTO）。

---

## 步驟 1：建立專案與模型

首先，建立一個新的 Console 應用程式，並定義代表訂單的資料模型。

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **小技巧：** 示範用的模型保持輕量即可，之後若需要加入明細、稅金等資訊，再自行擴充。

---

## 步驟 2：準備 Excel 範本

SmartMarker 需要以範本活頁簿作為基礎。建立一個名為 `InvoiceTemplate.xlsx` 的檔案，裡面只有一個工作表，名稱為 `InvoiceTemplate`。在 **A1** 儲存格放入 SmartMarker 佔位符，例如：

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

你可以自行設定儲存格格式——粗體標題、貨幣格式等。將檔案存放在專案根目錄下。

> **為什麼要使用範本？** 這樣可以把版面設計與程式碼分離，讓設計師在不觸碰程式邏輯的情況下調整外觀。

---

## 步驟 3：設定 SmartMarker 選項 – 重複與命名工作表

接下來，我們告訴 SmartMarker **為每筆訂單重複** 範本工作表，並為每個副本指定一個包含訂單編號的名稱。這就是 **動態工作表命名** 的核心。

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### 工作原理

- **`RepeatWorksheet = true`** 讓引擎依據 `orders` 集合的每個元素，複製來源工作表。這滿足 **如何重複工作表** 的需求。
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** 為命名樣板，`{OrderId}` 會在每次合併時被 SmartMarker 替換為當前訂單的 ID。這即是 **如何命名工作表** 以及 **動態工作表命名** 的解答。
- 處理器會把每筆訂單的欄位（`{{OrderId}}`、`{{Customer}}` 等）合併到複製出的工作表中，產生完整的發票。

---

## 步驟 4：執行程式並驗證輸出

編譯並執行 Console 應用程式：

```bash
dotnet run
```

你應該會在主控台看到成功訊息。開啟 `GeneratedInvoices.xlsx`，會看到三個分頁：

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

每張工作表都已將訂單資料填入佔位符，且保留了範本的版面配置，證明 **自動化發票產生** 能端對端運作。

### 預期截圖（SEO 用 alt 文字）

![自動化發票產生範例，顯示三個動態命名的工作表](/images/invoice-automation.png)

> *圖片 alt 文字包含主要關鍵字，以符合 SEO 需求。*

---

## 步驟 5：邊緣案例與常見變化

### 若 OrderId 含有非法字元該怎麼辦？

Excel 工作表名稱不能包含 `\ / ? * [ ] :`。如果你的 ID 可能出現這些字元，請先進行清理：

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

在 `Order` 類別加入計算屬性：

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### 想保留原始範本工作表嗎？

設定 `smartMarkerOptions.RemoveTemplate = false;`（預設為 `true`）。這樣原本的 `InvoiceTemplate` 仍會保留，作為參考。

### 想依客戶分組發票？

可以使用 **巢狀重複群組**。先依客戶重複，然後在每個客戶的工作表內再依訂單重複。語法會稍微複雜，但原理相同——使用 `RepeatWorksheet` 並以反映層級的命名模式。

---

## 完整範例（所有程式碼一次呈現）

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

將此內容貼到 `Program.cs`，並將 `InvoiceTemplate.xlsx` 放在同一目錄，即可執行。

---

## 常見問答

**Q: 這種做法能處理大量資料（數千張發票）嗎？**  
A: 能。SmartMarker 會有效率地串流資料，但仍需留意記憶體使用量。若遇到上限，可考慮分批處理，並將每批寫入不同的活頁簿。

**Q: 能否自動在每張發票上加入公司標誌？**  
A: 完全可以。只要把標誌圖片放在範本工作表上，因為工作表會被複製，標誌會自動出現在每張產生的發票上，無需額外程式碼。

**Q: 若需要保護工作表該怎麼做？**  
A: 處理完畢後，遍歷 `wb.Worksheets`，呼叫 `ws.Protect(Password, ProtectionType.All)` 即可。

---

## 結論

我們已透過 SmartMarker 的 **重複工作表** 功能與巧妙的命名模式，實作了 **自動化發票產生**。本教學說明了 **如何命名工作表**、展示了 **如何為每筆訂單重複工作表**，以及 **動態工作表命名** 的完整流程，讓你的活頁簿保持整潔且易於搜尋。

從取得資料、建立範本、設定 `SmartMarkerOptions`、到處理邊緣案例，你現在擁有一個完整、可執行的解決方案。接下來，可嘗試加入明細表、套用條件格式，或將同樣的資料匯出為 PDF，打造全自動化的開票流程。

想更進一步嗎？探索「大量 Excel 匯出與 Aspose.Cells」、「工作表 PDF 轉換」或「直接從 C# 發送產生的發票」等相關主題。天地無限，祝開發順利！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}