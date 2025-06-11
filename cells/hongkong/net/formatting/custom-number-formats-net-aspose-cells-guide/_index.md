---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells 在 .NET 中實作自訂數位格式以實現精確的 Excel 資料呈現。本指南涵蓋設定、格式化日期、百分比和貨幣。"
"title": "如何在 .NET 中使用 Aspose.Cells&#58; 自訂數字格式逐步指南"
"url": "/zh-hant/net/formatting/custom-number-formats-net-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 如何在.NET中使用Aspose.Cells自訂數字格式：逐步指南

## 介紹

使用 C# 和 .NET 增強您的 Excel 檔案操作，並精確控制數位格式。本教學將指導您使用 Aspose.Cells for .NET（專為 Excel 操作而設計的強大函式庫）在 .NET 應用程式中設定自訂數位格式。

透過利用 Aspose.Cells，可以輕鬆地將各種樣式應用於數據，確保報告的清晰度和準確性。無論是格式化日期、百分比或貨幣值，掌握此功能都可以簡化您的工作流程。

**您將學到什麼：**
- 設定 Aspose.Cells for .NET
- 使用 C# 實作自訂數字格式
- 以程式設計方式將樣式套用至 Excel 儲存格
- 自訂數字格式的實際應用

## 先決條件

開始之前請確保您已具備以下條件：
1. **開發環境**：具有 Visual Studio 或任何相容 IDE 的 .NET 工作設定。
2. **Aspose.Cells for .NET函式庫**：本指南需要 22.x 或更高版本。
3. **基本 C# 知識**：熟悉 C# 文法和程式設計概念將幫助您順利跟進。

## 設定 Aspose.Cells for .NET

若要在專案中使用 Aspose.Cells，請使用 Visual Studio 中的 .NET CLI 或套件管理器控制台安裝程式庫。

**.NET CLI 安裝：**
```bash
dotnet add package Aspose.Cells
```

**套件管理器安裝：**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### 許可證獲取

Aspose.Cells 提供免費試用評估，並透過臨時或購買授權提供延長使用期限的選項。
- **免費試用**：下載自 [這裡](https://releases。aspose.com/cells/net/).
- **臨時執照**申請 [Aspose 臨時許可證頁面](https://purchase.aspose.com/temporary-license/) 消除評估限制。
- **購買**：如需完整訪問權限，請訪問 [購買頁面](https://purchase。aspose.com/buy).

要在您的專案中初始化 Aspose.Cells：
```csharp
// 導入命名空間
using Aspose.Cells;

// 初始化新的 Workbook 對象
Workbook workbook = new Workbook();
```

## 實施指南

我們將介紹使用 Aspose.Cells 自訂數位格式的主要功能。

### 新增自訂日期格式
**概述**：學習使用自訂樣式來格式化 Excel 儲存格中的日期。
1. **建立或存取工作表**
   ```csharp
   int sheetIndex = workbook.Worksheets.Add();
   Worksheet worksheet = workbook.Worksheets[sheetIndex];
   ```
2. **使用自訂格式設定目前系統日期**
   將目前日期新增至儲存格「A1」並套用自訂顯示格式。
   ```csharp
   // 將目前系統日期插入 A1 中
   worksheet.Cells["A1"].PutValue(DateTime.Now);

   // 檢索樣式物件以進行自訂
   Style style = worksheet.Cells["A1"].GetStyle();

   // 將自訂數字格式設定為“d-mmm-yy”
   style.Custom = "d-mmm-yy";

   // 將自訂樣式套用回儲存格 A1
   worksheet.Cells["A1"].SetStyle(style);
   ```

### 將數值格式化為百分比
**概述**：以百分比格式顯示數值。
1. **插入並格式化值**
   ```csharp
   // 向儲存格 A2 新增數值
   worksheet.Cells["A2"].PutValue(20);

   // 取得格式化的樣式
   Style style = worksheet.Cells["A2"].GetStyle();

   // 將自訂數字格式套用為百分比
   style.Custom = "0.0%";

   // 將格式化樣式設定回儲存格 A2
   worksheet.Cells["A2"].SetStyle(style);
   ```

### 應用貨幣格式
**概述**：以貨幣格式顯示數字，並對負值採用特定格式。
1. **插入並設定貨幣值樣式**
   ```csharp
   // 向儲存格 A3 新增值
   worksheet.Cells["A3"].PutValue(2546);

   // 訪問樣式對象
   Style style = worksheet.Cells["A3"].GetStyle();

   // 設定自訂貨幣格式
   style.Custom = "\u00a3#,##0;[Red]$-#,##0";

   // 應用於單元格 A3
   worksheet.Cells["A3"].SetStyle(style);
   ```

## 實際應用

自訂數字格式在以下情況下非常有用：
1. **財務報告**：格式化貨幣值以便更清晰。
2. **銷售儀錶板**：以百分比形式顯示銷售數字以突顯績效指標。
3. **活動企劃**：使用日期格式無縫組織和呈現事件日程。

## 性能考慮
處理大型資料集時，優化 Aspose.Cells 的效能：
- 透過使用以下方式及時處理物件來最大限度地減少記憶體使用 `GC.Collect()` 儲存文件後。
- 利用流讀取/寫入 Excel 文件，而不是將整個文件載入到記憶體中。
- 實施 .NET 記憶體管理中的最佳實務以保持效率。

## 結論
透過遵循本指南，您已經學會如何使用 Aspose.Cells 在 .NET 應用程式中實現自訂數字格式。此功能增強了數據呈現並確保了報告和電子表格的準確性和視覺吸引力。

**後續步驟**：嘗試使用 Aspose.Cells 中可用的其他格式選項，例如條件格式或圖表增強功能。

## 常見問題部分
1. **如何取得 Aspose.Cells 的臨時授權？**
   - 申請 [臨時許可證頁面](https://purchase。aspose.com/temporary-license/).
2. **Aspose.Cells 中的自訂數字樣式支援哪些格式？**
   - 日期、百分比、貨幣等，使用標準 Excel 格式字串。
3. **我可以將 Aspose.Cells 與其他 .NET 語言（如 VB.NET）一起使用嗎？**
   - 是的，該程式庫相容於所有 .NET 支援的語言。
4. **如果我的格式化數字顯示不正確，我該怎麼辦？**
   - 仔細檢查您的自訂數字格式字串是否有拼字錯誤或語法錯誤。
5. **在哪裡可以找到更多 Aspose.Cells 使用範例？**
   - 探索詳細文件和範例程式碼 [Aspose 文檔](https://reference。aspose.com/cells/net/).

## 資源
- [Aspose.Cells for .NET文檔](https://reference.aspose.com/cells/net/)
- [下載最新版本](https://releases.aspose.com/cells/net/)
- [購買許可證](https://purchase.aspose.com/buy)
- [免費試用版下載](https://releases.aspose.com/cells/net/)
- [臨時許可證申請](https://purchase.aspose.com/temporary-license/)
- [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}