---
"description": "透過本教學學習如何使用 Aspose.Cells for .NET 設定 Excel 工作表中所有行的高度"
"linktitle": "使用 Aspose.Cells 設定 Excel 中所有行的高度"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用 Aspose.Cells 設定 Excel 中所有行的高度"
"url": "/zh-hant/net/size-and-spacing-customization/setting-height-of-all-rows/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 設定 Excel 中所有行的高度

## 介紹
在快節奏的資料管理世界中，控制電子表格的外觀至關重要。您可能會發現需要調整 Excel 中的行高，以獲得更好的可見度、組織性，或者只是為了增強工作的整體美感。如果您正在使用 .NET 應用程序，Aspose.Cells 是一個令人難以置信的程式庫，可讓您輕鬆操作 Excel 檔案。在本教學中，我們將引導您完成使用 Aspose.Cells 設定 Excel 工作表中所有行的高度的簡單流程。讓我們開始吧！
## 先決條件
在進入編碼部分之前，請確保您擁有開始所需的一切：
- Aspose.Cells for .NET：如果您還沒有，請從 [Aspose 下載頁面](https://releases。aspose.com/cells/net/).
- Visual Studio：用於編寫和執行 C# 程式碼的開發環境。
- C# 基礎知識：了解 C# 的基礎知識將幫助您掌握程式碼的工作原理。
## 導入包
要開始使用 Aspose.Cells 進行編碼，您需要匯入必要的命名空間。具體操作如下：
### 建立新的 C# 項目
首先，開啟 Visual Studio 並建立一個新的 C# 專案。
### 新增 Aspose.Cells 庫
接下來，您需要將 Aspose.Cells 庫新增到您的專案中。如果您下載了該庫，則可以像任何其他庫一樣引用其 DLL。
如果您喜歡自動化程度較高的方法，也可以執行下列指令透過 NuGet 套件管理器來安裝：
```bash
Install-Package Aspose.Cells
```
### 包含所需的命名空間
在 C# 檔案的頂部，包含以下命名空間：
```csharp
using System.IO;
using Aspose.Cells;
```
這些命名空間將提供操作 Excel 檔案所需的類別和方法。
現在，讓我們分解一下設定 Excel 檔案中所有行的高度的過程。
## 步驟 1：定義目錄路徑
第一步是指定 Excel 檔案的路徑。這很關鍵，因為它告訴您的應用程式在哪裡可以找到您想要操作的檔案。
```csharp
string dataDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用您的 Excel 檔案的實際儲存路徑。例如： `C:\Documents\`。
## 步驟2：建立檔案流
接下來，您需要建立一個 `FileStream` 將用於存取 Excel 文件。這使您可以打開和操作該文件。
```csharp
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
確保“book1.xls”是您的 Excel 檔案的名稱。這 `FileMode.Open` 參數表示您正在開啟一個現有文件。
## 步驟 3：實例化工作簿對象
現在是時候建立一個實例了 `Workbook` 類別將您的 Excel 檔案載入到記憶體中。
```csharp
Workbook workbook = new Workbook(fstream);
```
這行程式碼讀取你用以下指令開啟的 Excel 文件 `FileStream` 並做好操縱的準備。
## 步驟 4：訪問工作表
Aspose.Cells 允許您存取工作簿中的單一工作表。在這裡，我們將訪問第一個工作表。
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
工作表從零開始索引，因此 `[0]` 指的是工作簿中的第一個工作表。
## 步驟5：設定行高
現在，我們準備好設定所有行的高度。透過使用 `StandardHeight` 屬性，您可以為工作表中的每一行定義一個標準高度。
```csharp
worksheet.Cells.StandardHeight = 15;
```
在此範例中，我們將所有行的高度設為 15。您可以根據需要隨意調整該數字。
## 步驟6：儲存修改後的文件
完成所有變更後，必須將修改後的工作簿儲存到新文件或覆蓋現有文件。
```csharp
workbook.Save(dataDir + "output.out.xls");
```
此行將新的 Excel 檔案作為「output.out.xls」儲存在指定目錄中。如果要覆蓋原始文件，只需使用相同的名稱即可。
## 步驟 7：清理資源
最後，關閉 `FileStream` 以避免應用程式中出現任何資源洩漏。
```csharp
fstream.Close();
```
此行確保 `FileStream` 被釋放，這對於維持性能至關重要。
## 結論
就是這樣！您已成功學習如何使用 Aspose.Cells for .NET 設定 Excel 工作表中所有行的高度。這項技能不僅可以提高數據的可讀性，還可以為您的報告和電子表格增添專業感。有了 Aspose.Cells，可能性就變得無限大，調整 Excel 檔案也變得前所未有的簡單。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，使開發人員能夠在 .NET 應用程式中建立、讀取、操作和保存 Excel 檔案。
### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，雖然 Aspose.Cells 提供免費試用，但您需要許可證才能無限制地繼續使用。您可以查看 [此處提供臨時許可證選項](https://purchase。aspose.com/temporary-license/).
### 我可以更改特定行而不是所有行的行高嗎？
絕對地！您可以使用 `Cells.SetRowHeight(rowIndex, height)` 方法。
### Aspose.Cells 是跨平台的嗎？
是的，Aspose.Cells 可以在任何 .NET 框架中使用，使其適用於各種應用場景。
### 我如何獲得 Aspose.Cells 的支援？
您可以在 [Aspose 論壇](https://forum.aspose.com/c/cells/9) 致力於 Cells 用戶。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}