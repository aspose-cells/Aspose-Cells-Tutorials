---
"description": "透過我們全面的逐步教學學習如何使用 Aspose.Cells for .NET 控制 Excel 中的外部資源。"
"linktitle": "使用工作簿設定控制外部資源"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用工作簿設定控制外部資源"
"url": "/zh-hant/net/workbook-settings/control-external-resources/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用工作簿設定控制外部資源

## 介紹
在資料操作和呈現領域，有效處理外部資源可以改變遊戲規則。如果您正在使用 Excel 檔案並希望使用 Aspose.Cells for .NET 無縫管理外部資源，那麼您來對地方了！在本文中，我們將深入探討在使用 Excel 工作簿時控制外部資源。在本指南結束時，您將能夠毫不費力地實現從外部來源載入圖像和資料的客製化解決方案。
## 先決條件
在我們深入討論編碼細節之前，您需要滿足一些先決條件。請確保：
1. 擁有 Visual Studio：您需要一個 IDE 來編寫和測試您的 .NET 應用程式。 Visual Studio 因其廣泛的支援和易用性而成為最推薦的選項。
2. 下載 Aspose.Cells for .NET：如果您還沒有下載，請從 [下載連結](https://releases。aspose.com/cells/net/). 
3. 對 C# 的基本了解：熟悉 C# 和 .NET 框架概念將使您的流程更加順暢。
4. 設定您的環境：確保您的專案引用 Aspose.Cells 庫。您可以透過 Visual Studio 中的 NuGet 套件管理器執行此操作。
5. 範例文件：準備好包含外部資源（例如連結圖像）的範例 Excel 檔案。該文件將有助於演示我們討論的功能。
一旦設定好這些，您就可以開始使用 Aspose.Cells 控制外部資源了。
## 導入包
要開始編碼，您需要在 C# 檔案中匯入必要的套件。您需要：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
這些命名空間提供對操作 Excel 檔案和處理影像所需的功能的存取。
讓我們將其分解為可管理的步驟，以幫助您使用以下方法控制外部資源 `Workbook Settings`。我們將逐步建立自訂流程提供者、載入 Excel 檔案以及將工作表渲染為映像。請隨意關注！
## 步驟 1：定義來源和輸出目錄
首先，我們需要指定讀取檔案的目錄以及保存輸出的目錄。設定正確的路徑以避免文件未找到錯誤至關重要。
```csharp
// 來源目錄
static string sourceDir = "Your Document Directory";
// 輸出目錄
static string outputDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用您的文件所在的實際路徑。
## 步驟2：實作IStreamProvider接口
接下來，我們將建立一個自訂類別來實現 `IStreamProvider` 介面.此類別將管理如何存取外部資源（如圖像）。
```csharp
class SP : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        // 必要時清理所有資源
    }
    public void InitStream(StreamProviderOptions options)
    {
        // 開啟外部資源的文件流
        FileStream fi = new FileStream(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.png", FileMode.OpenOrCreate, FileAccess.Read);
        options.Stream = fi;
    }
}
```
在 `InitStream` 方法中，我們開啟作為外部資源的檔案並將其分配給 `Stream` 財產。這允許工作簿在渲染時存取資源。
## 步驟3：載入Excel文件
現在我們已經準備好串流提供程序，讓我們載入包含外部資源的 Excel 工作簿。
```csharp
public static void Run()
{
    // 載入範例 Excel 文件
    Workbook wb = new Workbook(sourceDir + "sampleControlExternalResourcesUsingWorkbookSetting_StreamProvider.xlsx");
    
    // 提供 IStreamProvider 的實現
    wb.Settings.StreamProvider = new SP();
```
在此程式碼片段中，我們載入 Excel 檔案並指派自訂 `StreamProvider` 處理外部資源的實作。
## 步驟 4：訪問工作表
載入工作簿後，我們可以輕鬆存取所需的工作表。讓我們抓住第一個。
```csharp
    // 訪問第一個工作表
    Worksheet ws = wb.Worksheets[0];
```
這很簡單，不是嗎？您可以透過指定索引來存取任何工作表。
## 步驟 5：設定影像或列印選項
現在我們將定義我們希望輸出圖像看起來是什麼樣子。我們將配置一些選項，例如確保每張紙有一頁並指定輸出影像類型。
```csharp
    // 指定影像或列印選項
    ImageOrPrintOptions opts = new ImageOrPrintOptions();
    opts.OnePagePerSheet = true;
    opts.ImageType = Drawing.ImageType.Png;
```
選擇 PNG 作為輸出格式可確保品質保持清晰！
## 步驟 6：將工作表渲染為影像
一切設定完畢後，讓我們將選擇的工作表渲染為圖像檔案！這是令人興奮的部分；您會看到您的 Excel 表變成了一個漂亮的圖像。
```csharp
    // 透過傳遞所需參數建立工作表渲染
    SheetRender sr = new SheetRender(ws, opts);
    // 將整個工作表轉換為 png 影像
    sr.ToImage(0, outputDir + "outputControlExternalResourcesUsingWorkbookSetting_StreamProvider.png");
    
    Console.WriteLine("ControlExternalResourcesUsingWorkbookSetting_StreamProvider executed successfully.");
}
```
這 `ToImage` 函數完成所有繁重的工作，將工作表轉換為映像。完成此步驟後，您會發現影像已儲存到輸出目錄中。
## 結論
就是這樣！現在，您掌握了使用 .NET 中的 Aspose.Cells 處理 Excel 檔案時控制外部資源的技巧。這不僅增強了應用程式的功能，而且使處理資料集和簡報變得輕而易舉。透過遵循提供的步驟，您可以輕鬆複製和調整此功能以滿足您的專案的特定需求。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的程式庫，專為 C# 和 .NET 開發人員設計，無需安裝 Microsoft Excel 即可建立、操作和管理 Excel 檔案。
### 如何下載 Aspose.Cells for .NET？
您可以從 [Aspose 網站](https://releases。aspose.com/cells/net/).
### 有免費試用嗎？
是的！您可以從他們的 [發布頁面](https://releases。aspose.com/).
### Aspose.Cells 支援哪些類型的檔案？
Aspose.Cells 支援各種 Excel 格式，包括 XLS、XLSX、CSV 等。
### 在哪裡可以找到對 Aspose.Cells 的支援？
您可以造訪 Aspose 支援論壇 [Aspose 論壇](https://forum.aspose.com/c/cells/9) 尋求幫助。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}