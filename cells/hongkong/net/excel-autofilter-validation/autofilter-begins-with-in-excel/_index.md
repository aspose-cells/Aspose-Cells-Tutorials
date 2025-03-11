---
title: Excel 中的自動篩選開頭
linktitle: Excel 中的自動篩選開頭
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這份全面的逐步指南，輕鬆了解如何在 .NET 中使用 Aspose.Cells 自動篩選 Excel 行。
weight: 10
url: /zh-hant/net/excel-autofilter-validation/autofilter-begins-with-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel 中的自動篩選開頭

## 介紹

在處理資料方面，Excel 已成為無數行業和用途的首選應用程式。它最強大的功能之一是自動過濾器，它使篩選大量資料集變得輕而易舉。如果您使用 Aspose.Cells for .NET，您可以透過程式設計方式利用此功能並顯著增強您的資料管理任務。在本指南中，我們將引導您完成實作根據 Excel 行是否以特定字串開頭來過濾行的功能的過程。

## 先決條件

在開始之前，請確保您具備以下先決條件：

1. 開發環境：熟悉.NET 開發環境。這可以是 Visual Studio 或您選擇的任何其他 IDE。
2.  Aspose.Cells for .NET：您需要安裝 Aspose.Cells for .NET。如果您還沒有這樣做，您可以方便地下載它[這裡](https://releases.aspose.com/cells/net/).
3. C# 基礎知識：對 C# 以及如何使用 .NET 程式庫的基本了解將幫助您無縫地進行操作。
4. 範例資料：您應該有一個 Excel 文件，最好命名為`sourseSampleCountryNames.xlsx`，位於您指定的來源目錄中。該文件將包含我們將要過濾的資料。
5. 許可：要獲得完整功能，請考慮透過此取得許可證[關聯](https://purchase.aspose.com/buy)。如果您想測試這些功能，您可以要求[臨時執照](https://purchase.aspose.com/temporary-license/).

一切都準備好了嗎？我們走吧！

## 導入包

首先，在 C# 檔案頂部導入必要的命名空間：

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

這將導入核心 Aspose.Cells 功能以及我們將依賴控制台互動的基本系統功能。

現在您已經設定了環境並匯入了必要的套件，讓我們將自動篩選功能分解為可管理的步驟。我們將實作一個過濾器，提取以“Ba”開頭的行。

## 第 1 步：定義來源目錄和輸出目錄

首先，讓我們定義輸入 Excel 檔案所在的位置，以及要儲存篩選輸出的位置：

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory\\";

//輸出目錄
string outputDir = "Your Document Directory\\";
```

說明：這裡，替換`"Your Document Directory\\"`與目錄的實際路徑。確保以雙反斜線結束目錄路徑 (`\\`）以避免任何路徑問題。

## 第 2 步：實例化工作簿對象

接下來，我們將建立一個指向 Excel 檔案的 Workbook 物件：

```csharp
//實例化包含範例資料的 Workbook 對象
Workbook workbook = new Workbook(sourceDir + "sourseSampleCountryNames.xlsx");
```

說明：此行使用指定的檔案路徑初始化一個新的 Workbook 實例。這`Workbook`類別是基礎，因為它代表整個 Excel 檔案。

## 第 3 步：存取第一個工作表

現在，我們需要存取我們想要使用的特定工作表：

```csharp
//存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```

解釋：`Worksheets`集合允許我們存取單獨的工作表。使用`[0]`引用 Excel 檔案中的第一個工作表，這通常是處理單一工作表檔案時的常見做法。

## 第 4 步：設定自動篩選

這就是魔法開始的地方！我們將為我們的數據創建一個自動過濾範圍：

```csharp
//透過指定單元格範圍建立自動篩選
worksheet.AutoFilter.Range = "A1:A18";
```

解釋：`AutoFilter.Range`屬性允許您指定要過濾的行。在本例中，我們過濾 A1 到 A18 範圍內的行，假定這些行保存我們的資料。

## 步驟 5：套用篩選條件

下一步是定義過濾條件。我們只想顯示第一列值以“Ba”開頭的行：

```csharp
//初始化以字串“Ba”開頭的行的過濾器
worksheet.AutoFilter.Custom(0, FilterOperatorType.BeginsWith, "Ba");
```

解釋：`Custom`方法定義了我們的濾波邏輯。第一個參數（`0` ) 表示我們正在根據第一列 (A) 進行過濾，並且`FilterOperatorType.BeginsWith`指定我們的條件來尋找以“Ba”開頭的行。

## 第 6 步：刷新過濾器

套用篩選條件後，我們需要確保 Excel 刷新以反映變更：

```csharp
//刷新過濾器以顯示/隱藏過濾的行
worksheet.AutoFilter.Refresh();
```

說明：此行呼叫自動篩選上的刷新，以確保可見行對應於應用的篩選條件。這類似於點擊 Excel 中的刷新按鈕。

## 步驟7：儲存修改後的Excel文件

現在是時候保存我們所做的更改了：

```csharp
//儲存修改後的Excel文件
workbook.Save(outputDir + "outSourseSampleCountryNames.xlsx");
```

解釋：`Save`方法將修改後的工作簿寫回指定的輸出路徑。這屬於將定義的篩選器寫入新檔案的範圍，以便原始資料保持完整。

## 步驟8：輸出確認

最後我們確認一下我們的操作是否成功：

```csharp
Console.WriteLine("AutofilterBeginsWith executed successfully.\r\n");
```

說明：這個簡單的行向控制台輸出一條確認訊息，讓您知道過濾過程已完成且沒有錯誤。

## 結論

在資料管理令人不知所措的世界中，透過 Aspose.Cells for .NET 掌握 Excel 中的 AutoFilter 等功能可讓您有效率且有效地操作資料。您已經了解如何篩選以「Ba」開頭的 Excel 行，並逐步實施該方法。透過練習，您將能夠適應此方法以滿足正在進行的專案中的各種資料過濾需求。

## 常見問題解答

### Excel 中自動篩選的用途是什麼？  
AutoFilter 允許使用者快速排序和過濾電子表格中的數據，從而輕鬆關注特定數據集。

### 我可以使用 Aspose.Cells 根據多個條件進行過濾嗎？  
是的，Aspose.Cells 支援進階過濾選項，可讓您設定多個條件。

### 我需要 Aspose.Cells 許可證才能使用它嗎？  
雖然您可以開始免費試用，但需要許可證才能使用完整功能並消除任何試用限制。

### 我可以使用 Aspose.Cells 執行哪些類型的過濾？  
您可以按值、條件（例如開頭或結尾）和自訂篩選來過濾數據，以滿足您的特定要求。

### 在哪裡可以找到有關 Aspose.Cells for .NET 的更多資訊？  
你可以查看文檔[這裡](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
