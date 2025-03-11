---
title: 在 Aspose.Cells .NET 中將文字轉換為列
linktitle: 在 Aspose.Cells .NET 中將文字轉換為列
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此詳細的逐步教學中，了解如何使用 Aspose.Cells for .NET 輕鬆將文字轉換為列。
weight: 15
url: /zh-hant/net/row-column-autofit-conversion/convert-text-to-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Aspose.Cells .NET 中將文字轉換為列

## 介紹
在當今快節奏的資料管理世界中，效率是關鍵。無論您是處理資料的分析師還是準備報告的業務專業人士，您經常會發現自己需要快速且準確地操作資料。如果您曾經需要處理單一儲存格中的名稱，並且需要將其拆分為單獨的列，您就會知道這有多乏味。值得慶幸的是，Aspose.Cells for .NET 提供了一個將文字分割為列的優雅解決方案。在本指南中，我們將逐步介紹使用 Aspose.Cells 將文字轉換為列的過程。
## 先決條件
在我們開始之前，讓我們確保您已完成所有設定。這是您需要的：
1.  Visual Studio：確保您的電腦上安裝了 Visual Studio。如果您還沒有，您可以從以下位置下載[微軟的網站](https://visualstudio.microsoft.com/downloads/).
2. .NET Framework：確保您正在處理的專案面向 .NET Framework 的相容版本。 Aspose.Cells 與 .NET Core、.NET Framework 和其他平台相容。
3.  Aspose.Cells 庫：您需要下載 Aspose.Cells 庫並在專案中引用。您可以從[Aspose 下載頁面](https://releases.aspose.com/cells/net/).
4. C# 基礎知識：熟悉 C# 程式設計將有助於您更輕鬆地理解本教學。
## 導入包
為了讓事情順利進行，我們需要導入必要的 Aspose.Cells 套件。您可以按照以下方法執行此操作：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```
這可讓您存取 Aspose.Cells 操作資料所需的所有功能。
現在我們已完成所有操作，讓我們開始將文字到列的轉換分解為幾個易於遵循的步驟。
## 第 1 步：設定文檔目錄
首先，您需要配置保存輸出檔案的目錄。整齊地組織文件總是一個好主意；這使得管理它們變得容易。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
- 代替`"Your Document Directory"`與您要儲存檔案的實際路徑。例如，您可能會使用`C:\\Documents\\AsposeOutput\\`.
## 步驟 2：建立工作簿實例
接下來，讓我們建立我們的工作簿。這本質上是處理所有資料的文件。
```csharp
//建立工作簿實例。
Workbook wb = new Workbook();
```
- 將工作簿視為空白畫布。你可以隨心所欲地畫畫！
## 第 3 步：存取第一個工作表
現在我們有了工作簿，我們需要存取第一個工作表以開始新增資料。
```csharp
//訪問第一個工作表。
Worksheet ws = wb.Worksheets[0];
```
- 工作表就像工作簿中的一頁。您可以有多個頁面，但為了簡單起見，我們將專注於第一個頁面。
## 第 4 步：將資料新增至工作表
讓我們用一些名稱填滿工作表。我們將輸入名稱列表，其中名字和姓氏之間以空格分隔。
```csharp
//在 A 欄中新增人員姓名。
ws.Cells["A1"].PutValue("John Teal");
ws.Cells["A2"].PutValue("Peter Graham");
ws.Cells["A3"].PutValue("Brady Cortez");
ws.Cells["A4"].PutValue("Mack Nick");
ws.Cells["A5"].PutValue("Hsu Lee");
```
- 您需要根據需要調整您的姓名；也許您想用自己的名單進行測試或創建更多樣化的名單。
## 第 5 步：建立文字載入選項
在分割名稱之前，我們必須定義如何分割文字。在本例中，我們將使用空格作為分隔符號。
```csharp
//建立以空格作為分隔符號的文字載入選項。
TxtLoadOptions opts = new TxtLoadOptions();
opts.Separator = ' ';
```
- 透過定義空格作為分隔符，我們通知 Aspose 這是它應該分割名稱的地方。
## 步驟 6：將列拆分為多個列
魔法來了！現在，我們將使用以下命令將 A 列的內容拆分為兩個單獨的欄位（A 列中的名字和 B 列中的姓氏）`TextToColumns`方法。
```csharp
//使用 TextToColumns() 方法將 A 列拆分為兩列。
//現在，A 列將具有名字，B 列將具有姓氏。
ws.Cells.TextToColumns(0, 0, 5, opts);
```
- 這一步將減輕您肩上的所有辛苦工作。就像有個勤奮的小幫手，知道該做什麼！
## 第 7 步：儲存工作簿
最後，讓我們儲存我們所做的更改的工作簿。看到您的工作被乾淨地保存總是令人滿意的！
```csharp
//將工作簿儲存為 xlsx 格式。
wb.Save(dataDir + "outputTextToColumns.xlsx");
```
- 確保為文件指定一個有意義的名稱。在本例中，我們將其另存為`outputTextToColumns.xlsx`，但請隨意將其重命名為您認為合適的任何名稱。
## 結論
現在你就擁有了！您剛剛學習如何使用 Aspose.Cells for .NET 將文字轉換為列。它是一個功能強大的工具，可以簡化資料處理，讓您只需幾行簡單的程式碼即可執行曾經需要花費數小時的操作。現在，下次您需要拆分名稱或其他文字時，您可以輕鬆完成。別忘了探索[Aspose 的文檔](https://reference.aspose.com/cells/net/)了解更多高級功能和定制，可以提高您的資料處理技能！
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個強大的 .NET 程式庫，可讓開發人員有效率地建立、操作和轉換 Excel 電子表格，而無需安裝 Microsoft Excel。
### 我可以免費使用 Aspose.Cells 嗎？
是的！您可以從以下位置開始免費試用：[Aspose的試用頁面](https://releases.aspose.com/).
### 在哪裡可以找到對 Aspose.Cells 的支援？
如有任何疑問或問題，您可以訪問[Aspose 支援論壇](https://forum.aspose.com/c/cells/9).
### Aspose.Cells容易學嗎？
絕對地！透過簡單的範例和豐富的文檔，即使是初學者也可以快速掌握。
### Aspose.Cells 還提供哪些其他功能？
除了文字操作之外，Aspose.Cells 還支援圖表建立、資料驗證、公式計算等等！

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
