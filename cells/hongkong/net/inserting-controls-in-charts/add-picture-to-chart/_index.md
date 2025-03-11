---
title: 新增圖片到圖表
linktitle: 新增圖片到圖表
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 輕鬆將圖片新增至 Excel 圖表。只需幾個簡單的步驟即可增強您的圖表和簡報。
weight: 11
url: /zh-hant/net/inserting-controls-in-charts/add-picture-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 新增圖片到圖表

## 介紹

您是否厭倦了缺乏個人風格的無聊圖表？想要了解如何透過新增圖片來增強 Excel 視覺效果？嗯，你很幸運！在本教程中，我們將深入了解 Aspose.Cells for .NET 的世界，並學習如何在 Excel 中的圖表中添加圖片。所以，拿起你最喜歡的一杯咖啡，讓我們開始吧！

## 先決條件

在我們深入了解編碼的本質之前，您需要順利遵循一些先決條件：

- Visual Studio：您將在此處編寫和執行 .NET 程式碼。確保您已安裝它。
-  Aspose.Cells for .NET：您需要這個函式庫來處理 Excel 檔案。你可以[在這裡下載](https://releases.aspose.com/cells/net/).
- 對 C# 的基本了解：雖然我將指導您完成程式碼，但掌握 C# 基礎知識將使事情變得更加清晰。

### 安裝步驟

1. 安裝Aspose.Cells：您可以透過NuGet套件管理器將Aspose.Cells加入您的Visual Studio專案。透過導航至「工具」>「NuGet 套件管理器」>「管理解決方案的 NuGet 套件」並蒐尋「Aspose.Cells」來執行此操作。點擊安裝。
2. 設定您的專案：在 Visual Studio 中建立一個新的 C# 控制台應用程式專案。

## 導入包

完成所有設定後，下一步是將必要的套件匯入到您的專案中。操作方法如下：

### 導入所需的命名空間

在 C# 程式碼檔案的頂部，您需要匯入以下命名空間：

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;
using Aspose.Cells.Drawing;
using System.IO;
```

這告訴你的程序，「嘿！我將使用 Aspose.Cells 的這些很酷的功能。

現在我們已經具備了先決條件，讓我們將這個過程分解為幾個小步驟。 

## 第 1 步：定義您的目錄

首先，我們需要設定輸入和輸出檔案的路徑。這一步驟至關重要，因為我們需要知道在哪裡可以找到現有的 Excel 文件以及在哪裡保存修改後的文件。

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory/";

//輸出目錄
string outputDir = "Your Output Directory/";
```

代替`Your Document Directory`和`Your Output Directory`與您計算機上的實際路徑。 

## 第 2 步：載入現有工作簿

現在，讓我們載入要將圖片新增至圖表中的現有 Excel 檔案。

```csharp
//開啟現有文件。
Workbook workbook = new Workbook(sourceDir + "sampleAddingPictureInChart.xls");
```

此程式碼將開啟工作簿，使其準備好進行編輯。

## 步驟 3：準備影像流

在新增圖片之前，我們需要讀取要插入圖表的圖像。 

```csharp
//將影像檔案擷取到流中。
FileStream stream = new FileStream(sourceDir + "sampleAddingPictureInChart.png", FileMode.Open, FileAccess.Read);
```

確保您已將圖片儲存在指定目錄中。

## 第 4 步：瞄準圖表

現在，讓我們指定要將圖片新增到哪個圖表。在此範例中，我們將定位第一個工作表上的第一個圖表。

```csharp
//在第二張紙中取得設計師圖表。
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```

您可以透過相應地更改索引來存取任何工作表。

## 第 5 步：將圖片加入圖表中

選擇圖表後，就可以加入圖片了！ 

```csharp
//將新圖片加入圖表中。
Aspose.Cells.Drawing.Picture pic0 = chart.Shapes.AddPictureInChart(50, 50, stream, 200, 200);
```

這裡，`50`和`50`是將放置影像的 X 和 Y 座標，以及`200`是影像的寬度和高度。

## 步驟6：自訂圖片的線條格式

想為您的照片添加一些風格嗎？您可以自訂它的邊框！操作方法如下：

```csharp
//取得圖片的lineformat類型。
Aspose.Cells.Drawing.LineFormat lineformat = pic0.Line; 

//設定破折號樣式。
lineformat.DashStyle = MsoLineDashStyle.Solid;

//設定線寬。
lineformat.Weight = 4;    
```

此程式碼片段可讓您選擇邊框的外觀和厚度。選擇與您的簡報產生共鳴的任何風格！

## 步驟7：儲存修改後的工作簿

經過所有這些艱苦的工作後，讓我們透過執行以下程式碼行來儲存您的修改：

```csharp
//儲存 Excel 檔案。
workbook.Save(outputDir + "outputAddingPictureInChart.xls");
```

現在您的圖片已成功整合到圖表中，並且您的輸出檔案已可供查看！

## 第 8 步：表示成功

最後，您可以新增一條簡單的訊息來確認您的操作是否成功：

```csharp
Console.WriteLine("AddingPictureInChart executed successfully.");
```

## 結論

在本教學中，我們探索如何透過使用 Aspose.Cells for .NET 新增圖片來為 Excel 圖表注入一點個性。只需幾個簡單的步驟，您就可以將平凡的演示提升為令人難忘的。那麼，你還在等什麼？試試一下，讓您的圖表大放異彩！

## 常見問題解答

### 我可以將多張圖片添加到單一圖表中嗎？
是的！您可以致電`AddPictureInChart`多次方法即可添加任意數量的圖片。

### Aspose.Cells 支援哪些圖像格式？
Aspose.Cells 支援多種圖片格式，包括 PNG、JPEG、BMP 和 GIF。

### 我可以自訂圖片的位置嗎？
當然！中的 X 和 Y 座標`AddPictureInChart`方法允許精確定位。

### Aspose.Cells 可以免費使用嗎？
Aspose.Cells 提供免費試用版，但要獲得完整功能，需要許可證。你可以找到價格[這裡](https://purchase.aspose.com/buy).

### 我在哪裡可以找到更多範例？
查看[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)有關更詳細的範例和功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
