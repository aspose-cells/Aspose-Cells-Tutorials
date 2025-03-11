---
title: 從 Excel 擷取 OLE 對象
linktitle: 從 Excel 擷取 OLE 對象
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 從 Excel 檔案中提取 OLE 物件。輕鬆擷取的逐步指南。
weight: 10
url: /zh-hant/net/excel-ole-picture-objects/extract-ole-object-from-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 擷取 OLE 對象

## 介紹
在當今技術精湛的世界中，處理 Excel 文件是一項常見任務，尤其是對於資料分析、財務和專案管理領域的人員。一個經常被忽略的方面是 Excel 電子表格中 OLE（物件連結和嵌入）物件的處理。這些可以是嵌入的文件、圖像，甚至是在增強 Excel 文件的功能和豐富性方面發揮關鍵作用的複雜資料類型。如果您是 Aspose.Cells 用戶，希望使用 .NET 以程式設計方式提取這些 OLE 對象，那麼您來對地方了！本指南將逐步引導您完成整個過程，確保您不僅了解如何操作，還了解為什麼流程的每個部分都很重要。
## 先決條件
在我們深入了解提取 OLE 物件的具體細節之前，您必須具備以下幾點：
1. C# 的基礎知識：如果您熟悉 C#，那麼您就已經走在正確的道路上了。如果沒有，別擔心！我們會讓事情簡單明了。
2. 安裝 Aspose.Cells：您需要 Aspose.Cells 函式庫。您可以從網站下載[這裡](https://releases.aspose.com/cells/net/).
3. 相容的開發環境：確保您已設定好 .NET 開發環境，例如 Visual Studio，隨時可以使用。
4. 範例 Excel 檔案：您需要一個嵌入了 OLE 物件的 Excel 檔案來進行測試。 
一旦滿足了這些先決條件，我們就可以開始進入 OLE 物件提取世界的旅程。
## 導入包
首先，讓我們導入我們將在教程中使用的必要套件。在您的 C# 專案中，您需要包含 Aspose.Cells 命名空間。您可以這樣做：
```csharp
using System.IO;
using Aspose.Cells;
```
## 步驟1：設定文檔目錄
在此步驟中，我們將定義 Excel 檔案所在的路徑。您可能想知道為什麼這很重要。這就像為表演搭建舞台一樣，它幫助腳本知道在哪裡可以找到演員（在我們的例子中是 Excel 文件）。
```csharp
string dataDir = "Your Document Directory";
```
代替`"Your Document Directory"`與您的 Excel 檔案的實際路徑（`book1.xls`) 被儲存。
## 步驟 2： 開啟 Excel 文件
現在我們已經設定了文檔目錄，下一步是開啟 Excel 文件。可以把這想像成在開始閱讀之前打開一本書——看看裡面有什麼是很重要的。
```csharp
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
## 步驟 3：存取 OLE 物件集合
Excel 工作簿中的每個工作表都可以包含各種對象，包括 OLE 對象。在這裡，我們正在存取第一個工作表的 OLE 物件集合。這類似於選擇頁面來查看嵌入的圖像和文件。
```csharp
Aspose.Cells.Drawing.OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
## 步驟 4：循環 OLE 對象
現在到了有趣的部分——循環遍歷集合中的所有 OLE 物件。這一步至關重要，因為它使我們能夠有效地處理多個 OLE 物件。想像一下透過寶箱尋找有價值的物品！
```csharp
for (int i = 0; i < oles.Count; i++)
{
    Aspose.Cells.Drawing.OleObject ole = oles[i];
    //處理每個物件的進一步邏輯
}
```
## 第 5 步：指定輸出檔名
當我們深入研究每個 OLE 物件時，我們需要為提取的物件提供一個檔案名稱。為什麼？因為一旦我們提取它們，我們就希望一切都井井有條，以便以後可以輕鬆找到我們的寶藏。
```csharp
string fileName = dataDir + "ole_" + i + ".";
```
## 步驟 6：確定文件格式類型
每個OLE 物件可以是不同的類型（例如，文件、電子表格、圖像）。確定格式類型至關重要，這樣您才能正確提取它。這就像知道一道菜的食譜一樣——您需要知道食材！
```csharp
switch (ole.FileFormatType)
{
    case FileFormatType.Doc:
        fileName += "doc";
        break;
    case FileFormatType.Xlsx:
        fileName += "xlsx";
        break;
    case FileFormatType.Ppt:
        fileName += "ppt";
        break;
    case FileFormatType.Pdf:
        fileName += "pdf";
        break;
    case FileFormatType.Unknown:
        fileName += "jpg";
        break;
    default:
        //處理其他文件格式
        break;
}
```
## 第 7 步：儲存 OLE 對象
現在，讓我們繼續儲存 OLE 物件。如果物件是 Excel 文件，我們將使用`MemoryStream`這允許我們在寫出之前處理記憶體中的資料。此步驟類似於在將您的財寶發送給朋友之前對其進行包裝。
```csharp
if (ole.FileFormatType == FileFormatType.Xlsx)
{
    MemoryStream ms = new MemoryStream();
    ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    Workbook oleBook = new Workbook(ms);
    oleBook.Settings.IsHidden = false;
    oleBook.Save(dataDir + "Excel_File" + i + ".out.xlsx");
}
```
對於其他類型的文件，我們將使用`FileStream`在磁碟上建立文件。
```csharp
else
{
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
}
```

## 結論
就這樣，您已經成功地使用 Aspose.Cells for .NET 進行了 OLE 物件擷取！透過執行這些步驟，您可以輕鬆地從 Excel 文件中提取和管理嵌入的物件。請記住，就像任何有價值的技能一樣，熟能生巧。因此，花點時間嘗試不同的 Excel 文件，很快您就會成為 OLE 提取專家！
## 常見問題解答
### Excel 中的 OLE 物件是什麼？
OLE 物件是允許在 Excel 工作表中嵌入和連結到其他應用程式中的文件和資料的技術。
### 為什麼我需要提取 OLE 物件？
提取 OLE 物件可讓您獨立於原始 Excel 文件存取和操作嵌入文件或映像。
### Aspose.Cells 可以處理所有類型的嵌入檔案嗎？
是的，Aspose.Cells 可以管理各種 OLE 對象，包括 Word 文件、Excel 工作表、PowerPoint 簡報和圖像。
### 如何安裝 Aspose.Cells for .NET？
您可以透過從他們的網站下載安裝 Aspose.Cells[發布頁面](https://releases.aspose.com/cells/net/).
### 在哪裡可以找到對 Aspose.Cells 的支援？
您可以在其網站上獲得對 Aspose.Cells 的支持[支援論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
