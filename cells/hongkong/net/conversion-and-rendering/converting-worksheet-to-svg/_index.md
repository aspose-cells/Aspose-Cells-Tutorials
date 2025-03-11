---
title: 在 .NET 中將工作表轉換為 SVG
linktitle: 在 .NET 中將工作表轉換為 SVG
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過此逐步指南，了解如何使用 Aspose.Cells for .NET 將 Excel 工作表轉換為 SVG。非常適合希望將 Excel 渲染為 SVG 的 .NET 開發人員。
weight: 11
url: /zh-hant/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中將工作表轉換為 SVG

## 介紹

如果您想要將 Excel 工作表轉換為 SVG 格式，那麼您來對地方了！ Aspose.Cells for .NET 是一個功能強大的工具，使開發人員能夠操作 Excel 檔案並將其轉換為各種格式，包括廣泛支援的 SVG（可縮放向量圖形）。本教學將引導您完成在 .NET 中將工作表轉換為 SVG 的過程，並逐步分解該過程，因此即使是初學者也可以輕鬆掌握。

## 先決條件

在深入研究程式碼之前，讓我們確保您擁有所需的一切：

1.  Aspose.Cells for .NET：從下列位置下載並安裝最新版本的 Aspose.Cells for .NET[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/).
2. .NET 開發環境：您需要安裝 Visual Studio 或任何其他 .NET IDE。
3. C# 基礎：需要熟悉 C#，但不用擔心，我們會清楚地解釋一切。
4. Excel 檔案：準備好您想要轉換為 SVG 格式的 Excel 檔案。

## 導入必要的套件

在開始編碼部分之前，請確保在 C# 檔案的頂部包含所需的命名空間。

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

這些套件對於使用 Aspose.Cells 和處理 SVG 匯出等渲染選項是必要的。

現在已經介紹了基礎知識，讓我們開始了解將 Excel 工作表轉換為 SVG 影像的實際步驟。

## 第 1 步：設定文檔目錄的路徑

我們需要做的第一件事是定義 Excel 檔案所在資料夾的路徑。這很重要，因為您的程式碼將引用目錄來載入和儲存檔案。

```csharp
//文檔目錄的路徑
string dataDir = "Your Document Directory";
```

確保更換`"Your Document Directory"`與 Excel 檔案所在的實際路徑。

## 步驟 2： 使用下列命令載入 Excel 文件`Workbook`

接下來，我們需要將 Excel 檔案載入到實例中`Workbook`班級。這`Workbook`類別代表整個 Excel 文件，包括其中的所有工作表。

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

這裡，`"Template.xlsx"`是您正在使用的 Excel 檔案的名稱。確保指定目錄中存在該文件，否則會遇到錯誤。

## 步驟 3：設定 SVG 轉換的影像或列印選項

在將工作表轉換為 SVG 格式之前，我們需要指定圖像選項。這`ImageOrPrintOptions`類別可讓您控制工作表的轉換方式。具體來說，我們需要設定`SaveFormat`到`SVG`並確保每個工作表都轉換為單頁。

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

這`SaveFormat.Svg`選項確保輸出格式為 SVG，同時`OnePagePerSheet`確保每個工作表將呈現在單一頁面上。

## 步驟 4：迭代工作簿中的每個工作表

現在我們需要循環遍歷 Excel 檔案中的所有工作表。每個工作表將單獨轉換。

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    //我們將一一處理每個工作表
}
```

此循環可確保無論工作簿中有多少個工作表，每個工作表都會處理。

## 第 5 步：建立一個`SheetRender` Object for Rendering

對於每個工作表，我們將建立一個`SheetRender`目的。此物件負責將工作表轉換為所需的影像格式，在本例中為 SVG。

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

這`SheetRender` object 有兩個參數：您要轉換的工作表和您之前定義的映像選項。

## 第 6 步：將工作表轉換為 SVG

最後，在循環中，我們將每個工作表轉換為 SVG 格式。我們使用巢狀循環來迭代頁面（儘管在本例中，每個工作表只有一頁，這要歸功於`OnePagePerSheet`選項）。

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    //將工作表輸出為 Svg 影像格式
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

此程式碼會將工作表另存為 SVG 文件，與 Excel 文件位於同一目錄中。每個 SVG 檔案將根據工作表名稱和索引號命名，以避免命名衝突。

## 結論

就是這樣！您已使用 Aspose.Cells for .NET 成功將 Excel 工作表轉換為 SVG 格式。此流程可讓您保留工作表的佈局和設計，同時使其可以在任何支援 SVG 的瀏覽器或裝置（幾乎所有這些）中查看。無論您使用的是複雜的 Excel 文件還是簡單的表格，此方法都可確保您的資料以 Web 友好的格式精美呈現。

## 常見問題解答

### 什麼是 SVG，為什麼要使用它？
SVG（可縮放向量圖形）是一種網路友善格式，可以無限縮放而不損失品質。它非常適合需要以各種尺寸顯示的圖表、圖表和圖像。

### Aspose.Cells 可以處理大型 Excel 檔案進行轉換嗎？
是的，Aspose.Cells 可以有效地處理大型 Excel 檔案並將其轉換為 SVG，而不會出現明顯的效能問題。

### 可以轉換為 SVG 的工作表數量有限制嗎？
不，Aspose.Cells 對於轉換多個工作表沒有固有的限制。唯一的限制是系統的記憶體和效能。

### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，Aspose.Cells 需要生產使用許可證。您可以獲得臨時許可證[這裡](https://purchase.aspose.com/temporary-license/)或探索[免費試用](https://releases.aspose.com/).

### 我可以自訂 SVG 輸出嗎？
是的，您可以調整`ImageOrPrintOptions`自訂 SVG 輸出的各個方面，例如解析度和縮放比例。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
