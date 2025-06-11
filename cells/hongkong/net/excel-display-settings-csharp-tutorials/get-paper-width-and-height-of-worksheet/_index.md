---
"description": "透過簡單的逐步指南了解如何在 Aspose.Cells for .NET 中取得工作表的紙張寬度和高度。"
"linktitle": "取得工作表的紙張寬度和高度"
"second_title": "Aspose.Cells for .NET API參考"
"title": "取得工作表的紙張寬度和高度"
"url": "/zh-hant/net/excel-display-settings-csharp-tutorials/get-paper-width-and-height-of-worksheet/"
"weight": 80
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 取得工作表的紙張寬度和高度

## 介紹

您是否曾嘗試列印 Excel 表格並處理各種紙張尺寸令人困惑的尺寸？如果你跟我一樣，你就會知道沒有什麼比佈局不正確更能毀掉你的一天了！無論您列印的是報告、發票還是簡單的列表，了解如何以程式方式調整紙張尺寸可以為您省去很多麻煩。今天，我們將深入研究 Aspose.Cells for .NET 的世界，研究如何在應用程式中直接檢索和設定紙張尺寸。讓我們捲起袖子，深入研究管理這些紙張尺寸的細節！

## 先決條件 

在我們進入編碼魔法之前，讓我們先收集一下開始所需的資料：

1. 對 C# 的基本了解：您應該對 C# 有初步的了解。如果您是程式設計新手，請不要擔心！我們將保持簡單明了。
2. Aspose.Cells 庫：確保您的機器上安裝了適用於 .NET 的 Aspose.Cells 庫。您可以從下載 [此連結](https://releases。aspose.com/cells/net/).
3. .NET 開發環境：設定 Visual Studio 或您選擇的任何 IDE 來編寫和執行您的 C# 程式碼。如果您不確定從哪裡開始，Visual Studio Community Edition 是一個不錯的選擇。
4. 參考文獻和文件：熟悉 Aspose.Cells 文件以獲得更深入的見解。你可以找到它 [這裡](https://reference。aspose.com/cells/net/).
5. 基本 Excel 文件知識：了解 Excel 文件的結構（工作表、行和列）將大有幫助。

偉大的！現在我們已經完成了基本工作，讓我們直接開始匯入必要的套件。

## 導入包

為了讓我們的生活更輕鬆並充分利用 Aspose.Cells 的全部功能，我們需要導入幾個套件。就像添加一個 `using` 程式碼檔案頂部的語句。以下是您需要匯入的內容：

```csharp
using System;
using System.IO;
```

此行允許我們存取 Aspose.Cells 庫中的所有類別和方法，從而更輕鬆地操作 Excel 檔案。現在，讓我們逐步指導如何擷取各種紙張尺寸的寬度和高度。

## 步驟 1：建立新工作簿

使用 Aspose.Cells 的第一步是建立一個新的工作簿。將工作簿想像成一個空白畫布，您可以在其中添加工作表、單元格，並且在我們的例子中，還可以定義紙張尺寸。

```csharp
//建立工作簿
Workbook wb = new Workbook();
```

此行實例化了一個新的工作簿對象，以供我們操作。您暫時還看不到任何東西，但我們的畫布已經設定好了！

## 第 2 步：存取第一個工作表

現在我們有了工作簿，我們需要存取其中的特定工作表。工作表就像工作簿中的一頁，所有操作都發生在這裡。

```csharp
//訪問第一個工作表
Worksheet ws = wb.Worksheets[0];
```

在這裡，我們從工作簿中抓取第一個工作表（索引 0）。您可以將其想像為翻到一本書的第一頁。 

## 步驟 3：設定紙張尺寸並取得尺寸

現在到了令人興奮的部分！我們將設定不同的紙張尺寸並逐一檢索它們的尺寸。這一步至關重要，因為它讓我們看到不同的尺寸如何影響佈局。

```csharp
//將紙張尺寸設定為 A2 並以英吋為單位列印紙張寬度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

在這個區塊中，我們將紙張尺寸設為 A2，然後擷取其寬度和高度。這 `PaperWidth` 和 `PaperHeight` 屬性提供以英吋為單位的尺寸。這就像在將圖片放入相框之前檢查其尺寸一樣。

## 步驟 4：重複其他紙張尺寸

讓我們對其他常見的紙張尺寸重複此過程。我們將檢查 A3、A4 和 Letter 尺寸。這種重複對於理解如何在 Aspose.Cells 框架內定義每個尺寸非常重要。

```csharp
//將紙張尺寸設為 A3 並以英吋為單位列印紙張寬度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//將紙張尺寸設為 A4 並以英吋為單位列印紙張寬度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
//將紙張大小設定為 Letter，並以英吋為單位列印紙張的寬度和高度
ws.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + ws.PageSetup.PaperWidth + "x" + ws.PageSetup.PaperHeight);
```

每個區塊都模仿前一步，但調整 `PaperSize` 相應的財產。只需更改尺寸指示器，您就可以輕鬆獲得不同的紙張尺寸。這就像根據您需要儲存的內容改變盒子的大小！

## 結論

就是這樣！遵循這些步驟，您可以輕鬆地在 Aspose.Cells for .NET 中設定和檢索各種紙張尺寸的尺寸。此功能不僅可以節省您的時間，還可以防止因頁面設定配置錯誤而發生的列印事故。因此，下次您需要列印 Excel 工作表或建立報表時，您可以放心地進行操作，因為您知道手中掌握著尺寸。 

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個 .NET 函式庫，專為處理 Excel 檔案而設計，無需安裝 Excel。

### 我可以免費使用 Aspose.Cells 嗎？
是的！您可以先從以下網址開始免費試用 [此連結](https://releases。aspose.com/).

### 如何設定自訂紙張尺寸？
Aspose.Cells 提供使用以下選項設定自訂紙張尺寸 `PageSetup` 班級。

### 使用 Aspose.Cells 是否需要編碼知識？
基本的編碼知識會有所幫助，但您可以按照教程更容易理解！

### 在哪裡可以找到更多範例？
這 [Aspose.Cells 文檔](https://reference.aspose.com/cells/net/) 提供了豐富的範例和教程。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}