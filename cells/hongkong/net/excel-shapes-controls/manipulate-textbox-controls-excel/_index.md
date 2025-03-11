---
title: 在 Excel 中操作 TextBox 控制項
linktitle: 在 Excel 中操作 TextBox 控制項
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這個易於理解的逐步教程，了解如何使用 Aspose.Cells for .NET 操作 Excel 中的文字方塊。
weight: 15
url: /zh-hant/net/excel-shapes-controls/manipulate-textbox-controls-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中操作 TextBox 控制項

## 介紹
如果您曾經使用過 Excel，您可能會遇到那些可讓您在電子表格中新增浮動文字的小文字方塊。但是，如果您需要以程式設計方式操作這些文字方塊怎麼辦？這就是 Aspose.Cells for .NET 派上用場的地方。有了它，您可以輕鬆存取和修改文字框，使其非常適合自動化任務或自訂報告。在本教學中，我們將引導您完成使用 Aspose.Cells for .NET 在 Excel 中操作文字方塊的過程。
## 先決條件
在深入研究實際程式碼之前，讓我們確保一切都設定正確：
1.  Aspose.Cells for .NET：您需要下載Aspose.Cells for .NET 函式庫。你可以找到下載鏈接[這裡](https://releases.aspose.com/cells/net/).
2. .NET 開發環境：任何支援 .NET 的 IDE（例如 Visual Studio）都可以使用。
3. C# 基礎：本教學假設您熟悉基本 C# 文法和 Excel 工作簿的架構。
4.  Excel 檔案：現有文字方塊的 Excel 檔案（我們將使用`book1.xls`在此範例中）。
5.  Aspose 授權：如果您不使用免費試用版，則需要[買](https://purchase.aspose.com/buy)許可證或獲得[臨時的一個](https://purchase.aspose.com/temporary-license/).
現在，讓我們深入了解步驟！
## 導入包
在使用 Aspose.Cells 操作 Excel 工作簿和文字方塊之前，您需要匯入必要的命名空間。以下是您將在 C# 檔案頂部使用的程式碼片段：
```csharp
using System.IO;
using Aspose.Cells;
```
這些套件可讓您存取工作簿操作、工作表存取和繪圖物件（如文字方塊）。
現在我們已經完成了所有設置，讓我們將操作文字方塊的過程分解為易於遵循的步驟。
## 第 1 步：設定您的工作簿目錄
第一步是指定 Excel 檔案在系統上的位置。您需要替換佔位符`Your Document Directory`與文件的實際路徑。該路徑儲存在`dataDir`變數以便在整個程式碼中輕鬆引用。
```csharp
string dataDir = "Your Document Directory";
```
這允許您的程式知道在哪裡可以找到輸入的 Excel 檔案（`book1.xls`）以及保存輸出檔案的位置。
## 步驟 2： 開啟 Excel 文件
接下來，您需要將現有的 Excel 檔案載入到 Aspose.Cells Workbook 物件中。此工作簿可作為 Excel 資料的容器，可讓您存取其工作表和任何繪圖物件（如文字方塊）。
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
這`Workbook` Aspose.Cells 中的類別將從您的目錄載入指定的 Excel 檔案。如果指定目錄中不存在該文件，則會拋出異常，因此請確保路徑正確。
## 第 3 步：存取第一個工作表
現在您已載入工作簿，您可以存取其工作表。在此範例中，我們正在存取工作簿中的第一個工作表，該工作表儲存在索引 0 處。
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
這`Worksheets`屬性可讓您存取工作簿中的所有工作表。在這裡，我們只對第一個工作表感興趣，但您可以透過指定正確的索引來處理任何工作表。
## 第 4 步：取得第一個 TextBox 對象
Excel 工作表中的文字方塊會視為繪圖物件。 Aspose.Cells.Drawing.TextBox 類別提供了操作它們的屬性和方法。要存取工作表上的第一個文字框，您只需引用`TextBoxes`按索引收集。
```csharp
Aspose.Cells.Drawing.TextBox textbox0 = worksheet.TextBoxes[0];
```
這將從中檢索第一個文字框對象`TextBoxes`收藏。如果您的工作表在該索引處沒有文字框，它將引發異常，因此請務必確保索引有效。
## 第 5 步：從第一個文字方塊中檢索文本
訪問文本框後，您可以使用以下命令提取其中包含的文本`.Text`財產。
```csharp
string text0 = textbox0.Text;
```
這會將第一個文字方塊中的文字捕獲到`text0`細繩。現在您可以在應用程式中顯示它、操作它或處理它。
## 第 6 步：存取第二個 TextBox 對象
要操作多個文字框，我們可以從工作表中檢索其他文字框。在這裡，我們將以與第一個文字方塊類似的方式存取第二個文字方塊：
```csharp
Aspose.Cells.Drawing.TextBox textbox1 = worksheet.TextBoxes[1];
```
再次，我們使用索引 1 存取第二個文字框`TextBoxes`收藏。
## 步驟 7：從第二個文字方塊中檢索文本
就像第一個文字方塊一樣，您可以從第二個文字方塊中檢索文字並將其儲存在字串中：
```csharp
string text1 = textbox1.Text;
```
這將從第二個文字方塊中捕獲當前文字。
## 步驟8：修改第二個文字方塊中的文本
現在，假設您要修改第二個文字方塊中的文字。您可以透過將新字串指派給`.Text`文字方塊物件的屬性。
```csharp
textbox1.Text = "This is an alternative text";
```
這會將第二個文字方塊中的文字變更為新內容。您可以根據您的要求在此處插入任何文字。
## 步驟 9：儲存更新的 Excel 文件
最後，修改文字方塊後，是時候儲存變更了。 Aspose.Cells 允許您使用以下指令儲存修改後的工作簿`.Save()`方法。您可以指定新檔案名稱或覆蓋現有檔案。
```csharp
workbook.Save(dataDir + "output.out.xls");
```
這會將修改後的 Excel 檔案儲存到您指定的輸出路徑。現在，當您開啟 Excel 檔案時，您將看到對文字方塊所做的變更。
## 結論
現在你就擁有了！您剛剛學習如何使用 Aspose.Cells for .NET 操作 Excel 中的文字方塊。無論您是自動產生報表、自訂 Excel 工作表還是建立動態內容，Aspose.Cells 都可以輕鬆地以程式設計方式控制 Excel 檔案的各個方面。從提取和修改文字到保存更新的文件，該程式庫對於在 .NET 環境中使用 Excel 的開發人員來說是一個強大的工具。
## 常見問題解答
### 除了文字方塊之外，我還可以使用 Aspose.Cells 操作其他繪圖物件嗎？
是的，Aspose.Cells 可讓您操作其他繪圖對象，例如形狀、圖表和圖片。
### 如果我嘗試存取不存在的文字方塊會發生什麼？
如果文字方塊的索引超出範圍，`IndexOutOfRangeException`將被拋出。
### 我可以使用 Aspose.Cells 將新文字方塊新增至 Excel 工作表嗎？
是的，Aspose.Cells 允許您使用以下命令新增文字框`AddTextBox`方法。
### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，您需要購買許可證，但 Aspose 也提供[免費試用](https://releases.aspose.com/).
### 我可以將 Aspose.Cells 與 C# 以外的其他程式語言一起使用嗎？
是的，Aspose.Cells 可以與任何 .NET 支援的語言一起使用，例如 VB.NET。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
