---
title: 變更 Excel 儲存格對齊方式而不遺失格式
linktitle: 變更 Excel 儲存格對齊方式而不遺失格式
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 變更 Excel 儲存格對齊方式而不遺失格式。請遵循我們全面的逐步指南以實現無縫控制。
weight: 10
url: /zh-hant/net/excel-data-alignment-formatting/change-cells-alignment-in-excel-without-losing-existing-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 變更 Excel 儲存格對齊方式而不遺失格式

## 介紹

管理 Excel 文件有時感覺就像在迷宮中行走，尤其是在維護格式的同時進行必要的調整（例如更改單元格對齊方式）時。如果您曾經嘗試調整 Excel 中儲存格的對齊方式，卻發現格式設定受到干擾，那麼您並不孤單！在本教學中，我們將深入研究如何使用 Aspose.Cells for .NET 變更 Excel 儲存格的對齊方式而不遺失任何格式。讓我們捲起袖子開始吧！

## 先決條件

在我們深入實際編碼之前，必須確保所有內容都設定正確。這是您需要的：

1. Visual Studio：確保您的電腦上安裝了 Visual Studio（任何支援 .NET 的版本）。
2. Aspose.Cells for .NET：從下列位置下載並安裝 Aspose.Cells 函式庫：[Aspose 的網站](https://releases.aspose.com/cells/net/).
3. C# 基本知識：稍微熟悉一下 C# 程式設計將會派上用場，因為我們將在 C# 上下文中運作。
4. 範例 Excel 檔案：為了演示，請準備一個範例 Excel 檔案（例如，`sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx`）包含一些初始儲存格格式。

## 導入包

使用 Aspose.Cells for .NET 的第一步是在專案中包含必要的命名空間。方法如下：

### 打開您的項目

開啟 Visual Studio 並建立一個新的 C# 專案（控制台應用程式可以正常運作）。

### 新增對 Aspose.Cells 的引用

- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 搜尋`Aspose.Cells`並安裝它。

### 導入所需的命名空間

在 C# 檔案的頂部，加入以下 using 指令：

```csharp
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Tables;
```

這將允許您無縫地使用 Aspose.Cells 庫提供的類別和方法。

現在我們已經對先決條件進行了排序並導入了包，讓我們逐步分解更改單元格對齊方式的過程。

## 第 1 步：設定來源目錄和輸出目錄

首先，您需要定義 Excel 檔案的儲存位置以及處理後要儲存的位置。

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory\\"; //替換為你的實際目錄

//輸出目錄
string outputDir = "Your Document Directory\\"; //替換為你的實際目錄
```

此程式碼設定輸入和輸出檔案的路徑。一定要更換`"Your Document Directory\\"`與您計算機上的實際路徑。

## 第 2 步：載入範例 Excel 文件

接下來，您需要將範例 Excel 檔案載入到應用程式中。

```csharp
//載入包含具有格式設定的儲存格的範例 Excel 檔案。
Workbook wb = new Workbook(sourceDir + "sampleChangeCellsAlignmentAndKeepExistingFormatting.xlsx");
```

這行程式碼使用 Workbook 類別來載入現有的 Excel 文件，以便我們可以操作其內容。

## 第 3 步：存取所需的工作表

載入工作簿後，存取要操作的工作表。 Excel 檔案可以包含多個工作表，因此請確保您定位的是正確的工作表。

```csharp
//訪問第一個工作表。
Worksheet ws = wb.Worksheets[0];
```

此範例存取第一個工作表。如果您的資料位於不同的工作表上，請相應地調整索引。

## 第 4 步：建立儲存格範圍

透過建立範圍來確定要變更的儲存格。此選擇將集中於指定範圍，例如“B2:D7”。

```csharp
//建立單元格範圍。
Range rng = ws.Cells.CreateRange("B2:D7");
```

該範圍將使我們能夠將新的對齊設定直接應用於這些單元格。

## 第 5 步：建立並自訂樣式對象

現在，我們需要定義我們希望套用的對齊樣式。

```csharp
//建立樣式物件。
Style st = wb.CreateStyle();

//將水平和垂直對齊設定為居中。
st.HorizontalAlignment = TextAlignmentType.Center;
st.VerticalAlignment = TextAlignmentType.Center;
```

在這裡，創建了一個新的 Style 對象，並將水平和垂直對齊設置為居中。這將有助於精確對齊所選單元格內的文字。

## 第 6 步：設定樣式標誌

設定樣式標誌在確保套用樣式變更方面起著至關重要的作用。 

```csharp
//建立樣式標誌物件。
StyleFlag flag = new StyleFlag();

//將樣式標誌對齊設定為 true。這是一個至關重要的聲明。
flag.Alignments = true;
```

透過設定`Alignments` StyleFlag 的屬性為`true`，您告訴 Aspose.Cells 正確套用對齊樣式。

## 第 7 步：將樣式套用到儲存格範圍

樣式和標誌就位後，是時候將這些樣式套用到儲存格範圍了：

```csharp
//將樣式套用至儲存格範圍。
rng.ApplyStyle(st, flag);
```

此步驟有效地更改了該範圍內所有單元格的對齊方式，同時保留任何現有格式。

## 第 8 步：儲存工作簿

最後，您需要將變更儲存到新檔案中，以便保持原始檔案完好無損。

```csharp
//將工作簿儲存為 XLSX 格式。
wb.Save(outputDir + "outputChangeCellsAlignmentAndKeepExistingFormatting.xlsx", SaveFormat.Xlsx);
```

此行將工作簿（包括對齊變更）保存在前面指定的輸出目錄中。

## 第9步：通知成功

儲存文件後，很高興能提供一切按預期運行的回饋！

```csharp
Console.WriteLine("ChangeCellsAlignmentAndKeepExistingFormatting executed successfully.");
```

如果您的操作順利完成，則控制台中會顯示此訊息。

## 結論

使用 Aspose.Cells for .NET 可以在保持現有格式不變的同時變更 Excel 中的儲存格對齊方式，這是一個無縫過程。透過執行這些步驟，您可以簡化應用程式中的 Excel 操作，並避免遺失有價值的格式的麻煩。無論您是在製作報告還是管理資料來源，掌握這項技能都可以改變遊戲規則！

## 常見問題解答

### Aspose.Cells 可以處理大型 Excel 檔案嗎？
絕對地！它針對效能進行了最佳化，可以有效地處理大檔案。

### Aspose.Cells 有試用版嗎？
是的！您可以從該網站下載免費試用版[免費試用](https://releases.aspose.com/).

### Aspose.Cells 支援哪些程式語言？
Aspose.Cells 主要透過各自的函式庫支援.NET、Java 和其他幾種語言。

### 我如何獲得 Aspose.Cells 的支援？
如有任何疑問或支援相關問題，請訪問[支援論壇](https://forum.aspose.com/c/cells/9).

### 我可以一次套用多種樣式嗎？
是的，您可以建立多個 Style 對象，並根據需要順序或有條件地套用它們。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
