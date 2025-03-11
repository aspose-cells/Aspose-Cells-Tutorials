---
title: 在 .NET 中以程式設計方式將 JSON 轉換為 CSV
linktitle: 在 .NET 中以程式設計方式將 JSON 轉換為 CSV
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells 在 .NET 中以程式設計方式將 JSON 轉換為 CSV。遵循我們的逐步指南以確保無縫資料轉換。
weight: 15
url: /zh-hant/net/converting-excel-files-to-other-formats/converting-json-to-csv/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式將 JSON 轉換為 CSV

## 介紹
在當今的數位世界中，處理多種格式的資料已變得司空見慣，而 JSON（JavaScript 物件表示法）是最廣泛使用的資料交換格式之一。但是，當您需要將 JSON 轉換為更易於分析的格式（例如 CSV（逗號分隔值））時，會發生什麼情況？本教學將引導您完成使用 Aspose.Cells for .NET（一種易於使用但功能強大的電子表格操作 API）以程式設計方式將 JSON 轉換為 CSV 的過程。 
## 先決條件
在我們深入研究程式碼之前，必須確保您擁有所有必要的組件並對我們將使用的工具有基本的了解。讓我們概述一下您需要什麼：
-  Aspose.Cells for .NET：這是我們將用於將 JSON 轉換為 CSV 的主要函式庫。你可以[在這裡下載](https://releases.aspose.com/cells/net/).
- Visual Studio：您需要像 Visual Studio 這樣的整合開發環境 (IDE) 來編寫和執行 .NET 程式碼。
- .NET Framework：確保您已安裝 .NET Framework。 Aspose.Cells 與 .NET Core 和 .NET Framework 相容。
- C# 基礎知識：雖然本指南將分解程式碼的每個部分，但如果您對 C# 有一定的了解，它將有所幫助。
## 導入包
要在 .NET 專案中使用 Aspose.Cells，首先需要安裝該程式庫。您可以透過 NuGet 套件管理器執行此操作：
1. 打開視覺工作室。
2. 前往工具 > NuGet 套件管理器 > 管理解決方案的 NuGet 套件。
3. 搜尋 Aspose.Cells 並安裝最新版本。
安裝後，請確保在程式碼中包含以下命名空間：
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
現在一切都已設定完畢，讓我們逐步分解程式碼，以便您可以看到使用 Aspose.Cells 將 JSON 檔案轉換為 CSV 有多容易。
## 第 1 步：讀取 JSON 文件
我們需要做的第一件事是從檔案中讀取 JSON 資料。我們假設您已經有一個 JSON 檔案（我們稱之為`SampleJson.json`）儲存在系統上的目錄中。
您可以使用`File.ReadAllText()`C# 中的方法將 JSON 檔案的內容讀取為字串。
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
//讀取 JSON 文件
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

此步驟至關重要，因為您需要原始 JSON 資料來啟動轉換過程。透過將其作為字串讀取，您就可以準備將其由 Aspose.Cells 進行處理。
## 第 2 步：建立一個空白工作簿
Aspose.Cells 主要在工作簿（Excel 檔案）上運作。要開始匯入 JSON 數據，您首先需要建立一個空白工作簿，並將在其中插入此數據。
```csharp
//建立空工作簿
Workbook workbook = new Workbook();
```
在這裡，您正在初始化一個空工作簿，該工作簿最終將保存 CSV 格式的資料。可以將其視為在 Excel 中建立空白電子表格，該電子表格很快就會填入您的 JSON 資料。
## 步驟 3：存取工作簿中的儲存格
現在我們有一個空的工作簿，我們需要存取它的儲存格。這`Cells`Aspose.Cells 中的集合代表工作表中的所有儲存格，您將在其中放置 JSON 資料。
```csharp
//取得細胞
Cells cells = workbook.Worksheets[0].Cells;
```
此程式碼片段選擇第一個工作表（索引 0 處的工作表）並取得其`Cells`收藏。這些單元格就像電子表格的網格，將在其中添加資料。
## 第 4 步：設定 JsonLayoutOptions
 Aspose.Cells 為如何匯入 JSON 資料提供了多個自訂選項。在這裡，我們定義`JsonLayoutOptions`指定 Aspose 應如何處理陣列、數值資料和物件標題。
```csharp
//設定 JsonLayoutOptions
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate：自動轉換數字或日期值的字串值。
- ArrayAsTable：將 JSON 中的陣列視為工作簿中的表。
- IgnoreArrayTitle 和 IgnoreObjectTitle：這些選項忽略陣列和物件的標題，確保僅匯入原始資料。
## 第5步：導入JSON數據
設定佈局選項後，就可以引入 JSON 資料了。這`JsonUtility.ImportData()`方法在這裡完成繁重的工作，將 JSON 資料插入工作簿的儲存格中。
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
此方法需要幾個參數：
- `str`：我們在步驟 1 中讀取的 JSON 字串。
- `cells`：將放置資料的儲存格集合。
- `0, 0`：這些是行索引和列索引，指示資料應從何處開始（即左上角）。
- `importOptions`：我們在步驟 4 中設定的佈局選項。
## 步驟 6：將工作簿另存為 CSV
現在 JSON 資料已在工作簿中，我們可以輕鬆地將工作簿儲存為 CSV 檔案。 CSV 是一種簡單、輕量級的格式，用於儲存表格數據，這使其非常適合數據分析。
```csharp
//輸出目錄
string outputDir = "Your Document Directory";
//儲存工作簿
workbook.Save(outputDir + @"SampleJson_out.csv");
```
在此步驟中，我們將工作簿儲存為 CSV 檔案。您指定路徑和檔案名稱（`SampleJson_out.csv`) CSV 的保存位置。
## 第7步：確認流程
為了確保一切按預期工作，我們可以在控制台中列印一條確認訊息。
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
一則簡單的成功訊息有助於確認流程是否順利進行。
## 結論
使用 Aspose.Cells for .NET 將 JSON 轉換為 CSV 是一個簡單而強大的過程。只需幾行程式碼，您就可以將複雜的 JSON 資料轉換為更易於存取的 CSV 格式。無論您處理的是陣列、物件或數值數據，Aspose.Cells 都可以輕鬆配置轉換過程以滿足您的需求。
## 常見問題解答
### Aspose.Cells 可以處理大型 JSON 檔案嗎？
是的，Aspose.Cells 旨在有效處理大型資料集，使其適合處理大型 JSON 檔案而不會出現效能問題。
### 如何自訂 CSV 輸出？
您可以透過調整來自訂 CSV 輸出`JsonLayoutOptions`或在將工作簿儲存為 CSV 之前對其格式進行操作。
### 有沒有辦法在轉換過程中從 JSON 中排除某些資料？
是的，透過在匯入之前調整 JSON 或使用自訂程式碼邏輯，您可以排除或過濾掉特定資料欄位。
### 除了 CSV 之外，Aspose.Cells 是否支援其他檔案格式？
絕對地！ Aspose.Cells 支援多種格式，包括 Excel（XLS、XLSX）、PDF、HTML 等。
### 如何免費試用 Aspose.Cells？
你可以[在這裡下載免費試用版](https://releases.aspose.com/)在購買前測試所有功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
