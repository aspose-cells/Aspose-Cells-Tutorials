---
title: 在工作表中實作頁首和頁尾
linktitle: 在工作表中實作頁首和頁尾
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過逐步教學、實際範例和實用提示，了解如何使用 Aspose.Cells for .NET 在 Excel 工作表中設定頁首和頁尾。
weight: 22
url: /zh-hant/net/worksheet-page-setup-features/implement-header-and-footer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在工作表中實作頁首和頁尾

## 介紹

使用 Excel 電子表格時，頁首和頁尾在向受眾提供重要的上下文資訊（例如檔案名稱、日期或頁碼）方面發揮關鍵作用。無論您是自動化報告還是產生動態文件，Aspose.Cells for .NET 都可以讓您輕鬆以程式設計方式自訂工作表中的頁首和頁尾。本指南深入探討了使用 Aspose.Cells for .NET 新增頁首和頁尾的全面、逐步方法，使您的 Excel 檔案更加精緻和專業。

## 先決條件

在開始之前，請確保您已具備以下條件：

1.  Aspose.Cells for .NET：您需要安裝 Aspose.Cells for .NET。[在這裡下載](https://releases.aspose.com/cells/net/).
2. IDE 設定：安裝了 .NET 框架的 Visual Studio（或您首選的 IDE）。
3. 許可證：雖然您可以開始免費試用，但獲得完整或臨時許可證將釋放 Aspose.Cells 的全部潛力。[獲得臨時許可證](https://purchase.aspose.com/temporary-license/).

Aspose.Cells 的文件是整個過程中可供參考的便利資源。你可以找到它[這裡](https://reference.aspose.com/cells/net/).

## 導入包

在您的專案中，匯入所需的命名空間：

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

透過匯入此包，您將可以存取在 Aspose.Cells 中使用頁首、頁尾和其他 Excel 功能所需的類別和方法。

在本指南中，我們將分解每個步驟，以便您可以輕鬆遵循，即使您是 Aspose.Cells 或 .NET 的新手。

## 第 1 步：設定工作簿和頁面設置

首先要做的事情是：建立一個新工作簿並存取工作表的頁面設定。這將為您提供修改工作表頁首和頁尾所需的工具。

```csharp
//定義儲存文件的路徑
string dataDir = "Your Document Directory";

//實例化 Workbook 物件
Workbook excel = new Workbook();
```

在這裡，我們創建了一個`Workbook`對象，它代表我們的 Excel 檔案。這`PageSetup`工作表的頂部是我們可以修改頁首和頁尾選項的地方。


## 第 2 步：存取工作表和頁面設定屬性

在Aspose.Cells中，每個工作表都有一個`PageSetup`控制佈局功能的屬性，包括頁首和頁尾。讓我們得到`PageSetup`我們的工作表的物件。

```csharp
//取得第一個工作表的PageSetup的引用
PageSetup pageSetup = excel.Worksheets[0].PageSetup;
```

有了這個，`pageSetup`現在包含自訂頁首和頁尾所需的所有設定。


## 步驟 3：設定標題的左側部分

Excel 中的標題分為三個部分：左、中、右。我們首先設定左側部分以顯示工作表名稱。

```csharp
//在標題左側設定工作表名稱
pageSetup.SetHeader(0, "&A");
```

使用`&A`允許您動態顯示工作表名稱。如果工作簿中有多個工作表並且希望每個標題反映其工作表標題，這尤其有用。


## 步驟 4：將日期和時間加入標題中心

接下來，讓我們將當前日期和時間新增到標題的中心部分。此外，我們將使用自訂字體進行樣式設定。

```csharp
//在標題的中間部分以粗體設定日期和時間
pageSetup.SetHeader(1, "&\"Times New Roman,Bold\"&D-&T");
```

在此程式碼中：
- `&D`插入目前日期。
- `&T`插入當前時間。
- `"Times New Roman,Bold"`對這些元素應用粗體 Times New Roman。


## 步驟 5：在標題右側顯示檔案名稱

為了完成標題，讓我們在右側顯示檔案名稱以及字體調整。

```csharp
//以自訂字體大小在標題右側顯示檔案名
pageSetup.SetHeader(2, "&\"Times New Roman,Bold\"&12&F");
```

- `&F`代表文件名，明確列印的頁面屬於哪個文件。
- `&12`將此部分的字體大小變更為 12。


## 第 6 步：將具有自訂字體的文字新增至左頁腳部分

轉到頁腳！我們首先使用自訂文字和指定的字體樣式來設定左頁腳部分。

```csharp
//將具有字體樣式的自訂文字新增至頁腳的左側部分
pageSetup.SetFooter(0, "Hello World! &\"Courier New\"&14 123");
```

這`&\"Courier New\"&14`上述程式碼中的設定將大小為 14 的「Courier New」字體套用至指定文字（`123`）。其餘文字保留預設頁腳字體。


## 步驟 7：在頁尾中央插入頁碼

在頁腳中包含頁碼是幫助讀者追蹤多頁文件的好方法。

```csharp
//在頁腳的中間部分插入頁碼
pageSetup.SetFooter(1, "&P");
```

這裡，`&P`將目前頁碼新增至頁尾的中心部分。這是一個小細節，但對於具有專業外觀的文件至關重要。


## 步驟 8：在右頁腳部分顯示總頁數

最後，讓我們透過在右側部分顯示總頁數來完成頁尾。

```csharp
//在頁腳右側顯示總頁數
pageSetup.SetFooter(2, "&N");
```

- `&N`提供總頁數，讓讀者知道文件的長度。


## 第 9 步：儲存工作簿

設定頁首和頁尾後，就可以儲存工作簿了。這是產生具有完全自訂頁首和頁尾的 Excel 檔案的最後一步。

```csharp
//儲存工作簿
excel.Save(dataDir + "SetHeadersAndFooters_out.xls");
```

此行將檔案儲存到您指定的目錄，並放置自訂頁首和頁尾。


## 結論

在 Excel 工作表中新增頁首和頁尾是建立有組織的專業文件的寶貴技能。使用 Aspose.Cells for .NET，您可以完全控制 Excel 檔案的頁首和頁腳，從顯示工作表名稱到插入自訂文字、日期、時間，甚至動態頁碼。現在您已經了解了每個步驟的實際操作，您可以將 Excel 自動化提升到一個新的水平。

## 常見問題解答

### 我可以對頁首和頁尾的不同部分使用不同的字體嗎？  
是的，Aspose.Cells for .NET 可讓您使用特定的字體標籤為頁首和頁尾的每個部分指定字體。

### 如何刪除頁首和頁尾？  
您可以透過將頁首或頁尾文字設定為空白字串來清除頁首和頁尾`SetHeader`或者`SetFooter`.

### 我可以使用 Aspose.Cells for .NET 將圖像插入頁首或頁尾嗎？  
目前，Aspose.Cells 主要支援頁首和頁尾中的文字。圖像可能需要解決方法，例如將圖像插入工作表本身。

### Aspose.Cells 是否支援頁首和頁尾中的動態資料？  
是的，您可以使用各種動態程式碼（例如`&D`用於日期或`&P`頁碼）新增動態內容。

### 如何調整頁首或頁尾高度？  
 Aspose.Cells 提供了以下選項`PageSetup`類別來調整頁首和頁腳邊距，使您可以控制間距。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
