---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells for .NET 將 DataTables 中的 HTML 格式資料無縫匯入 Excel 電子表格，保留所有文字樣式並提高您的工作效率。"
"title": "如何使用 Aspose.Cells for .NET 將 HTML 格式的資料表匯入 Excel"
"url": "/zh-hant/net/import-export/aspose-cells-net-data-table-import-html-formatting/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 如何使用 Aspose.Cells for .NET 將 HTML 格式的資料表匯入 Excel

## 介紹

您是否正在為在 Excel 中手動格式化匯入的網頁或資料庫資料而苦惱？你並不孤單！開發人員經常需要維護粗體和斜體等文字樣式，這對於可讀性至關重要。使用 Aspose.Cells for .NET，將包含 HTML 格式字串的 DataTable 匯入 Excel 工作簿並保留樣式變得毫不費力。

在本教學中，您將學習如何使用 Aspose.Cells 將 DataTable 中的 HTML 格式資料匯入 Excel，確保您的資料在電子表格中完全按照預期顯示。

**您將學到什麼：**
- 設定和配置 Aspose.Cells for .NET
- 使用 Aspose.Cells 匯入 HTML 格式的資料表
- 自動調整行和列的大小以適應內容
- 以多種格式儲存工作簿，例如 XLSX 和 ODS

首先確保您具備必要的先決條件！

## 先決條件

在深入研究之前，請確保您已：
- **所需庫：** Aspose.Cells for .NET（版本 21.9 或更高版本）
- **環境設定要求：** 安裝了 .NET Core SDK 的 Visual Studio
- **知識前提：** 對 C# 有基本的了解，並熟悉 .NET 中的 DataTables

## 設定 Aspose.Cells for .NET

首先，透過以下方式在您的專案中安裝 Aspose.Cells 庫：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.Cells
```

**使用套件管理器控制台：**
```plaintext
PM> NuGet\Install-Package Aspose.Cells
```

取得完整功能的許可證 [Aspose 網站](https://purchase.aspose.com/temporary-license/) 不受限制地探索所有功能。

### 基本初始化

以下是使用 Aspose.Cells 初始化專案的方法：
```csharp
using Aspose.Cells;

// 初始化新的 Workbook 對象
Workbook workbook = new Workbook();
```

這為使用 Aspose.Cells 在 .NET 中處理 Excel 檔案奠定了基礎。

## 實施指南

讓我們將匯入 HTML 格式的 DataTables 分解為清晰的步驟。

### 準備資料來源

**概述：**
首先設定一個包含 HTML 格式字串的範例資料 DataTable，以示範 Aspose.Cells 的樣式功能。
```csharp
using System.Data;

// 在此設定來源目錄和輸出目錄
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string OutputDir = "YOUR_OUTPUT_DIRECTORY";

// 準備一個包含一些 HTML 格式值的 DataTable
dataTable = new DataTable("Products");
dataTable.Columns.Add("Product ID", typeof(Int32));
dataTable.Columns.Add("Product Name", typeof(string));
dataTable.Columns.Add("Units In Stock", typeof(Int32));

// 使用 HTML 格式新增一行
DataRow dr = dataTable.NewRow();
dr[0] = 1;
dr[1] = "<i>Aniseed</i> Syrup"; // 產品名稱的 HTML 斜體
dr[2] = 15;
dataTable.Rows.Add(dr);

dr = dataTable.NewRow();
dr[0] = 2;
dr[1] = "<b>Boston Crab Meat</b>"; // 產品名稱 HTML 加粗
dr[2] = 123;
dataTable.Rows.Add(dr);
```

### 設定導入選項

**配置導入表選項：**
使用 `ImportTableOptions` 指定單元格值應解釋為 HTML 字串。
```csharp
// 建立導入選項來處理 HTML 格式的字串
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.IsFieldNameShown = true; // 在匯入中包含列標題
importOptions.IsHtmlString = true; // 將單元格值解釋為 HTML 字串
```

### 將資料導入 Excel

**概述：**
建立工作簿和工作表，然後使用 `ImportData` 將您的 DataTable 以完整的格式匯入 Excel。
```csharp
// 建立工作簿並取得第一個工作表
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// 從第 0 行、第 0 列開始匯入 DataTable
worksheet.Cells.ImportData(dataTable, 0, 0, importOptions);

// 調整行和列的大小以提高可讀性
worksheet.AutoFitRows();
worksheet.AutoFitColumns();
```

### 儲存工作簿

最後，以 XLSX 和 ODS 格式儲存您的工作簿，以確保跨不同電子表格應用程式的相容性。
```csharp
string output1Path = OutputDir + "Output.out.xlsx";
string output2Path = OutputDir + "Output.out.ods";

// 以兩種格式儲存工作簿
workbook.Save(output1Path);
workbook.Save(output2Path);
```

## 實際應用

此功能對於資料呈現很重要的場景非常有用，例如：
- **報告：** 自動將樣式套用至財務報告。
- **資料遷移：** 將網頁抓取的資料移至 Excel 中，同時保留 HTML 格式。
- **庫存管理：** 顯示產品詳細信息，並強調關鍵屬性。

整合此功能可以顯著簡化業務分析和報告任務的流程。

## 性能考慮

處理大型資料集時，請考慮以下事項：
- **優化資料表大小：** 僅包含必要的列以減少記憶體使用量。
- **管理工作簿資源：** 將工作簿儲存到可用資源後立即處理。
- **使用 Aspose.Cells 功能：** 利用內建優化來有效處理複雜的資料結構。

## 結論

您已經掌握了使用 Aspose.Cells for .NET 將 HTML 格式的 DataTables 匯入 Excel 的方法。這項技能可以節省時間並提高報告和文件的呈現品質。

為了進一步探索，請考慮嘗試其他 Aspose.Cells 功能，如圖表整合或條件格式。準備好更進一步了嗎？嘗試在您的下一個專案中實施此解決方案！

## 常見問題部分

**Q：如何處理包含 HTML 內容的大型資料集？**
答：使用 Aspose.Cells 提供的最佳實踐，優化 DataTable 大小並確保 .NET 內高效的記憶體管理。

**Q：我可以從 DataTables 以外的來源匯入資料嗎？**
答：是的，Aspose.Cells 支援各種資料來源。查看文件以了解更多詳細資訊。

**Q：如果我的 HTML 標籤在 Excel 中無法正確呈現怎麼辦？**
答：確保您的 `ImportTableOptions` 配置有 `IsHtmlString = true`。

**Q：Aspose.Cells 有免費版本嗎？**
答：試用許可證可讓您暫時探索全部功能。訪問 [Aspose 網站](https://purchase.aspose.com/temporary-license/) 了解更多。

**Q：我可以將工作簿儲存為 XLSX 和 ODS 以外的格式嗎？**
答：是的，Aspose.Cells 支援多種文件格式，包括 PDF、CSV 等。

## 資源

如需進一步閱讀和獲取資源，請造訪：
- [Aspose.Cells文檔](https://reference.aspose.com/cells/net/)
- [下載最新版本](https://releases.aspose.com/cells/net/)
- [購買許可證](https://purchase.aspose.com/buy)
- [免費試用版下載](https://releases.aspose.com/cells/net/)
- [取得臨時許可證](https://purchase.aspose.com/temporary-license/)
- [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}