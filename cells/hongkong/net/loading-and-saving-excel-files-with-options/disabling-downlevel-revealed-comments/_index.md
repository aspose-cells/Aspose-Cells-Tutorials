---
title: 儲存為 HTML 時停用下層顯示註釋
linktitle: 儲存為 HTML 時停用下層顯示註釋
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過此詳細的逐步指南，了解如何在使用 Aspose.Cells for .NET 將 Excel 工作簿儲存為 HTML 時停用下層顯示的註解。
weight: 11
url: /zh-hant/net/loading-and-saving-excel-files-with-options/disabling-downlevel-revealed-comments/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 儲存為 HTML 時停用下層顯示註釋

## 介紹
您是否曾經需要將 Excel 工作簿轉換為 HTML，並希望確保在此過程中不會洩露任何不必要的註釋或隱藏內容？這就是禁用下層顯示的評論派上用場的地方。如果您使用 Aspose.Cells for .NET，您可以完全控制 Excel 工作簿如何呈現為 HTML 檔案。在本教程中，我們將引導您完成一個簡單的逐步指南，以幫助您在將工作簿儲存為 HTML 時停用下層顯示的註解。 
閱讀本文後，您將清楚地了解如何使用此功能並確保您的 HTML 輸出乾淨且無註解。
## 先決條件
在我們深入了解逐步指南之前，我們先介紹一下您需要具備的一些事項，以便順利進行操作：
1. Aspose.Cells for .NET：您需要安裝 Aspose.Cells 函式庫。如果您還沒有安裝，可以下載[這裡](https://releases.aspose.com/cells/net/).
2. IDE：類似 Visual Studio 的開發環境，用於編寫和執行 C# 程式碼。
3. C# 基礎知識：熟悉 C# 語法和物件導向程式設計將有助於您理解程式碼。
4. 臨時或許可版本：您可以使用免費試用版或從以下位置申請臨時許可證[這裡](https://purchase.aspose.com/temporary-license/)。這確保了庫的運行沒有任何限制。
現在您已經準備好了，讓我們立即開始吧！
## 導入命名空間
在我們進入程式碼範例之前，必須包含 Aspose.Cells 所需的命名空間。如果沒有這些，您的程式碼將無法存取操作 Excel 檔案所需的方法和屬性。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
確保將此行放在 C# 檔案的頂部以匯入 Aspose.Cells 命名空間。
## 第 1 步：設定目錄路徑
在進行任何操作之前，我們需要設定來源目錄（儲存 Excel 檔案的位置）和輸出目錄（儲存 HTML 檔案的位置）。這一點至關重要，因為 Aspose.Cells 需要準確的檔案路徑來存取和保存檔案。
```csharp
// Excel 檔案所在的來源目錄
string sourceDir = "Your Document Directory";
//將保存生成的 HTML 檔案的輸出目錄
string outputDir = "Your Document Directory";
```
在此步驟中，替換`"Your Document Directory"`與系統上的實際檔案路徑。您還可以建立自訂目錄以更好地組織輸入和輸出檔案。
## 第 2 步：載入 Excel 工作簿
在此步驟中，我們將 Excel 工作簿載入到記憶體中，以便我們可以對其進行操作。出於演示目的，我們將使用名為的範例文件`"sampleDisableDownlevelRevealedComments.xlsx"`。您可以使用您喜歡的任何工作簿。
```csharp
//從來源目錄載入範例工作簿
Workbook wb = new Workbook(sourceDir + "sampleDisableDownlevelRevealedComments.xlsx");
```
這將建立一個 Workbook 對象，其中包含 Excel 檔案的所有資料和結構。從這裡，您可以修改它、應用設置，並最終以不同的格式保存它。
## 第 3 步：設定 HTML 儲存選項
現在，我們需要設定 HtmlSaveOptions 物件以停用下層顯示的註解。此選項可確保任何註解或隱藏內容不會在產生的 HTML 檔案中顯示。
```csharp
//建立一個新的 HtmlSaveOptions 物件來配置保存選項
HtmlSaveOptions opts = new HtmlSaveOptions();
//停用下層顯示的評論
opts.DisableDownlevelRevealedComments = true;
```
透過設定`DisableDownlevelRevealedComments`到`true`，您確保將工作簿另存為 HTML 檔案時，任何下級註解都會被停用。
## 步驟 4：將工作簿另存為 HTML
配置 HtmlSaveOptions 物件後，下一步是使用指定的選項將工作簿儲存為 HTML。這是實際文件轉換發生的地方。
```csharp
//使用指定的儲存選項將工作簿儲存為 HTML 文件
wb.Save(outputDir + "outputDisableDownlevelRevealedComments_true.html", opts);
```
在這行程式碼中，我們將工作簿儲存到您先前指定的輸出目錄，並套用DisableDownlevelRevealedComments 設定。結果將會是一個乾淨的 HTML 文件，沒有任何不需要的註解。
## 第五步：驗證並執行
最後，為了確保一切按預期工作，您可以向控制台輸出成功訊息。
```csharp
//向控制台輸出成功訊息
Console.WriteLine("DisableDownlevelRevealedCommentsWhileSavingToHTML executed successfully.");
```
這讓您知道操作已完成且沒有錯誤。
## 結論
現在你就擁有了！您已經成功學習如何在使用 Aspose.Cells for .NET 將 Excel 工作簿儲存為 HTML 時停用下層顯示的註解。借助此功能，您現在可以控制工作簿如何呈現為 HTML，並避免洩露任何不必要的內容。無論您是開發 Web 應用程式還是只需要乾淨的 HTML 輸出，此方法都可確保您的工作簿轉換精確且安全。
如果您發現本教學有幫助，請考慮探索 Aspose.Cells 的其他功能，以進一步增強您的 Excel 處理能力。
## 常見問題解答
### 什麼是底層透露評論？
下層顯示註解通常用於 Web 開發，為不支援某些 HTML 功能的舊瀏覽器提供額外資訊。在 Excel 到 HTML 的轉換中，它們有時會顯示隱藏的內容或註釋，因此停用它們會很有用。
### 如果需要，我可以啟用下級評論嗎？
是的，只需設定`DisableDownlevelRevealedComments`財產給`false`如果您想在將工作簿儲存為 HTML 時啟用下級註解。
### 如何取得 Aspose.Cells 的臨時授權？
您可以透過造訪以下網站輕鬆申請臨時許可證[阿斯普斯網站](https://purchase.aspose.com/temporary-license/).
### 停用下級註解是否會影響 HTML 的外觀？
不會，停用下層顯示註解不會影響 HTML 輸出的視覺外觀。它只能防止暴露舊版瀏覽器的額外資訊。
### 除了 HTML 之外，我還可以將工作簿儲存為其他格式嗎？
是的，Aspose.Cells 支援多種輸出格式，例如 PDF、CSV 和 TXT。您可以探索更多選項[文件](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
