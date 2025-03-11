---
title: 將標籤替換為 Excel 文字方塊中的文本
linktitle: 將標籤替換為 Excel 文字方塊中的文本
second_title: Aspose.Cells .NET Excel 處理 API
description: 使用 Aspose.Cells for .NET 輕鬆取代 Excel 工作表中文字方塊中的文字。 Excel 自動化的逐步指南。
weight: 11
url: /zh-hant/net/excel-shape-text-modifications/replace-tag-text-textbox-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將標籤替換為 Excel 文字方塊中的文本

## 介紹
在本文中，我們將深入研究一項特定任務：使用 Aspose.Cells 將標籤替換為 Excel 工作表中文字方塊中的文字。我們將逐步指導您完成整個過程，確保您掌握每個細節。學完本教學後，您不僅可以增強對 Aspose.Cells 的理解，還可以簡化與 Excel 相關的任務！
## 先決條件
在開始之前，您需要準備一些東西：
1. Visual Studio：確保您已安裝 Visual Studio。它是一個靈活的 IDE，使 C# 編碼變得輕而易舉。
2.  Aspose.Cells 函式庫：如果您還沒有這樣做，請從下列位置下載 .NET 的 Aspose.Cells 函式庫：[頁](https://releases.aspose.com/cells/net/)。您還可以獲得免費試用版來查看其功能。
3. C# 基礎知識：對 C# 程式設計的基本了解將有助於您輕鬆遵循本指南。
現在一切都準備好了，讓我們繼續有趣的部分——編寫程式碼！
## 導入包
首先，讓我們導入必要的套件。這很重要，因為如果沒有正確的導入，您的程式碼將無法識別我們將使用的類別和方法。
## 啟動您的 C# 項目
打開 Visual Studio 並建立一個新的 C# 項目，最好是控制台應用程序，因為它可以讓您輕鬆查看輸出。
## 加入 Aspose.Cells 參考
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“新增”>“參考”。
- 瀏覽到您下載 Aspose.Cells 庫的位置並將其包含在您的專案中。
## 導入必要的命名空間
新增引用後，加入以下內容`using`主文件頂部的指令：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Drawing;
```
這可讓您存取 Aspose.Cells 命名空間中的類別。
現在我們已經設定了環境，讓我們進入有趣的部分——編碼！我們的目標是在 Excel 文件內的文字方塊中尋找特定標籤，並將其替換為提供的文字。
## 第 1 步：定義來源目錄和輸出目錄
首先，我們需要指定來源 Excel 檔案的位置以及修改後的版本的儲存位置。
```csharp
//來源目錄和輸出目錄
string sourceDir = "Your Document Directory"; //更改為您的目錄
string outputDir = "Your Document Directory"; //更改為您的目錄
```
## 第 2 步：載入工作簿
這是我們載入 Excel 工作簿的位置。如果該檔案不存在，則會拋出錯誤。所以，請確保您的檔案路徑正確！
```csharp
Workbook wb = new Workbook(sourceDir + "sampleReplaceTagWithText.xlsx");
```
在這裡，我們正在載入一個名為的現有 Excel 文件`sampleReplaceTagWithText.xlsx`.
## 第 3 步：定義標籤和替換文字
接下來，我們需要定義我們正在尋找的標籤以及我們想要用什麼來取代它們。
```csharp
string tag = "TAG_2$TAG_1";
string replace = "1$ys";
```
在此範例中，標籤使用下列方式分割`$`。您可以將其替換為您喜歡的任何分隔符號。
## 第 4 步：循環標籤並替換
我們將建立一個循環來遍歷要替換的每個標籤。這就是奇蹟發生的地方！
```csharp
for (int i = 0; i < tag.Split('$').Length; i++)
{
    sheetReplace(wb, "<" + tag.Split('$')[i] + ">", replace.Split('$')[i]);
}
```
## 第 5 步：儲存工作簿
現在我們已經進行了替換，是時候將修改後的工作簿儲存為所需的格式了。以下是我們將其轉換為 PDF 的方法。
```csharp
PdfSaveOptions opts = new PdfSaveOptions();
wb.Save(outputDir + "outputReplaceTagWithText.pdf", opts);
```
您也可以將其儲存為各種其他格式，包括 XLSX。
## 第 6 步：實現替換邏輯
這是我們功能的核心所在。這`sheetReplace`方法將處理 Excel 工作表中的實際替換。
```csharp
public static void sheetReplace(Workbook workbook, string sFind, string sReplace)
{
    string finding = sFind;
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sheet.Replace(finding, sReplace);
        for (int j = 0; j < 3; j++)
        {
            if (sheet.PageSetup.GetHeader(j) != null)
                sheet.PageSetup.SetHeader(j, sheet.PageSetup.GetHeader(j).Replace(finding, sReplace));
                
            if (sheet.PageSetup.GetFooter(j) != null)
                sheet.PageSetup.SetFooter(j, sheet.PageSetup.GetFooter(j).Replace(finding, sReplace));
        }
    }
    foreach (Worksheet sheet in workbook.Worksheets)
    {
        sFind = sFind.Replace("<", "&lt;");
        sFind = sFind.Replace(">", "&gt;");
        foreach (Aspose.Cells.Drawing.TextBox mytextbox in sheet.TextBoxes)
        {
            if (mytextbox.HtmlText != null)
            {
                if (mytextbox.HtmlText.IndexOf(sFind) >= 0)
                {
                    mytextbox.HtmlText = mytextbox.HtmlText.Replace(sFind, sReplace);
                }
            }
        }
    }
}
```
- 首先，我們循環遍歷工作簿中的每個工作表。
- 我們不僅取代儲存格內容中的主標記，還取代頁首和頁尾（如果存在）中的主標記。
- 最後，我們檢查工作表中的每個文字框，並根據我們要尋找的標籤取代其中的文字。
## 結論
瞧！現在您已經了解如何使用 Aspose.Cells for .NET 將標籤替換為 Excel 文件中文字方塊中的文字。這確實可以節省時間，尤其是在處理電子表格中的重複任務時。
## 常見問題解答
### 我可以同時替換多個 Excel 檔案中的標籤嗎？
是的，透過循環文件列表，您可以將相同的邏輯套用到多個 Excel 文件。
### 我需要付費許可證才能使用 Aspose.Cells 嗎？
您可以從免費試用開始，但要獲得完整功能，您需要購買許可證。查看[Aspose 的購買選項](https://purchase.aspose.com/buy).
### 我可以使用 Aspose.Cells 取代文字方塊中的圖像嗎？
Aspose.Cells 主要處理文字。但是，如果需要，您可以單獨操作圖像。
### 我可以將修改後的 Excel 檔案儲存為哪些格式？
您可以將其儲存為各種格式，包括 XLSX、PDF、CSV 等。
### 在哪裡可以找到對 Aspose.Cells 的支援？
您可以在以下位置找到支援並提出問題[Aspose論壇](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
